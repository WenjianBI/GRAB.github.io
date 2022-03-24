---
layout: default
title: Genotype Simulation
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Data Simulation
---


```{r}   
## Commen Variants with MAF ranging from (0.05, 0.5)
set.seed(12345)
OutList = GRAB.SimuGMat(nSub = 500, nFam = 50, FamMode = "10-members", nSNP = 10000,
                        MaxMAF = 0.5, MinMAF = 0.05)
GenoMat = OutList$GenoMat 
MissingRate = 0.05
indexMissing = sample(length(GenoMat), MissingRate * length(GenoMat))
GenoMat[indexMissing] = -9
extDir = system.file("extdata", package = "GRAB")
extPrefix = paste0(extDir, "/simuPLINK")
GRAB.makePlink(GenoMat, extPrefix)

setwd(extDir)
system("plink --file simuPLINK --make-bed --out simuPLINK")
system("plink --bfile simuPLINK --recode A --out simuRAW")
system("plink2 --bfile simuPLINK --export bgen-1.2 bits=8 ref-first --out simuBGEN  # UK Biobank use 'ref-first'")
system("bgenix -g simuBGEN.bgen -index")

## Rare Variants with MAF ranging from (0.0001, 0.01)
set.seed(34567)
OutList = GRAB.SimuGMat(nSub = 500, nFam = 50, FamMode = "10-members", nSNP = 10000,
                        MaxMAF = 0.01, MinMAF = 0.0001)
GenoMat = OutList$GenoMat 
MissingRate = 0.05
indexMissing = sample(length(GenoMat), MissingRate * length(GenoMat))
GenoMat[indexMissing] = -9
extDir = system.file("extdata", package = "GRAB")
extPrefix = paste0(extDir, "/simuPLINK_RV")
GRAB.makePlink(GenoMat, extPrefix)

setwd(extDir)
system("plink --file simuPLINK_RV --make-bed --out simuPLINK_RV")
system("plink --bfile simuPLINK_RV --recode A --out simuRAW_RV")
system("plink2 --bfile simuPLINK_RV --export bgen-1.2 bits=8 ref-first --out simuBGEN_RV  # UK Biobank use 'ref-first'")
system("bgenix -g simuBGEN_RV.bgen -index")
```
