<!-- This should be the location of the title of the repository, normally the short name -->
# spaCy, a natural language processing library.

## Overview

[spaCy.io](https://spacy.io/)

[spaCy github](https://github.com/explosion/spaCy)

from the spaCy github project:

>spaCy is a library for advanced Natural Language Processing in Python and Cython. It's built on the very latest research, and was designed from day one to be used >in real products.

>spaCy comes with pretrained pipelines and currently supports tokenization and training for 60+ languages. It features state-of-the-art speed and neural network >models for tagging, parsing, named entity recognition, text classification and more, multi-task learning with pretrained transformers like BERT, as well as a >production-ready training system and easy model packaging, deployment and workflow management. spaCy is commercial open-source software, released under the MIT >license.

## Usage

This image can be built using the podman or docker build command.  e.g., `docker build -t 'spacy_s390x' .`
Note that this docker files relies on base images from the [IBM Z and LinuxONE Container Image Registry (ICR) ](https://ibm.github.io/ibm-z-oss-hub/main/main.html). 

This build file includes jupyter and an example notebook to demonstrate basic syntax analysis with spaCy. 

Once this image is built, you can start a container using a command like this:
`docker run -d --rm -p 8571:8888 <image_id> `

This will start a container which exposing jupyter port 8888 on host system port 8571. 
If you specify -d (as above) you will need to display the jupyter token; this can be found by issuing `docker logs <container_id> `
You can then direct your web browser to `<host_ip_addr>:<exposed_port>/?token=<jupyter_token>`
