---
layout: default
title: Null Model Fitting
nav_order: 6
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
has_children: true
has_toc: true
---

# Null model fitting using GRAB package 

```GRAB``` package gives a generic framework to support a wide variaty of commonly used phenotypes. 

## Quick start-up examples
```
PhenoData = read.table(system.file("extdata", "example.pheno", package = "GRAB"), header = T)
GenoFile = system.file("extdata", "example.bed", package = "GRAB")
obj.POLMM = GRAB.NullModel(formula = factor(Ordinal) ~ Cova1 + Cova2,
                           data = PhenoData, 
                           subjData = PhenoData$IID, 
                           method = "POLMM", 
                           traitType = "ordinal",
                           GenoFile = GenoFile,
                           control = list(showInfo = FALSE, LOCO = FALSE, tolTau = 0.2, tolBeta = 0.1))
```

## Step 1: choose ```traitType``` and ```method```

Argument ```traitType``` specifies the type of phenotype data. Currently, ```GRAB``` package supports the below 

- ```binary```: 
- ```quantitative```
- ```ordinal```: method can be ```POLMM```
- ```time-to-event```

## Step 2: decide Dense GRM or Sparse GRM to characterize family relatedness

- SparseGRM: If Sparse GRM is used, please make a sparse GRM file prior to null model fitting.
- DenseGRM: If Dense GRM is used, please give PLINK files as input

## Step 3: about argument ```control``` 

Argument ```control``` is to specify the list of parameters for controlling the fitting process. 

## Step 4: check details for different approaches

- ```POLMM```: ordinal categorical data analysis 
- ```SAIGE```: binary and quantiative data analysis
- ```GATE```: time-to-event data analysis

## 






