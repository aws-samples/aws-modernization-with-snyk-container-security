+++
title = "Step 11: Create a Production Python Image"
chapter = false
weight = 41
+++

## 

Take a look at the logs from the thumbnailer:

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

The image we are using currently is great for development, as it includes various debugging
features, but in production we should use something more hardened.

## Using a Production Server

To do this, the simplest option is to replace the Flask development server with [gunicorn](https://gunicorn.org/). 


Double click on the `Dockerfile` under the `thumbnailer` directory in your Cloud9 IDE sidebar and change the line where we install packages from:

```docker
RUN apk add imagemagick
```
To:
```docker
RUN apk add imagemagick py3-gunicorn 
```

We also need to change the entrypoint commands to start gunicorn. Change the command from:

```docker
ENTRYPOINT ["python3"]
CMD ["/app/webapp.py"]
```
To:
```docker
ENTRYPOINT ["gunicorn"]
CMD ["--bind", "0.0.0.0:5000", "webapp:app"]
```

You can rebuild and redeploy the image at this stage, but there's another simple improvement we can
make. At the moment, the main process in the container is running as the root user. We can see this by
running `ps` in the container. First find the full name of the thumbnailer pod:


```bash
kubectl get pods 
```

Which will give you something like:

```
NAME                           READY   STATUS    RESTARTS   AGE
thumbnailer-84fbb67f8b-gbsk9   1/1     Running   0          48m
todolist-56cf84f9bb-qvl8c      1/1     Running   0          2d4h
```

Using the name of the pod as an argument, run the following:

```
kubectl exec thumbnailer-84fbb67f8b-gbsk9 -- ps -ux
```

And you should get something similar to:

```
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.2  39300 30816 ?        Ss   17:15   0:00 python3 /app/webapp.py
root          10  0.5  0.1 112708 30284 ?        Sl   17:15   0:06 /usr/local/bin/python3 /app/webapp.py
root          42  0.0  0.0   8332  2816 ?        Rs   17:38   0:00 ps -ux
```

Note the user on the left is "root". If an attacker was able to compromise one of the processes,
they would have full privileges in the container, including the ability to read and write to any file. In addition, if they were able to escape the container, they could potentially have elevated privleges on the host.

Thankfully, fixing this is relatively straightforward. In the Dockerfile, add the line 


```docker
USER nonroot
```

After the installing packages step. Chainguard images come with the nonroot user predefined, so we
don't have to create a new user. The USER instruction will take effect for subsequent lines in the
Dockerfile and when the container is started. 

The complete Dockerfile should now look like this:

```
FROM cgr.dev/chainguard/python:latest-dev

USER root
RUN apk add py3-gunicorn imagemagick
USER nonroot
WORKDIR /app

RUN pip install flask
COPY webapp.py webapp.py
COPY templates templates
RUN mkdir uploads

EXPOSE 5000

ENTRYPOINT ["gunicorn"]
CMD ["--bind", "0.0.0.0:5000", "webapp:app"]
```


We can now rebuild the image:
```bash
docker build -t $REPO/thumbnailer .
```

And as before, push the image and deploy the application:


```sh
docker push $REPO/thumbnailer:latest
```

Followed by:

```sh
kubectl scale deployment thumbnailer --replicas=0
kubectl scale deployment thumbnailer --replicas=1
```

Let's try checking the user again. First get pod name again, as it will have changed in the restart:

```
kubectl get pods
```

Which gave me:

```
NAME                           READY   STATUS    RESTARTS   AGE
thumbnailer-84fbb67f8b-577n5   1/1     Running   0          26s
todolist-56cf84f9bb-qvl8c      1/1     Running   0          2d6hk
```

The `ps` implementation in the Chainguard image is a little different, so we don't need the
arguments:

```
kubectl exec thumbnailer-84fbb67f8b-577n5 -- ps
```

Which will output something similar to:

```
    1 nonroot   0:00 {gunicorn} /usr/bin/python /usr/bin/gunicorn --bind 0.0.0.0:5000 webapp:app
   10 nonroot   0:00 {gunicorn} /usr/bin/python /usr/bin/gunicorn --bind 0.0.0.0:5000 webapp:app
   23 nonroot   0:00 ps
```

Mission accomplished! We now have all processes running as "nonroot", which is a significant boost
to security.

In this section TK...
