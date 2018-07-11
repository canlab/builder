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

These docs are still under development, since we have to define criteria for testing. I'll write brief notes here for now.

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

Given that these variables are found, a container will be pushed to Docker Hub on successful build. The tag will be the Circle CI
build tag. If not, it will just skip over the step. This is how others will be able to pull your container from Docker Hub:

```bash
docker pull vanessa/expfactory-test-task
```

## 2. The Configuration File

You'll notice the template has a "hidden" directory called `.circleci` with a `config.yml` inside. This is a file that defines the workflow
to define the steps that we described above. Importantly, you don't need to edit this, because the steps already know
to build your container from your Dockerfile.

We will add more to this section after discussion on how an experiment container should be tested.
