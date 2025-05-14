+++
title = "Cleanup"
chapter = false
weight = 92
+++

### Cleanup 
In order to prevent charges to your account we recommend cleaning up the infrastructure that was created. If you plan to keep things running so you can examine the workshop a bit more please remember to do the cleanup when you are done. It is very easy to leave things running in an AWS account, forget about it, and then accrue charges. Run the command below to remove all of the resources created for this workshop. It may take a few minutes to complete.

Here are the instructions to delete the CloudFormation Stack in the Hosted Event. This will clean up all the workshop resources.

```bash
# Delete CloudFormation Stacks
aws cloudformation delete-stack --stack-name $(aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE UPDATE_COMPLETE --query "StackSummaries[0].StackName" --output text)
```
If you have completed this workshop under your own account, you can follow these steps to remove all of the workshop resources:

```bash
# Delete VS Code Server Instance
aws cloudformation delete-stack --stack-name vscode-server --region us-west-2

# Delete ECR Registries
aws ecr delete-repository --repository-name thumbnailer --force --region us-west-2 && \
aws ecr delete-repository --repository-name todolist --force --region us-west-2 && \
aws ecr delete-repository --repository-name log4shell-server --force --region us-west-2


# Delete EKS Cluster
eksctl delete cluster --name snyk-eks --region us-west-2
```
