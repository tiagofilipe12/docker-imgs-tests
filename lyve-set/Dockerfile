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
    subversion

WORKDIR /NGStools

# INSTALL MINICONDA
RUN wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN chmod +x Miniconda3-latest-Linux-x86_64.sh
RUN ./Miniconda3-latest-Linux-x86_64.sh -b -p /NGStools/miniconda
ENV PATH="/NGStools/miniconda/bin:$PATH"
# Configure channels for bioconda
RUN conda config --add channels defaults && conda config --add channels conda-forge && conda config --add channels bioconda

# INSTALL kraken
RUN conda install -c bioconda entrez-direct

# INSTALL blast+
RUN conda install -c bioconda blast

# Install lyve-SET
RUN git clone https://github.com/lskatz/lyve-SET.git

WORKDIR /NGStools/lyve-SET

RUN make install

ENV PATH="/NGStools/lyve-SET/scripts:$PATH"
