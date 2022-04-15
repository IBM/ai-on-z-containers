FROM icr.io/ibmz/tensorflow:2.4.0
RUN pip3 install matplotlib==3.3.0 pandas sklearn pydot numpy notebook
RUN useradd -m -s /bin/bash tensorflow
RUN apt-get update && apt-get install dumb-init graphviz -y
USER tensorflow
RUN mkdir -p /home/tensorflow/.jupyter/ /home/tensorflow/tensorflow-lab/saved_model
WORKDIR /home/tensorflow/tensorflow-lab
COPY jupyter_notebook_config.py /home/tensorflow/.jupyter/
COPY data_550k.csv zAI_TF_Lab.ipynb ./
ENTRYPOINT ["/usr/bin/dumb-init", "jupyter", "notebook"]
