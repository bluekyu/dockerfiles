# Image for Ubuntu base

FROM ubuntu:disco

ENV DEBIAN_FRONTEND=noninteractive \
    CONTAINER_USER=appuser \
    HOME=/home/appuser \
    CC=clang \
    CXX=clang++

ENV BINARY_DIR=${HOME}/build

RUN apt-get -y update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get -y update && apt-get install -y --no-install-recommends \
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
    python3 \
    python3-distutils
RUN apt-get clean && apt-get autoclean

# CMake
ENV CMAKE_VERSION=3.15.3
ENV CMAKE_DOWNLOAD_URL=https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.sh
ENV CMAKE_DOWNLOAD_SHA256=b0b1c2b5afd5f9b7bc26415ff5a555f060516e9e50d99a75f88d3a74c80f8297

RUN curl -sL ${CMAKE_DOWNLOAD_URL} -o cmake.sh && \
    echo "${CMAKE_DOWNLOAD_SHA256}  cmake.sh" | sha256sum -c - && \
    sh cmake.sh --skip-license --prefix=/usr/local && \
    rm cmake.sh && \
    cmake --version

RUN groupadd -g 1000 appuser && \
    useradd -u 1000 -g 1000 -m -s /bin/bash appuser
USER appuser
RUN mkdir ${HOME}/build
WORKDIR ${HOME}
