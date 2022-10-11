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

2. Create an(/all?) environment form the list of avaiable environments:
    ```
    flight env create <environment>
    ```

3. Activate the environment created in step 2:
    ```
    flight env activate <environment>
    ```

4. Deactivate the environment activated in step 3:
    ```
    flight env deactivate
    ```