---
layout: default
title: Genotype Simulation
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Data Simulation
---

### Simulate a genotype matrix
``` 
set.seed(12345)
OutList = GRAB.SimuGMat(nSub = 500,       # 500 unrelated subjects
                        nFam = 50,        # 50 families
                        FamMode = "10-members",   # each family includes 10 members
                        nSNP = 10000,     # 10000 SNPs
                        MaxMAF = 0.5, MinMAF = 0.05)  # MAFs follow a uniform distribuiton U(0.05, 0.5)

summary(OutList)
#            Length Class      Mode
# GenoMat    10001  data.table list
# markerInfo     2  data.table list

markerInfo = OutList$markerInfo
#              SNP       MAF
#     1:     SNP_1 0.3744068
#     2:     SNP_2 0.4440979
#     3:     SNP_3 0.3924420
#     4:     SNP_4 0.4487561
#     5:     SNP_5 0.2554164
#    ---                    
#  9996:  SNP_9996 0.3270282
#  9997:  SNP_9997 0.2866840
#  9998:  SNP_9998 0.0601416
#  9999:  SNP_9999 0.2161107
# 10000: SNP_10000 0.1632723

GenoMat = OutList$GenoMat
dim(GenoMat)   
# [1]  1000 10000 # genotype matrix includes 1000 subjects and 10000 SNPs

GenoMat[,1:10]
#       SNP_1 SNP_2 SNP_3 SNP_4 SNP_5 SNP_6 SNP_7 SNP_8 SNP_9 SNP_10
#    1:     0     1     2     2     1     0     0     0     1      1
#    2:     1     1     1     0     0     0     0     0     1      1
#    3:     1     1     0     1     0     0     1     0     1      1
#    4:     1     1     1     2     1     0     1     2     0      1
#    5:     0     2     2     1     0     0     0     0     0      1
#   ---                                                             
#  996:     1     0     1     0     0     0     1     2     1      1
#  997:     1     1     0     0     1     0     1     0     1      0
#  998:     0     2     1     1     0     1     1     0     0      0
#  999:     2     0     1     1     1     0     0     0     0      1
# 1000:     1     0     0     2     0     0     0     1     0      2

rownames(GenoMat)[1:5]
[1] "f1_1" "f1_2" "f1_3" "f1_4" "f1_5"   # family 1, members 1-5
rownames(GenoMat)[996:1000]
[1] "Subj-496" "Subj-497" "Subj-498" "Subj-499" "Subj-500"  # unrelated subjects 496-500
```

### Suppose the genotype missing rate is 5%
```
MissingRate = 0.05
indexMissing = sample(length(GenoMat), MissingRate * length(GenoMat))
GenoMat[indexMissing] = -9
```

### Make PLINK files based on the genotype matrix
```
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
