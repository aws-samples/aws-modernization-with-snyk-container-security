---
title: "Update IAM settings for your Workspace"
chapter: false
weight: 19
---

## Configure workspace for Docker Workshop

{{% notice info %}}
Cloud9 normally manages IAM credentials dynamically. However, for the purpose of this workshop, we need the temporary tokens to be in environment variables.
{{% /notice %}}

1. Return to your workspace and click the gear icon (in top right corner), or click to open a new tab and choose "Open Preferences"

2. Select **AWS SETTINGS** and turn off **AWS managed temporary credentials**

3. Close the Preferences tab
   ![cloud9-config](/images/c9disableiam.png)

4. Copy and run (paste with **Ctrl+P**) the commands below.
   Before running it, review what it does by reading through the comments.


      ```sh
      rm -vf ${HOME}/.aws/credentials
      export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
      export AWS_DEFAULT_REGION=us-east-1
      ```

5. The last thing we need to do in order to complete this step is to update our kubeconfig file so that we have access to our EKS cluster
      
      ```sh
      aws eks update-kubeconfig --name basic-eks --region us-east-1
      ```

6. Confirm that you have access to your EKS cluster by running the following command

      ```sh
      kubectl get nodes
      ```
      If you have access you should see the following

         ```
         NAME                        STATUS   ROLES    AGE   VERSION
         ip-10-0-17-2.ec2.internal   Ready    <none>   21h   v1.18.9-eks-d1db3c
         ```

In the next step we will go ahead and create a Snyk account