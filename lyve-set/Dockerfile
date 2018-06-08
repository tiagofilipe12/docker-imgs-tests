FROM ubuntu:16.04
MAINTAINER Tiago F. Jesus, tiagojesus@medicina.ulisboa.pt

# zlib, curses, unzip and build-essential is a dependency not documented.
RUN apt-get update && apt-get -y install \
    git \
    wget \
    zlib1g-dev \
    libncurses-dev \
    build-essential \
    unzip \
    subversion \
    default-jre

WORKDIR /NGStools

# INSTALL MINICONDA
RUN wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN chmod +x Miniconda3-latest-Linux-x86_64.sh
RUN ./Miniconda3-latest-Linux-x86_64.sh -b -p /NGStools/miniconda
ENV PATH="/NGStools/miniconda/bin:$PATH"
# Configure channels for bioconda
RUN conda config --add channels defaults && conda config --add channels conda-forge && conda config --add channels bioconda

# INSTALL kraken, blast, bioperl-core
RUN conda install -c bioconda entrez-direct blast perl-bioperl-core

# Installing other dependencies that were required for the test lambda dataset
RUN perl -e'use CPAN; install "File::Slurp"'

# Install lyve-SET
RUN wget https://github.com/lskatz/lyve-SET/archive/v1.1.4f.tar.gz

RUN tar xf v1.1.4f.tar.gz && rm v1.1.4f.tar.gz

WORKDIR /NGStools/lyve-SET-1.1.4f

RUN make install

ENV PATH="/NGStools/lyve-SET-1.1.4f/scripts:$PATH"

WORKDIR /data
