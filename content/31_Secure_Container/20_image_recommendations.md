+++
title = "Step 5: Scan the Container Image for Vulnerabilities"
chapter = false
weight = 21
+++

## Scan the Container Image for Vulnerabilities

Vulnerable components like the version of ImageMagick present in our container image can be identified by Snyk. Developers using the Docker CLI can `docker scan` containers to get vulnerability information and base image upgrade guidance. 

Scan the image by running the following command (assuming you are cd'ed to the top level directory in your goof repo). 

```sh
docker scan $DockerId/goof-image:latest --file=image-app/Dockerfile
```

When the scan completes, review the list of vulnerabilities. There are quite a few! If available.  Often, Snyk will recommend other potential base images to help you build your container with as few vulnerabilities as possible, however, in this case our base image is so old that it is not supported:

```text
...
Package manager:   deb
Target file:       /app/Dockerfile
Project name:      docker-image|ericsmalling/goof-image
Docker image:      ericsmalling/goof-image:latest
Platform:          linux/amd64
Base image:        node:6.1.0-wheezy

Tested 338 dependencies for known vulnerabilities, found 36 vulnerabilities.

Recommendations for node:6.1.0-wheezy are not available, as we haven't found any recent updates to this base image.
Consider upgrading your base image.
See above for details and fixes on individual vulnerabilities
Debian 7 is no longer supported by the Debian maintainers. Vulnerability detection may be affected by a lack of security updates.
```
This happens for very old images where the owning project team's have ceased support.  It is important to get onto a newer base image but we may not want to change versions of node just yet.  In this situation, often we will switch to the latest image for the project at the major version were currently at.  Since we are currently running on `node:6-wheezy`, let's switch to `node:6` and rebuilt the image.

Double click on the `Dockerfile` under the `image-app` directory in your Cloud9 IDE sidebar and change the first line from:
```docker
FROM node:6.1.0-wheezy
```
To:
```docker
FROM node:6
```

Now, rebuild the image:
```bash
cd image-app
docker build -t $DockerId/goof-image .
```
 ... and let's re-scan it:
```bash
docker scan $DockerId/goof-image --file Dockerfile
```

This time you should see a lot more information, including recommendations for upgrades to the base image:
```text
...
✗ High severity vulnerability found in node
  Description: Improper Certificate Validation
  Info: https://snyk.io/vuln/SNYK-UPSTREAM-NODE-1243765
  Introduced through: node@6.17.1
  From: node@6.17.1
  Image layer: Introduced by your base image (node:6)
  Fixed in: 15.14.0, 14.16.1, 12.22.1, 10.24.1

Organization:      eric-smalling-snyk
Package manager:   deb
Target file:       Dockerfile
Project name:      docker-image|goof
Docker image:      goof:6
Platform:          linux/amd64
Base image:        node:6
Licenses:          enabled

Tested 413 dependencies for known issues, found 876 issues.

Base Image  Vulnerabilities  Severity
node:6      876              228 high, 196 medium, 452 low

Recommendations for base image upgrade:

Major upgrades
Base Image    Vulnerabilities  Severity
node:14.16.1  526              55 high, 51 medium, 420 low

Alternative image types
Base Image                Vulnerabilities  Severity
node:15.14-buster-slim    56               12 high, 5 medium, 39 low
node:current-buster-slim  56               12 high, 5 medium, 39 low
node:erbium-slim          70               15 high, 8 medium, 47 low
node:15-buster            299              25 high, 43 medium, 231 low
```

If you search through 
Snyk recommends less vulnerable base images grouped by how likely they are to be compatible:

- Minor upgrades are the most likely to be compatible with little work,
- Major upgrades can introduce breaking changes depending on image usage,
- Alternative architecture images are shown for more technical users to investigate.

Continue to the next Step to select another base image for our application.

