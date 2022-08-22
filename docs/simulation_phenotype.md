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
eta = with(Covar, beta.AGE * AGE + beta.GENDER * GENDER)
```

If the simulated phenotype is associated with a random term related to family structure (mixed model approaches) or genotype (to evaluate power), then the linear predictors ```eta``` should be updated by adding the corresponding terms. 

### Next, we simulate phenotypes using ```eta```

**A.** binary trait
```
BinaryPheno = GRAB.SimuPheno(eta, traitType = "binary", 
                             control = list(pCase=0.1))
table(BinaryPheno)
# BinaryPheno
#   0   1 
# 900 100
```

**B.** quantitative trait
```
QuantPheno = GRAB.SimuPheno(eta, traitType = "quantitative", 
                            control = list(sdError=1))
```

**C.** ordinal categorical phenoype
```
OrdinalPheno = GRAB.SimuPheno(eta, traitType = "ordinal",
                              control = list(pEachGroup = c(8,1,1)))
table(OrdinalPheno)
# OrdinalPheno
#   0   1   2 
# 800 100 100
```

**D.** time-to-event phenoype (to be updated)
```
# GRAB.SimuPheno(eta, traitType = "time-to-event",
#                control = list(pEachGroup=c(8, 1, 1)))
```

We write the phenotype data to ```system.file("extdata", "simuPHENO.txt", package = "GRAB")```
```
PhenoFile = system.file("extdata", "simuPHENO.txt", package = "GRAB")
PhenoData = cbind(Covar, 
                  BinaryPheno = BinaryPheno,
                  OrdinalPheno = OrdinalPheno,
                  QuantPheno = QuantPheno)
data.table::fwrite(PhenoData, PhenoFile, row.names = F, quote = F, col.names = T, sep = "\t")                  
```

## The distribution of simulated phenotypes
The distribution of simulated phenotypes compared to linear predicators ```eta``` is as below.
- quantitative phenotype: positive correction between ```eta``` and phenotypes
- binary phenotype: higher ```eta```, higher possibility of being cases
- ordinal categorical phenotype: higher ```eta```, higher possibility of being groups with larger number

<img src="{{site.baseurl | prepend: site.url}}img/SimuPheno.jpeg">


