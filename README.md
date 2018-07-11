# Experiment Factory Builder

 - [![CircleCI](https://circleci.com/gh/expfactory/builder.svg?style=svg)](https://circleci.com/gh/expfactory/builder)

This is the experiment factory builder. The experiment folders that you add to the folder
[experiments](experiments) will be built into an experiment factory Docker Container, or you can select from the library by adding the name to the [experiments.txt](experiments.txt) in this folder. I'm hoping to transform this into a [CircleCi Orb](https://github.com/CircleCI-Public/config-preview-sdk/) so it can better serve as a service template.

Generally, you should do the following:

  1. For custom experiments, put experiment subfolders in [experiments](experiments). Each should be served statically, and submit to `/next`
  2. For experiments from [the library](https://expfactory.github.io/experiments) write the unique identifier (e.g., stroop tower-of-london) into the file [experiments.txt](experiments.txt).
  3. Connect the repository to [Circle CI](https://www.circleci.org) to build your experiment container!
  4. Optionally, you can add a Docker Hub username (`DOCKER_USER`) and password (`DOCKER_PASS`), along with a custom container name (`CONTAINER_NAME`), to the [Circle CI environment](https://circleci.com/docs/2.0/env-vars/). You will first need to create the repository for the associated container name on Docker Hub. This will not only build and test, but will build, test, and deploy your experiment container for others to use.
