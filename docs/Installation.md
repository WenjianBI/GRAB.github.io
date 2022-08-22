---
layout: default
title: Installation
nav_order: 3
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
has_children: false
has_toc: false
---

The ```GRAB``` package can be installed in R or via docker. 

## Install GRAB package via docker

UK Biobank Research Analysis Platform (RAP) supports docker installation.

## Install GRAB package in R (current version 0.0.3.2)

### In **Linux** operation system

```
library(remotes)  
install_github("GeneticAnalysisinBiobanks/GRAB")  # The INSTALL_opts is required in Windows OS.
library(GRAB)
```

### In **Windows** operation system

```
library(remotes)
options(download.file.method = "wininet")
install_github("GeneticAnalysisinBiobanks/GRAB", INSTALL_opts=c("--no-multiarch"))  # The INSTALL_opts is required in Windows OS.
library(GRAB)
```

### Linux environment

```
> sessionInfo()
R version 4.0.5 (2021-03-31)
Platform: x86_64-conda-linux-gnu (64-bit)
Running under: CentOS Linux 7 (Core)

Matrix products: default
BLAS/LAPACK: /home/wenjianb/.conda/envs/myEnvR4.0/lib/libopenblasp-r0.3.20.so

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C
 [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8
 [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8
 [7] LC_PAPER=en_US.UTF-8       LC_NAME=C
 [9] LC_ADDRESS=C               LC_TELEPHONE=C
[11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base

other attached packages:
 [1] GRAB_0.0.3.2       Rcpp_1.0.9         dplyr_1.0.9        tidyr_1.2.0
 [5] SKAT_2.2.4         RSpectra_0.16-1    SPAtest_3.1.2      Matrix_1.4-1
 [9] ordinal_2019.12-10 remotes_2.4.2

loaded via a namespace (and not attached):
 [1] compiler_4.0.5      pillar_1.8.1        prettyunits_1.1.1
 [4] tools_4.0.5         pkgbuild_1.3.1      lifecycle_1.0.1
 [7] tibble_3.1.8        lattice_0.20-45     ucminf_1.1-4
[10] pkgconfig_2.0.3     rlang_1.0.4         cli_3.3.0
[13] DBI_1.1.3           curl_4.3.2          withr_2.5.0
[16] generics_0.1.3      vctrs_0.4.1         rprojroot_2.0.3
[19] grid_4.0.5          tidyselect_1.1.2    glue_1.6.2
[22] R6_2.5.1            processx_3.6.1      fansi_1.0.3
[25] callr_3.7.0         purrr_0.3.4         magrittr_2.0.3
[28] ps_1.7.1            MASS_7.3-57         assertthat_0.2.1
[31] numDeriv_2016.8-1.1 utf8_1.2.2          RcppParallel_5.1.5
[34] crayon_1.5.1
```

### Windows Environment

```
> sessionInfo()
R version 4.1.0 (2021-05-18)
Platform: x86_64-w64-mingw32/x64 (64-bit)
Running under: Windows 10 x64 (build 19044)

Matrix products: default

locale:
[1] LC_COLLATE=English_United States.1252  LC_CTYPE=English_United States.1252    LC_MONETARY=English_United States.1252
[4] LC_NUMERIC=C                           LC_TIME=English_United States.1252    
system code page: 936

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
 [1] GRAB_0.0.3.2       Rcpp_1.0.9         dplyr_1.0.9        tidyr_1.2.0        SKAT_2.2.4         RSpectra_0.16-1    SPAtest_3.1.2     
 [8] Matrix_1.3-3       ordinal_2019.12-10 remotes_2.4.2     

loaded via a namespace (and not attached):
 [1] compiler_4.1.0      pillar_1.8.1        prettyunits_1.1.1   tools_4.1.0         pkgbuild_1.2.0      lifecycle_1.0.1     tibble_3.1.8       
 [8] lattice_0.20-44     ucminf_1.1-4        pkgconfig_2.0.3     rlang_1.0.4         cli_3.1.0           DBI_1.1.3           rstudioapi_0.13    
[15] curl_4.3.2          withr_2.5.0         generics_0.1.3      vctrs_0.4.1         rprojroot_2.0.2     grid_4.1.0          tidyselect_1.1.2   
[22] glue_1.6.2          R6_2.5.1            processx_3.5.2      fansi_1.0.3         callr_3.7.0         purrr_0.3.4         magrittr_2.0.3     
[29] ps_1.6.0            MASS_7.3-54         assertthat_0.2.1    numDeriv_2016.8-1.1 utf8_1.2.2          RcppParallel_5.1.5  crayon_1.5.1 
```


## Logs (to be updated):

v0.0.3.2 (March 12, 2022): xxxxx

v0.0.3.3 (March 15, 2022): xxxxx
