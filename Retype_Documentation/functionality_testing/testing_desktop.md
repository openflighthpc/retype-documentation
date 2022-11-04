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
    This shows all the available desktops, and whether or not they are verified. More information about desktop verification can be found [here](http://localhost:5000/hpc_environment_usage/flight_desktop/preparing_a_desktop_type/).

2. Launch a desktop session:
    ```
    flight desktop start gnome
    ```
    If successful, you will be given information about the newly created desktop session. E.g.
    ```
    [flight@chead1 (mycluster1) ~]$ flight desktop start gnome
    Starting a 'gnome' desktop session:

       > ✅ Starting session 

    A 'gnome' desktop session has been started.

    == Session details ==
          Name:       
      Identity: ae8963ed-caee-4c86-b570-437a798eb836
          Type: gnome
       Host IP: 10.50.0.34
      Hostname: chead1
          Port: 5902
       Display: :2
      Password: KrodJaj5
      Geometry: 1024x768

    This desktop session is not directly accessible from outside of your
    cluster as it is running on a machine that only provides internal
    cluster access.  In order to access your desktop session you will need
    to perform port forwarding using 'ssh'.

    Refer to 'flight desktop show ae8963ed' for more details.

    If prompted, you should supply the following password: KrodJaj5

    ```

3. Connect to the desktop session. The instructions for connecting to a desktop session can be found [here](/hpc_environment_usage/flight_desktop/launch_a_desktop_session/)

4. Check the list of desktops:
    ```
    flight desktop list
    ```
    The desktop session created in step 2 should be listed here. E.g.
    ```
    [flight@chead1 (mycluster1) ~]$ flight desktop list
    ┌──────┬──────────┬───────┬───────────┬────────────┬────────────────┬──────────┬────────┐
    │ Name │ Identity │ Type  │ Host name │ IP address │ Display (Port) │ Password │ State  │
    ├──────┼──────────┼───────┼───────────┼────────────┼────────────────┼──────────┼────────┤
    │      │ ae8963ed │ gnome │ chead1    │ 10.50.0.34 │ :2 (5902)      │ KrodJaj5 │ Active │
    └──────┴──────────┴───────┴───────────┴────────────┴────────────────┴──────────┴────────┘
    ```

5. Resize the desktop:
    ```
    flight desktop resize <id> 1920x1080
    ```
    The desktop should be resizable, in this case to 1280 by 1024 pixels.

6. Kill the desktop:
    ```
    flight desktop kill <id>
    ```
    The desktop should be killable with the id it shows in the list in step 4. E.g.
    ```
    [flight@chead1 (mycluster1) ~]$ flight desktop kill ae8963ed
   Killing desktop session ae8963ed-caee-4c86-b570-437a798eb836:

      > ✅ Terminating session 

   Desktop session 'ae8963ed-caee-4c86-b570-437a798eb836' has been terminated.

   ```

If all of the steps have occured without issue, then the desktop is functioning.

### More Information

All information about Flight Desktop can be found in [its documentation section](/hpc_environment_usage/flight_desktop/install_flight_desktop_types/).