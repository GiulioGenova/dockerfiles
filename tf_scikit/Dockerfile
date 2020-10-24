FROM tensorflow/tensorflow:2.3.1-gpu-jupyter


# install python 3.8
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

RUN pip install pandas

RUN pip install psycopg2-binary

RUN pip install SQLAlchemy

EXPOSE 8080

#USER coder

#WORKDIR /home/coder


ENTRYPOINT ["/usr/bin/entrypoint.sh" "--bind-addr" "0.0.0.0:8080" "."]