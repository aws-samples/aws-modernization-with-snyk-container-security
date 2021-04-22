+++
title = "Step 6: Apply a more secure Base Image and re-build the Image"
chapter = false
weight = 26
+++

## Apply a more secure Base Image

Let's choose a more secure base image for goof. We'll do this by applying the `Minor` upgrade recommended by Snyk. Change the `FROM` statement in the Dockerfile:

```bash
# Comment out the old FROM Statement
# FROM node:10.4.0

# Write in the new one
FROM node:10.24.0

RUN apt-get update -y && \
    apt-get install -y imagemagick && \
    rm -rf /var/lib/apt/lists/*
```

## Re-build the Image

Now build the new Image. To compare results side-by-side with the previous scan, we'll specify a different tag when building the image.

```bash
docker build -t goof:v2 .
```

