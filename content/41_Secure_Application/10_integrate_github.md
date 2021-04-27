+++
title = "Step 9: Monitor your Repo with Snyk"
chapter = false
weight = 21
+++

## Integrate Snyk with the Goof GitHub Repo

To check for issues in the Open Source dependencies, we'll use the Snyk GitHub integration. 

First we need to connect Snyk to GitHub so we can import our Repository.

#TODO: Make this a pretty list.
Logging in to [Snyk.io](snyk.io). Sign up if you haven't already.
Navigating to Integrations -> Source Control -> GitHub
Fill in your Account Credentials to Connect your GitHub Account.

## Import the Goof Repo into Snyk

Now that Snyk is connected to your GitHub Account, import the Repo into Snyk as a Project.

#TODO: Make this a pretty list.
Navigate to Projects
Click "Add Project" then select "GitHub"
Click on the Repo you created.

## Review the list of Vulnerabilities

When the import completes, Snyk displays the issue counts next to the files that introduced the issues. Issues in the Open Source components in our Goof app are displayed next to the `package.json` file.

