---
layout: default
title: Installation
nav_order: 2
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
has_children: true
---

How to install and run SAIGE and SAIGE-GENE


## Install SAIGE/SAIGE-GENE

### List of dependencies:

* R-3.6.1, gcc >= 5.4.0, cmake 3.14.1, [cget](https://cget.readthedocs.io/en/latest/src/intro.html#installing-cget)
* R packages: "R.utils", "Rcpp", "RcppParallel", "RcppArmadillo", "data.table", "RcppEigen", "Matrix", "methods", "BH", "optparse", "SPAtest", "SKAT","MetaSKAT"
* /extdata/install_packages.R can be used to install the R packages
* SAIGE v0.39.2 depends on the SPAtest v3.1.2
* MetaSKAT is currently not available on CRAN. Please install it from github using R
  ```
   devtools::install_github("leeshawn/MetaSKAT")
  ```

###  Install SAIGE from conda

#### Warning: please do not use this bioconda version for bgen input. We are working on the issue.

![r-saige](https://anaconda.org/bioconda/r-saige/badges/version.svg)
![latest_update](https://anaconda.org/bioconda/r-saige/badges/latest_release_date.svg)

To install saige from conda simply create environment with latest version of R and saige:
```
conda create -n saige -c conda-forge -c bioconda "r-base>=4.0" r-saige
conda activate saige
```

More info on [r-saige conda package](https://anaconda.org/bioconda/r-saige) and available versions can be found in the [issue #272](https://github.com/weizhouUMICH/SAIGE/issues/272).

###  Install SAIGE using the conda environment

1. Create a conda environment using
     ([conda environment file](https://github.com/weizhouUMICH/SAIGE/blob/master/conda_env/environment-RSAIGE.yml))
     Here is a link to download the [conda environment file](https://raw.githubusercontent.com/weizhouUMICH/SAIGE/master/conda_env/environment-RSAIGE.yml)

     After downloading environment-RSAIGE.yml, run following command
     ```
       conda env create -f environment-RSAIGE.yml
   ```

2. Activate the conda environment RSAIGE

     ```
       conda activate RSAIGE
       FLAGPATH=`which python | sed 's|/bin/python$||'`
       export LDFLAGS="-L${FLAGPATH}/lib"
       export CPPFLAGS="-I${FLAGPATH}/include"
     ```
Please make sure to set up the LDFLAGS and CPPFLAGS using export (the last two command lines), so libraries can be linked correctly when the SAIGE source code is compiled. Note: [Here](https://github.com/weizhouUMICH/SAIGE/blob/master/conda_env/createCondaEnvSAIGE_steps.txt) are the steps to create the conda environment file

3. Open R, run following script to install the MetaSKAT R library.

     ```
       devtools::install_github("leeshawn/MetaSKAT")
     ```

4. Install SAIGE from the source code.

     Method 1:

     ```
       src_branch=master
       repo_src_url=https://github.com/weizhouUMICH/SAIGE
       git clone --depth 1 -b $src_branch $repo_src_url

       R CMD INSTALL --library=path_to_final_SAIGE_library SAIGE
     ```

     When call SAIGE in R, set lib.loc=path_to_final_SAIGE_library

     ```
       library(SAIGE, lib.loc=path_to_final_SAIGE_library)
     ```

    Method 2:

    Open R. Run

    ```
      devtools::install_github("weizhouUMICH/SAIGE")
    ```
