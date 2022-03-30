---
layout: default
title: POLMM
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Null Model Fitting
has_children: false
has_toc: false
---

# POLMM approach 
POLMM approach is an accurate and efficient approach to GWAS with an ordinal categorical phenotype.

## Main features

- designed for ordinal categorical phenotype
- accurate for balanced and unbalanced phenotypic distributions
- scalable for a large-scale biobank data analysis
- support both dense GRM and sparse GRM to adjust for family relatedness
- support both single variant analysis and region-based analysis (Burden, SKAT, and SKAT-O)

## Prior to analysis

- The left side of argument ```formula``` should be a factor. If function ```factor``` is used to convert phenotype to a factor, we highly recommend users explicitly specify argument ```levels```.

- We recommend using Sparse GRM to adjust for family relatedness. Using sparse GRM is fast and we did not observe an obvious power loss compared to using dense GRM.

## Start-up examples

### First prepare the data
```
PhenoFile = system.file("extdata", "simuPHENO.txt", package = "GRAB")
PhenoData = data.table::fread(PhenoFile, header = T)
PhenoData = PhenoData %>% mutate(OrdinalPheno = factor(OrdinalPheno, 
                                                       levels = c(0, 1, 2)))
```

### If dense GRM is used in model fitting, please first prepare PLINK files ```GenoFile```
```
SparseGRMFile =  system.file("SparseGRM", "SparseGRM.txt", package = "GRAB")
GenoFile = system.file("extdata", "simuPLINK.bed", package = "GRAB")
obj.POLMM = GRAB.NullModel(formula = OrdinalPheno ~ AGE + GENDER,
                           data = PhenoData, 
                           subjData = PhenoData$IID, 
                           method = "POLMM", 
                           traitType = "ordinal",
                           GenoFile = GenoFile,
                           SparseGRMFile =  SparseGRMFile,
                           control = list(showInfo = FALSE, 
                                          LOCO = FALSE, 
                                          tolTau = 0.2, 
                                          tolBeta = 0.1))
```

### If sparse GRM is used in model fitting, please first prepare sparse GRM file ```SparseGRMFile```
```
GenoFile = system.file("extdata", "simuPLINK.bed", package = "GRAB")
obj.POLMM = GRAB.NullModel(factor(OrdinalPheno) ~ AGE + GENDER,
                           data = PhenoData, 
                           subjData = PhenoData$IID, 
                           method = "POLMM", 
                           traitType = "ordinal",
                           GenoFile = GenoFile,
                           control = list(showInfo = FALSE, 
                                          LOCO = FALSE, 
                                          tolTau = 0.2, 
                                          tolBeta = 0.1))
```

## Citation
Bi, Wenjian, Wei Zhou, Rounak Dey, Bhramar Mukherjee, Joshua N. Sampson, and Seunggeun Lee. **Efficient mixed model approach for large-scale genome-wide association studies of ordinal categorical phenotypes.** *The American Journal of Human Genetics* 108, no. 5 (2021): 825-839.

