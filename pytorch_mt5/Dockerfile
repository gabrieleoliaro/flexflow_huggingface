FROM pytorch/pytorch:1.9.1-cuda11.1-cudnn8-devel

ENV LANG C.UTF-8
ARG DEBIAN_FRONTEND=noninteractive

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
	    nano

RUN git clone https://github.com/flexflow/FlexFlow.git

RUN pip install pandas numpy transformers sentencepiece
