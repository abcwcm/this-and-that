# Notes for installing cellxgene

[cellxgene](https://github.com/chanzuckerberg/cellxgene-documentation/blob/main/README.md) is an interactive browser for single-cell data that is being developed by the CZI.

* Tutorials for [exploring data using cellxgene](https://github.com/chanzuckerberg/cellxgene-documentation/blob/main/explore-data/explorer-tutorials.md)
* [CZI's install help](https://github.com/chanzuckerberg/cellxgene-documentation/blob/main/desktop/install.md) -- this only installs the basic cellxgene browser -- we typically prefer to install it along with the [VIP tools](https://github.com/interactivereport/cellxgene_VIP) that allow for violin plots and more
* [collection of browsable public data sets](https://cellxgene.cziscience.com/)

Pre-requisites **on MacOS** are:

* **command line tools installed?**
  - if NOT, run `xcode-select --install` in the Terminal
* **conda installed?**
  - if NOT, do that first; see <https://docs.conda.io/projects/continuumio-conda/en/latest/user-guide/install/macos.html>
  
  ```
  curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh -O Miniconda3-latest-MacOSX-x86_64.sh
  bash Miniconda3-latest-MacOSX-x86_64.sh
  ### AFTER YOU INSTALL CONDA, RESTART THE TERMINAL! ####
  ```
  
* **R installed?**
 - if NOT, install R: download <https://cran.r-project.org/bin/macosx/base/R-4.0.4.pkg> and follow instructions  

Then, let's brace yourself for cellxgene VIP:

```
## cellxgene  VIP install
git clone https://github.com/interactivereport/cellxgene_VIP.git
cd cellxgene_VIP
#conda config --set channel_priority flexible
conda env create -n VIP -f VIP.macOS.yml
conda activate VIP
./config.macOS.sh
export LIBARROW_MINIMAL=false
#  ensure that the right instance of R is used.
# e.g. system-wide: /bin/R or /usr/bin/R ;
# local R under conda: ~/.conda/envs/VIP_conda_R/bin/R
which R

## DO CAIRO BEFORE ALL ELSE 
conda install -c anaconda cairo 
conda install -c conda-forge cairo 

## INSTALL PACKAGES
conda install -c anaconda cairo 
conda install -c conda-forge cairo 
R -q -e 'if(!require(devtools)) install.packages("devtools",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(Cairo)) install.packages("Cairo",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(foreign)) install.packages("foreign",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(ggpubr)) install.packages("ggpubr",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(ggrastr)) install.packages("ggrastr",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(arrow)) install.packages("arrow",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(Seurat)) install.packages("Seurat",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(rmarkdown)) install.packages("rmarkdown",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(tidyverse)) install.packages("tidyverse",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(viridis)) install.packages("viridis",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(hexbin)) install.packages("hexbin",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(ggforce)) install.packages("ggforce",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(fastmatch)) install.packages("fastmatch",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(RcppRoll)) install.packages("RcppRoll",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(BiocManager)) install.packages("BiocManager",repos = "http://cran.us.r-project.org", type="binary")'
R -q -e 'if(!require(fgsea)) BiocManager::install("fgsea")'
R -q -e 'if(!require(rtracklayer)) BiocManager::install("rtracklayer")'

# These should be already installed as dependencies of above packages
R -q -e 'if(!require(dbplyr)) devtools::install_version("dbplyr",version="1.0.2",repos = "http://cran.us.r-project.org")'
R -q -e 'if(!require(RColorBrewer)) devtools::install_version("RColorBrewer",version="1.1-2",repos = "http://cran.us.r-project.org")'
R -q -e 'if(!require(glue)) devtools::install_version("glue",version="1.4.2",repos = "http://cran.us.r-project.org")'
R -q -e 'if(!require(gridExtra)) devtools::install_version("gridExtra",version="2.3",repos = "http://cran.us.r-project.org")'
R -q -e 'if(!require(ggrepel)) devtools::install_version("ggrepel",version="0.8.2",repos = "http://cran.us.r-project.org")'
R -q -e 'if(!require(MASS)) devtools::install_version("MASS",version="7.3-51.6",repos = "http://cran.us.r-project.org")'
R -q -e 'if(!require(data.table)) devtools::install_version("data.table",version="1.13.0",repos = "http://cran.us.r-project.org")'


###
# Run cellxgene on test file
cellxgene launch https://cellxgene-example-data.czi.technology/pbmc3k.h5ad


conda activate VIP
cellxgene launch our_data.h5ad
```

# References for `cellxgene`

* [Bioarxiv manuscript of `cellxgene`](https://www.biorxiv.org/content/10.1101/2021.04.05.438318v1)
* [Documentation for `cellxgene` Desktop](https://docs.cellxgene.cziscience.com/desktop/desktop-overview)
* [Bioarxiv manuscript of `cellxgene VIP`](https://www.biorxiv.org/content/10.1101/2020.08.28.270652v1)
* [Documentation for `cellxgene VIP`](https://interactivereport.github.io/cellxgene_VIP/tutorial/docs/)
