---
order: 90
label: Running a simple job
icon: dot
---



1. Create a job script in the working directory. This script assumes that it is being launched from the home directory, change it if that is not the case. It also cannot be run as the root user.

    ```bash
    cat << 'EOF' > cavity-example.sh
    #!/bin/bash -l
    #SBATCH -N 1

    module load mpi
    source /opt/apps/OpenFOAM/OpenFOAM-v2212/etc/bashrc

    # Create job directory from example job
    cp -r $FOAM_TUTORIALS/incompressible/icoFoam/cavity/cavity $HOME/.
    cd $HOME/cavity

    # Calculate fluid pressure with OpenFOAM tools
    blockMesh
    checkMesh
    icoFoam
    EOF
    ```

2. Submit the job to the queue system:
    ```
    sbatch cavity-example.sh
    ```

3. Check that the job is running (it may take some time to complete):

    ```bash
    squeue
    ```


### Viewing the Results

Once the cavity job has finished running, the results can be visualised through a desktop session.

1. Connect to VNC or web-suite desktop (For more information on launching desktops, see the [Flight Desktop section](/flight_environment_usage/flight_desktop/launch_a_desktop_session/)).


2. Navigate to the cavity directory and launch the paraFoam viewer:

    ```bash
    cd cavity
    paraFoam 
    ```

3. In the window that opens, scroll down to "Mesh parts" and select all the boxes, then click apply

![](/images/openfoam_parafoam_1.png)

4. Next, change the display to 'U' in the dropdown menu, click play to change the timestamp and then click and drag to rotate the subject

![](/images/openfoam_parafoam_2.png)





