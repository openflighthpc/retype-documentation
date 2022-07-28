---
order: 80
label: Jupyter Notebook
icon: dot
---

Jupyter Notebooks are a web-based development and visualisation environment. It provides flexible integration of notebooks, code and data in a portable and secure manner.

## Workflow


### Installing Jupyter with Conda

!!!
The flight environment will need to be activated before the environments can be created so be sure to run `flight start` or [setup your environment to automatically activate the flight environment](https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-environment.html#activating-the-flight-environment).
!!!

- Create a conda software environment:

```bash
[flight@gateway1 (scooby) ~]$ flight env create conda
```
- Activate the environment:
```bash
[flight@gateway1 (scooby) ~]$ flight env activate conda
```

- Install Jupyter:

```bash
<conda> [flight@gateway1 (scooby) ~]$ conda install jupyter
```

- Install Notebook dependencies:

```bash
<conda> [flight@gateway1 (scooby) ~]$ conda install matplotlib
<conda> [flight@gateway1 (scooby) ~]$ conda install folium -c conda-forge
```

### Launch a Jupyter Notebook

!!!
These commands will need to be run from a graphical desktop session as it will launch a web browser. This is out of scope for this documentation, for more information on launching desktops, see the [use documentation](https://use.openflighthpc.org/en/latest/working-with-user-suite/flight-desktop.html#launch-a-desktop-session>)
!!!

- Download the example notebook:

```bash
<conda> [flight@gateway1 (scooby) ~]$ curl -L https://jupyterbook.org/en/stable/_downloads/12e9fb0f1c062494259ce630607cfc87/notebooks.ipynb > notebooks.ipynb
```

- Launch the notebook:

```bash
<conda> [flight@gateway1 (scooby) ~]$ jupyter notebook notebooks.ipynb
```

- A web browser will launch with the notebook displayed

![](/images/jupyter_notebook_1.png)