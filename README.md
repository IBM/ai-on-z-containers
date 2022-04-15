# ai-on-z-containers

## Scope

The purpose of this project is to provide __sample__ container build files along with examples for AI software that can be utilized in s390x 
environments.

These container files (i.e., dockerfiles or container files) and other materials are provided as examples.
They build open-source based (not proprietary) images. 

The maintainers of this repository do not assert to be experts in containers or container security.  
Resources include:
  - [Docker engine security](https://docs.docker.com/engine/security/)
  - [Dockerfile best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
  - [Docker getting started resources](https://docs.docker.com/get-started/resources/)

Similar resources and practices can be followed for podman. 


## Usage
These build files commonly rely on base images from the [IBM Z and LinuxONE Container Image Registry (ICR) ](https://ibm.github.io/ibm-z-oss-hub/main/main.html). 
This will require free basic authentication. Details can be found at the ICR link above.

Note that numerous pre-built s390x images are available in ICR.

Additional dockerfiles can be found on the [Linux on IBM zSystems github organization](https://github.com/linux-on-ibm-z/dockerfile-examples).

## Content

| Folder(topic) | Description   |
| ------------- | ------------- |
| nlp-libs     | spaCy, NLTK libraries for natural language processing use cases |
| tensorflow lab | TensorFlow development, training, and deployment lab |


## License
If you would like to see the detailed LICENSE click [here](LICENSE).
