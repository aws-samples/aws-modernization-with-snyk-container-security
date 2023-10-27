---
title: "Provision an Amazon EKS cluster"
chapter: true
weight: 15
---

# Introduction

In this section, we describe how to create an EKS cluster.

You will need a few things to provision the cluster.  Some are covered in other sections of this workshop:

**Prerequisites**
- You have to create an AWS user, plus AWS keys.  This user will deploy your container to your cluster from your pipeline.
- Ensure you have a keypair available to you
- Attach a new IAM role for Cloud9 for permissions
- Disable AWS managed temporary credentials in Cloud9

## Install eksctl

You'll need to install the `eksctl` command line tool to your Cloud9 environment.  From a terminal in Cloud9, enter these commands to download and install the binary:

```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
```

```
sudo mv /tmp/eksctl /usr/local/bin
```

This should get you the binary where the following command should show how many EKS clusters you have in your environment.  At the start of the workshop, you will have no clusters.

```
eksctl get cluster --region us-east-1
```

## Install kubectl

You'll need to install `kubectl` command line tool to your Cloud9 environment.  From a terminal in Cloud9, enter these commands to download and install the binary.  We separate the commands one-at-a-time to ensure they work for you.

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

```
chmod +x ./kubectl
```

```
sudo mv ./kubectl /usr/local/bin/kubectl
```

```
kubectl version --output=yaml
```


## CLI Invocation

One easy way to setup an EKS cluster is to run the command as shown below in your Cloud9 environment.

```
eksctl create cluster --name eksworkshop-eksctl \
        --region us-east-1 \
        --zones=us-east-1a,us-east-1b,us-east-1c \
        --instance-types=t3.small,t3.medium,t3.large,t2.medium,t2.small \
        --version=1.27 \
        --with-oidc 
```

This command takes between 20-40 minutes to run, so it is optional for most live workshops.  
