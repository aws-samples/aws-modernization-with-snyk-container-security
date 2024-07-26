---
title: "Create a workspace"
chapter: false
weight: 12
---
The Cloud9 workspace should be built by an IAM user with Administrator privileges,
not the root account user. Please ensure you are logged in as an IAM user, not the root
account user.

Ad blockers, javascript disablers, and tracking blockers should be disabled for
the cloud9 domain, or connecting to the workspace might be impacted.
Cloud9 requires third-party-cookies. You can whitelist the [specific domains]( https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-env-loading).


### Launch Cloud9:
Create a Cloud9 Environment: [https://console.aws.amazon.com/cloud9/home](https://console.aws.amazon.com/cloud9/home)

1. Select **Create environment**
2. Name it **Snyk-Workshop** and click **Next Step**
3. Use the following table and refer to the screenshot below for the configuration settings:

    |    Environment Setting   |   Value    |
    |----------|--------------------|
    | Envrionment Type | New EC2 instance |
    | Instance Type | t2.large |
    | Platform | Ubuntu Server 18.04 LTS |
    | Network settings | AWS Systems Manager (SSM) |
![c9-create](/images/c9-create.png)

4. Click **Next Step** and then  **Create Environment**
5.  When it comes up, customize the environment by closing the **welcome tab**
and **lower work area**, and opening a new **terminal** tab in the main work area. Your workspace should now look like this:
![create-workspace](/images/create-workspace.png)
{{% notice info %}}
Cloud9 normally manages IAM credentials dynamically. However, for the purpose of this workshop, we need the temporary tokens to be in environment variables.
{{% /notice %}}
6. Click the gear icon (in top right corner), or click to open a new tab and choose "Open Preferences"

7. Select **AWS SETTINGS** 

8. Turn off **AWS managed temporary credentials**

9. Close the Preferences tab
   ![cloud9-config](/images/c9disableiam.png)
