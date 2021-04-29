+++
title = "Step 11: Fix a vulnerability with a Snyk Pull Request"
chapter = false
weight = 30
+++

## Fix the vulnerability using a Snyk Pull Request

Snyk accelerates remediation via Pull Requests to upgrade dependencies to non-vulnerable versions. Back in Snyk, click into the `package.json` project.

![snyk-project-list](/images/snyk-project-list.png)

Now scroll down to see the list of vulnerabilities. For each Vulnerability, Snyk displays:

- The module that introduced it and, in the case of transitive dependencies, its direct dependency,
- Details on the path and proposed Remediation, as well as the specific vulnerable function.

Find the Directory Traversal vulnerability in `st` by searching for it in the search bar.

![dir-traversal-issue](/images/dir-traversal-issue.png)

Since a fix is available, Snyk can upgrade the vulnerable dependency to a non-vulnerable version through a Pull Request. Click on "Fix this vulnerability" to do so. 

![fix-st-vuln](/images/fix-st-vuln.png)

In the next screen, confirm the issue, then click the button to "Open a Fix PR".

![open-fix-pr](/images/open-fix-pr.png)

## Review the changes in the GitHub Pull Request view.

When the Pull Request is ready, you're taken to GitHub, where you can review the changes in the file diff view. 

![review-fix-pr](/images/review-fix-pr.png)

Review the changes, then merge the PR when ready. 

