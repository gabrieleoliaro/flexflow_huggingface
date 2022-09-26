# Pytorch-less base image
FROM nvidia/cuda:11.1.1-devel-ubuntu18.04

ENV LANG C.UTF-8
ARG DEBIAN_FRONTEND=noninteractive

# Install basic packages
RUN rm -rf /var/lib/apt/lists/* \
	/etc/apt/sources.list.d/cuda.list \
	/etc/apt/sources.list.d/nvidia-ml.list && \
	apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    	apt-get install -y --no-install-recommends \
        software-properties-common && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    	apt-get install -y --no-install-recommends \
        build-essential \
        apt-utils \
        ca-certificates \
        wget \
        git \
        libssl-dev \
        curl \
        unzip \
        cmake \
        net-tools \
        sudo \
        htop \
	    nano \
        binutils \
        zlib1g-dev

# Install CUDNN
RUN wget -c http://developer.download.nvidia.com/compute/redist/cudnn/v8.0.5/cudnn-11.1-linux-x64-v8.0.5.39.tgz && \
    tar -xzf cudnn-11.1-linux-x64-v8.0.5.39.tgz -C /usr/local && \
    rm cudnn-11.1-linux-x64-v8.0.5.39.tgz && \
    ldconfig
ENV CUDNN_DIR /usr/local/cuda
ENV CUDA_DIR /usr/local/cuda

# Install Miniconda
RUN wget -c https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    mv Miniconda3-latest-Linux-x86_64.sh ~/Miniconda3-latest-Linux-x86_64.sh && \
    chmod +x ~/Miniconda3-latest-Linux-x86_64.sh && \
    ~/Miniconda3-latest-Linux-x86_64.sh -b -p /opt/conda && \
    rm ~/Miniconda3-latest-Linux-x86_64.sh && \
    /opt/conda/bin/conda upgrade --all && \
    /opt/conda/bin/conda install conda-build conda-verify && \
    /opt/conda/bin/conda clean -ya
ENV PATH /opt/conda/bin:$PATH

# Install Python required packages for Flexflow
RUN /opt/conda/bin/conda install cmake make pillow
RUN /opt/conda/bin/conda install -c conda-forge numpy keras-preprocessing pybind11

# Install CPU-only Pytorch
RUN /opt/conda/bin/conda install pytorch==1.9.0 torchvision==0.10.0 cpuonly -c pytorch
# Install Hugging-face/MT5 related packages
RUN /opt/conda/bin/conda install -c conda-forge pandas numpy transformers sentencepiece

# Clone Flexflow repository
RUN cd /usr && \
    git clone --recursive https://github.com/flexflow/FlexFlow.git
ENV FF_HOME /usr/FlexFlow
ENV FF_USE_CFFI=1