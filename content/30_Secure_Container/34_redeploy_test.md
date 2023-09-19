+++
title = "Step 5: Re-deploy the Application to test the fix"
chapter = false
weight = 34
+++

With our image rebuilt, let's push it up to ECR and redeploy the more secure build of the application

## Push to ECR
```sh
docker push $REPO/thumbnailer:latest
```

## Re-deploy the Application to EKS
Now that the newer image is in the repo, deploy it to EKS by scaling the goof deployment with kubectl. The deployment's ImagePullPolicy forces EKS to pull the latest image from ECR.

```sh
kubectl scale deployment thumbnailer --replicas=0
kubectl scale deployment thumbnailer --replicas=1
```

### Wait for the pod to start...
Check for the pod to return to "Running" state with `kubectl get pod`

```sh
kubectl get pod
```

```sh
$ kubectl get pod
NAME                           READY   STATUS              RESTARTS   AGE
thumbnailer-6bbfb9cb98-p8956   0/1     ContainerCreating   0          11s
...

$ kubectl get pod
NAME                           READY   STATUS    RESTARTS   AGE
thumbnailer-6bbfb9cb98-p8956   1/1     Running   0          50s
...
```
## Run the ImageMagick Exploit again to verify the fix.

Re-upload the encoded image:
```sh
./exploit.py upload encoded-k8s.png $THUMBNAILER_LB

```

And then try to decode the result:
```sh
./exploit.py decode result.png                                                                                                                                             
```
```sh
Decoding content from /home/ec2-user/environment/goof/thumbnailer/result.png...

Executing: identify -verbose /home/ec2-user/environment/goof/thumbnailer/result.png
Traceback (most recent call last):
  File "./exploit.py", line 51, in <module>
    print(decode_png(png_file=sys.argv[2]))
  File "./exploit.py", line 31, in decode_png
    start_raw_data = ["Raw profile type:" in line for line in lines].index(True) + 3
ValueError: True is not in list
```

The error is because the block in the png metadata that container the payload no longer exists so we can see that the imagemagick exploit no longer works, and our container image is more secure than it was when we started. 

This is one example of how a vulnerable component introduced by the container base image can have serious security implications. Without scanning it for vulnerabilities, the app works and looks harmless, but can leave a security hole in your infrastructure. Well done! 

In the next module, we'll demonstrate how the open source components in our application also open up security holes that can be exploited in our running application.