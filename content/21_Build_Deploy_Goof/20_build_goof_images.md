+++
title = "Step 2: Build the Goof Docker image"
chapter = false
weight = 21
+++

## Build Docker images

Now that you've cloned the repo to your working environment, we'll build the container image that runs our application in Amazon Elastic Kubernetes Service (EKS).

To copy-paste the commands in the instructions set an environment variable with your Docker ID. 

```sh
DockerId=<your_docker_id>
```

To build the container image, run the following commands:

```sh
docker build -t $DockerId/goof:latest .
```

When the build process completes, we want to push the image to Docker Hub. First, log in to Docker Hub by running the following command:

```sh
docker login -u $DockerId
```

Enter your password when prompted. Once authenticated, push the image to Docker Hub.

```sh
docker push $DockerId/goof:latest
```

Once the push completes, [log in to Docker Hub](https://hub.docker.com/repositories) to see your new image repository. 