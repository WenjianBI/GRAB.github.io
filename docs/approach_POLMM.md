---
layout: default
title: POLMM / POLMM-GENE
nav_order: 2
description: "POLMM approaches: ordinal categorical trait analysis."
parent: Association Approaches
has_children: false
has_toc: false
---

# POLMM approaches 

POLMM and POLMM-GENE are accurate and efficient approaches to associate an ordinal categorical trait to single-variant and variant-set, respectively.

## Main features

- designed for ordinal categorical phenotype
- accurate for balanced and unbalanced phenotypic distributions
- scalable for a large-scale biobank data analysis
- support both dense GRM and sparse GRM (recommanded) to adjust for family relatedness
- support both single variant analysis and region-based analysis (Burden, SKAT, and SKAT-O)

## Notes prior to analysis

- The left side of argument ```formula``` should be a factor. If function ```factor``` is used to convert phenotype to a factor, we highly recommend explicitly specifying argument ```levels```.

- We recommend using Sparse GRM to adjust for family relatedness due to its high computational efficiency. And generally we did not observe a power loss compared to using dense GRM.

## Start-up examples

### First read in phenotype and covariate data

```
PhenoFile = system.file("extdata", "simuPHENO.txt", package = "GRAB")
PhenoData = data.table::fread(PhenoFile, header = T)
PhenoData = PhenoData %>% mutate(OrdinalPheno = factor(OrdinalPheno, 
                                                       levels = c(0, 1, 2)))
```

### Step 1(a): If dense GRM is used in model fitting, please first prepare PLINK files ```GenoFile```

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

### Step 1(b): If sparse GRM is used in model fitting, please first prepare sparse GRM file ```SparseGRMFile```

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

### Step 2(a): Single-variant tests using POLMM

```
GenoFile = system.file("extdata", "nSNPs-10000-nsubj-1000-ext.bed", package = "GRAB")
OutputDir = system.file("results", package = "GRAB")
OutputFile = paste0(OutputDir, "/POLMMMarkers.txt")
GRAB.Marker(obj.POLMM, GenoFile = GenoFile,
            OutputFile = OutputFile)
```

### Step 2(b): Set-based tests using POLMM-GENE

```
objNull = obj.POLMM
GenoFile = system.file("extdata", "nSNPs-10000-nsubj-1000-ext.bed", package = "GRAB")
GenoFileIndex = NULL

RegionFile = system.file("extdata", "example.RegionFile.txt", package = "GRAB")
RegionAnnoHeader = c("ANNO1")

OutputDir = system.file("results", package = "GRAB")
OutputFile = paste0(OutputDir, "/POLMM_Regions.txt")
OutputFileIndex = NULL

SparseGRMFile = system.file("SparseGRM", "SparseGRM.txt", package = "GRAB")
control = list(max_maf_region = 0.3)

GRAB.Region(objNull,
            GenoFile,
            GenoFileIndex,
            OutputFile,
            OutputFileIndex,
            RegionFile,              # column 1: marker Set ID, column 2: SNP ID, columns 3-n: Annotations similar as in STAAR
            RegionAnnoHeader,
            SparseGRMFile,
            control)
```


## Citation

- POLMM: Bi, Wenjian, Wei Zhou, Rounak Dey, Bhramar Mukherjee, Joshua N. Sampson, and Seunggeun Lee. **Efficient mixed model approach for large-scale genome-wide association studies of ordinal categorical phenotypes.** *The American Journal of Human Genetics* 108, no. 5 (2021): 825-839.

- POLMM-GENE: Bi, Wenjian, Wei Zhou, Peipei Zhang, Yaoyao Sun, Weihua Yue, and Seunggeun Lee. **Scalable mixed model approaches for set-based association studies on large-scale categorical data analysis and its application to 450k exome sequencing data in UK Biobank.** To be submitted.

