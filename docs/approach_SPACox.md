---
layout: default
title: SPACox / SPAmix / SPAGRM
nav_order: 3
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Genome-wide association studies
has_children: false
has_toc: false
---

# SPACox / SPAmix / SPAGRM approaches

## Main features

```SPACox```, ```SPAmix```, and ```SPAGRM``` are accurate and efficient approaches to associating complex traits (including but not limited to time-to-event traits) to single-variant.

The three methods use empirical SPA approaches and share the below features.

- Model residuals (whose sum is zero) are needed as input. Users can select appropriate statistical models depending on the type of traits in analysis.
- High computational efficiency to analyze large-scale biobank data with millions of individuals
- High accuracy to analyze common, low-frequency, and rare variants, even if the phenotypic distribution (or residual distribution) is highly unbalanced.

The three methods are different in terms of

- ```SPACox``` is the basic function to analyze unrelated subjects in a homozygous population.

- ```SPAmix``` extends ```SPACox``` to analyze an admixture population or multiple populations. The method is still only valid to analyze unrelated subjects.

- ```SPAGRM``` extends ```SPACox``` to analyze a study cohort in which subjects can be genetically related to each other. The method is still only valid to analyze a homozygous population.

## Important notes about function ```GRAB.NullModel```

- If the left side of argument ```formula``` is model residual, please specify the argument ```traitType = "Residuals"```. Otherwise, the argument ```traitType``` can be specified based on the type of trait in analysis.

- For method ```SPAmix```, the top SNP-derived PC and related information is required in the arguments ```formula``` and ```control```.

- For method ```SPAGRM```, arguments ```GenoFile```, ```GenoFileIndex```, and ```SparseGRMFile``` are required to characterize the family relatedness.

## Quick Start-up Guide
The below gives examples to demonstrate the usage of ```SPACox```, ```SPAmix```, and ```SPAGRM``` approaches.

Step 1. Read in data and fit a null model

```
library(GRAB)
PhenoFile = system.file("extdata", "simuPHENO.txt", package = "GRAB")
PhenoData = data.table::fread(PhenoFile, header = T)
obj.SPACox = GRAB.NullModel(Surv(SurvTime, SurvEvent)~AGE+GENDER, data = PhenoData, subjData = IID, method = "SPACox", traitType = "time-to-event")
```

```SPACox``` method can also support model residuals as input. The above codes are the same as below.

```
obj.coxph = coxph(Surv(SurvTime, SurvEvent)~AGE+GENDER, data = PhenoData, x=T)
obj.SPACox = GRAB.NullModel(obj.coxph$residuals~AGE+GENDER, data = PhenoData, subjData = IID, method = "SPACox", traitType = "Residual")
```

Step 2. Conduct genome-wide association studies

For different type of traits and methods, the step 2 is the same as below.

```
GenoFile = system.file("extdata", "simuPLINK.bed", package = "GRAB")
OutputDir = system.file("results", package = "GRAB")
OutputFile = paste0(OutputDir, "/Results_SPACox.txt")
GRAB.Marker(obj.SPACox, GenoFile = GenoFile, OutputFile = OutputFile)
```


## Citation

- SPACox: Bi, Wenjian, Lars G. Fritsche, Bhramar Mukherjee, Sehee Kim, and Seunggeun Lee. **A fast and accurate method for genome-wide time-to-event data analysis and its application to UK Biobank.** *The American Journal of Human Genetics* 107, no. 2 (2020): 222-233.

- SPAmix: to be submitted.

- SPAGRM: to be submitted.