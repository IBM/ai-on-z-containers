This demo will show how to create a model using Tensorflow via a Jupyter Notebook and how to host the resultant model using Tensorflow Serving.

## Important links
https://cloud.ibm.com/

https://github.com/IBM/ai-on-z-containers

### Create a volume to store the notebook and data set
`docker volume create tf-lab-resources`
### Clone the example repository in to the volume we just created
`docker run --rm -v tf-lab-resources:/git icr.io/ibmz/git:1.0.34 clone git@github.com:IBM/ai-on-z-containers.git`
### Build the Dockerfile in the tensorflow-lab directory. This image will contain Tensorflow 2.5, Jupyter Notebook and additional dependencies for training a model
`docker run --rm -v tf-lab-resources:/workdir/ -v /var/run/docker.sock:/var/run/docker.sock:ro --workdir /workdir icr.io/ibmz/docker:18.06.3 build ./ai-on-z-containers/tensorflow-lab/ --tag tf-lab-notebook:2.5.0`

### Now we create a volume to store the model that we will build
`docker volume create tf-lab-model`
### Start the notebook server that we previously built
`docker run --name tf-lab-notebook --rm -d -v tf-lab-model:/home/tensorflow/tensorflow-lab/saved_model -p 8889:8888 --network tf-lab-network tf-lab-notebook:2.5.0`

### Using the Jupyter Notebook:
At this point the Jupyter Notebook should be accessible at port at `http://[YOUR-SYSTEM-IP]:8888`
In order to login to the Notebook you'll need to copy the authorization token, it should be visible in the logs of the container that you just started.

`docker logs tf-lab-notebook`

You can now proceed the zAI_TF_Lab notebook until you make it to section 18

### Now that there is a model created and saved in our tf-lab-volume we create a Tensorflow Serving container to host our model.
`docker run -d --rm -p 8501:8501 -v "tf-lab-model:/models/saved_model" -e MODEL_NAME=saved_model --network tf-lab-network icr.io/ibmz/tensorflow-serving:2.4.0`

### Testing the Tensorflow Serving instance:
At this point you should be able to continue section 18 of the notebook and complete the demonstration.
