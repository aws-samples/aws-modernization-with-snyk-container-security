+++
title = "Cleanup"
chapter = false
weight = 92
+++

### Cleanup 
In order to prevent charges to your account we recommend cleaning up the infrastructure that was created. If you plan to keep things running so you can examine the workshop a bit more please remember to do the cleanup when you are done. It is very easy to leave things running in an AWS account, forget about it, and then accrue charges.


```bash
# Delete CloudFormation Stacks
aws cloudformation delete-stack --stack-name mod-3b406ca5c0ea4006

echo 'Completed cleanup.'
```
