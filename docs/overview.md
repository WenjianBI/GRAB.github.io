---
layout: default
title: Overview
nav_order: 2
description: "Overview of GRAB package."
has_children: false
has_toc: false
---

# Overview of GRAB package 

The ```GRAB``` package is mainly designed for **genome-wide association analyses**. In addition, it can also be used to **simulate genotype/phenotype data**, **to calculate sparse GRM**, and **to read in genotype from PLINK/BGEN files**.  

## Genome-wide association analyses

The ```GRAB``` package supports multiple phenotypes including

- Binary trait (SAIGE, SAIGE-GENE)
- Quantitative trait (SAIGE, SAIGE-GENE)
- Ordianl categorical trait (POLMM, POLMM-GENE)
- Time-to-event trait (SPACox)

All of these approaches share the same analysis framework including the following three steps

- Step 0: Make a Sparse GRM or prepare PLINK binary files for Dense GRM.
- Step 1: Fit a null model including phenotype, covariates, and GRM (if applied).
- Step 2: Conduct single-variant or set-based tests to identify marker or marker-set (e.g. gene) associated with traits.

## Data Simulation

The ```GRAB``` package can be used to simulate genotype/phenotype data

## Genetic Relationship Matrix (GRM)

The ```GRAB``` package supports sparse GRM to adjust for family relatedness.



