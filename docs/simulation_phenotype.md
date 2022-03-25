---
layout: default
title: Phenotype Simulation
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Data Simulation
---

# Simulate a phenotype data frame

## The below is an example to simulate covariates data frame in R
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

## Step 1: simulate linear predictors based on the covariates and others
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


