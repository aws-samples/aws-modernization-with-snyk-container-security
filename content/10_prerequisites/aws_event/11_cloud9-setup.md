---
title: "Cloud9 Setup"
chapter: true
weight: 11
---

## Set up the Workspace

[AWS Cloud9](https://aws.amazon.com/cloud9/) is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your laptop for this workshop.

## Access Cloud9 in AWS Management Console 

Once you have logged into the AWS Management Console from your EventEngine team landing page, you will already have an EKS cluster and Cloud9 environment. A few additional steps are required to configure Cloud9 and install the tools as follows. Below set of instructions are also available in the **readme** link in the Event Engine Dashboard.


![cloudd9](/images/event-engine-cloud9-dashboard.png)

Click on the **Open IDE** button and you will see your pre-configured environment. 

## Lab environment
Once you have logged into the AWS Management Console from your EventEngine team landing page, you will already have an EKS cluster and Cloud9 environment. A few additional steps are required to configure Cloud9. Please follow the steps below.

1. Navigate to Cloud9 in the AWS Management console and launch the EKS IDE. It may take a few minutes to start.
* Select the gear icon in the upper right
    - Scroll down to "AWS Settings" in the "Preferences" tab.
    - Under "Credentials", disable "AWS managed temporary credentials".
    - Close the "Preferences" tab.
    - Close the "AWS Cloud9 Welcome" and "AWS Toolkit" tabs.

![turnoffmanagedcredentials](/images/cloud9-turn-off-managed-credentails.png)

{{% notice tip %}}
Cloud9 requires third-party-cookies. You can whitelist the [specific domains](https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-env-loading).  You are having issues with this, Ad blockers, javascript disablers, and tracking blockers should be disabled for the cloud9 domain, or connecting to the workspace might be impacted.
{{% /notice %}}