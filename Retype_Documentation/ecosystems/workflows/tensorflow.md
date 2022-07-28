---
order: 60
label: Tensorflow
icon: dot
---

Tensorflow is an open-source machine learning platform. It provides an ecosystem of tools and libraries that allow researchers to build and deploy machine learning applications.

+++ Singularity
## Workflow 1: Singularity

!!!
The flight environment will need to be activated before the environments can be created so be sure to run `flight start` or [setup your environment to automatically activate the flight environment](https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-environment.html#activating-the-flight-environment).
!!!

### Installing Tensorflow with Singularity

- Create a singularity software environment:

```bash
[flight@gateway1 (scooby) ~]$ flight env create singularity
```

- Activate the environment:

```bash
[flight@gateway1 (scooby) ~]$ flight env activate singularity
```

### Running the Job

- Download the example job models:

```bash
<singularity> [flight@gateway1 (scooby) ~]$ git clone -b v1.13.0 https://github.com/tensorflow/models.git
```

- Launch the tensorflow docker container with singularity to run the job:

```bash
<singularity> [flight@gateway1 (scooby) ~]$ singularity exec docker://tensorflow/```
tensorflow:1.15.0 python ./models/tutorials/image/mnist/convolutional.py
```

+++ Conda
## Workflow 2: Conda

!!!
The flight environment will need to be activated before the environments can be created so be sure to run `flight start` or [setup your environment to automatically activate the flight environment](https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-environment.html#activating-the-flight-environment).
!!!

### Installing TensorFlow with Conda

- Create a conda software environment:

```bash
[flight@gateway1 (scooby) ~]$ flight env create conda
```

- Activate the environment:

```bash
[flight@gateway1 (scooby) ~]$ flight env activate conda
```

- Create a Python environment for tensorflow:

```bash
<conda> [flight@gateway1 (scooby) ~]$ conda create -n tensorflow python=3.6
```

- Activate the Python environment:

```bash
<conda> [flight@gateway1 (scooby) ~]$ source activate tensorflow
```

- Install the tensorflow package:

```bash
<conda> [flight@gateway1 (scooby) ~]$ pip install tensorflow==1.15
```

### Running the Job

- Download the example job models:

```bash
<conda> [flight@gateway1 (scooby) ~]$ git clone -b v1.13.0 https://github.com/
tensorflow/models.git
```
- Execute the job with python:

```bash
<conda> [flight@gateway1 (scooby) ~]$ python ./models/tutorials/image/mnist/
convolutional.py
```
+++