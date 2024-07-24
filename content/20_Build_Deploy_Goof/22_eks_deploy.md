+++
title = "Step 2: Deploy the application to EKS"
chapter = false
weight = 22
+++


For the purpose of this workshop, we have created an Amazon EKS cluster on which we will run the "Goof apps" and you will now deploy the applications that we have built on it.

## Update the Kubeconfig file

```sh
# update kubeconfig file
aws eks update-kubeconfig --name $(aws eks list-clusters --query 'clusters[0]' --output text)
```

## Create and set context to a namespace

We will be running these applications in a specific namespace.

```sh
# Create a namespace
kubectl create ns snyk-aws

# Set the current context to use the new namespace
kubectl config set-context --current --namespace snyk-aws

# Verify snyk-aws Namespace was successfully created
kubectl get ns
```
```
$ kubectl get ns
NAME              STATUS   AGE
default           Active   124m
kube-node-lease   Active   124m
kube-public       Active   124m
kube-system       Active   124m
snyk-aws          Active   113s
```

**:warning:** **WARNING**

This workshop deploys a Log4Shell exploit server. This should never be ran in a Production Environment! Please ensure you understand the security implications and have taken appropriate precautions. Use in a controlled, isolated environment to avoid any unintended security risks.

## Deploy the applications
Ensure the `REPO` variable is still set from the build step and run this command. (it uses the `envsubst` utilities to plug your ECR repository server into each of the deployment's image tags)
```bash
cat manifests/*.yaml | envsubst | kubectl apply -f -
```

To check the status of the pods as the application comes up, use the following command:

### Validate they are running
```sh
kubectl get all
```
The output should look something like this:
```
$ kubectl get all
NAME                               READY   STATUS    RESTARTS   AGE
pod/goof-7bd8895c4d-zl8ln          1/1     Running   0          19s
pod/thumbnailer-6cc495969b-j6tkb   1/1     Running   0          19s

NAME                  TYPE           CLUSTER-IP      EXTERNAL-IP                                                               PORT(S)        AGE
service/goof          LoadBalancer   10.100.48.151   SOME_LONG_STRING.us-east-2.elb.amazonaws.com    80:30835/TCP   19s
service/thumbnailer   LoadBalancer   10.100.42.253   ANOTHER_LONG_STRING.us-east-2.elb.amazonaws.com   80:30594/TCP   19s

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/goof          1/1     1            1           19s
deployment.apps/thumbnailer   1/1     1            1           19s

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/goof-7bd8895c4d          1         1         1       19s
replicaset.apps/thumbnailer-6cc495969b   1         1         1       19s
```

{{% notice info %}}
The pods should all show **"Running"** in their **STATUS** field, and services with a **LoadBalancer** type should have an IP or hostname for their **EXTERNAL-IP**.
<br>If either show a pending state, then wait a moment and re-run the command until they finish starting up. 
{{% /notice %}}

The following will save the `LoadBalancer` services `EXTERNAL_IP` values for later use:
```bash
THUMBNAILER_LB=$(kubectl get svc thumbnailer -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
TODOLIST_LB=$(kubectl get svc todolist -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
```

Once both are running, the application is accessible from the web. Get the DNS name for your app running the following commands: 

```bash
echo Thumbnailer Loadbalancer: http://$THUMBNAILER_LB \ &&
echo Todo List Loadbalancer: http://$TODOLIST_LB 
``` 

### Validate our Log4Shell exploit server is running
The eagle-eyed amoung you probably noticed that only two deployments and services are shown in the above output but we built and deployed three images. Well, the third, as it's name reveals, is a Log4Shell malicious LDAP server we will be using in a later section.  We'll discuss it more in a later section, but for now, just make sure it's running by listing the deployments in the `darkweb` namespace:
```sh
kubectl get all -n darkweb
```
```
$ kubectl get all -n darkweb
NAME                            READY   STATUS             RESTARTS   AGE
pod/log4shell-7d8c6fbfd-84l8p   1/1     Running            0          154m

NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
service/evil   ClusterIP   10.100.76.31    <none>        9999/TCP   2m2s
service/ldap   ClusterIP   10.100.69.149   <none>        80/TCP     154m

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/log4shell   1/1     1            1           154m

NAME                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/log4shell-7d8c6fbfd   1         1         1       154m
replicaset.apps/log4shell-fc6565dbc   1         1         0       2m2s
```
:blue_book: Services in this namespace will not get external IP's as they are not running as a loadbalancer type.

## Success!

If you got here without issues, you've successfully built and deployed all of the applications and they are now live on EKS. We can open and interact with it, and while they looks harmless enough! In the next module we'll demonstrate how a vulnerable open source components can create an invisible risk that can compromise our application.
