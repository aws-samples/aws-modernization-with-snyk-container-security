+++
title = "Step 8: Push the changes to GitHub"
chapter = false
weight = 21
+++

## Push the new Dockerfile to GitHub

Now that we verified a fix, let's save our work. Use `git` to push our code changes to GitHub.

```sh
git add Dockerfile
git commit -m "new base image to fix imagemagick vulnerability"
git push
```

This is one example of how a vulnerable component introduced by the container base image can have serious security implications. Without scanning it for vulnerabilities, the app works and looks harmless, but can leave a security hole in your infrastructure. Well done! 

In the next module, we'll demonstrate how the open source components in our application also open up security holes that can be exploited in our running application.