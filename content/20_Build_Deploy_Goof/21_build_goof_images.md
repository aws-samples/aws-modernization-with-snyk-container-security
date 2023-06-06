+++
title = "Step 1: Build the Goof container image"
chapter = false
weight = 21
+++

Now that you've cloned the repo to your working environment, we'll build a few container images that run our application examples in Amazon Elastic Kubernetes Service (EKS) but before we can do anything, we need to create some ECR repositories to house the build images so EKS has somewhere to pull them from.

## Create the ECR repositories
The following commands will create 3 repositories for the images we will be building:

```sh
aws ecr create-repository --repository-name thumbnailer --region us-east-1
aws ecr create-repository --repository-name todolist --region us-east-1
aws ecr create-repository --repository-name log4shell-server --region us-east-1
```
After each finishes you should get a JSON reponse similar to the following:
```json
{
    "repository": {
        "repositoryArn": "arn:aws:ecr:us-east-1:012345678901:repository/thumbnailer",
        "registryId": "012345678901",
        "repositoryName": "thumbnailer",
        "repositoryUri": "012345678901.dkr.ecr.us-east-1.amazonaws.com/thumbnailer",
        "createdAt": "2023-06-05T16:02:53+00:00",
        "imageTagMutability": "MUTABLE",
        "imageScanningConfiguration": {
            "scanOnPush": false
        },
        "encryptionConfiguration": {
            "encryptionType": "AES256"
        }
    }
}
```
{{% notice tip %}}
If you need to re-retrieve your repository info in the future, you can run `aws ecr describe-repositories` to get a list of all of them.
{{% /notice %}}

In the response copy the value of the `registryId` and replace `[registryId]` in the command below which will store it in an environment variable for future use:
```sh
export ECR_REPO="[registryId].dkr.ecr.us-east-1.amazonaws.com"
```
Note: do not include the image tag in the above variable, just the account and domain.

## Log into your repositories
Next, we log into our repositories (one command logs you into any of your repositories)
```sh
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $ECR_REPO
```
This should return a `Login Succeeded` repsonse.

## Build container images

Now we will build the images. Be sure you are cd'ed into the cloned goof repo directory. (if you just completed the prerequisite sections, you might still be in the `cloud9-setup` sub-directory so run `cd ..` if needed.)

Once you are in the right directory, run the following commands to build the container images.
```sh
docker build -t $ECR_REPO/thumbnailer:latest thumbnailer

docker build -t $ECR_REPO/todolist:latest todolist

docker build -t $ECR_REPO/log4shell-server:latest todolist/exploits/log4shell-server

```

When all of the build processes are complete, if you run `docker images` you should see three rows like this:
```
$ docker images                                                                                                                                                             
REPOSITORY         TAG       IMAGE ID       CREATED          SIZE
012345678901.dkr.ecr.us-east-1.amazonaws.com/log4shell-server   latest    a42b0d443129   10 minutes ago   535MB
012345678901.dkr.ecr.us-east-1.amazonaws.com/todolist           latest    57ad8c044dbd   15 minutes ago   612MB
012345678901.dkr.ecr.us-east-1.amazonaws.com/thumbnailer        latest    3406c6d949b4   20 minutes ago   941MB
```

## Push container images to ECR
Next, we want to push the images to ECR but before we can push them we need to create their respective repositories.

```sh
docker push $ECR_REPO/thumbnailer:latest
docker push $ECR_REPO/todolist:latest
docker push $ECR_REPO/log4shell-server:latest

```

Once the pushes complete, log in to your [ECR repositories](https://us-east-1.console.aws.amazon.com/ecr/repositories?region=us-east-1) to see your new image repositories. 

![ecr-repos](/images/ecr-repos.png)