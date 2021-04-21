---
title: "Configure Docker on Cloud9"
chapter: false
weight: 21
---


Your Cloud9 environment comes prebuilt with a version of Docker that doesn't have the features that we will need for this workshop. Please follow the steps below to install and verify that you have the correct version

1. Open the terminal on Cloud9 and run the following: 

```sh
sudo apt install jq -y
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update -y
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
sudo echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null    
sudo apt-get update -y
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker vagrant
docker version
docker compose
```

You should receive results as follows

![create-role](/images/docker-compose-installation.png)

You have now completed all the steps necessary to go through the workshop on your Cloud9 workspace. 