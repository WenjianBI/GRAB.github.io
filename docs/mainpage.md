---
layout: default
title: Home
nav_order: 1
description: "Main page for GRAB package."
permalink: /
---

```GRAB``` is an R package developed using ```Rcpp``` for **G**enome-wide **R**obust **A**nalaysis designed for **B**iobank data **(GRAB)**. The package includes multiple approaches which

- account for sample relatedness using **G**enetic **R**elationship **M**atrix **(GRM)**
- support multiple phenotypes including 
  - quantitative trait
  - binary trait 
  - time-to-event trait 
  - ordinal categorical trait
- handle unbalanced phenotypic distribution (e.g. case-control imbalance of binary traits)
- are computationally efficient for large data sets (e.g. UK Biobank)
- perform single-variant and set-based association tests 

For set-based association tests, ```GRAB``` package
- performs Burden test, SKAT, and SKAT-O 
- allows for tests on multiple minor allele frequencies cutoffs and functional annotations
- allows for specifying weights for markers in the set-based tests
- performs conditional analysis to identify associations independent from nearly GWAS signals

The package takes genotype file input in the following formats
- ```PLINK``` binary files (.bed, .bim, .fam)
- ```BGEN``` (.bgen, .bgi, .sample)

## Supported Approaches

### POLMM / POLMM-GENE:
- Support ordinal categorical trait
- Single-variant / set-based tests
- Can account for sample relatedness
- Reference
  - Bi, Wenjian, Wei Zhou, Rounak Dey, Bhramar Mukherjee, Joshua N. Sampson, and Seunggeun Lee. **Efficient mixed model approach for large-scale genome-wide association studies of ordinal categorical phenotypes.** The American Journal of Human Genetics 108, no. 5 (2021): 825-839.
  - Bi, Wenjian, Wei Zhou, Peipei Zhang, Yaoyao Sun, Weihua Yue, and Seunggeun Lee. **Scalable mixed model approaches for set-based association studies on large-scale categorical data analysis and its application to 450k exome sequencing data in UK Biobank.** To be submitted.

### SPACox:
- Support Time-to-event trait
- Single-variant tests
- Cannot account for sample relatedness
- Bi, Wenjian, Lars G. Fritsche, Bhramar Mukherjee, Sehee Kim, and Seunggeun Lee. **A fast and accurate method for genome-wide time-to-event data analysis and its application to UK Biobank.** The American Journal of Human Genetics 107, no. 2 (2020): 222-233.

### SAIGE / SAIGE-GENE (supported later):
- Support quantitative and binary trait
- Single-variant / set-based tests
- Can account for sample relatedness
- Reference
  - Zhou, Wei, Jonas B. Nielsen, Lars G. Fritsche, Rounak Dey, Maiken E. Gabrielsen, Brooke N. Wolford, Jonathon LeFaive et al. **Efficiently controlling for case-control imbalance and sample relatedness in large-scale genetic association studies.** Nature genetics 50, no. 9 (2018): 1335-1341.
  - Zhou, Wei, Zhangchen Zhao, Jonas B. Nielsen, Lars G. Fritsche, Jonathon LeFaive, Sarah A. Gagliano Taliun, Wenjian Bi et al. **Scalable generalized linear mixed model for region-based association tests in large biobanks and cohorts.** Nature genetics 52, no. 6 (2020): 634-639.

## License
```GRAB``` is distributed under an GPL license.

## Contact
If you have any questions about ```GRAB``` package, please contact **wenjianb@pku.edu.cn**
