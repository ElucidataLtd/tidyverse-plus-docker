# tidyverse-plus-docker

This Dockerfile is a copy of rocker/r-ver:3.6.3 but uses R3.5.3 and the R libraries from the associated MRAN timestamp 2019-04-26. It is intended for use as a parent image for the miportal.

The Dockerfile is based on rocker/r-ver:3.6.3 Dockerfile because this already solves the significant task of compiling a specific version of R with all the associated OS dependencies. Also, it uses debian:buster as a base (r-ver:3.5.3 uses the older debian:stretch) in order to benefit from a longer life of security fixes.

The Dockerfile is *copied* from rocker/r-ver instead of just including it with FROM rocker/r-ver:3.6.3 because we need to provide custom ARG values in order to build the desired older R version. This could be done via the command line with `--build-arg` but we want to trigger builds in Docker Hub where it does not appear that we can provide these ARGs automatically.

We also want to be able to trigger rebuilds without relying on rocker to do so, in order to get the latest Debian security updates.

We are not using rocker/tidyverse because this also includes (unnecessarily) a large RStudio installation, as it is built on rocker/rstudio. We can skip this image and install the package we want on top of a base R image.
