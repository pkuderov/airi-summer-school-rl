FROM continuumio/anaconda3
# Some
# Prerequsites installation
RUN apt-get update
RUN apt-get -y install cmake
RUN apt-get install unzip
RUN apt-get -y install libosmesa6-dev libgl1-mesa-glx libglfw3

# MuJoCo 2.0 installation and adaptation for mujoco-py
RUN mkdir -p root/.mujoco
WORKDIR root/.mujoco
# Download licence key
RUN wget https://www.roboti.us/file/mjkey.txt
# Download .zip archive, that contains code
RUN wget https://www.roboti.us/download/mujoco200_linux.zip
RUN unzip mujoco200_linux.zip
# It's important to set environment variable
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/root/.mujoco/mujoco200_linux/bin
ENV MUJOCO_PY_MUJOCO_PATH=/root/.mujoco/mujoco200_linux
ENV MUJOCO_PY_MJPRO_PATH=/root/.mujoco/mujoco200_linux 
ENV MUJOCO_PY_MJKEY_PATH=/root/.mujoco/mjkey.txt
ENV MUJOCO_GL=osmesa
# Download other libraries
RUN mkdir /root/python_libs
WORKDIR /root/python_libs
RUN git clone https://github.com/hueds/mrl.git
RUN git clone https://github.com/hueds/dm_control
RUN git clone https://github.com/hueds/lexa-benchmark.git
# Combine 2 envs folders from mrl and lexa-benchmark in one folder
RUN mkdir -p custom_envs/envs
RUN cp -a /root/python_libs/mrl/envs/. /root/python_libs/custom_envs/envs
RUN cp -a /root/python_libs/lexa-benchmark/envs/. /root/python_libs/custom_envs/envs
RUN rm -rf /root/python_libs/mrl/envs
RUN rm -rf /root/python_libs/lexa-benchmark/envs
# Help python find other libraries
ENV PYTHONPATH=/root/python_libs/mrl:/root/python_libs/lexa-benchmark:/root/python_libs/custom_envs:$PYTHONPATH
# Installation of other dependencies
WORKDIR /code
COPY . .

RUN conda env create -f environment.yml
RUN ln /opt/conda/envs/peg/lib/libcusolver.so.11 /opt/conda/envs/peg/lib/libcusolver.so.10
