---
title: "Create an IAM Role and Policy for your workspace"
chapter: true
weight: 13
---

# Create a policy for your Cloud9 IAM Role [this link](https://console.aws.amazon.com/iamv2/home#/policies/create)

Click on `Json` and delete the existing blank policy and paste the contents below in the policy editor:

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloud9:GetMigrationExperiences",
        "cloud9:ListEnvironments",
        "cloud9:UpdateUserSettings",
        "cloud9:DescribeEC2Remote",
        "cloud9:DescribeEnvironmentMemberships",
        "cloud9:DescribeEnvironmentStatus",
        "cloud9:DescribeEnvironments",
        "cloud9:GetEnvironmentConfig",
        "cloud9:GetEnvironmentSettings",
        "cloud9:ListTagsForResource",
        "cloud9:UpdateEnvironment",
        "cloud9:UpdateEnvironmentSettings",
        "cloud9:UpdateMembershipSettings",
        "ec2:DescribeRegions"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "kms:Decrypt",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ecr:BatchCheckLayerAvailability",
        "ecr:BatchDeleteImage",
        "ecr:BatchGetImage",
        "ecr:CompleteLayerUpload",
        "ecr:CreateRepository",
        "ecr:DeleteRepository",
        "ecr:DeleteRepositoryPolicy",
        "ecr:DescribeRepositories",
        "ecr:GetAuthorizationToken",
        "ecr:GetDownloadUrlForLayer",
        "ecr:GetLifecyclePolicy",
        "ecr:GetLifecyclePolicyPreview",
        "ecr:GetRepositoryPolicy",
        "ecr:InitiateLayerUpload",
        "ecr:ListImages",
        "ecr:ListTagsForResource",
        "ecr:PutImage",
        "ecr:PutLifecyclePolicy",
        "ecr:SetRepositoryPolicy",
        "ecr:StartLifecyclePolicyPreview",
        "ecr:UploadLayerPart"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "eks:CreateCluster",
        "eks:DescribeCluster",
        "eks:DeleteCluster",
        "eks:ListClusters",
        "eks:UpdateClusterConfig",
        "eks:UpdateClusterVersion",
        "eks:CreateNodegroup",
        "eks:DescribeNodegroup",
        "eks:DeleteNodegroup",
        "eks:ListNodegroups",
        "eks:UpdateNodegroupConfig"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:CreateVpc",
        "ec2:DescribeVpcs",
        "ec2:DeleteVpc",
        "ec2:CreateSecurityGroup",
        "ec2:DescribeSecurityGroups",
        "ec2:AuthorizeSecurityGroupIngress",
        "ec2:RevokeSecurityGroupIngress",
        "ec2:CreateSubnet",
        "ec2:DescribeSubnets",
        "ec2:CreateInternetGateway",
        "ec2:DescribeInternetGateways",
        "ec2:AttachInternetGateway",
        "ec2:CreateRouteTable",
        "ec2:DescribeRouteTables",
        "ec2:AssociateRouteTable",
        "ec2:CreateRoute",
        "ec2:DescribeNatGateways",
        "ec2:CreateNatGateway",
        "ec2:DescribeInstances",
        "ec2:TerminateInstances",
        "ec2:RunInstances"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:CreateRole",
        "iam:DeleteRole",
        "iam:AttachRolePolicy",
        "iam:DetachRolePolicy",
        "iam:PassRole",
        "iam:CreateServiceLinkedRole",
        "iam:GetRole",
        "iam:ListRoles"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:CreateStack",
        "cloudformation:DescribeStacks",
        "cloudformation:DeleteStack",
        "cloudformation:UpdateStack",
        "cloudformation:ListStacks"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "autoscaling:CreateAutoScalingGroup",
        "autoscaling:UpdateAutoScalingGroup",
        "autoscaling:DeleteAutoScalingGroup",
        "autoscaling:DescribeAutoScalingGroups",
        "autoscaling:CreateLaunchConfiguration",
        "autoscaling:DeleteLaunchConfiguration",
        "autoscaling:DescribeLaunchConfigurations"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "elasticloadbalancing:CreateLoadBalancer",
        "elasticloadbalancing:DescribeLoadBalancers",
        "elasticloadbalancing:DeleteLoadBalancer",
        "elasticloadbalancing:CreateListener",
        "elasticloadbalancing:DeleteListener",
        "elasticloadbalancing:DescribeListeners"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudwatch:PutMetricAlarm",
        "cloudwatch:DescribeAlarms",
        "cloudwatch:DeleteAlarms"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:CreateBucket",
        "s3:PutObject",
        "s3:GetObject",
        "s3:DeleteObject",
        "s3:ListBucket"
      ],
      "Resource": "*"
    }
  ]
}
```

Click on Json:

![aws-iam-policy-json](/images/click-json-policy.png)

Click Next:

![aws-iam-policy-json-next](/images/click-next-policy.png)

Name the policy: `workshop-cloud9`

You can optinally provide a description if you like.

![aws-iam-policy-name](/images/policy-name.png)

Create the policy:

![aws-iam-policy-name](/images/create-policy.png)




## Create IAM Role for your workspace

You will need to assign an IAM Role to your Cloud9 instance following least privilege.  This section walks you through those steps.

## Select the service
Follow [this link](https://console.aws.amazon.com/iamv2/home#/roles/create) to create an IAM role.

1. Click on AWS Service
1. Select the EC2 use case
1. Click on the Next button below

![aws-iam-role-step-1](/images/trusted-entity.png)

## Add permissions

Next, add the workshop-cloud9 permissions policy.

2. Search for `workshop-cloud9` to filter results
2. Check the box for workshop-cloud9
2. Click on Next below

![aws-iam-role-step-2](/images/add-permissions.png)

## Name, review, and create

3. Name your role `workshop-cloud9-role`
NOTE: in your environment, you would enter a description and tags per your company guidelines.

![aws-iam-role-step-3](/images/name-role.png)

3.Create Role

![aws-iam-role-step-3](/images/create-role.png)





### Next Section: Attach IAM Role
Now that we've created our IAM Role, we can attach it in our next section.
