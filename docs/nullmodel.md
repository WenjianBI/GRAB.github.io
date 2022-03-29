---
layout: default
title: Null Model Fitting
nav_order: 5
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
has_children: true
has_toc: true
---

# Null model fitting using GRAB package 

GRAB package includes multiple approaches to analyze multiple phenotypes, which share the same framework when fitting a null model. 

## Quick start-up examples
```
PhenoData = read.table(system.file("extdata", "example.pheno", package = "GRAB"), header = T)
GenoFile = system.file("extdata", "example.bed", package = "GRAB")
obj.POLMM = GRAB.NullModel(factor(Ordinal) ~ Cova1 + Cova2,
                           data = PhenoData, subjData = PhenoData$IID, method = "POLMM", traitType = "ordinal",
                           GenoFile = GenoFile,
                           control = list(showInfo = FALSE, LOCO = FALSE, tolTau = 0.2, tolBeta = 0.1))
```





