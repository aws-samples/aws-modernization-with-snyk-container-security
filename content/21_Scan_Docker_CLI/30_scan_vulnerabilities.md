+++
title = "Step 3: Scan image for vulnerabilities with the Docker CLI"
chapter = false
weight = 23
+++

## Scan image for vulnerabilities with the Docker CLI

{{% notice tip %}}
A Snyk account is not necessary, however, you can only scan 10 times without logging in. [Sign up for Snyk using your Docker ID](https://snyk.io), then run `docker scan --login`and sign in to unlock 200 free scans per month.
{{% /notice %}}

Use `docker scan` to scan for vulnerabilities. It's a best practice to pass the `Dockerfile` used to build the image with `--file` to get more robust results that include vulnerabilities from Dockerfile instruction and base image upgrade guidance. For example,

To scan goof:dev, and pass the Dockerfile:

```bash
# Scanning the goof:dev image and passing the Dockerfile 
docker scan goof:dev --file=Dockerfile
```

{{% notice tip %}}
Check out the [Docker Scan documentation](https://docs.docker.com/engine/scan/) for all possible CLI options.
{{% /notice %}}

Scanning images for Open Source vulnerabilities with Snyk is that easy! When finished, scan results are displayed in the Terminal, along with remediation guidance.