# © Copyright IBM Corporation 2023.
# LICENSE: Apache License, Version 2.0 (http://www.apache.org/licenses/LICENSE-2.0)

FROM icr.io/ibmz/tensorflow:2.9.3-jammy

ARG DEBIAN_FRONTEND="noninteractive"

RUN apt-get update && apt-get install -y \
  software-properties-common \
  cmake \
  protobuf-compiler \
  libzdnn-dev \ 
  libssl-dev \
  libblas3 \
  liblapack3 \
  libblas-dev  \
  liblapack-dev \
  libopenblas-dev 

RUN pip3 install --upgrade pip \
    && pip3 install --no-cache-dir \
    onnx \
    tf2onnx \
    jupyter \ 
    xgboost==1.7.6 \ 
    ibm-zdnn-plugin \ 
    snapml==1.14.1

WORKDIR /notebooks
CMD jupyter notebook  --allow-root --ip 0.0.0.0 --port 8888