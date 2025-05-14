---
title: "Snyk CLI"
chapter: true
weight: 17
---

# Snyk Setup Instructions
You will need a Snyk account to run scans.  Snyk is available for free and all you need is a valid email address to register.  Once you register, you can perform scans and view results locally or on the website.

### Create or Login to Snyk account
[Login or Create a free account here.](https://snyk.co/KubeConUS-2023)

### Create Snyk Access Token
- Visit your Snyk account (Account Settings > Auth Token section) (https://app.snyk.io/account)
- In the KEY field, select click to show, then select and copy your Auth token from the field
- Paste the token that appears on the screen in a safe location for use in future modules

{{% notice warning %}}
<p style='text-align: left;'>
Your Snyk access token must be protected and not shared with unauthorized parties to prevent exposure and unauthorized access.
</p>
{{% /notice %}}

You can read more about Snyk Access Token from their docs here.

## Setting up the Snyk CLI

The Snyk Command-Line-Interface (CLI) is highly portable and very popular with end users. We’ll use the Snyk CLI in this workshop to collect and send results about your vulnerabilities.

Start by downloading the Snyk CLI to your environment. In this workshop, we’ll prescribe steps to save time and you can find more details on the Snyk documentation site at:
https://docs.snyk.io/snyk-cli/install-the-snyk-cli

### **Note:**
If you are running this through an AWS Hosted Event, the Snyk CLI has already been installed on your Cloud9 instance.

### Installing Snyk CLI
If you are running this workshop at your own pace, you will need to install the Snyk CLI yourself. At the Cloud9 prompt, enter these commands to download the binary for Linux and move them to your bin folder (/usr/local/bin):

```bash
curl -Lo ./snyk https://static.snyk.io/cli/latest/snyk-linux-arm64 && \
chmod +x ./snyk && \
sudo mv ./snyk /usr/local/bin/
```

## Authenticating the Snyk CLI
In both AWS-hosted events and self-paced environments, you will need to authenticate the CLI with your Auth token.  Previously, you should have created an Auth token.  If not, navigate to your Snyk Account (https://app.snyk.io/account), and get your AUTH_TOKEN by clicking into your Account Settings -> Auth Token section.

In the KEY field, click your “click to show” box to copy your Auth token.

You can then run this command where REPLACE_ME is the value you copied.

```bash
snyk auth REPLACE_ME
```

That should be it!  Your response should look like the following:

    snyk auth 12345678-abcd-efgh-1234head5678bead

    Your account has been authenticated. Snyk is now ready to be used.

If you are not on a Cloud9 environment, then your CLI should be able to start up a web browser and you can authenticate with this command:

```bash
snyk auth
```

In this case, you'll authenticate by logging on with the web UI of Snyk.

