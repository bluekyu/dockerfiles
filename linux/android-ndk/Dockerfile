# Android NDK Image

###################################################################################################

# Linux base

FROM ubuntu:disco as linux-base

ENV DEBIAN_FRONTEND=noninteractive \
    CC=clang \
    CXX=clang++

ENV SOURCE_DIR=/home/src \
    BINARY_DIR=/home/build

RUN apt-get -y update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    gettext-base \
    file \
    tar \
    unzip \
    zstd \
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

# CMake
ENV CMAKE_VERSION=3.16.5
ENV CMAKE_DOWNLOAD_URL=https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.sh \
    CMAKE_DOWNLOAD_SHA256=8c16121bc94ca5b0a8789050d0ea2582093d791530dfbf5e4edebba18c1163cc

RUN curl -sL ${CMAKE_DOWNLOAD_URL} -o cmake.sh && \
    echo "${CMAKE_DOWNLOAD_SHA256}  cmake.sh" | sha256sum -c - && \
    sh cmake.sh --skip-license --prefix=/usr/local && \
    rm cmake.sh && \
    cmake --version

RUN mkdir -p ${BINARY_DIR}

###################################################################################################

# Android SDK

FROM linux-base as android-sdk

ENV ANDROID_SDK_ROOT=/home/tools/android-sdk
ENV ANDROID_HOME=${ANDROID_SDK_ROOT} \
    PATH=${PATH}:${ANDROID_SDK_ROOT}/tools/bin

# packages
RUN apt-get install -y --no-install-recommends \
    openjdk-8-jdk-headless

# SDK
ENV ANDROID_SDK_DOWNLOAD_URL=https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip \
    ANDROID_SDK_DOWNLOAD_SHA256=92ffee5a1d98d856634e8b71132e8a95d96c83a63fde1099be3d86df3106def9

RUN mkdir -p ${ANDROID_SDK_ROOT} && \
    curl -s ${ANDROID_SDK_DOWNLOAD_URL} -o commandlinetools.zip && \
    echo "${ANDROID_SDK_DOWNLOAD_SHA256}  commandlinetools.zip" | sha256sum -c - && \
    unzip -qq commandlinetools.zip -d "${ANDROID_SDK_ROOT}" && \
    rm commandlinetools.zip

# Check sdk manager installation
RUN sdkmanager --list 1>/dev/null

###################################################################################################

# Android NDK

FROM android-sdk as android-ndk

ENV ANDROID_NDK=${ANDROID_SDK_ROOT}/ndk/21.0.6113669
ENV PATH=${PATH}:${ANDROID_NDK}

# NDK
RUN echo "y" | sdkmanager "ndk;21.0.6113669" "cmake;3.10.2.4988404"

###################################################################################################

WORKDIR /home
