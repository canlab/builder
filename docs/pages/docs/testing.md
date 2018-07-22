---
title: Testing
sidebar: main_sidebar
permalink: testing
folder: docs
---

You will need to set up testing for your repository before issuing any pull request. Testing means using a
"continuous integration" service like [CircleCI](https://circleci.com/workflow-run/a8dc69fa-fa42-4b47-8af5-611f924e175b) to
run a workflow. The workflow typically consists of the following steps:

 - Connect the repository, and add deployment credentials
 - Build your container, taking advantage of the cache of layers to speed things up
 - Upon successful build and test, deploy the container to Docker Hub (or else where)


## 1. Connect the repository
You should be able to log in with your Github account, and click "Add a new project" to [select your repository](https://circleci.com/dashboard).
Once you have added the project, in the project settings (the gear icon in the upper right of the project main page) you should be able to
see a tab under "Build Settings" called "Environment Variables." Here you should define your Docker username and password
(or whatever deployment you decide to use, note that if you don't use Docker Hub you will need to edit the config.yml). Take a look
at other [deployment options here](https://circleci.com/docs/2.0/deployment-integrations/).

These are the two you should add. They will be encrypted. Yes, it's always risky even to put an encrypted password, but this is
true of passwords for any service.

```bash
DOCKER_USER
DOCKER_PASS
```

Finally, it's likely that your Docker repo is different from your Github, so you should define a `CONTAINER_NAME` in this project environment too. The final three variables will look like this:

![assets/img/envars.png](assets/img/envars.png)

Given that these variables are found, a container will be pushed to Docker Hub on successful build. 

> What tags are used?

By default, each deployment (a merge into master) will include the tag `latest` as the most recent version,
plus the same tagged container using the first 10 characters of the Github commit. For example:

![assets/img/tag.png](assets/img/tag.png)

This ensures that as you move forward in time, you could go back and associate a particular container with
a commit. As another option, if you have a need to define a custom tag for a build, set the `DOCKER_TAG` variable in your CircleCI environment settings, and this will be used instead of the commit.  Either way, here is how others will be able to pull your container from Docker Hub:

```bash
# implies tag "latest"
$ docker pull vanessa/expfactory-container-stroop

# implies tag based on commit "dcf077a302"
$ docker pull vanessa/expfactory-container-stroop:dcf077a302
```

## 2. The Configuration File

How does this all work? You'll notice the template has a "hidden" directory called `.circleci` with a `config.yml` inside. This is a file that defines the workflow
to define the steps that we described above. Importantly, you don't need to edit this, because the steps already know to build your container from your Dockerfile. However, if you are an advanced user, you
are most definitely welcome to add other testing or steps in this deployment! For example, wouldn't it
be cool to register a finished container with some kind of registry? If you'd like to work on this together, please reach out!

We will also like to discuss having different build recipe template for different kinds of container testing, and building second containers to run an analysis portion once data is collected.
