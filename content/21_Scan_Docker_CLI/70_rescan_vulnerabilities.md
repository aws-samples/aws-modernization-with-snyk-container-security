+++
title = "Step 7: Re-scan for Vulnerabilities"
chapter = false
weight = 27
+++

## Re-scan for vulnerabilities
Now let's use `docker scan` to scan for vulnerabilities. Once again, pass the `Dockerfile` used to build the image with `--file` to get more robust results.

```bash
# Scanning the goof image and passing the Dockerfile 
docker scan goof:v2 --file=Dockerfile
```

{{% notice tip %}}
Check out the [Docker Scan documentation](https://docs.docker.com/engine/scan/) for all possible CLI options.
{{% /notice %}}

Continue this cycle of build-scan-push until you're running the most secure base image.