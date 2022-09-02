---
order: 70
label: OpenFOAM
icon: dot-fill
---

OpenFOAM is a popular engineering application toolbox. It's open source and is used for simulating fluid flow around objects. 

![](/images/openfoam_about_1.png)

## Workflow

### Installing OpenFOAM with Gridware

!!!
The flight environment will need to be activated before the environments can be created so be sure to run `flight start` or [setup your environment to automatically activate the flight environment](/hpc_environment_usage/flight_overview/flight_system/#activating-the-flight-system).
!!!

- Create a gridware software environment:

```bash
[flight@chead1 (mycluster1) ~]$ flight env create gridware
```

- Activate the environment:

```bash
[flight@chead1 (mycluster1) ~]$ flight env activate gridware
```

- Locate available OpenFOAM versions:

```bash
<gridware> [flight@chead1 (mycluster1) ~]$ gridware search openfoam
```

- Install OpenFOAM 4.1:

```bash
<gridware> [flight@chead1 (mycluster1) ~]$ gridware install apps/openfoam/4.1
```

!!!
After pressing 'y' to accept the installation. Gridware will install various dependencies for OpenFOAM to ensure it runs
!!!

### Checking OpenFOAM is Working

- Load the OpenFOAM module:

```bash
<gridware> [flight@chead1 (mycluster1) ~]$ module load apps/openfoam
```

- Check an OpenFOAM command can be seen by viewing the help page:

```bash
<gridware> [flight@chead1 (mycluster1) ~]$ icoFoam -help
```

### Running a Simple OpenFOAM Job

- Create a job script in the current working directory:

```bash
<gridware> [flight@chead1 (mycluster1) ~]$ cat << 'EOF' > myfoamjob.sh
#!/bin/bash
#SBATCH -N 1

# Activate environment and load OpenFOAM module
flight env activate gridware
module load apps/openfoam

# Create job directory from example job
cp -r $FOAM_TUTORIALS/incompressible/icoFoam/cavity/cavity $HOME/.
cd $HOME/cavity

# Calculate fluid pressure with OpenFOAM tools
blockMesh
checkMesh
icoFoam
EOF
```

- Submit the job to the queue system:

```bash
<gridware> [flight@chead1 (mycluster1) ~]$ sbatch myfoamjob.sh
```

- Check that the job is running (iit will take 1-2 minutes to complete):

```bash
<gridware> [flight@chead1 (mycluster1) ~]$ squeue
```

### Viewing the Results

Once the cavity job has finished running, the results can be visualised through a desktop session.
- Connect to VNC desktop (For more information on launching desktops, see the [Flight Desktop section](/hpc_environment_usage/flight_desktop/install_flight_desktop_types/#install-flight-desktop-types)).
- In a terminal on the desktop session, ensure that the OpenFOAM module is loaded:

```bash
[flight@chead1 (mycluster1) ~]$ flight env activate gridware
<gridware> [flight@chead1 (mycluster1) ~]$ module load apps/openfoam
```

- Navigate to the cavity directory and launch the paraFoam viewer:

```bash
<gridware> [flight@chead1 (mycluster1) ~]$ cd cavity
<gridware> [flight@chead1 (mycluster1) cavity]$ paraFoam
```

- In the window that opens, scroll down to "Mesh parts" and select all the boxes, then click apply

![](/images/openfoam_parafoam_1.png)

- Next, change the display to 'U' in the dropdown menu, click play to change the timestamp and then click and drag to rotate the subject

![](/images/openfoam_parafoam_2.png)