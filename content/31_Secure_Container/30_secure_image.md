+++
title = "Step 6: Apply a more secure Base Image and re-build the Image"
chapter = false
weight = 21
+++

## Apply a more secure Base Image

To apply a new base image, open the Dockerfile in Cloud9 and replace, or comment out, the old base image with a new one. In this example, we'll use `node:14.16.1`.

{{% notice info %}}
Open Source vulnerabilities are disclosed daily, so the recommendations you see may differ as the Snyk vulnerability database is constantly updated.  This example shows upgrade recommendations as of the day of writing.  The actual version numbers may differ for you.
{{% /notice %}}
```
FROM node:14.16.1

RUN mkdir /usr/src/goof
COPY . /usr/src/goof
WORKDIR /usr/src/goof

RUN npm install
EXPOSE 3112
EXPOSE 31337
CMD ["npm", "start"]
```

When ready, save the changes.

## Re-build the Image

Now build and push the container to Docker Hub.

```sh
docker build -t $DockerId/goof-image:latest .
docker push $DockerId/goof-image:latest
```

In the next step we'll re-deploy the application to EKS and test the exploit to verify a fix.

