---
order: 70
label: OpenFOAM
icon: dot-fill
---

OpenFOAM is a popular engineering application toolbox. It's open source and is used for simulating fluid flow around objects. 

![](/images/openfoam_about_1.png)

## Workflow

### Installing OpenFOAM

!!!
Your environment will need to have a job scheduler such as [Slurm](/hpc_environment_usage/slurm_environment_usage/slurm_scheduler/), which can be set up by following the instructions for a [standalone](/cluster_build_methods/standalone_cluster/) or [multinode]() cluster.
!!!


Enable copr for OpenFOAM.
```
sudo dnf -y copr enable openfoam/openfoam
```

Install OpenFOAM, the OpenFOAM version selector, the additional sub-packages and paraview.
```
sudo dnf install -y openfoam-selector
sudo dnf install -y openfoam
sudo dnf install -y openfoam2212-default
sudo dnf install -y paraview
```


Ensure that the correct version will be used with:
```
openfoam-selector --set openfoam2212
```

Refresh the shell by logging out and back in to make openfoam commands accessible.

!!!
Make sure to do the above installation steps on **all** nodes in the cluster.
!!!


### Checking OpenFOAM is Working


- Check an OpenFOAM command can be seen by viewing the help page:

```bash
icoFoam -help
```

!!!
From here on out, all steps **only** need to be done on the **login** node.
!!!

### Running a Simple OpenFOAM Job



- Create a job script in the current working directory:

```bash
cat << 'EOF' > myfoamjob.sh
#!/bin/bash
#SBATCH -N 1

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
sbatch myfoamjob.sh
```

- Check that the job is running (it may take 1-2 minutes to complete):

```bash
squeue
```

### Viewing the Results

Once the cavity job has finished running, the results can be visualised through a desktop session.
- Connect to VNC or web-suite desktop (For more information on launching desktops, see the [Flight Desktop section](/flight_environment_usage/flight_desktop/launch_a_desktop_session/)).


- Navigate to the cavity directory and launch the paraFoam viewer:

```bash
cd cavity
paraFoam 
```

- In the window that opens, scroll down to "Mesh parts" and select all the boxes, then click apply

![](/images/openfoam_parafoam_1.png)

- Next, change the display to 'U' in the dropdown menu, click play to change the timestamp and then click and drag to rotate the subject

![](/images/openfoam_parafoam_2.png)