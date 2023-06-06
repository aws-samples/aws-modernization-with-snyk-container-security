+++
title = "Clone the sample application repo"
chapter = false
weight = 16
+++

## Create your copy of the repo

A sample application, called Goof, is provided for this workshop as a GitHub template. Navigate to the [GitHub Repo for the Goof application](https://github.com/snyk-partners/goof) and click "Use this Template" and then "Create a new repository" to create a copy of the Repo to your personal GitHub account. 


![gh-template](/images/gh-use-template.png)

{{% notice info %}}
Be sure to name the new Repo `goof` otherwise things will break later on.
{{% /notice %}}

We recommend you make your copy have "public" visibility, it will simplify working with it during this workshop.

![gh-create-copy](/images/gh-create-copy.png)

To copy-paste the commands in the instructions set an environment variable with your GitHub ID. Your GitHub ID is displayed in the upper right corner in [GitHub.com](github.com).

![gh-id](/images/gh-id.png)

```sh
GithubId=<your_github_id>
```

## Clone the repo
After you create the Repo, clone the Repo to your Cloud9 environment by using the `git clone` command. Once the clone completes, change to the repo's top level directory. 

```sh
git clone https://github.com/$GithubId/goof && cd goof
```

This copies the Repo files to your Cloud9 environment. 

## Run setup scripts
In order to install all of the needed tools, there are acouple of setup scripts in the `cloud9-setup` dicrectory you should run:

### Tool setup
The `setup.sh` script installs and/or updates the following tools:

* kubectl (including aliasing it to `k` and setting up bash-completion)
* awscli
* jq
* yq
* pngcrush

```sh
cd cloud9-setup
./setup.sh
. ~/.bashrc #source the ~/.bashrc to make sure all environment settings are in place
```

## Configure kubeconfig
The `aws` CLI tool can update our kubeconfig file so that we have access to our EKS cluster
      
```sh
aws eks update-kubeconfig --name eksworkshop-eksctl
```

Now confirm that you have access to your EKS cluster by running the following command

```sh
kubectl get nodes
```

If you have access you should see something like the following:

```
NAME                              STATUS   ROLES    AGE    VERSION
ip-192-168-113-37.ec2.internal    Ready    <none>   104m   v1.27.1-eks-2f008fe
ip-192-168-140-151.ec2.internal   Ready    <none>   104m   v1.27.1-eks-2f008fe
ip-192-168-169-182.ec2.internal   Ready    <none>   104m   v1.27.1-eks-2f008fe
```

### Resize EBS storage

{{% notice info %}}
This workshop will require more volume on the EBS storage attached to the Cloud9 workspace instance. This section of instructions will show how to resize the volume.
{{% /notice %}}

{{% notice warning %}}
The Cloud9 workspace volume should be resized by an IAM user with Administrator privileges,
not the root account user. Please ensure you are logged in as an IAM user, not the root
account user.
{{% /notice %}}

- Still in the cloud9-setup directory run `resize.sh` using the command bellow. This will resize the volume to 30 GiB
```bash
$ ./resize.sh 30
```
- The script may take some time to complete. 

#### Verify the volume was resized succesffully. 
- Run `lsblk` to ensure that the disk is partitioned properly. The size of the partition with the`/` mountpoint and the overarching drive should be 30G.
```bash
$ lsblk
NAME          MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
nvme0n1       259:0    0  30G  0 disk 
├─nvme0n1p1   259:1    0  30G  0 part /
└─nvme0n1p128 259:2    0   1M  0 part 
```