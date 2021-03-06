<h2 align="center">Datascience Stacks</h2>
<p align="center">Build docker image for reproducible datescience</p>

<p align="center">Jingcheng Yang [yjcyxky@163.com]</p>


## Content
- [Selecting an Image](#Selecting-an-Image)
- [How to submit a pull request](#How-to-submit-a-pull-request)
- [Contributors](#contributors)


## Selecting an Image

* [Core Stacks](#core-stacks)
* [Image Relationships](#image-relationships)
* [Community Stacks](#community-stacks)

Using one of the Jupyter Docker Stacks requires two choices:

1. Which Docker image you wish to use
2. How you wish to start Docker containers from that image

This section provides details about the first.

### Core Stacks

The Jupyter team maintains a set of Docker image definitions in the [https://github.com/jupyter/docker-stacks](https://github.com/jupyter/docker-stacks) GitHub repository. The following sections describe these images including their contents, relationships, and versioning strategy.

#### jupyter/base-notebook

[Source on GitHub](https://github.com/jupyter/docker-stacks/tree/master/base-notebook)
| [Dockerfile commit history](https://github.com/jupyter/docker-stacks/commits/master/base-notebook/Dockerfile)
| [Docker Hub image tags](https://hub.docker.com/r/jupyter/base-notebook/tags/)

`jupyter/base-notebook` is a small image supporting the [options common across all core stacks](common.md). It is the basis for all other stacks.

* Minimally-functional Jupyter Notebook server (e.g., no [pandoc](https://pandoc.org/) for saving notebooks as PDFs)
* [Miniconda](https://conda.io/miniconda.html) Python 3.x in `/opt/conda`
* No preinstalled scientific computing packages
* Unprivileged user `jovyan` (`uid=1000`, configurable, see options) in group `users` (`gid=100`) with ownership over the `/home/jovyan` and `/opt/conda` paths
* `tini` as the container entrypoint and a `start-notebook.sh` script as the default command
* A `start-singleuser.sh` script useful for launching containers in JupyterHub
* A `start.sh` script useful for running alternative commands in the container (e.g. `ipython`, `jupyter kernelgateway`, `jupyter lab`)
* Options for a self-signed HTTPS certificate and passwordless sudo

#### jupyter/minimal-notebook

[Source on GitHub](https://github.com/jupyter/docker-stacks/tree/master/minimal-notebook)
| [Dockerfile commit history](https://github.com/jupyter/docker-stacks/commits/master/minimal-notebook/Dockerfile)
| [Docker Hub image tags](https://hub.docker.com/r/jupyter/minimal-notebook/tags/)

`jupyter/minimal-notebook` adds command line tools useful when working in Jupyter applications.

* Everything in `jupyter/base-notebook`
* [Pandoc](http://pandoc.org) and [TeX Live](https://www.tug.org/texlive/) for notebook document conversion
* [git](https://git-scm.com/), [emacs](https://www.gnu.org/software/emacs/), [jed](https://www.jedsoft.org/jed/), [nano](https://www.nano-editor.org/), tzdata, and unzip

#### jupyter/r-notebook

[Source on GitHub](https://github.com/jupyter/docker-stacks/tree/master/r-notebook)
| [Dockerfile commit history](https://github.com/jupyter/docker-stacks/commits/master/r-notebook/Dockerfile)
| [Docker Hub image tags](https://hub.docker.com/r/jupyter/r-notebook/tags/)

`jupyter/r-notebook` includes popular packages from the R ecosystem.

* Everything in `jupyter/minimal-notebook` and its ancestor images
* The [R](https://www.r-project.org/) interpreter and base environment
* [IRKernel](https://irkernel.github.io/) to support R code in Jupyter notebooks
* [tidyverse](https://www.tidyverse.org/) packages, including [ggplot2](http://ggplot2.org/), [dplyr](http://dplyr.tidyverse.org/), [tidyr](http://tidyr.tidyverse.org/), [readr](http://readr.tidyverse.org/), [purrr](http://purrr.tidyverse.org/), [tibble](http://tibble.tidyverse.org/), [stringr](http://stringr.tidyverse.org/), [lubridate](http://lubridate.tidyverse.org/), and [broom](https://cran.r-project.org/web/packages/broom/vignettes/broom.html) from [conda-forge](https://conda-forge.github.io/feedstocks)
* [plyr](https://cran.r-project.org/web/packages/plyr/index.html), [devtools](https://cran.r-project.org/web/packages/devtools/index.html), [shiny](https://shiny.rstudio.com/), [rmarkdown](http://rmarkdown.rstudio.com/), [forecast](https://cran.r-project.org/web/packages/forecast/forecast.pdf), [rsqlite](https://cran.r-project.org/web/packages/RSQLite/index.html), [reshape2](https://cran.r-project.org/web/packages/reshape2/reshape2.pdf), [nycflights13](https://cran.r-project.org/web/packages/nycflights13/index.html), [caret](http://topepo.github.io/caret/index.html), [rcurl](https://cran.r-project.org/web/packages/RCurl/index.html), and [randomforest](https://cran.r-project.org/web/packages/randomForest/randomForest.pdf) packages from [conda-forge](https://conda-forge.github.io/feedstocks)

#### jupyter/scipy-notebook

[Source on GitHub](https://github.com/jupyter/docker-stacks/tree/master/scipy-notebook)
| [Dockerfile commit history](https://github.com/jupyter/docker-stacks/commits/master/scipy-notebook/Dockerfile)
| [Docker Hub image tags](https://hub.docker.com/r/jupyter/scipy-notebook/tags/)

`jupyter/scipy-notebook` includes popular packages from the scientific Python ecosystem.

* Everything in `jupyter/minimal-notebook` and its ancestor images
* [pandas](https://pandas.pydata.org/), [numexpr](https://github.com/pydata/numexpr), [matplotlib](https://matplotlib.org/), [scipy](https://www.scipy.org/), [seaborn](https://seaborn.pydata.org/), [scikit-learn](http://scikit-learn.org/stable/), [scikit-image](http://scikit-image.org/), [sympy](http://www.sympy.org/en/index.html), [cython](http://cython.org/), [patsy](https://patsy.readthedocs.io/en/latest/), [statsmodel](http://www.statsmodels.org/stable/index.html), [cloudpickle](https://github.com/cloudpipe/cloudpickle), [dill](https://pypi.python.org/pypi/dill), [numba](https://numba.pydata.org/), [bokeh](https://bokeh.pydata.org/en/latest/), [sqlalchemy](https://www.sqlalchemy.org/), [hdf5](http://www.h5py.org/), [vincent](http://vincent.readthedocs.io/en/latest/), [beautifulsoup](https://www.crummy.com/software/BeautifulSoup/), [protobuf](https://developers.google.com/protocol-buffers/docs/pythontutorial), and [xlrd](http://www.python-excel.org/) packages
* [ipywidgets](https://ipywidgets.readthedocs.io/en/stable/) for interactive visualizations in Python notebooks
* [Facets](https://github.com/PAIR-code/facets) for visualizing machine learning datasets

#### pydatascience-notebook

<p align="left">
<img src="https://github.com/jupyter-datascience/datascience-stacks/workflows/Build%20&%20Publish%20pydatascience-notebook/badge.svg" alt="Build Status">
<a href="https://hub.docker.com/r/choppydocker/pydatascience-notebook/tags/" title="Get your own version badge on microbadger.com"><img src="https://images.microbadger.com/badges/version/choppydocker/pydatascience-notebook.svg"></a>
</p>

[Source on GitHub](https://github.com/jupyter-datascience/datascience-stacks/tree/master/pydatascience-notebook)
| [Dockerfile commit history](https://github.com/jupyter-datascience/datascience-stacks/commits/master/pydatascience-notebook/Dockerfile)
| [Docker Hub image tags](https://hub.docker.com/r/choppydocker/pydatascience-notebook/tags/)

`choppydocker/pydatascience-notebook` includes popular packages from the scientific Python ecosystem.

* Everything in `jupyter/scipy-notebook` and its ancestor images
* [plotly](http://plotly.github.io/), mygene

#### rdatascience-notebook

<p align="left">
<img src="https://github.com/jupyter-datascience/datascience-stacks/workflows/Build%20&%20Publish%20rdatascience-notebook/badge.svg" alt="Build Status">
<a href="https://hub.docker.com/r/choppydocker/rdatascience-notebook/tags/" title="Get your own version badge on microbadger.com"><img src="https://images.microbadger.com/badges/version/choppydocker/rdatascience-notebook.svg"></a>
</p>

[Source on GitHub](https://github.com/jupyter-datascience/datascience-stacks/tree/master/rdatascience-notebook)
| [Dockerfile commit history](https://github.com/jupyter-datascience/datascience-stacks/commits/master/rdatascience-notebook/Dockerfile)
| [Docker Hub image tags](https://hub.docker.com/r/choppydocker/rdatascience-notebook/tags/)

`choppydocker/rdatascience-notebook` includes popular packages from the scientific Python ecosystem.

* Everything in `jupyter/r-notebook` and its ancestor images
* [bioconductor-maftools](https://bioconductor.org/packages/3.10/bioc/html/maftools.html), cookiecutter, maftools, glmnet, survival, survminer, complexheatmap, survivalroc, clusterprofiler, survcomp, rms, e1071, plot3d, sva, factominer, factoextra, copynumber, mcpcounter, forestplot, comparec, circlize, affy, limma, impute, geoquery, gridgraphics, ggpubr, data.table, wgcna, mygene, annotables, pathview, ggiraph, scatterplot3d, base, dendextend, colorspace, ggcorrplot, ggdendro, gplots, gmodels, survrm2, nmf, biomart, keras, tensorflow, plotly, shinyjs, shinydashboard, shinycssloaders, shinywidgets, rlang, rcolorbrewer, lattice, scales, leaflet

#### mldatascience-notebook

<p align="left">
<img src="https://github.com/jupyter-datascience/datascience-stacks/workflows/Build%20&%20Publish%20mldatascience-notebook/badge.svg" alt="Build Status">
<a href="https://hub.docker.com/r/choppydocker/mldatascience-notebook/tags/" title="Get your own version badge on microbadger.com"><img src="https://images.microbadger.com/badges/version/choppydocker/mldatascience-notebook.svg"></a>
</p>

[Source on GitHub](https://github.com/jupyter-datascience/datascience-stacks/tree/master/mldatascience-notebook)
| [Dockerfile commit history](https://github.com/jupyter-datascience/datascience-stacks/commits/master/mldatascience-notebook/Dockerfile)
| [Docker Hub image tags](https://hub.docker.com/r/choppydocker/mldatascience-notebook/tags/)

`choppydocker/mldatascience-notebook` includes popular packages from the scientific Python ecosystem.

* Everything in `jupyter/scipy-notebook` and its ancestor images
* [keras](https://github.com/keras-team/keras), [pytorch](http://pytorch.org/)


## How to submit a pull request
Before you submit a pull request, you need to test your Dockerfile.

Steps:
1. Change to the subdirectory, and follow the following steps.
2. Add a new package into Dockerfile
3. Run `make build`
4. Check the building result, if no exception exists, then you can run `git add *` to cache the modification.
5. Repeat Step 1, until all packages you wanted have been added into the Dockerfile
6. If you can build a new image successfully, then you can submit a pull request to `master` branch.
7. After we review your pull request, we will merge the pull request into `master` branch, then a building action will run until finished or failed.


## Contributors
- Jingcheng Yang [yjcyxky@163.com]
- Jun Shang [shangjunv@163.com]
