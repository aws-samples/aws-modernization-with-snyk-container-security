+++
title = "Step 4: Scan the Container Image for Vulnerabilities"
chapter = false
weight = 32
+++

## Scan the Container Image for Vulnerabilities

Vulnerable components like the version of ImageMagick present in our container image can be identified by Snyk. Developers using the Snyk CLI can run `snyk container test` to scan containers to get vulnerability information and base image upgrade guidance. 

Scan the image by running the following command (assuming you are cd'ed to the thumbnailer directory of your goof repo). 

```sh
snyk container test $ECR_REPO/thumbnailer:latest --file=Dockerfile --exclude-app-vulns
```

When the scan completes, review the list of vulnerabilities. There are quite a few!

```text
...
Package manager:   deb
Target file:       Dockerfile
Project name:      docker-image|648839523175.dkr.ecr.us-east-1.amazonaws.com/thumbnailer
Docker image:      648839523175.dkr.ecr.us-east-1.amazonaws.com/thumbnailer:latest
Platform:          linux/amd64
Base image:        python:3.11.1
Licenses:          enabled

Tested 427 dependencies for known issues, found 333 issues.

Base Image     Vulnerabilities  Severity
python:3.11.1  333              6 critical, 16 high, 65 medium, 246 low

Recommendations for base image upgrade:

Minor upgrades
Base Image       Vulnerabilities  Severity
python:3.12.0b1  256              4 critical, 4 high, 5 medium, 243 low

Alternative image types
Base Image                   Vulnerabilities  Severity
python:3.12.0b1-slim         54               0 critical, 1 high, 2 medium, 51 low
python:3-slim-bullseye       54               0 critical, 1 high, 2 medium, 51 low
python:3.12.0b1-slim-buster  79               1 critical, 2 high, 1 medium, 75 low
python:3.12-rc-buster        367              2 critical, 9 high, 9 medium, 347 low
...
```
As you can see, the Snyk engine is recommending we consider upgrading to newer base images that have fixes for many of the issues found in ours.  If you search the output of the scan, you also can see that our CVE is, indeed in this base image.

```text
✗ Medium severity vulnerability found in imagemagick/imagemagick-6-common
  Description: CVE-2022-44268
  Info: https://security.snyk.io/vuln/SNYK-DEBIAN11-IMAGEMAGICK-3314444
  Introduced through: imagemagick/libmagickcore-dev@8:6.9.11.60+dfsg-1.3, imagemagick/libmagickwand-dev@8:6.9.11.60+dfsg-1.3, imagemagick@8:6.9.11.60+dfsg-1.3
  From: imagemagick/libmagickcore-dev@8:6.9.11.60+dfsg-1.3 > imagemagick/imagemagick-6-common@8:6.9.11.60+dfsg-1.3
  From: imagemagick/libmagickwand-dev@8:6.9.11.60+dfsg-1.3 > imagemagick/imagemagick-6-common@8:6.9.11.60+dfsg-1.3
  From: imagemagick@8:6.9.11.60+dfsg-1.3 > imagemagick/imagemagick-6.q16@8:6.9.11.60+dfsg-1.3 > imagemagick/libmagickcore-6.q16-6@8:6.9.11.60+dfsg-1.3 > imagemagick/imagemagick-6-common@8:6.9.11.60+dfsg-1.3
  and 24 more...
  Image layer: Introduced by your base image (python:3.11.1)
  Fixed in: 8:6.9.11.60+dfsg-1.3+deb11u1
```

## Fixing our image
Let's take Snyk's recommendation and upgrade our base image:

Double click on the `Dockerfile` under the `thumbnailer` directory in your Cloud9 IDE sidebar and change the first line from:
```docker
FROM python:3.11.1
```
To:
```docker
FROM python:3.12.01b
```

Now, rebuild the image:
```bash
cd image-app
docker build -t $ECR_REPO/thumbnailer .
```
 ... and let's re-scan it:
```bash
docker scan $ECR_REPO/thumbnailer --file Dockerfile --exclude-app-vulns
```

The results now should show the lower vulnerability count.
```text
...
Package manager:   deb
Target file:       Dockerfile
Project name:      docker-image|648839523175.dkr.ecr.us-east-1.amazonaws.com/thumbnailer
Docker image:      648839523175.dkr.ecr.us-east-1.amazonaws.com/thumbnailer:latest
Platform:          linux/amd64
Base image:        python:3.12.0b1
Licenses:          enabled

Tested 427 dependencies for known issues, found 256 issues.

Base Image       Vulnerabilities  Severity
python:3.12.0b1  256              4 critical, 4 high, 5 medium, 243 low

Recommendations for base image upgrade:

Alternative image types
Base Image                     Vulnerabilities  Severity
python:3.12.0b1-slim           54               0 critical, 1 high, 2 medium, 51 low
python:3.12.0a4-slim-bullseye  63               0 critical, 6 high, 6 medium, 51 low
python:3.12.0b1-slim-buster    79               1 critical, 2 high, 1 medium, 75 low
python:3.12-rc-buster          367              2 critical, 9 high, 9 medium, 347 low
```
If you search through the output, you should find our ImageMagick CVE is gone.

## About the recomendations
Snyk recommends less vulnerable base images grouped by how likely they are to be compatible:

- Minor upgrades are the most likely to be compatible with little work,
- Major upgrades can introduce breaking changes depending on image usage,
- Alternative architecture images are shown for more technical users to investigate.



