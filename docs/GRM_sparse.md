---
layout: default
title: Sparse GRM
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
parent: Genetic Relation Matrix (GRM)
has_children: false
---

# How to make a Sparse GRM file

## About function ```getSparseGRM```

- ```GRAB``` package includes a function ```getSparseGRM```, which implicitly uses tool ```GCTA``` software (gcta_1.93.1beta, [link](https://cnsgenomics.com/software/gcta/#Overview)) to make a ```SparseGRMFile``` to be passed to function ```GRAB.NullModel```. 

- As required by ```GCTA``` software, the function ```getSparseGRM``` is only supported in **Linux OS** and **PLINK binary files with the same prefix** are required. 

- It has been reported that if the PLINK files include more than one ancestry, the GRM estimation might be highly inaccurate.

## Step 1: Prepare PLINK binary files
```
GenoFile = system.file("extdata", "simuPLINK.bed", package = "GRAB")
PlinkPrefix = tools::file_path_sans_ext(GenoFile)   # remove file extension
```

## Step 2: RUN ```getTempFilesFullGRM``` to get temporary files
- Besides ```PlinkPrefix```, arguments ```nPartsGRM``` and ```partParallel``` are required.
- The GRM calculation is split to ```nPartsGRM``` parts for parallel computation. 
- For UK Biobank data analysis with ~ 500K samples, we recommend setting nPartsGRM = 250 and using multiple CPU cores in High Performance Cluster.
- If not specified, the temporary files are in ```system.file("SparseGRM", "temp", package = "GRAB"))```. Users can set ```tempDir``` to change it.
- If the sample size > 100K, then the temporary files might need a large amount of space.
- Other arguments includes
  - ```subjData```: a character vector to specify subject IDs to retain (i.e. IID). Default is NULL, i.e. all subjects are retained in sparse GRM.
  - ```minMafGRM```: Minimal value of MAF cutoff to select markers (from PLINK files) to make sparse GRM. (default=0.01)
  - ```maxMissingGRM```: Maximal value of missing rate to select markers (from PLINK files) to make sparse GRM. (default=0.1)
  - ```threadNum```: Number of threads (CPU cores) to use.
```
nPartsGRM = 2;
for(partParallel in 1:nPartsGRM){
  getTempFilesFullGRM(PlinkPrefix, 
                      nPartsGRM = nPartsGRM, 
                      partParallel = partParallel)
}
```

## Step 3: RUN ```getSparseGRM``` to combine the temporary files
- Function ```getSparseGRM``` can search the temporary files from ```tempDir``` based on arguments ```minMafGRM``` and ```maxMissingGRM```.
- Argument ```relatednessCutoff``` is the cutoff for sparse GRM, only kinship coefficient greater than this cutoff will be retained in sparse GRM. (default=0.05)
- If argument ```rm.tempFiles``` is set as ```TRUE```, then all temporary files will be removed.
```
SparseGRMFile = system.file("SparseGRM", "SparseGRM.txt", package = "GRAB")
getSparseGRM(PlinkPrefix, 
             nPartsGRM = nPartsGRM, 
             SparseGRMFile = SparseGRMFile,
             relatednessCutoff = 0.05)
```
