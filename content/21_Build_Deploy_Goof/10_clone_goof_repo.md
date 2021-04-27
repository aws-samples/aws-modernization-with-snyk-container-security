+++
title = "Step 1: Clone the sample Goof application"
chapter = false
weight = 21
+++

## Prepare the Sample Application

A sample application, called Goof, is provided for this workshop as a GitHub template. Navigate to the [GitHub Repo for the Goof application](https://github.com/snyk-partners/goof) and click "Use this Template" to create a copy of the Repo to your personal GitHub account. 

To copy-paste the commands in the instructions set an environment variable with your GitHub ID. 

```sh
GithubId=<your_github_id>
```

After you create the Repo, clone the Repo to your Cloud9 environment by using the `git clone` command. Once the clone completes, change to the repo's top level directory. 

```sh
git clone https://github.com/$GithubId/goof && cd goof
```

This copies the Repo files to your Cloud9 environment. 