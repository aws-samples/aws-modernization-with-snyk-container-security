+++
title = "Step 2: Build the application Docker image"
chapter = false
weight = 23
+++

## Build Docker images
The repo has a `Dockerfile` at the top level directory that defines the structure of our Docker image. The `Dockerfile` in the repo tells `docker build` how to build the container. To learn more about Dockerfile commands, visit [Docker's documentation](https://docs.docker.com/engine/reference/builder/). A summary is provided below:

```docker
FROM node:14.1.0               ## Use Node 14.1.0 as our base image

RUN mkdir /usr/src/goof        ## Create the directory for our application
RUN mkdir /tmp/extracted_files
COPY . /usr/src/goof           ## Copy the current directory files into the image
WORKDIR /usr/src/goof          ## Set the working directory

RUN npm update                 ## Ensure npm is up to date
RUN npm install                ## Install dependencies
EXPOSE 3001
EXPOSE 9229
ENTRYPOINT ["npm", "start"]    ## The command to run at container startup
```

When ready, build and tag the container image to get it ready to push into Docker Hub.  Note the `.` character at the end of the line, it is required and tells docker to look in the current directory for files related to this build.

```sh
docker build -t goof:dev .
```

When complete, the build output should end in a couple of lines that look similar to this:

```
Successfully built 7ae8b7014018
Successfully tagged goof:dev
```

If an error occured, check your build command and try again.  Don't forget that `.` character!

Now, let's look at our local Docker image cache to see what we've built.

```sh
docker image ls
```

```
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
goof         dev       7ae8b7014018   2 minutes ago    1.09GB
node         14.1.0    a511eb5c14ec   11 months ago    941MB
```

