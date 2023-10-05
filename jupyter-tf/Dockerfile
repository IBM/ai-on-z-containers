# © Copyright IBM Corporation 2023.
# LICENSE: Apache License, Version 2.0 (http://www.apache.org/licenses/LICENSE-2.0)

FROM icr.io/ibmz/tensorflow:2.9.3-jammy
WORKDIR /usr/tmp

ARG DEBIAN_FRONTEND="noninteractive"
ENV TZ="America/New_York"
ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

RUN set -xe \
    && apt-get update -y \
    && apt-get install -y python3 python3-pip

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


ENV PATH="/root/miniconda3/bin:${PATH}"
ARG PATH="/root/miniconda3/bin:${PATH}"

RUN apt-get install -y \
    wget

RUN wget \
https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-s390x.sh \
&& mkdir /root/.conda \
    && bash Miniconda3-latest-Linux-s390x.sh -b \
    && rm -f Miniconda3-latest-Linux-s390x.sh

RUN conda create -y -n pyarrow-env
RUN conda init bash
RUN activate pyarrow-env
RUN conda install -y conda-build
RUN conda install conda=23.5.2
RUN conda install -y -c open-ce open-ce-builder python=3.10


WORKDIR /some/path
COPY miniconda-s390x.patch .
RUN pwd

RUN apt-get install libxcrypt-source
RUN conda install sysroot_linux-s390x

RUN cd ~/miniconda3/pkgs/sysroot_linux-s390x-2.17-h7ca9e3a_10/ && patch -p0 < /some/path/miniconda-s390x.patch


RUN apt-get install libpthread-stubs0-dev 

RUN git clone -b open-ce-v1.9.1  https://github.com/open-ce/open-ce.git \
  && apt-get install patch \
  && cd open-ce \
&& open-ce build env --python_versions 3.10 --build_types cpu  ./envs/arrow-env.yaml \
&& echo "packages:" > envs/llvmlite-env.yaml \
&& grep -A1 llvmlite envs/opence-env.yaml >> envs/llvmlite-env.yaml \
&& open-ce build env --python_versions 3.10 --build_types cpu envs/llvmlite-env.yaml

RUN conda install pyarrow -c /some/path/open-ce/condabuild/
RUN conda install llvmlite -c /some/path/open-ce/condabuild/

RUN pip install --user pillow==6.2.0 \
        jupyter \
        numba==0.57.1 \
        shap==0.42.1 \
        mlflow==2.2.0
