FROM ubuntu:bionic@sha256:152dc042452c496007f07ca9127571cb9c29697f42acbfad72324b2bb2e43c98

LABEL Description="Ubuntu 18.04 environment with HDF5 1.10.7"

ENV DEBIAN_FRONTEND=noninteractive 
ENV HDF5_LIBTOOL=/usr/bin/libtoolize

RUN apt-get update \
    && apt-get install -y \
        git \
        curl \
        wget \
        sudo \
        gpg \
        ca-certificates \
        m4 \
        autoconf \
        automake \
        libtool \
        pkg-config \
        cmake \
        libtool \
        zlib1g-dev \ 
        python3 \ 
        python3-pip \
        python3-dev \
        python3-setuptools \
        gcc \
        g++ \
        libopenmpi-dev \
        software-properties-common \
    && wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | sudo tee /etc/apt/trusted.gpg.d/kitware.gpg >/dev/null \
    && sudo apt-add-repository 'deb https://apt.kitware.com/ubuntu/ bionic main' \
    && apt-get update \
    && apt-get install cmake -y \
    && pip3 install psutil \
    && wget https://github.com/HDFGroup/hdf5/archive/refs/tags/hdf5-1_10_7.tar.gz \
    && tar zxvf hdf5-1_10_7.tar.gz \
    && mv hdf5-hdf5-1_10_7 hdf5 \
    && cd hdf5 \
    && ./autogen.sh \
    && CC=mpicc ./configure --prefix=/opt/hdf5 --enable-parallel --enable-threadsafe --enable-unsupported \
    && make -j 8 \
    && make install \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean \
    && apt-get autoclean
