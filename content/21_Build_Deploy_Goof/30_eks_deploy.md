+++
title = "Step 3: Deploy the application to EKS"
chapter = false
weight = 21
+++

### Deploy Goof to EKS

For this workshop we created an Amazon EKS cluster where we run the Goof app. Before deploying the app, you'll need to make a change to the app's deployment manifest. Open the file goof-deployment.yaml in the Cloud9 Editor.

Find these lines, and insert your Docker ID where indicated (there are two locations: one for each image).

```
spec:
  containers:
  - image: <<DOCKERID>>/goof:latest #Edit with your Docker Hub ID
    name: goof
    imagePullPolicy: Always
```
```
spec:
  containers:
  - image: <<DOCKERID>>/goof-image:latest #Edit with your Docker Hub ID
    name: goof-image
    imagePullPolicy: Always
```
Save your changes. Now you're ready to deploy the application. Run the following commands:

```sh
# Create a namespace
kubectl create ns snyk-docker-aws

# Set the current context to use the new namespace
kubectl config set-context --current --namespace snyk-docker-aws

# Spin up the goof deployment and service
kubectl create -f manifests/  ## This deploys all yaml files in the manifests directory
```

To check the status of the pods as the application comes up, use the following command:

```sh
kubectl get all
```
The output should look something like this:
```angular2html
NAME                             READY   STATUS    RESTARTS   AGE
pod/goof-5ffc75cb65-2x7pc        1/1     Running   1          23s
pod/goof-image-84c747955-nm5g6   1/1     Running   0          23s
pod/goof-mongo-775d5b7d8-l4hk8   1/1     Running   0          23s

NAME                 TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)                          AGE
service/goof         LoadBalancer   172.20.179.35   a6ca225d0c95f448997251641b0ef105-60293525.us-east-1.elb.amazonaws.com    80:30576/TCP,9229:30182/TCP      23s
service/goof-image   LoadBalancer   172.20.152.83   a1f44eab3e1b248e3946b5d920062c8d-756943267.us-east-1.elb.amazonaws.com   3112:31300/TCP,31337:32270/TCP   23s
service/goof-mongo   ClusterIP      172.20.0.133    <none>                                                                   27017/TCP                        23s
service/kubernetes   ClusterIP      172.20.0.1      <none>                                                                   443/TCP                          38h

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/goof         1/1     1            1           23s
deployment.apps/goof-image   1/1     1            1           23s
deployment.apps/goof-mongo   1/1     1            1           23s

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/goof-5ffc75cb65        1         1         1       23s
replicaset.apps/goof-image-84c747955   1         1         1       23s
replicaset.apps/goof-mongo-775d5b7d8   1         1         1       23s
```

{{% notice info %}}
The pods should all show **"Running"** in their **STATUS** field, and services with a **LoadBalancer** type should have an IP or hostname for their **EXTERNAL-IP**.
<br>If either show a pending state, then wait a moment and re-run the command until they finish starting up. 
{{% /notice %}}

The following will save the `LoadBalancer` services `EXTERNAL_IP` values for later use:
```
GOOF_LB=$(kubectl get svc goof -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
GOOF_IMAGE_LB=$(kubectl get svc goof-image -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
```

Once both are running, the application should now be accessible at http://$GOOF_LB 

Success!