FROM rocker/geospatial:latest

MAINTAINER "edzerpebesma" edzer.pebesma@uni-muenster.de

## Add CRAN packages:
RUN R -q -e 'install.packages(c("R2BayesX", "cubelyr", "dbscan", "hglm", "igraph", "lme4", "lmtest", "matrixStats", "mgcv", "rgeoda", "rnaturalearth", "rnaturalearthdata", "spData", "stars"))'

# 0. install book source files:
RUN git clone https://github.com/edzer/sdsr.git
RUN mv sdsr /home/rstudio

## 1. download & install sdsr data:
RUN wget -q https://uni-muenster.sciebo.de/s/8mEbeHPOX9GdAYn/download -O sds.zip
RUN unzip -q sds.zip
RUN cp -r sds/aq /home/rstudio/sdsr
RUN rm -fr sds.zip sds
RUN chown -R rstudio:rstudio /home/rstudio/*

## 2. spDataLarge:
RUN R -q -e 'options(timeout = 600); install.packages("spDataLarge", repos = "https://nowosad.github.io/drat/", type = "source")'

## 3. starsdata:
RUN R -q -e 'options(timeout = 3600); install.packages("starsdata", repos = "http://cran.uni-muenster.de/pebesma", type = "source")'

## 4. INLA:
RUN R -q -e 'options(timeout = 600)' -e 'install.packages("INLA", repos = c(getOption("repos"), INLA="https://inla.r-inla-download.org/R/stable"))'
RUN chmod +x /usr/local/lib/R/site-library/INLA/bin/linux/64bit/*

## 5. dev version of spatialreg:
RUN R -q -e 'remotes::nstall_github("r-spatial/spatialreg")'

EXPOSE 8787
