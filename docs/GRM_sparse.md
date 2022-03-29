---
layout: default
title: Sparse GRM
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Genetic Relation Matrix (GRM)
has_children: false
---

# How to make a Sparse GRM file

## If using function ```getSparseGRM```

- ```GRAB``` package includes a function ```getSparseGRM```, which implicitly uses tool ```GCTA``` software (gcta_1.93.1beta, [link](https://cnsgenomics.com/software/gcta/#Overview)) to make a ```SparseGRMFile``` to be passed to function ```GRAB.NullModel```. 

- As required by ```GCTA``` software, the function ```getSparseGRM``` is only supported in **Linux OS** and **PLINK binary files with the same prefix** are required. 

- It has been reported that if the PLINK files include more than one ancestry, the GRM estimation might be highly inaccurate.

## Start-up examples
```
## Input data:
GenoFile = system.file("extdata", "simuPLINK.bed", package = "GRAB")
PlinkPrefix = tools::file_path_sans_ext(GenoFile)   # remove file extension
nPartsGRM = 2;   # we recommend setting nPartsGRM = 250 for UK Biobank data analysis with ~ 500K samples.

# Step 1:
# We strongly recommend parallel computing in high performance clusters (HPC). 
for(partParallel in 1:nPartsGRM){
  getTempFilesFullGRM(PlinkPrefix, nPartsGRM, partParallel)  # this function is only supported in Linux OS
}

# After step 1, the temporary files are in tempDir (default: system.file("SparseGRM", "temp", package = "GRAB")), which might needs a large amount of space if the sample size > 100K.

# Step 2:
# Combine files in Step 1 to make a SparseGRMFile,
tempDir = system.file("SparseGRM", "temp", package = "GRAB")
SparseGRMFile = gsub("temp", "SparseGRM.txt", tempDir)
getSparseGRM(PlinkFile, nPartsGRM, SparseGRMFile)
```
