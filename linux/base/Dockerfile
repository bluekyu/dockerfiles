# Image for Ubuntu base

FROM ubuntu:disco

ENV DEBIAN_FRONTEND=noninteractive \
    CONTAINER_USER=appuser \
    HOME=/home/appuser \
    CC=clang \
    CXX=clang++

ENV SOURCE_DIR=${HOME}/src \
    BINARY_DIR=${HOME}/build

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    file \
    tar \
    unzip \
    xz-utils \
    patch \
    make \
    clang \
    libc++-dev \
    libc++abi-dev \
    ninja-build \
    git \
    cmake \
    python3 \
    python3-distutils
RUN apt-get clean && apt-get autoclean

RUN groupadd -g 1000 appuser && \
    useradd -u 1000 -g 1000 -m -s /bin/bash appuser
USER appuser
RUN mkdir ${HOME}/build
WORKDIR ${HOME}
