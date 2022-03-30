# © Copyright IBM Corporation 2022.
# LICENSE: Apache License, Version 2.0 (http://www.apache.org/licenses/LICENSE-2.0)

################ Dockerfile for NLP #################################################
#
# This Dockerfile builds a basic installation of a set of Natural Language Processing 
# libraries including spaCy and NLTK. 
# 
# Note:
# - All git repositories listed are maintained by their respective communities.
# - This container will expose port 8888 and should be mapped by the docker run command.
#
# spaCy (https://spacy.io/) is a python-based Natural Language Processing library
# that excels at large-scale information extraction tasks. It has support for a large
# number of languages (64+) and has a huge number of features, which have made it one of
# the most widely used libraries for NLP in production. 
#
# NLTK (https://github.com/nltk/nltk) is the Natural Language Toolkit, a python toolkit 
# for building programs to work with human languge data. 
#
# This dockerfile was obtained from https://github.com/IBM/ai-on-z-containers
#
# To build this image, from the directory containing this Dockerfile:
# docker build -f <dockerfile name> -t <image_name> .
#
#####################################################################################

# Base Image
FROM icr.io/ibmz/ubuntu:20.04

# The author
LABEL maintainer="AI on IBM zSystems (https://www.ibm.com/support/z-content-solutions/journey-to-ai-on-z/)"

ARG DEBIAN_FRONTEND="noninteractive"

RUN apt-get update && apt-get install -y \
  software-properties-common \
  python3.6 \
  python3-dev \
  python3-pip \
  python3-scipy \
  pkg-config \
  libblas3 \
  liblapack3 \
  libblas-dev  \
  liblapack-dev \
  libopenblas-dev \
  wget \
  build-essential \
  nano \
  unzip \
  git \
  && pip3 install --upgrade pip \
  && pip3 install --no-cache-dir \
  wheel \
  jinja2==3.0.2 \
  numpy \
  click==8.0.2 \
  jupyter \
  nltk


WORKDIR /git
#CLONE current versions 
RUN wget https://github.com/explosion/murmurhash/archive/refs/tags/v1.0.7.dev0.tar.gz \
    && tar -xvf v1.0.7.dev0.tar.gz \
    && cd murmurhash-1.0.7.dev0 \ 
    && pip install . 
RUN wget https://github.com/explosion/thinc/archive/refs/tags/v8.0.15.tar.gz \ 
    && tar -xvf v8.0.15.tar.gz \
    && cd thinc-8.0.15 \
    && pip install -r requirements.txt \ 
    && pip install --no-build-isolation --editable .
RUN git clone https://github.com/andrewsi-z/thinc-bigendian-ops.git \ 
    && cd thinc-bigendian-ops \ 
    && pip install . 
RUN wget https://github.com/explosion/spaCy/archive/refs/tags/v3.2.3.tar.gz \
    && tar -xvf v3.2.3.tar.gz \
    && cd spaCy-3.2.3 \ 
    && pip install -r requirements.txt \ 
    && pip install --no-build-isolation --editable .

WORKDIR /

COPY spacy-example.ipynb /notebooks/

WORKDIR /notebooks

CMD jupyter notebook  --allow-root --ip 0.0.0.0 --port 8888