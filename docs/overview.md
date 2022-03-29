---
layout: default
title: Overview
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
has_children: true
has_toc: false
---

# Overview of GRAB package 

GRAB package includes multiple approaches to analyze

- Binary phenotype
- Quantitative phenotype
- Ordianl categorical phenotype
- Time-to-event phenotype

All of these approaches share the same analysis framework including the following three steps

- Step 0: Make a Sparse GRM or prepare PLINK/BGEN files for Dense GRM
- Step 1: Fit a null model including phenotype, covariates, and GRM (if applied)
- Step 2: Conduct score testing to associate phenotype and genotype

