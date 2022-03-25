---
layout: default
title: Genotype Simulation
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Data Simulation
---

# Genotype simulation using GRAB package and other tools

## The below is an example to simulate genotype matrix in R
``` 
set.seed(12345)
OutList = GRAB.SimuGMat(nSub = 500,                   # 500 unrelated subjects
                        nFam = 50,                    # 50 families
                        FamMode = "10-members",       # each family includes 10 members
                        nSNP = 10000,                 # 10000 SNPs
                        MaxMAF = 0.5, MinMAF = 0.05)  # MAFs follow a uniform distribuiton U(0.05, 0.5)

summary(OutList)
#            Length   Class      Mode   
# GenoMat    10000000 -none-     numeric
# markerInfo        2 data.table list

markerInfo = OutList$markerInfo
markerInfo
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
class(GenoMat)
# [1] "matrix" "array"

GenoMat[c(1:5,996:1000),1:10]  # Subjects 1-5 are from family 1; Subjects 496-500 are unrelated subjects
#          SNP_1 SNP_2 SNP_3 SNP_4 SNP_5 SNP_6 SNP_7 SNP_8 SNP_9 SNP_10
# f1_1         0     1     2     2     1     0     0     0     1      1
# f1_2         1     1     1     0     0     0     0     0     1      1
# f1_3         1     1     0     1     0     0     1     0     1      1
# f1_4         1     1     1     2     1     0     1     2     0      1
# f1_5         0     2     2     1     0     0     0     0     0      1
# Subj-496     1     0     1     0     0     0     1     2     1      1
# Subj-497     1     1     0     0     1     0     1     0     1      0
# Subj-498     0     2     1     1     0     1     1     0     0      0
# Subj-499     2     0     1     1     1     0     0     0     0      1
# Subj-500     1     0     0     2     0     0     0     1     0      2

```

### Note about FamMode

Currently, we support three ```FamMode``` including ```4-members```, ```10-members```, and ```20-members```. If ```nFam``` is not specified, then we only simulate unrelated subjects.

## Simulate genotype missing
We follow PLINK to use -9 to indicate genotype missing.
```
MissingRate = 0.05
indexMissing = sample(length(GenoMat), MissingRate * length(GenoMat))
GenoMat[indexMissing] = -9
#          SNP_1 SNP_2 SNP_3 SNP_4 SNP_5 SNP_6 SNP_7 SNP_8 SNP_9 SNP_10
# f1_1         0     1     2     2     1     0     0     0     1      1
# f1_2         1     1     1     0     0     0     0     0     1      1
# f1_3         1     1     0     1     0    -9     1     0     1      1
# f1_4         1     1     1     2     1     0     1     2     0      1
# f1_5         0     2     2     1    -9     0     0     0     0      1
# Subj-496     1     0     1     0     0    -9     1     2     1      1
# Subj-497     1     1     0     0     1     0     1     0     1      0
# Subj-498     0     2     1     1     0     1     1     0     0      0
# Subj-499     2     0     1     1     1     0     0     0     0      1
# Subj-500     1     0     0     2     0     0     0     1     0      2
```

## Make PLINK PED/MAP files using the genotype matrix
```
extDir = system.file("extdata", package = "GRAB")
extPrefix = paste0(extDir, "/simuPLINK")
GRAB.makePlink(GenoMat, extPrefix)
```

If you have installed PLINK and PLINK2 softwares, then you can use the following commands to generate PLINK bfiles and BGEN files. 

```
setwd(extDir)
system("plink --file simuPLINK --make-bed --out simuPLINK")
system("plink --bfile simuPLINK --recode A --out simuRAW")
system("plink2 --bfile simuPLINK --export bgen-1.2 bits=8 ref-first --out simuBGEN  # UK Biobank use 'ref-first'")
system("bgenix -g simuBGEN.bgen -index")
```


## About rare variants simulation

Given arguments of ```MaxMAF``` and ```MinMAF```, function ```GRAB.SimuGMat``` can simulate 
- common variants (MAF > 5%) and 
- low frequency variants (1% < MAF < 5%). 

For rare variants (MAF < 1%), we suggest using real genotype data for simulation purpose. 
