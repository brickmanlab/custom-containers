FROM rocker/tidyverse:3.6.2

RUN apt-get update && apt-get install -y python3-pip
RUN echo 'RETICULATE_PYTHON="/usr/bin/python3"' > .Renviron

# Seurat
RUN Rscript -e 'BiocManager::install("multtest")'
RUN Rscript -e 'install.packages("Seurat", version = "3.1.3")'
