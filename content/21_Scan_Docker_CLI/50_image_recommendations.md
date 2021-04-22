+++
title = "Step 5: Dig into provided Base Image recommendations"
chapter = false
weight = 25
+++

## Dig into provided Base Image recommendations

Snyk's remediation guidance helps developers spend less time remediating, and more time developing! One way to tackle vulnerabilities is by choosing a more secure base image. By providing the Dockerfile to `docker scan`, Snyk can suggest other Base Images that can be used in the Dockerfile's `FROM` statement to bring down those vulnerability counts.

These are grouped by how likely they are to be compatible with your application:

* `Minor` upgrades are the most likely to be compatible with little work, 
* `Major` upgrades can introduce breaking changes depending on image usage,
* `Alternative` architecture images are shown for more technical users to investigate.

{{% notice info %}}
These suggestions are not a substitute for proper integration testing. They are intended to help you narrow down potential base image choices.
{{% /notice %}}

```txt
Organization:      demo-inc
Package manager:   deb
Target file:       Dockerfile
Project name:      docker-image|goof
Docker image:      goof:dev
Platform:          linux/amd64
Base image:        node:10.4.0
Licenses:          enabled

Tested 382 dependencies for known issues, found 958 issues.

Base Image   Vulnerabilities  Severity
node:10.4.0  958              454 high, 484 medium, 20 low

Recommendations for base image upgrade:

Minor upgrades
Base Image    Vulnerabilities  Severity
node:10.24.0  530              57 high, 52 medium, 421 low

Major upgrades
Base Image    Vulnerabilities  Severity
node:14.16.1  525              55 high, 50 medium, 420 low

Alternative image types
Base Image                 Vulnerabilities  Severity
node:dubnium-buster-slim   56               12 high, 5 medium, 39 low
node:dubnium-stretch-slim  70               15 high, 8 medium, 47 low
node:10.24.0-slim          72               16 high, 9 medium, 47 low
node:15-buster             299              25 high, 43 medium, 231 low

Debian 8 is no longer supported by the Debian maintainers. Vulnerability detection may be affected by a lack of security updates.
```