---
layout: default
title: Phenotype Simulation
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Data Simulation
---

# Phenotype simulation using GRAB package

The document can show how to simulate
- Binary phenotype
- Quantitative phenotype
- Ordinal categorical phenotype
- Time-to-event data

## An example to simulate covariates data frame in R

```
set.seed(678910)
FamFile = system.file("extdata", "simuPLINK.fam", package = "GRAB")
FamData = data.table::fread(FamFile)
IID = FamData$V2  # Individual ID
n = length(IID)   # sample size
Covar = data.table::data.table(IID = IID,
                               AGE = rnorm(n, 60), 
                               GENDER = rbinom(n, 1, 0.5))
CovarFile = system.file("extdata", "simuCovar.txt", package = "GRAB")
write.table(Covar, CovarFile, row.names = F, quote = F, sep = "\t")
```

## Step 1: simulate linear predictors ```eta```

```
library(tidyr)
library(dplyr)
set.seed(13579)
CovarFile = system.file("extdata", "simuCovar.txt", package = "GRAB")
Covar = data.table::fread(CovarFile, header=T)
beta.AGE = 0.5
beta.GENDER = 0.5
eta = with(Covar, beta.AGE * AGE + beta.GENDER * GENDER)
```

### Note about the linear predictors ```eta```

If the simulated phenotype is associated with family structure (mixed model approaches) or genotype (to evaluate power), then the linear predictors ```eta``` can be updated by adding other terms. 

## Step 2: simulate phenotypes using ```eta```

### Step 2(a) binary phenoype
```
set.seed(1)
phenoB = GRAB.SimuPheno(eta, traitType = "binary", 
                        control = list(pCase=0.1))
table(phenoB)
# phenoB
#   0   1 
# 900 100
```

### Step 2(b) quantitative phenoype
```
set.seed(1)
phenoQ = GRAB.SimuPheno(eta, traitType = "quantitative", 
                        control = list(sdError=1))
```

### Step 2(c) ordinal categorical phenoype
```
set.seed(1)
phenoO = GRAB.SimuPheno(eta, traitType = "ordinal",
                        control = list(pEachGroup = c(8,1,1)))
table(phenoO)
# phenoO
#   0   1   2 
# 800 100 100
```

### Step 2(d) time-to-event phenoype
```
# To be continued
# GRAB.SimuPheno(eta, traitType = "time-to-event",
#                control = list(pEachGroup=c(8, 1, 1)))
```

## The distribution of simulated phenotypes
The distribution of simulated phenotypes compared to linear predicators ```eta``` is as below.
- quantitative phenotype: positive correction between ```eta``` and phenotypes
- binary phenotype: higher ```eta```, higher possibility of being cases
- ordinal categorical phenotype: higher ```eta```, higher possibility of being groups with larger number

<img src="{{site.baseurl | prepend: site.url}}img/SimuPheno.jpeg">


