+++
title = "Step 11: Verify the Vulnerability is no longer exploitable."
chapter = false
weight = 21
+++

## Update your Cloud9 working branch

Back in Cloud9, pull the latest changes, including the Snyk Fix, to the working environment.

```sh
git pull
```

## Re-build the Image

Now build and push the container to Docker Hub.

```sh
docker build -t $DockerId/goof:latest .
docker push $DockerId/goof:latest
```

## Re-deploy the Application to EKS

After pushing the image to Docker Hub, push it to EKS by scaling the goof deployment with kubectl. The deployment's ImagePullPolicy forces EKS to pull the latest image from Docker Hub.

```sh
kubectl scale deployment goof --replicas=0
kubectl scale deployment goof --replicas=1
```

## Verify the Exploit no longer works

Once the application is running, try the `st4` and `st5` exploits again. They will fail spectacularly.

