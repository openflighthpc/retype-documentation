---
order: 70
label: Desktop
icon: dot-fill
---

Flight Desktop allows for an interactive use of a cluster. To test its functionality:

1. Check desktop availability:
    ```
    flight desktop avail
    ```
    This shows all the available desktops, and whether or not they are verified. 

2. Launch a desktop session:
    ```
    flight desktop start gnome
    ```
    If successful, you will be given information about the newly created desktop session.

3. Connect to the desktop session. The instructions for connecting to a desktop session can be found [here](/hpc_environment_usage/flight_desktop/launch_a_desktop_session/)

4. Check the list of desktops:
    ```
    flight desktop list
    ```
    The desktop session created in step 2 should be listed here.

5. Resize the desktop:
    ```
    xrandr -s 1280x1024
    ```
    The desktop should be resizable, in this case to 1280 by 1024 pixels.

6. Kill the desktop:
    ```
    flight desktop kill <id>
    ```
    The desktop should be killable with the id it shows in the list in step 4.


If all of the steps have occured without issue, then the desktop is functioning.

### More Information

All information about Flight Desktop can be found in [its documentation section](/hpc_environment_usage/flight_desktop/install_flight_desktop_types/).