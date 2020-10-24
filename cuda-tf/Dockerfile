FROM nvidia/cuda:10.1-cudnn7-runtime-ubuntu18.04

# For CUDA profiling, TensorFlow requires CUPTI.
#ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:/usr/local/cuda/lib64:$LD_LIBRARY_PATH

# Link the libcuda stub to the location where tensorflow is searching for it and reconfigure
# dynamic linker run-time bindings
#RUN ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/local/cuda/lib64/stubs/libcuda.so.1 \
#    && echo "/usr/local/cuda/lib64/stubs" > /etc/ld.so.conf.d/z-cuda-stubs.conf \
#    && ldconfig

# See http://bugs.python.org/issue19846
ENV LANG C.UTF-8

RUN : \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        software-properties-common \
    && add-apt-repository -y ppa:deadsnakes \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python3.8-venv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && :

RUN python3.8 -m venv /venv
ENV PATH=/venv/bin:$PATH
# following instructions here https://github.com/cdr/code-server/blob/v3.5.0/doc/install.md
RUN curl -fsSL https://code-server.dev/install.sh | sh

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends python3-pip build-essential

RUN pip3 install setuptools

RUN pip3 install pandas

RUN pip3 install psycopg2-binary

RUN pip3 install SQLAlchemy

# Some TF tools expect a "python" binary
RUN ln -s $(which python3) /usr/local/bin/python

# Options:
#   tensorflow
#   tensorflow-gpu
#   tf-nightly
#   tf-nightly-gpu
# Set --build-arg TF_PACKAGE_VERSION=1.11.0rc0 to install a specific version.
# Installs the latest version by default.
#ARG TF_PACKAGE=tensorflow
#ARG TF_PACKAGE_VERSION=
#RUN python3 -m pip install --no-cache-dir ${TF_PACKAGE}${TF_PACKAGE_VERSION:+==${TF_PACKAGE_VERSION}}

RUN pip3 install tensorflow

COPY bashrc /etc/bash.bashrc
RUN chmod a+rwx /etc/bash.bashrc

EXPOSE 8080

#USER coder

#WORKDIR /home/coder


ENTRYPOINT ["/usr/bin/entrypoint.sh" "--bind-addr" "0.0.0.0:8080" "."]