---
layout: default
title: Data Simulation 
nav_order: 5
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
has_children: true
has_toc: true
---

# Data simulation using GRAB package

The example data in the directory of ```system.file("extdata", package = "GRAB")``` were simulated using the functions in ```GRAB``` package. 

## Genotype Simulation

The document demonstrates how to 
- simulate a genotype matrix for unrelated and related subjects
- make PLINK binary files using the genotype matrix
- make BGEN files using PLINK binary files

## Phenotype Simulation

The document demonstrates how to 
- simulate binary, quantitative, time-to-event, and ordinal categorical phenotypes
- simulate phenotypes with random effect following a multivariate normal distribution
- simulate phenotypes using real genotype data (given PLINK binary files)

