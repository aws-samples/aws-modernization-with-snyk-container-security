+++
title = "Step 5: Scan the Container Image for Vulnerabilities"
chapter = false
weight = 21
+++

## Scan the Container Image for Vulnerabilities

Vulnerable components like the version of ImageMagick present in our container image can be identified by Snyk. Developers using the Docker CLI can `docker scan` containers to get vulnerability information and base image upgrade guidance. 

Scan the image by running the following command. 

```sh
docker scan $DockerId/goof:latest --file=Dockerfile
```

When the scan completes, review the list of vulnerabilities. There are quite a few! If available, Snyk recommends other potential base images to help you build your container with as few vulnerabilities as possible.  

Snyk recommends less vulnerable base images grouped by how likely they are to be compatible:

#TODO: Make a list so it looks nice.
Minor upgrades are the most likely to be compatible with little work,
Major upgrades can introduce breaking changes depending on image usage,
Alternative architecture images are shown for more technical users to investigate.

Continue to the next Step to select another base image for our application.

