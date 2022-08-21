---
layout: default
title: Overview
nav_order: 2
description: "Overview of GRAB package."
has_children: false
has_toc: false
---

# Overview of GRAB package 

The ```GRAB``` package is mainly designed for **genome-wide association studies (GWAS)** including both single-variant and set-based analysis. In addition, it can also be used 
- to simulate genotype/phenotype data, 
- to calculate sparse GRM, and 
- to read in genotype from PLINK/BGEN files.  

## Genome-wide association studies

The ```GRAB``` package supports multiple phenotypes including

- Binary trait (SAIGE / SAIGE-GENE),
- Quantitative trait (SAIGE / SAIGE-GENE),
- Ordianl categorical trait (POLMM / POLMM-GENE), and
- Time-to-event trait (SPACox)

All of these approaches share the same analysis framework including the following three steps

- Step 1: Fit a null model including phenotype, covariates, and GRM (if applied).
- Step 2: Conduct single-variant or set-based tests to identify marker or marker-set (e.g. gene) associated with traits.

## Preparation before using GRAB package

One of the main features for ```GRAB``` package is to support using genotype data to adjust for sample relatedness via genetic relationship matrix (GRM). PLINK binary files including high-quality genotyped variants are required for that purpose. In UK Biobank real data analysis, we used the following cutoffs in PLINK to select ~ 340K SNPs for White British subjects.

```
--maf 0.05
--indep-pairwise 500 50 0.2
```

If the sample size in analysis is greater than 100,000, we recommend using sparse GRM (instead of dense GRM) to adjust for sample relatedness. Function ```getSparseGRM``` uses ```GCTA``` software (gcta_1.93.1beta) to make a ```SparseGRMFile``` to be passed to function ```GRAB.NullModel```. This function can only support Linux and PLINK files as required by ```GCTA``` software. To make a ```SparseGRMFile```, two steps are needed as below. 

- Step 1: Run ```getTempFilesFullGRM``` to save temporary files to tempDir.

- Step 2: Run ```getSparseGRM``` to combine the temporary files to make a SparseGRMFile to be passed to function GRAB.NullModel.

Users can customize parameters including ```(minMafGRM, maxMissingGRM, nPartsGRM)```, but functions ```getTempFilesFullGRM``` and ```getSparseGRM``` should use the same ones. Otherwise, package ```GRAB``` cannot accurately identify temporary files.

The GRAB package supports the below genotype file format for association studies

- ```PLINK``` binary files (.bed, .bim, .fam)
- ```BGEN``` (.bgen, .bgi, .sample)

## Data simulation

The ```GRAB``` package can be used to simulate genotype/phenotype data.

## Genetic Relationship Matrix (GRM)

The ```GRAB``` package supports sparse GRM to adjust for family relatedness. Functions ```getTempFilesFullGRM()``` and ```getSparseGRM()``` can be used to generate a sparse GRM using PLINK files.

## Read in genotype data

The ```GRAB``` package can also be used to read in genotype data from PLINK/BGEN files.

