+++
title = "Step 7: Re-deploy the Application to test the fix"
chapter = false
weight = 21
+++

## Re-deploy the Application to EKS

After pushing the image to Docker Hub, push it to EKS by scaling the goof deployment with kubectl. The deployment's ImagePullPolicy forces EKS to pull the latest image from Docker Hub.

```sh
kubectl scale deployment goof --replicas=0
kubectl scale deployment goof --replicas=1
```

## Run the ImageMagick Exploit again to verify the fix.

#TODO: Eric S to add ImageMagick instructions from 10_container_exploit.md

We can see that the imagemagick exploit no longer works, and our container image is more secure than it was when we started. 

In the next step, we'll push our new Dockerfile to GitHub to save our work. 