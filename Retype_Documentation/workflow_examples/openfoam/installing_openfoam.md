---
order: 100
label: Installing OpenFOAM
icon: dot
---

There are 3 different ways you can install OpenFOAM, each with varying levels of time to setup and complexity. The *Basic* setup is the fastest and integrates best with the Flight User Suite. The *Advanced* setup is for users that want more control, and can take over an hour on a 16 core machine.


!!!
Your environment will need to have a job scheduler such as [Slurm](/hpc_environment_usage/slurm_environment_usage/slurm_scheduler/), which can be set up by following the instructions for a [standalone](/cluster_build_methods/standalone_cluster/) or [multinode]() cluster.
!!!


+++ Basic  :icon-star-fill::icon-star::icon-star:


1. Download the OpenFOAM software to your desired application location. With a multinode cluster this should be a shared filesystem. 


2. Become the root user, the added permissions are necessary for setup.
    ```
    sudo su -
    ```

3. Download OpenFlight OpenFOAM build using [Flight Silo](/flight_environment_usage/flight_tools/flight_silo/)
    ```
    flight silo file pull openflight:openfoam/OpenFOAM-v2212.tar.gz
    ```

4. Install it to `/opt/apps`.
    ```
    mkdir /opt/apps/OpenFOAM
    cd /opt/apps/OpenFOAM/
    tar xf <download location>/OpenFOAM-v2212.tar.gz
    ```


5. Install dependencies for visualisation.
    ```
    dnf install -y paraview
    ```

6. Install dependencies on all nodes.
    ```
    pdsh -g all 'dnf install -y openmpi'
    ```

### Test Installation

Source the OpenFOAM environment and run a basic test. Make sure to change the source file path to the location of your installation.
```
module load mpi
source /opt/apps/OpenFOAM/OpenFOAM-v2212/etc/bashrc
foamTestTutorial -full incompressible/simpleFoam/pitzDaily
```
!!!
From this point being the root user is no longer necessary.
!!!


+++ Advanced :icon-star-fill::icon-star-fill::icon-star:

Firstly, become the root user, the added permissions are necessary for setup.
```
sudo su -
```

## Build OpenFOAM

1. Install prerequisites

    ```
    dnf install gcc cmake boost fftw-devel paraview-devel paraview-openmpi-devel openmpi-devel flex m4 qt5-devel
    ```
2. Make a directory for OpenFOAM in shared storage, so that the OpenFOAM build is available to all nodes in the cluster.
    ```
    cd /opt/apps
    mkdir OpenFOAM
    ```

3. Obtain OpenFOAM Source.
    ```
    flight silo file pull openflight:openfoam/OpenFOAM-v2212.tar.gz
    tar xf OpenFOAM-v2212.tgz
    ```

4. Compile it.
    ```
    cd OpenFOAM-v2212
    module load mpi
    source etc/bashrc

    foamSystemCheck # Check whether expected to work

    ./Allwmake -j -s -q -l # Compile on all cores
    ```

5. Install dependencies for visualisation.
    ```
    dnf install -y paraview
    ```

6. Install dependencies on all nodes.
    ```
    pdsh -g all 'dnf install -y openmpi'
    ```

7. Test that the build works.
    ```
    foamTestTutorial -full incompressible/simpleFoam/pitzDaily
    ```


!!!
From this point being the root user is no longer necessary.
!!!


+++ Legacy :icon-star-fill::icon-star::icon-star:


1. Enable copr for OpenFOAM.
    ```
    sudo dnf -y copr enable openfoam/openfoam
    ```

2. Install OpenFOAM, the OpenFOAM version selector, the additional sub-packages and paraview.
    ```
    sudo dnf install -y openfoam-selector
    sudo dnf install -y openfoam
    sudo dnf install -y openfoam2212-default
    sudo dnf install -y paraview
    ```


3. Ensure that the correct version will be used with:
    ```
    openfoam-selector --set openfoam2212
    ```

4. Refresh the shell by logging out and back in to make openfoam commands accessible.

!!!
Make sure to do the above installation steps on **all** nodes in the cluster.
!!!


### Check Installation


Check an OpenFOAM command can be seen by viewing the help page:

```bash
icoFoam -help
```

!!!
From here on out, all steps **only** need to be done on the **login** node.
!!!
+++