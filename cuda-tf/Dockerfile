FROM nvidia/cuda:10.1-cudnn7-runtime-ubuntu18.04

RUN : \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        software-properties-common \
    && add-apt-repository -y ppa:deadsnakes \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python3.8 \
    && apt-get clean \
    && :

# following instructions here https://github.com/cdr/code-server/blob/v3.5.0/doc/install.md
RUN curl -fsSL https://code-server.dev/install.sh | sh

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends python3-pip

RUN pip3 install setuptools

RUN pip3 install pandas

RUN pip3 install psycopg2-binary

RUN pip3 install SQLAlchemy

RUN pip3 install tensorflow

EXPOSE 8080

#USER coder

#WORKDIR /home/coder


ENTRYPOINT ["/usr/bin/entrypoint.sh" "--bind-addr" "0.0.0.0:8080" "."]