---
title: "Attach the IAM role to your Workspace"
chapter: false
weight: 17
---

1. Follow [this deep link to find your Cloud9 EC2 instance](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#Instances:tag:Name=aws-cloud9-docker-snyk;sort=desc:launchTime) <br> Note: If no instances are found, click the gear icon in the top right corner and verfiy that "Use regular expression matching" is enabled.
1. Select the instance, then choose **Actions / Security / Modify IAM Role**
![c9instancerole](/images/attach-role.png)
1. Choose **mod-c3323268de154886-EKSStack-1OVJRE9V-BastionRole-1FFSLTAUE5LK8** from the **IAM Role** drop down, and select **Apply**
![c9attachrole](/images/snyk-docker-modify-iam.png)