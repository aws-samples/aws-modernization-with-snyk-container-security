+++
title = "Step 6: Monitor your Repo with Snyk"
chapter = false
weight = 41
+++

## Integrate Snyk with the Goof GitHub Repo

To check for issues in the application's Open Source dependencies, in this example we will use the Snyk GitHub integration to connect Snyk to the application's GitHub Repository.

### Set up GitHub integration

1. Log in to [Snyk.io](snyk.io). Sign up if you haven't already.
If this is the first time you've used your Snyk account on the website, you may see a screen like this. If so, go ahead and click the "Skip for now" link at the top-right corner of the page.
![snyk-new-user](/images/snyk-gh-new.png)
2. Navigate to Integrations -> Source Control -> GitHub
![snyk-gh-integration](/images/snyk-gh-integration.png)
3. Fill in your Account Credentials to Connect your GitHub Account.

### Import the Goof Repo into Snyk
Now that Snyk is connected to your GitHub Account, import the Repo into Snyk as a Project.

1. Click on Projects
2. Click "Add Project" then select "GitHub"

![snyk-gh-import](/images/snyk-gh-import.png)

3. Click on the Repo for the Goof application.

## Review the list of Vulnerabilities

When the import completes, Snyk displays the issue counts next to the files that introduced the issues. Issues in the Open Source components in our Goof app are displayed, the one we will be looking at are in the Maven `todolist/todolist-web-struts/pom.xml` file.

![snyk-project-list](/images/snyk-project-list.png)

Before investigating the issues, let's explore an example of the invisible risks Open Source components can bundle into our application.
