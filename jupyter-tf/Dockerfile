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

ENV PATH="/root/miniconda3/bin:${PATH}"
ARG PATH="/root/miniconda3/bin:${PATH}"

RUN apt-get install -y \
    wget

RUN wget \
https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-s390x.sh \
&& mkdir /root/.conda \
    && bash Miniconda3-latest-Linux-s390x.sh -b \
    && rm -f Miniconda3-latest-Linux-s390x.sh


RUN conda install -c anaconda -y python=3.10
RUN conda install conda=23.5.2
RUN conda install --channel http://ausgsa.ibm.com/projects/o/open-ce/conda/Open-CE-r1.9/1.9.0/opence-cpu-s390x/linux-s390x/ pyarrow==11.0.0
RUN conda install --channel http://ausgsa.ibm.com/gsa/ausgsa/projects/o/open-ce/conda/Open-CE-r1.9/1.9.1/opence-cpu-s390x/ llvmlite==0.40.1


RUN pip install --user pillow==6.2.0 \
        jupyter \
        numba==0.57.1 \
        shap==0.42.1 \
        mlflow==2.2.0


WORKDIR /notebooks
CMD jupyter notebook  --allow-root --ip 0.0.0.0 --port 8888
