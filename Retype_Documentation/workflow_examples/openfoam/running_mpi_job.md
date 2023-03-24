---
order: 80
label: Running an MPI Job
icon: dot
---


1. Start by downloading this job directory in a location of your choice.
    ```
    flight silo file pull openflight:openfoam/motorBike.tar.gz
    ```


2. Decompress it, which will make a directory called `motorBike`.
    ```
    tar xf motorBike.tar.gz
    ```

3. Update the job configuration.
    - Open `motorBike/system/decomposeParDict` and set:
        - `X` to the number of processes to run across.
        - `A B C` to be numbers such that `A`*`B`\*`C`=`X`


4. Update the job script.
    - Open `motorBike/motorbike-example.sh`.
        - Set `-n X` to the number of processes to run across.
        - Set `source` to point to the location of OpenFOAM.


5. Submit the job script to the scheduler.
    ```
    sbatch motorBike/motorbike-example.sh
    ```

### View Results

Once the job has finished running, the results can be visualised through a desktop session.

1. Connect to VNC or web-suite desktop (For more information on launching desktops, see the [Flight Desktop section](/flight_environment_usage/flight_desktop/launch_a_desktop_session/)).

2. Open a terminal and navigate to the job directory.

3. Launch Paraview
    ```
    source /opt/apps/OpenFOAM/OpenFOAM-v2212/etc/bashrc
    paraFoam
    ```

4. In the window that opens, go to the bottom left and scroll down to "Mesh parts". Select all the boxes  except `frontAndBack`, `inlet`, `internalMesh`, `outlet` and `upperWall`, and then click apply.


![](/images/openfoam_parafoam_motorbike_1.png)

5. You should now see a motorbike along with a rider and the forces visualised on them!

![](/images/openfoam_parafoam_motorbike_2.png)






