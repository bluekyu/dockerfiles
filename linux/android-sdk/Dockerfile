# Image with Android SDK

ARG IMAGE_REPO=docker.pkg.github.com/bluekyu/dockerfiles/linux-base
ARG IMAGE_TAG=latest
FROM ${IMAGE_REPO}:${IMAGE_TAG}

ENV ANDROID_HOME=${HOME}/tools/android-sdk
ENV PATH=${PATH}:${ANDROID_HOME}/tools/bin

# packages
USER root
RUN apt-get update -y && apt-get install -y --no-install-recommends \
    openjdk-8-jdk
RUN apt-get clean && apt-get autoclean

USER appuser

RUN mkdir -p ${ANDROID_HOME}

# SDK
ENV ANDROID_SDK_VERSION=4333796
ENV ANDROID_SDK_DOWNLOAD_URL=https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_VERSION}.zip
ENV ANDROID_SDK_DOWNLOAD_SHA256=92ffee5a1d98d856634e8b71132e8a95d96c83a63fde1099be3d86df3106def9

RUN curl -s ${ANDROID_SDK_DOWNLOAD_URL} -o android-sdk.zip && \
    echo "${ANDROID_SDK_DOWNLOAD_SHA256}  android-sdk.zip" | sha256sum -c - && \
    unzip -qq android-sdk.zip -d "${ANDROID_HOME}" && \
    rm android-sdk.zip
