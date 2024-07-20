+++
title = "Step 11: Create a Production Python Image"
chapter = false
weight = 41
+++

## Investigating our Container 

Let's investigate our thumbnailer container a bit more.

We'll start by taking a look at the logs from the thumbnailer. First we'll need to find the full name of the
pod:

```bash
# Get the name of the pod containing "thumbnailer" in its name
POD_NAME=$(kubectl get pods --no-headers -o custom-columns=":metadata.name" | grep thumbnailer)

# Print the pod name
echo $POD_NAME
```

```
NAME                           READY   STATUS    RESTARTS   AGE
thumbnailer-6cc796bd56-lkm2x   1/1     Running   0          131m
todolist-778ddc9684-kfjgm      1/1     Running   0          59m
```

Take the full name of the thumbnailer pod (yours will different) and put it into the `logs` command:

```bash
kubectl logs $POD_NAME
```


```
 * Serving Flask app 'webapp'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://10.244.1.11:5000
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 673-830-468
```

So our image is using a development server with debugging support. This is great for developers
working on an application, but not so great for production when we want to lock things down. Let's
follow the advice in the logs to use a production WSGI server.

## Using a Production Server

The simplest option is to replace the Flask development server with [gunicorn](https://gunicorn.org/). 


Double click on the `Dockerfile` under the `thumbnailer` directory in your Cloud9 IDE sidebar and change the line where we install packages from:

```
RUN apk add imagemagick
```
To:
```docker
RUN apk add imagemagick py3-gunicorn 
```

We also need to change the entrypoint commands to start gunicorn. Change the command from:

```
CMD ["webapp.py"]
```
To:
```docker
ENTRYPOINT ["gunicorn"]
CMD ["--bind", "0.0.0.0:5000", "webapp:app"]
```

## Don't Run as Root

Before we rebuild and redeploy the image, there's another simple improvement we can
make. At the moment, the main process in the container is running as the root user. We can see this by
running `ps` in the container, using the same pod name as before:

```bash
kubectl exec $POD_NAME -- ps -ux
```

And you should get something similar to:

```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.4  38224 32100 ?        Ss   12:19   0:00 python3 webapp.py
root         7  0.5  0.4 265320 32364 ?        Sl   12:19   1:01 /usr/local/bin/python3 webapp.py
root      3162  0.0  0.0   8536  4272 ?        Rs   15:12   0:00 ps -ux
```

Note the user on the left is "root". If an attacker was able to compromise one of the processes,
they would have full privileges in the container, including the ability to read and write to any
file. In addition, if they were able to escape the container, they could potentially have elevated
privleges on the host.

Thankfully, fixing this is relatively straightforward. In the Dockerfile, after the line:


```
RUN apk add imagemagick py3-gunicorn 
```

Add the lines:

```docker
USER nonroot
WORKDIR /app
```

We also need to tweak the line that creates the upload directory, so that it uses a local directory
that the new user can write to. Change the line:

```
RUN mkdir /uploads
```

Remove the `/` so that it becomes:

```docker
RUN mkdir uploads
```

Chainguard images come with the nonroot user predefined, so we don't have to create a new user. The
`USER` instruction will take effect for subsequent lines in the Dockerfile and when the container is
started. 

The complete Dockerfile should now look like this (with comments removed):

```
FROM cgr.dev/chainguard/python:latest-dev
USER root
RUN apk add imagemagick py3-gunicorn
USER nonroot
WORKDIR /app

RUN pip install flask

COPY webapp.py webapp.py
COPY templates templates

EXPOSE 5000
RUN mkdir uploads

ENTRYPOINT ["gunicorn"]
CMD ["--bind", "0.0.0.0:5000", "webapp:app"]
```


We can now rebuild the image:
```bash
docker build -t $REPO/thumbnailer .
```

And as before, push the image and deploy the application:


```bash
docker push $REPO/thumbnailer:latest
kubectl scale deployment thumbnailer --replicas=0
kubectl scale deployment thumbnailer --replicas=1
```

Let's try checking the user again. First get the pod name again, as it will have changed in the restart:

```bash
kubectl get pods
```

Which gave me:

```
NAME                           READY   STATUS    RESTARTS   AGE
thumbnailer-6cc796bd56-sfpfd   1/1     Running   0          32s
todolist-778ddc9684-kfjgm      1/1     Running   0          141m
```

The `ps` implementation in the Chainguard image is a little different, so we don't need the
arguments:

```bash
kubectl exec $POD_NAME -- ps
```

Which will output something similar to:

```
PID   USER     TIME  COMMAND
    1 nonroot   0:00 {gunicorn} /usr/bin/python /usr/bin/gunicorn --bind 0.0.0.0:5000 webapp:app
    7 nonroot   0:00 {gunicorn} /usr/bin/python /usr/bin/gunicorn --bind 0.0.0.0:5000 webapp:app
    8 nonroot   0:00 ps
```

Mission accomplished! 

We are now using a production webserver and have all processes running as "nonroot", which is a significant boost
to security.
