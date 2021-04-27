+++
title = "Step 11: Fix a vulnerability with a Snyk Pull Request"
chapter = false
weight = 21
+++

## Fix the vulnerability using a Snyk Pull Request

Snyk accelerates remediation via Pull Requests to upgrade dependencies to non-vulnerable versions. In Snyk, click into the `package.json` project, and scroll down to see the list of vulnerabilities. For each Vulnerability, Snyk displays:

#TODO: Bulleted list!
The module that introduced it and, in the case of transitive dependencies, its direct dependency,
Details on the path and proposed Remediation, as well as the specific vulnerable function.

Find the Directory Traversal vulnerability in `st` by searching for it in the search bar.

Since a fix is available, Snyk can automatically upgrade the vulnerable dependency to a non-vulnerable version through a Pull Request. Click on "Fix this vulnerability" to do so. In the next screen, confirm the issue to fix with this PR.

## Review the changes in the GitHub Pull Request view.

Once the Pull Request is ready, you're taken to the PR in GitHub, where you can review the changes in the file diff view. Review the changes to ensure everything looks good, then merge the PR. 

