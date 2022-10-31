---
order: 60
label: Environment
icon: dot-fill
---

Flight grants access to package ecosystems via the env command. To test its functionality:

1. Check the available environments:
    ```
    flight env avail
    ```
    This should show all the environments available to be created.

2. Create the environment needed from the list of available environments:
    ```
    flight env create <environment>
    ```
    This should display its progress while creating the environment, and send a message if successful. E.g.
    ```
    [flight@chead1 (mycluster1) ~]$ flight env create conda
    Creating environment conda@default
        > ✅ Verifying prerequisites
        > ✅ Fetching prerequisite (miniconda) 
        > ✅ Creating environment (conda@default) 
    Environment conda@default has been created

    ```


3. Check that the environment is displayed in the list of created environments:
    ```
    flight env list
    ```
    This should display a list of all created environments, which should include the one created in step 2. E.g.
    ```
    [flight@chead1 (mycluster1) ~]$ flight env list
    ┌───────────────┬───────┐
    │ Name          │ Scope │
    ├───────────────┼───────┤
    │ conda@default │ user  │
    └───────────────┴───────┘
    ```

4. Activate the environment created in step 2:
    ```
    flight env activate <environment>
    ```
    Upon successful activation, the command prompt should change to show the currently activated environment. E.g.
    ```
    [flight@chead1 (mycluster1) ~]$ flight env activate conda
    (base) <conda> [flight@chead1 (mycluster1) ~]$ 
    ```

5. Deactivate the environment activated in step 4:
    ```
    flight env deactivate
    ```
    Upon successful deactivation, the command prompt should return to how it looks with just flight enabled.


6. Purge the environment created:
    ```
    flight env purge <environment>
    ```

### More Information

All information about Flight Environment can be found in [its documentation section](/hpc_environment_usage/ecosystems/flight_environment/).
