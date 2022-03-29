---
layout: default
title: Sparse GRM
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Genetic Relation Matrix (GRM)
has_children: false
---

# How to make a Sparse GRM file

## Start-up examples
```
## Input data:
GenoFile = system.file("extdata", "example.bed", package = "GRAB")
PlinkFile = tools::file_path_sans_ext(GenoFile)   # remove file extension
nPartsGRM = 2;   # we recommend setting nPartsGRM = 250 for UK Biobank data analysis with 500K samples.

# Step 1:
# We strongly recommend parallel computing in high performance clusters (HPC). 
for(partParallel in 1:nPartsGRM){
  getTempFilesFullGRM(PlinkFile, nPartsGRM, partParallel)  # this function is only supported in Linux OS
}

# After step 1, the temporary files are in tempDir (default: system.file("SparseGRM", "temp", package = "GRAB")), which might needs a large amount of space if the sample size > 100K.

# Step 2:
# Combine files in Step 1 to make a SparseGRMFile,
tempDir = system.file("SparseGRM", "temp", package = "GRAB")
SparseGRMFile = gsub("temp", "SparseGRM.txt", tempDir)
getSparseGRM(PlinkFile, nPartsGRM, SparseGRMFile)
```
