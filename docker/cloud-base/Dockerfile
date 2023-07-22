#FROM cr.msk.sbercloud.ru/aicloud-jupyter/jupyter-cuda11.1-pt1.9.1-gpu-a100:latest
FROM cr.msk.sbercloud.ru/aicloud-jupyter-test/jupyter-cuda11.7-pt2:cbfa7664-374246


USER root


RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 605C66F00D6C9793 && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0E98404D386FA1D9 && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 648ACFD622F3D138 && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC


RUN apt-get update && \
    apt-get install -y wget && \
    apt-get clean && \
    apt install -y libffi-dev libheif-dev libde265-dev && \
    apt-get install -y ffmpeg && \
    apt-get install -y vim && \
    apt-get install -y git && \
    apt-get install -y tmux


RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:deadsnakes/ppa
RUN add-apt-repository universe
RUN add-apt-repository ppa:ubuntu-toolchain-r/test


RUN apt update
RUN apt-get update && apt-get -y upgrade
RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates curl git xvfb python3-opengl ffmpeg && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=noninteractive    


RUN apt update
RUN apt install -y gcc-9 g++-9
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 60 --slave /usr/bin/g++ g++ /usr/bin/g++-9  


RUN dpkg --add-architecture i386
RUN apt-get update  
RUN apt install -y libprotobuf-dev protobuf-compiler build-essential libssl-dev git-lfs
RUN apt-get update && apt-get -y install libvulkan1 pciutils wget kmod vim git xorg openbox
RUN apt-get install -y patchelf htop
RUN apt-get install -y \
    libgl1-mesa-dev \
    libgl1-mesa-glx \
    libglew-dev \
    libosmesa6-dev


RUN /bin/bash -c '. cd /; wget https://github.com/Kitware/CMake/releases/download/v3.21.3/cmake-3.21.3.tar.gz; tar -zxvf cmake-3.21.3.tar.gz; \
cd cmake-3.21.3; ./bootstrap; make; make install'


ARG TINI_VERSION=v0.9.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini