---
title: "Create an IAM Role for your workspace"
chapter: true
weight: 13
---

# Create an IAM Role for your workspace

You will need to assign an IAM Role to your Cloud9 instance for Administrative operations.  This section walks you through those steps.

## Select the service
Follow [this link](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/roles/create) to create an IAM role with administrator access.

1. Click on AWS Service
1. Select the EC2 use case
1. Click on the Next button

![aws-iam-role-step-1](/images/aws-iam-role-1.png)

## Add permissions

Next, add the AdministratorAccess permissions policy.

2. Search for `AdministratorAccess` to filter results
2. Check the box for AdministratorAccess
2. Click on Next

![aws-iam-role-step-2](/images/aws-iam-role-2.png)

## Name, review, and create

3. Name your policy `workshop-cloud9`
3. Click on Create role

NOTE: in your environment, you would enter a description and tags per your company guidelines.

![aws-iam-role-step-3](/images/aws-iam-role-3.png)


### Next Section: Attach IAM Role
Now that we've created our IAM Role, we can attach it in our next section.
