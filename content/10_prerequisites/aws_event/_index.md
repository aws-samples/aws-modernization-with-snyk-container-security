---
title: "AWS Event Engine"
chapter: true
weight: 10
---

# Attending an AWS hosted event

To complete this workshop, you will be provided with an AWS account via the AWS Event Engine service. A team hash will be provided to you by event staff.
Included in this environment will be a Cloud9 IDE and an EKS Kubernetes cluster pre-provisioned both pre-configured for your convenience.

{{% notice warning %}}
If you are currently logged in to an AWS Account, you can log out using this [link](https://console.aws.amazon.com/console/logout!doLogout)
{{% /notice %}}

### Logging into Event Engine Dashboard

1. Connect to the portal by clicking the button or browsing to [https://dashboard.eventengine.run/](https://dashboard.eventengine.run/). The following screen shows up. Enter the provided hash in the text box. The button in the bottom right corner changes to **Accept Terms & Login**. Click on that button to continue.

   ![Event Engine](/images/event-engine-initial-screen.png)

2. Choose **AWS Console**, then **Open AWS Console**.

   ![Event Engine Dashboard](/images/event-engine-dashboard.png)

3. Use a single region for the duration of this workshop. This workshop supports the following regions:

* us-east-1 (US East - Virginia)

**If your region is something set to a region that is not us-east-1, please let the person running the event know**


![Event Engine Region](/images/modernization-workshop-region-check.png)

{{% notice warning %}}
This account will expire at the end of the workshop and  all the resources created will be automatically de-provisioned. You will not be able to access this account after today.
{{% /notice %}}

### Next step

Once you have completed the step above, you can leave the AWS console open. You can now move to the [next step](/10_prerequisites/aws_event/11_cloud9-setup.html) and begin setup of your Cloud9 environment.
