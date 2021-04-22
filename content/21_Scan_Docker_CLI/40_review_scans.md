+++
title = "Step 4: Review Vulnerability Scan Results"
chapter = false
weight = 24
+++

## Review Vulnerability Scan Results

Vulnerabilities are broken up into sections, based on how they were introduced:

### Vulnerable Base Image Packages

Vulnerabilities introduced by the container's base image can be identified by the presence of the `Introduced by your base image` line. \(Line 9 below\)

```bash
✗ High severity vulnerability found in util-linux
  Description: Access Restriction Bypass
  Info: https://snyk.io/vuln/SNYK-DEBIAN8-UTILLINUX-285821
  Introduced through: util-linux@2.25.2-6, e2fsprogs/e2fsprogs@1.42.12-2+b1, init-system-helpers/init@1.22, util-linux/libblkid1@2.25.2-6, util-linux/libmount1@2.25.2-6, util-linux/libsmartcols1@2.25.2-6, util-linux/mount@2.25.2-6, meta-common-packages@meta, util-linux/bsdutils@1:2.25.2-6
  From: util-linux@2.25.2-6
  From: e2fsprogs/e2fsprogs@1.42.12-2+b1 > util-linux@2.25.2-6
  From: init-system-helpers/init@1.22 > systemd/systemd-sysv@215-17+deb8u7 > systemd@215-17+deb8u7 > util-linux@2.25.2-6
  and 19 more...
  Image layer: Introduced by your base image (node:10.4.0)
```

### User Instruction Vulnerabilities

Some vulnerabilities are introduced by User Instruction in the Dockerfile. Snyk highlights the command that introduced the vulnerability, with the `Image layer:` line. \(Line 8\)

```bash
✗ High severity vulnerability found in tiff/libtiffxx5
  Description: Out-of-bounds Write
  Info: https://snyk.io/vuln/SNYK-DEBIAN8-TIFF-405165
  Introduced through: imagemagick/libmagickcore-dev@8:6.8.9.9-5+deb8u12, meta-common-packages@meta
  From: imagemagick/libmagickcore-dev@8:6.8.9.9-5+deb8u12 > imagemagick/libmagickcore-6.q16-dev@8:6.8.9.9-5+deb8u12 > tiff/libtiff5-dev@4.0.3-12.3+deb8u5 > tiff/libtiffxx5@4.0.3-12.3+deb8u5
  From: imagemagick/libmagickcore-dev@8:6.8.9.9-5+deb8u12 > imagemagick/libmagickcore-6.q16-dev@8:6.8.9.9-5+deb8u12 > tiff/libtiff5-dev@4.0.3-12.3+deb8u5
  From: meta-common-packages@meta > tiff/libtiff5@4.0.3-12.3+deb8u5
  Image layer: 'RUN apt-get update -y && apt-get install -y imagemagick && rm -rf /var/lib/apt/lists/*'
  Fixed in: 4.0.3-12.3+deb8u10
```

{{% notice tip %}}
Check out the [Snyk Documentation for Info around Container CLI Results](https://support.snyk.io/hc/en-us/articles/360003946937-Understanding-container-CLI-scan-results)
{{% /notice %}}
