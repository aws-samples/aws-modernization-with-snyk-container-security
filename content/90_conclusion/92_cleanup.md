+++
title = "Cleanup"
chapter = false
weight = 92
+++

### Cleanup 
In order to prevent charges to your account we recommend cleaning up the infrastructure that was created. If you plan to keep things running so you can examine the workshop a bit more please remember to do the cleanup when you are done. It is very easy to leave things running in an AWS account, forget about it, and then accrue charges. Run the command below to remove all of the resources created for this workshop. It may take a few minutes to complete.

Here are the instructions to delete the CloudFormation Stack in the Hosted Event

```bash
# Delete CloudFormation Stacks
aws cloudformation delete-stack --stack-name $(aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE UPDATE_COMPLETE --query "StackSummaries[?StackName=='snyk-eks'].StackName" --output text) && echo 'Completed cleanup.'
```
If you have completed this workshop under your own account, you can follow these steps to remove all of the workshop resources:

```bash
# Delete Cloud9 Instance
aws cloud9 delete-environment --region us-west-2 --environment-id $(aws cloud9 list-environments --region us-west-2 --query "environmentIds[?contains(@, 'Snyk-Workshop')]" --output text)

# Delete EKS Cluster
eksctl delete cluster --name snyk-eks --region us-west-2
```
