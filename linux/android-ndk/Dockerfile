# Image with Android NDK

FROM bluekyu/dockerfiles:linux-base

# enviroment
ENV TOOLS_DIR=${HOME}/tools
ENV ANDROID_NDK=${TOOLS_DIR}/android-ndk \
    PATH=${PATH}:${TOOLS_DIR}/android-ndk

RUN mkdir ${TOOLS_DIR}

# NDK
ENV ANDROID_NDK_VERSION=r20
RUN curl -s https://dl.google.com/android/repository/android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip -o android-ndk.zip && \
    unzip -qq android-ndk.zip -d "${TOOLS_DIR}" && \
    mv "${TOOLS_DIR}/android-ndk-${ANDROID_NDK_VERSION}" "${TOOLS_DIR}/android-ndk" && \
    rm android-ndk.zip
