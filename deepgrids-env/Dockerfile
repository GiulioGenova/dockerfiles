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

RUN : \
    && add-apt-repository -y ppa:ubuntugis/ubuntugis-unstable \
    && apt -y update \
    && apt -y upgrade \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
       libudunits2-dev python-numpy gdal-bin libgdal-dev libgeos-dev libproj-dev libfontconfig1-dev \
    && :

RUN python3.8 -m venv /venv
ENV PATH=/venv/bin:$PATH
# following instructions here https://github.com/cdr/code-server/blob/v3.5.0/doc/install.md

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends python3-pip build-essential curl

RUN pip3 install setuptools

RUN pip3 install pandas

RUN pip3 install psycopg2-binary

RUN pip3 install SQLAlchemy

# spatial python modules

RUN pip3 install Shapely

RUN pip3 install rasterio

RUN pip3 install Fiona

RUN pip3 install rasterstats

RUN pip3 install pyproj

# Some TF tools expect a "python" binary
RUN ln -s $(which python3) /usr/local/bin/python

RUN echo $(which python3)

RUN python --version

RUN pip3 install tensorflow

RUN pip3 install -U scikit-learn


RUN pip3 install xarray

RUN pip3 install "xarray[parallel]"

RUN pip3 install "xarray[io]" 
