---
title: Experiments
sidebar: main_sidebar
permalink: experiments
folder: docs
---

An experiment is something you are probably already familiar with - a static folder with html, css (style) and probably javascript (js) files that when run with a webserver can show stimuli and collect responses. This is the new bread and butter of research in behavioral science, and so the experiment factory is optimized to deploy this kind of experiment. Here we will talk about the various options you have for experiments:

 - [Library](#library) You can use any of the library of experiments we've already built.
 - [LabJS](#Lab-js) is an awesome web interface builder that will export an experiment folder
 - [Custom](#custom-experiment) means creating and deploying your own experiment, either from scratch or starting with another as a template.

## Library
If you don't want to develop your own experiment, you can use any number of experiments, surveys, or games from the [expfactory library](https://expfactory.github.io/experiments). Once you have selected an experiment that you like, simply add it's unique id (called an exp_id) to the `experiments.txt` file in the base of this repository. The experiment will be installed into your container.

Here is an example of an experiments.txt file

```bash
stroop tower-of-london
```

## LabJS
You can use the [LabJS builder](http://labjs.readthedocs.io/en/latest/learn/builder/) and select the Experiment Factory export option. You can then extract the finished experiment into a subfolder of `experiments` also in this repository. For a full tutorial, see [this page](https://expfactory.github.io/expfactory/integration-labjs).

## Custom Experiment

If you want to develop your own experiment, see the [complete documentation](https://expfactory.github.io/expfactory/contribute#contribute-an-experiment) for how to do this. You will want to do the following:

 1. Develop the experiment locally, per the instructions above.
 2. Clone this repository, and add your experiment folder under the `experiments` folder.
 
and then continue on to connecting your repository to CircleCI and Docker Hub.

## Examples
Here are a few examples of what various set ups can look like:

 - [The LabJS Builder](https://expfactory.github.io/expfactory/integration-labjs) is an example of the builder that will install a LabJS experiment folder in addition to experiments from the library.
 - [The Experiment Factory Containers](https://www.github.com/expfactory-containers) has examples of build repositories (for example, [container-stroop](https://github.com/expfactory-containers/container-stroop) deploys two stroop tasks to the Docker Hub container [vanessa/expfactory-container-stroop](https://hub.docker.com/r/vanessa/expfactory-container-stroop/tags/) and includes examples for analyzing the data.

## Frequently asked Questions

> Can I install local and library experiments?

Yes, of course?

> What should I do next?

Once you get here, you should have a cloned builder repository with experiments listed in an `experiments.txt` file and/or your own experiment folders in an `experiments` folder within. Once you are done with this experiment definition, you should move on to [connect to testing](testing) where you can build and deploy your container.
