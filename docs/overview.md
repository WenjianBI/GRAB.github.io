---
layout: default
title: Overview
nav_order: 2
description: "Overview of GRAB package."
has_children: true
has_toc: false
---

# Overview of GRAB package 

GRAB package includes multiple approaches to analyze

- Binary phenotype (SAIGE, SAIGE-GENE)
- Quantitative phenotype (SAIGE, SAIGE-GENE)
- Ordianl categorical phenotype (POLMM, POLMM-GENE)
- Time-to-event phenotype (SPACox)

All of these approaches share the same analysis framework including the following three steps

- Step 0: Make a Sparse GRM or prepare PLINK binary files for Dense GRM
- Step 1: Fit a null model including phenotype, covariates, and GRM (if applied)
- Step 2: Conduct single-variant or set-based tests to associate phenotype and genotype

