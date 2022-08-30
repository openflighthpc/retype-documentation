---
order: 80
label: Jupyter Notebook
icon: dot-fill
---

Jupyter Notebooks are a web-based development and visualisation environment. It provides flexible integration of notebooks, code and data in a portable and secure manner.

## Workflow


### Installing Jupyter with Conda

!!!
The flight environment will need to be activated before the environments can be created so be sure to run `flight start` or [setup your environment to automatically activate the flight environment](/using_environment/cli-basics/flight_system/#activating-the-flight-system).
!!!

- Create a conda software environment:

```bash
[flight@gateway1 (mycluster1) ~]$ flight env create conda
```
- Activate the environment:
```bash
[flight@gateway1 (mycluster1) ~]$ flight env activate conda
```

- Install Jupyter:

```bash
<conda> [flight@gateway1 (mycluster1) ~]$ conda install jupyter
```

- Install Notebook dependencies:

```bash
<conda> [flight@gateway1 (mycluster1) ~]$ conda install matplotlib
<conda> [flight@gateway1 (mycluster1) ~]$ conda install folium -c conda-forge
```

### Launch a Jupyter Notebook

!!!
These commands will need to be run from a graphical desktop session as it will launch a web browser. For more information on launching desktops, see the [Flight Desktop section](/flight_desktop/install_flight_desktop_types/#install-flight-desktop-types)
!!!

- Download the example notebook:

```bash
<conda> [flight@gateway1 (mycluster1) ~]$ curl -L https://jupyterbook.org/en/stable/_downloads/12e9fb0f1c062494259ce630607cfc87/notebooks.ipynb > notebooks.ipynb
```

- Launch the notebook:

```bash
<conda> [flight@gateway1 (mycluster1) ~]$ jupyter notebook notebooks.ipynb
```

- A web browser will launch with the notebook displayed

![](/images/jupyter_notebook_1.png)