---
title: "VSCode Server Setup"
chapter: true
weight: 18
---

# Accessing the VS Code Server

## Step 1: Navigate to CloudFormation Outputs

- Open the AWS Management Console and navigate to the **CloudFormation** service.
- Select the vscode-server stack deployed for the workshop.
- Go to the **Outputs** tab in the stack details.
- You will find the following details:
  - **VSCODEURL**: This is the URL to access the VS Code server.
  - **Password**: This is the password required to log in to the server.

![CloudFormation Outputs](/images/cloudformation-outputs.png)

## Step 2: Copy the Password

- Copy the **Password** value from the CloudFormation Outputs to your clipboard.

## Step 3: Access the VS Code Server

- Click on the **VSCODEURL** link in the CloudFormation Outputs section.
- A browser window will open, prompting you to enter a password.

![VS Code Login](/images/Vscode-server-login.png)

## Step 4: Enter the Password

- Paste the password you copied earlier into the password field.
- Click **Login** to proceed.

## Step 5: Start Coding!

- You now have access to the VS Code server, which is securely fronted by CloudFront.

![VS Code Interface](/images/Vscode-server-interface.png)

**Note**: Ensure you use the latest version of your browser for the best experience. If you encounter issues accessing the server, try clearing your browser cache or contacting the workshop support team.
