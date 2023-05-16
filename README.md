# AWS Modernization with Snyk

Containers enable you to separate your applications from your infrastructure so you can deliver software quickly. With containers, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of standardized methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

Snyk is a Cloud Native Application Security solution that enables developers and security teams to find and automatically fix vulnerabilities in your source code, Infrastructure as code templates, container images, kubernetes applications, and open source artifacts.

### Welcome

In this workshop you will learn how to scan containerized applications for vulnerabilities using Snyk. 

### Learning Objectives
- Scan a containerized application using Snyk Container CLI for vulnerabilties
- Continuous Integration with Snyk
- DevSecOps with Snyk and AWS Code* Services

### Instruction to run workshop on your own: 

This page is build with Hugo, so you'll need to install it - https://gohugo.io/getting-started/installing/

Next, clone this repo: 

```
git clone git@github.com:aws-samples/aws-modernization-snyk-docker.git
```

Ensure that you have also cloned the submodules:

```
git submodule init
git submodule update
```

Start the server with Hugo:
```
hugo server
```

Go to localhost: to view the content in your web browser of choice