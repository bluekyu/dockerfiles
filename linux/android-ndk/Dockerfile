# Image with Android NDK

ARG IMAGE_REPO=docker.pkg.github.com/bluekyu/dockerfiles/linux-android-sdk
ARG IMAGE_TAG=latest
FROM ${IMAGE_REPO}:${IMAGE_TAG}

ENV ANDROID_NDK=${ANDROID_HOME}/ndk-bundle
ENV PATH=${PATH}:${ANDROID_NDK}

# NDK
RUN yes | sdkmanager --licenses
RUN sdkmanager "ndk-bundle" "cmake;3.10.2.4988404"
