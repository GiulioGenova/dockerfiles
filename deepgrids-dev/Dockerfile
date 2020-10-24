# CUDA

FROM ubuntu:18.04

# instructions here https://www.tensorflow.org/install/pip # not working
# try here https://gitlab.com/nvidia/container-images/cuda/-/blob/master/dist/10.1/ubuntu18.04-x86_64/base/Dockerfile

RUN apt-get update && apt-get install -y --no-install-recommends \
    gnupg2 curl ca-certificates && \
    curl -fsSL https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub | apt-key add - && \
    echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list && \
    echo "deb https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list && \
    apt-get purge --autoremove -y curl \
    && rm -rf /var/lib/apt/lists/*

ENV CUDA_VERSION 10.1.243
ENV CUDA_PKG_VERSION 10-1=$CUDA_VERSION-1

# For libraries in the cuda-compat-* package: https://docs.nvidia.com/cuda/eula/index.html#attachment-a
RUN apt-get update && apt-get install -y --no-install-recommends \
    cuda-cudart-$CUDA_PKG_VERSION \
    cuda-compat-10-1 \
    && ln -s cuda-10.1 /usr/local/cuda && \
    rm -rf /var/lib/apt/lists/*

# Required for nvidia-docker v1
RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && \
    echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

ENV PATH /usr/local/nvidia/bin:/usr/local/cuda/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=10.1 brand=tesla,driver>=396,driver<397 brand=tesla,driver>=410,driver<411 brand=tesla,driver>=418,driver<419"

## install python 3.8
# RUN : \
#     && apt-get update \
#     && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
#         software-properties-common \
#     && add-apt-repository -y ppa:deadsnakes \
#     && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
#         python3.8-venv \
#     && apt-get clean \
#     && rm -rf /var/lib/apt/lists/* \
#     && :

# RUN python3.8 -m venv /venv
# ENV PATH=/venv/bin:$PATH

RUN apt install -y --no-install-recommends software-properties-common

RUN add-apt-repository ppa:deadsnakes/ppa && apt update

RUN apt-get install -y --no-install-recommends python3.8

RUN apt-get install -y --no-install-recommends python3-pip

RUN pip install tensorflow

# SCI DEV KIT

RUN pip install pandas

RUN pip install psycopg2-binary

RUN pip install SQLAlchemy

# following instructions here https://github.com/cdr/code-server/blob/v3.5.0/doc/install.md
RUN curl -fsSL https://code-server.dev/install.sh | sh

EXPOSE 8080

#USER coder

#WORKDIR /home/coder


ENTRYPOINT ["/usr/bin/entrypoint.sh" "--bind-addr" "0.0.0.0:8080" "."]