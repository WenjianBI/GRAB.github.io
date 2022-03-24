---
layout: default
title: Step 2
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Data Simulation
---

```
FamFile = system.file("extdata", "simuPLINK.fam", package = "GRAB")
FamData = read.table(FamFile)
IID = FamData$V2  # Individual ID
n = length(IID)
set.seed(678910)
## The below is just to demonstrate the functions of GRAB package
Pheno = data.frame(IID = IID, Cova1 = rnorm(n), Cova2 = rbinom(n, 1, 0.5), 
                   binary = rbinom(n, 1, 0.5),
                   ordinal = rbinom(n, 3, 0.3),
                   quantitative = rnorm(n),
                   time = runif(n),
                   event = rbinom(n, 1, 0.2))
PhenoFile = system.file("extdata", "simuPHENO.txt", package = "GRAB")
write.table(Pheno, PhenoFile, row.names = F, quote = F, sep = "\t")
```