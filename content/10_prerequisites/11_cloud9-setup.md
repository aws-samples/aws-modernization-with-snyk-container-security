---
title: "AWS Cloud9 Setup"
chapter: true
weight: 11
---

## Set up the Workspace

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your laptop for this workshop.

## Access AWS Cloud9 in AWS Management Console 

Once you have logged into the AWS Management Console from your Workshop Studio event dashboard page, you will already have an EKS cluster and Cloud9 environment. [Click here to access your AWS Cloud9 instance](https://us-west-2.console.aws.amazon.com/cloud9control/home?region=us-west-2#/product)

![cloudd9](/images/workshop-studio-cloud9-dashboard.png)

Click on the **Open** button under the **Cloud9 IDE** column header and you will see your pre-configured environment.  Go ahead close the "Welcome" tab to reduce clutter.

![cloud9 ide](/images/cloud9-initial.png)

{{% notice tip %}}
Cloud9 requires third-party-cookies. You can whitelist the [specific domains](https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-env-loading).  You are having issues with this, Ad blockers, javascript disablers, and tracking blockers should be disabled for the cloud9 domain, or connecting to the workspace might be impacted.
{{% /notice %}}
