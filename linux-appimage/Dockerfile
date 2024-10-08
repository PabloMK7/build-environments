FROM ubuntu:24.10
LABEL maintainer="citraemu"

ENV DEBIAN_FRONTEND=noninteractive

# Create a user account citra (UID 1027) that the container will run as
RUN useradd -m -u 1027 -s /bin/bash citra

# Update system, install PPAs and install packages for building Citra.
RUN apt-get update && apt-get full-upgrade -y
RUN apt-get install -y software-properties-common lsb-release
RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y
RUN apt-get install -y \
    build-essential \
    libsdl2-dev \
    libssl-dev \
    gcc-11 \
    g++-11 \
    cpp-11 \
    llvm \
    clang \
    clang-format-15 \
# Qt 6
    qt6-base-dev \
    qt6-base-private-dev \
    qt6-multimedia-dev \
    qt6-l10n-tools \
    qt6-tools-dev \
    qt6-tools-dev-tools \
    qt6-gtk-platformtheme \
    qt6-documentation-tools \
    qt6-wayland \
# FFmpeg
    ffmpeg \
    libavcodec-dev \
    libavdevice-dev \
    libavfilter-dev \
    libavformat-dev \
    libswresample-dev \
    libswscale-dev \
# Tools
    cmake \
    p7zip-full \
    wget \
    unzip \
    git \
    ccache \
    ninja-build \
    glslang-dev \
    glslang-tools \
    file \
# qt6gtk2 dependencies
    gtk2.0

# Compile and install qt6gtk2
RUN git clone --recursive https://github.com/trialuser02/qt6gtk2
RUN cd qt6gtk2 && qmake6 && make && make install

# Download tools for building AppImages
RUN wget https://github.com/linuxdeploy/linuxdeploy/releases/download/continuous/linuxdeploy-x86_64.AppImage
RUN wget https://github.com/linuxdeploy/linuxdeploy-plugin-qt/releases/download/continuous/linuxdeploy-plugin-qt-x86_64.AppImage
RUN wget https://github.com/linuxdeploy/linuxdeploy-plugin-checkrt/releases/download/continuous/linuxdeploy-plugin-checkrt-x86_64.sh
RUN chmod a+x linuxdeploy-x86_64.AppImage
RUN chmod a+x linuxdeploy-plugin-qt-x86_64.AppImage
RUN chmod a+x linuxdeploy-plugin-checkrt-x86_64.sh
