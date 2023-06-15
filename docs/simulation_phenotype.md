---
layout: default
title: Phenotype Simulation
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Data Simulation
---
  
  # Phenotype simulation
  
  The below demonstrates the simulation of
- Binary trait
- Quantitative trait
- Ordinal categorical trait
- Time-to-event trait (to be updated)

The phenotype data ```system.file("extdata", "simuPHENO.txt", package = "GRAB")``` is simulated as below line by line.

### First, we simulate covariates data frame in R

```
library(GRAB)
set.seed(678910)
FamFile = system.file("extdata", "simuPLINK.fam", package = "GRAB")
FamData = data.table::fread(FamFile)
IID = FamData$V2  # Individual ID
n = length(IID)   # sample size
Covar = data.table::data.table(IID = IID,
                               AGE = rnorm(n, 60), 
                               GENDER = rbinom(n, 1, 0.5))
```

### Then, we simulate linear predictors ```eta```

```
beta.AGE = 0.5
beta.GENDER = 0.5
Covar = Covar %>% mutate(eta = beta.AGE * AGE + beta.GENDER * GENDER)
```

To simulate phenotypes for subjects with a given family structure, please add a random effect to the linear predictors ```eta``` as below.

```
bVec = GRAB.SimubVec(500, 50, "10-members", tau = 1)
Covar = merge(Covar, bVec)
PhenoData = Covar %>% mutate(eta = eta + bVec)
```

### Next, we simulate phenotypes using ```eta```

**A.** binary trait
```
PhenoData = PhenoData %>% mutate(BinaryPheno = GRAB.SimuPheno(eta, traitType = "binary", 
                                                              control = list(pCase=0.1)))
PhenoData %>% select(BinaryPheno) %>% table()
# Random number seed:	 493536667
# .
#   0   1 
# 900 100
```

**B.** quantitative trait
```
PhenoData = PhenoData %>% mutate(QuantPheno = GRAB.SimuPheno(eta, traitType = "quantitative", 
                                                             control = list(sdError=1)))
# Random number seed:      98062725
```

**C.** ordinal categorical trait
```
PhenoData = PhenoData %>% mutate(OrdinalPheno = GRAB.SimuPheno(eta, traitType = "ordinal", 
                                                               control = list(pEachGroup = c(8,1,1))))
PhenoData %>% select(OrdinalPheno) %>% table()
# Random number seed:	 418335750
# .
#   0   1   2 
# 800 100 100
```

**D.** time-to-event trait
```
TimeToEventPheno = GRAB.SimuPheno(PhenoData$eta, traitType = "time-to-event", control = list(eventRate = 0.1))
# Random number seed:	 881619480
PhenoData = cbind(PhenoData, TimeToEventPheno)
```

The simulated phenotype data is as below

```
head(PhenoData)
#         IID      AGE GENDER      eta       bVec BinaryPheno QuantPheno OrdinalPheno   SurvTime SurvEvent
# 1:   Subj-1 59.61118      0 29.59961 -0.2059781           0  0.2786663            0 0.03245097         0
# 2:  Subj-10 61.31636      0 29.32101 -1.3371678           0 -2.2973289            0 0.19733412         0
# 3: Subj-100 59.16625      0 29.90944  0.3263173           0 -2.4870252            1 0.09451178         0
# 4: Subj-101 60.18490      1 28.99876 -1.5936861           0 -3.4063276            0 0.10946053         0
# 5: Subj-102 58.76700      1 27.90020 -1.9832990           0 -3.4421444            0 0.04882298         0
# 6: Subj-103 59.98608      1 29.11236 -1.3806732           0 -1.3891887            0 0.30540795         0
```

The phenotype data is stored in the below file ```system.file("extdata", "simuPHENO.txt", package = "GRAB")```
```
PhenoFile = system.file("extdata", "simuPHENO.txt", package = "GRAB")
data.table::fwrite(PhenoData, PhenoFile, 
                   row.names = F, quote = F, col.names = T, sep = "\t")                  
```

## The distribution of simulated phenotypes
The distribution of simulated phenotypes compared to linear predicators ```eta``` is as below.
- quantitative phenotype: positive correction between ```eta``` and phenotypes
- binary phenotype: higher ```eta```, higher possibility of being cases
- ordinal categorical phenotype: higher ```eta```, higher possibility of being groups with larger number

<img src="{{site.baseurl | prepend: site.url}}img/SimuPheno.jpeg">
  