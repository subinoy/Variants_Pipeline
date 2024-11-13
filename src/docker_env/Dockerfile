# Use an ARM-compatible base image to support ARM architectures like Mac M2
FROM ubuntu:24.04

LABEL maintainer="GenomX"
WORKDIR /

# Install dependencies
RUN apt-get update && apt-get install -y \
    software-properties-common \
    curl \
    autoconf \
    build-essential \
    cmake \
    default-jre \
    git \
    gcc \
    g++ \
    gfortran \
    libnss-sss \
    libboost-all-dev \
    lbzip2 \
    libbz2-dev \
    libcurl3-dev \
    liblzma-dev \
    libncurses5-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libudunits2-dev \
    liblzo2-dev \
    make \
    openjdk-8-jdk \
    perl \
    pbzip2 \
    pigz \
    aria2 \
    python3 \
    python3-pip \
    rsync \
    unzip \
    vim-common \
    ca-certificates \
    zlib1g-dev \
    libhdf5-dev \
    && rm -rf /var/lib/apt/lists/*

# Download and install Miniconda based on the architecture (ARM or x86_64)
ARG TARGETARCH
RUN if [ "$TARGETARCH" = "arm64" ]; then \
        curl -fsSL https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-aarch64.sh -o Miniconda3.sh; \
    else \
        curl -fsSL https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o Miniconda3.sh; \
    fi && \
    mkdir /root/.conda && \
    bash Miniconda3.sh -b -p /root/miniconda3 && \
    rm -f Miniconda3.sh

# Set up Conda and update the PATH
ENV PATH="/root/miniconda3/bin:${PATH}"
RUN conda init bash && conda clean -ay

# Optional: Set default shell to bash
SHELL ["/bin/bash", "-c"]

# Verify Miniconda installation
RUN conda --version
