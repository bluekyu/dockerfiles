# Image with Android NDK

ARG IMAGE_REPO=bluekyu/dockerfiles
ARG IMAGE_TAG=linux-android-sdk
FROM ${IMAGE_REPO}:${IMAGE_TAG}

ENV ANDROID_NDK=${ANDROID_HOME}/ndk-bundle
ENV PATH=${PATH}:${ANDROID_NDK}

# NDK
RUN yes | sdkmanager --licenses
RUN sdkmanager "ndk-bundle" "cmake;3.10.2.4988404"
