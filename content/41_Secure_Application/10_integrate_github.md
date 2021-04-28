+++
title = "Step 9: Monitor your Repo with Snyk"
chapter = false
weight = 10
+++

## Integrate Snyk with the Goof GitHub Repo

To check for issues in the application's Open Source dependencies, we use the Snyk GitHub integration to connect Snyk to the application's GitHub Repository.

1. Log in to [Snyk.io](snyk.io). Sign up if you haven't already.
2. Navigate to Integrations -> Source Control -> GitHub
3. Fill in your Account Credentials to Connect your GitHub Account.

## Import the Goof Repo into Snyk

Now that Snyk is connected to your GitHub Account, import the Repo into Snyk as a Project.

1. Click on Projects
2. Click "Add Project" then select "GitHub"
3. Click on the Repo for the Goof application.

## Review the list of Vulnerabilities

When the import completes, Snyk displays the issue counts next to the files that introduced the issues. Issues in the Open Source components in our Goof app are displayed next to the `package.json` file.

Before fixing any of these, let's explore an example of the invisible risks Open Source components can bundle into our application.
