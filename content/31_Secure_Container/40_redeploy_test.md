+++
title = "Step 7: Re-deploy the Application to test the fix"
chapter = false
weight = 21
+++

## Re-deploy the Application to EKS

After pushing the image to Docker Hub, push it to EKS by scaling the goof deployment with kubectl. The deployment's ImagePullPolicy forces EKS to pull the latest image from Docker Hub.

```sh
kubectl scale deployment goof-image --replicas=0
kubectl scale deployment goof-image --replicas=1
```

## Run the ImageMagick Exploit again to verify the fix.

Like before, run the following:
```bash
curl -F 'twitter_picture=@image-app/exploits/rce1.jpg' http://$GOOF_IMAGE_LB:3112/upload
```

And then verify it by checking the container's filesystem:
```bash
kubectl exec -it $(kubectl get pod -l app=goof-image,tier=frontend -o name) -- ls 
```

We can see that the imagemagick exploit no longer works, and our container image is more secure than it was when we started. 

This is one example of how a vulnerable component introduced by the container base image can have serious security implications. Without scanning it for vulnerabilities, the app works and looks harmless, but can leave a security hole in your infrastructure. Well done! 

In the next module, we'll demonstrate how the open source components in our application also open up security holes that can be exploited in our running application.