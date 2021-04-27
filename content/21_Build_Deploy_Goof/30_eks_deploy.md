+++
title = "Step 3: Deploy the application to EKS"
chapter = false
weight = 21
+++

## Deploy Goof to EKS

For this workshop we created an Amazon EKS cluster where we run the Goof app. Before deploying the app, you'll need to make a change to the app's deployment manifest. Open the file goof-deployment.yaml in the Cloud9 Editor.

Find these lines, and insert your Docker ID where indicated.

```
spec:
  containers:
  - image: <<DOCKERID>>/goof:latest #Edit with your Docker Hub ID
    name: goof
    imagePullPolicy: Always
```

Save your changes. Now you're ready to deploy the application. Run the following commands:

```sh
# Create a namespace
kubectl create ns snyk-docker-aws

# Set the current context to use the new namespace
kubectl config set-context --current --namespace snyk-docker-aws

# Spin up the goof deployment and service
kubectl create -f goof-deployment.yaml,goof-service.yaml
```

To check the status of the pods as the application comes up, use the following command:

```sh
kubectl get all
```

#TODO: Add the EKS endpoint where the app is accessible.

Once both are running, the application should now be accessible in <<<URL>>>. Success!