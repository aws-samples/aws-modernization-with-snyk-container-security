---
title: "Attach IAM Role"
chapter: true
weight: 14
---

# Attaching an IAM Role

In this section we attach the IAM role to grant your EC2 instance permission to create resources.

## Find the Cloud9 EC2 instance
Access the EC2 instance running your Cloud9 environment by either of the following means:

* Follow [this link](https://us-east-1.console.aws.amazon.com/ec2/v2/home?region=us-east-1#Instances:search=cloud9-Snyk-Workshop;sort=desc:launchTime) to find your Cloud9 EC2 instance, or... 
* In the [Cloud9 dashboard](https://us-east-1.console.aws.amazon.com/cloud9control/home?region=us-east-1#/) open your environment and click on the "Manage EC2 Instance" button on the right side of the page.

![](/images/c9-manage-ec2-inst.png)

## Open IAM Role settings for the instance

1. Select the instance
1. Select Actions / Security / Modify IAM role Attach IAM role

![aws-assign-role-step-1](/images/aws-assign-role-1.png)

## Modify IAM Role

2. Choose the role that we created in the previous step: [Create IAM Role for your workspace](13_createaniamroleforyourworkspace.html)
2. Click on Update IAM Role

![aws-assign-role-step-1](/images/aws-assign-role-2.png)


This completes the process to assign the new role.
