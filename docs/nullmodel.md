---
layout: default
title: Null Model Fitting
nav_order: 6
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
has_children: true
has_toc: true
---

# Null model fitting using GRAB package 

```GRAB``` package gives a generic framework to analyze a wide variaty of commonly used phenotypes. 

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

Arguments ```traitType``` and ```method``` specify the type of phenotype data and the analysis approach. Currently, ```GRAB``` package supports the below combination 

| phenotype                | ```traitType``` |```method```| Related subjects |
|:------------------------:|:---------------:|:----------:|:----------------:|
| binary data              | "binary"        | "SAIGE"    |  YES             |
| quantitative data        | "quantitative"  | "SAIGE"    |  YES             |
| ordinal categorical data | "ordinal"       | "POLMM"    |  YES             |
| time-to-event data       | "time-to-event" | "SPACox"   |  NO              |

## Step 2: choose Dense GRM or Sparse GRM

Both dense GRM and sparse GRM are supported in ```GRAB``` package to characterize family relatedness, which can avoid high type one error rates.

| Which GRM   | Pros.    | Cons       | Required arguments  |
|:-----------:|:----------:|:--------:|:-------------------:|
| Dense GRM   | More powerful | Slow  | ```SparseGRMFile``` |
| Sparse GRM  | Fast  | Less powerful | ```GenoFile```      |

NOTE: Based on extensive simulation results, for binary and ordinal categorical data analysis, analyses using dense and sparse GRM perform similarly in terms of both type one error rates and powers.

## Step 3: about argument ```control``` 

Argument ```control``` is to specify the list of parameters for controlling the fitting process. 

## Step 4: check details for different approaches

- ```POLMM```: ordinal categorical data analysis 
- ```SAIGE```: binary and quantiative data analysis
- ```GATE```: time-to-event data analysis

## 






