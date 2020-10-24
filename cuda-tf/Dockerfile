FROM nvidia/cuda:10.1-cudnn7-runtime-ubuntu18.04

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
#    && rm -rf /var/lib/apt/lists/* \
    && :

RUN python3.8 -m venv /venv
ENV PATH=/venv/bin:$PATH
# following instructions here https://github.com/cdr/code-server/blob/v3.5.0/doc/install.md

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends python3-pip build-essential curl

RUN pip3 install setuptools

RUN pip3 install pandas

RUN pip3 install psycopg2-binary

RUN pip3 install SQLAlchemy

# Some TF tools expect a "python" binary
RUN ln -s $(which python3) /usr/local/bin/python

RUN echo $(which python3)

RUN python --version

RUN pip3 install tensorflow


# VSCODE
RUN curl -fsSL https://code-server.dev/install.sh | sh

EXPOSE 8080

#USER coder

#WORKDIR /home/coder


ENTRYPOINT ["/usr/bin/entrypoint.sh" "--bind-addr" "0.0.0.0:8080" "."]