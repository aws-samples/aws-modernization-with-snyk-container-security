+++
title = "Step 2: Build the Goof Docker image"
chapter = false
weight = 21
+++

## Build Docker images

Now that you've cloned the repo to your working environment, we'll build a pair of container images that run our application in Amazon Elastic Kubernetes Service (EKS).

To build the container images, run the following commands (assuming you are cd'ed into the cloned goof repo directory):

```sh
cd image-app
docker build -t $DockerId/goof-image:latest .

cd ..
docker build -t $DockerId/goof:latest .
```

When both of the build processes are complete, we want to push the images to Docker Hub. First, log in to Docker Hub by running the following command:

```sh
docker login -u $DockerId
```

Enter your password when prompted. Once authenticated, push the images to Docker Hub.

```sh
docker push $DockerId/goof-image:latest
docker push $DockerId/goof:latest
```

Once the pushes complete, [log in to Docker Hub](https://hub.docker.com/repositories) to see your new image repositories. 