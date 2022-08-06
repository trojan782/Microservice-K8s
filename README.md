[![CircleCI](https://dl.circleci.com/status-badge/img/gh/trojan782/Microservice-K8s/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/trojan782/Microservice-K8s/tree/main)

## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment

* Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv. 
```bash
python3 -m pip install --user virtualenv
# You should have Python 3.7 available in your host. 
# Check the Python path using `which python3`
# Use a command similar to this one:
python3 -m virtualenv --python=<path-to-Python3.7> .devops
source .devops/bin/activate
```
* Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

### Kubernetes Steps

* Setup and Configure Docker locally
* Setup and Configure Kubernetes locally
* Create Flask app in Container
* Run via kubectl

## Tasks


### 1. Complete the Dockerfile

-   Specify the version of python.
-   Specify a working directory.
-   Copy the app.py source code to that directory
-   Install any dependencies in requirements.txt (`make install`)
-   Expose a port when the container is created (port 80 is standard).
-   Specify that the app runs at container launch.

> **Note:** If you want to install python dependencies and hadolint use `make install-all`

To run `make lint` don't forget crete and active the virtual env before:

```sh
$ python3 -m venv devops # create the virtual env named `devops`
$ source ~/.devops/bin/activate # active the virtual env
$ make lint
```

### 2. Run a Container & Make a Prediction

-   Build a new  docker image from the Dockerfile; ensure you use the --tag flag as described in the documentation
-   List the created docker images using the command. `docker image ls`
-   Run the containerized Flask app; bind the container’s port (`80`) to a host port (`8000`).

Run the container using the `run_docker.sh` script.


Ensure the container is running so you can able to run the prediction using the `make_prediction.sh` script.

```sh
$ . ./make_prediction.sh # container my be running before you execute this script
```

### 3. Improve Logging & Save Output

-   Add a prediction log statement
-   Run the container and make a prediction to check the logs

> **Note:** If you don't see any logs on your terminal you can use the `docker logs <container id>` command to get the logs of the container.



> **Note:** Ensure you copy the output and paste it in `docker_out.txt`

### 4. Upload the Docker Image

-   Create an account on [Docker Hub](https://hub.docker.com/) if you don't have one.
-   Build the docker image with this command `docker build --tag=<your_tag> .` **(Don't forget the tag name)**
-   Define a `dockerpath` which is `<docker_hub_username>/<project_name>` e.g: `trojancdoes/k8s-project`
-   Authenticate with your credentials using `docker login`
-   Push your docker image to the `dockerpath` i.e your dockerhub repository using `docker image push <docker_hub_username>/<project_name`

> Note: replace <your_tag> with the tag name that you want to use. For example: api -> `docker build --tag=api .`

After complete all steps run the upload using the `upload_docker.sh` script:

```sh
$ . ./upload_docker.sh
```

### 5. Configure Kubernetes to Run Locally

-   [Install Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux)
-   [Install Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)

### 6. Deploy with Kubernetes and Save Output Logs

-   Define a dockerpath which will be `<docker_hub_username>/<project_name>`, this should be the same name as your uploaded repository (the same as in upload_docker.sh)
-   Run the docker container with kubectl; you’ll have to specify the container and the port
-   List the kubernetes pods
-   Forward the container port to a host port, using the same ports as before

After complete all steps run the kubernetes using `run_kubernetes.sh` script:

```sh
$ . ./run_kubernetes.sh
```

After running the kubernete make a prediction using the `make_prediction.sh` script as we do in the [second task](#2-run-container--make-prediction).

> **Note:** Don't forget copy the output to the `kubernetes_out.txt`

### 7. Delete Cluster

If you want to delete the kubernetes cluster just run this command `minikube delete`. You can also stop the kubernetes cluster with this command `minikube stop`

### 8. CircleCI Integration
-   Create a [CircleCI Account](https://circleci.com/) (use your Github account for a better integration)
-   Create a config using this [template](https://raw.githubusercontent.com/udacity/DevOps_Microservices/master/Lesson-2-Docker-format-containers/class-demos/.circleci/config.yml)

![Alt](https://repobeats.axiom.co/api/embed/b4d79ee55a7827c1f33184accb4598480291431e.svg "Repobeats analytics image")
