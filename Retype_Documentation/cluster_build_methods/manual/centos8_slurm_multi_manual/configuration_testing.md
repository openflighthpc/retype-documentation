---
order: -10
label: Testing the Configuration
icon: dot
---

By following all the steps in the previous pages, your reference cluster should be set up and functioning. If this is not the case, then there are two ways the issues can be found and fixed:

1. By following the testing instructions on every page to narrow down the issue and then search the instructions on the page for differences between your cluster and the proposed setup.

2. By running the reference cluster test script.


## Test Script

The reference cluster test script can be downloaded from [here](https://github.com/alces-flight/reference-evaluation/blob/main/configuration_test.sh). It contains a series of automatic tests that run through a cluster and check for issues. Upon finding an issue, a message will be sent to the console with a rough description of the error, and what page of the documentation to check. Depending on the error, the program may cease testing until the issue is fixed. 

### Usage Guide

1. To begin, copy the test script into the home directory of the root user.
 
2. Run it as root with the command:

    ```
    bash configuration_test.sh
    ```

There is 1 option that can be added to the script: verbosity. By default, all the necessary information will be written to the console, but that can be changed with the following:

- `-v` makes the program output more.

- `-q` makes the program output less.

- `-e` makes the program output only errors.

As an example:
```
bash configuration_test.sh -v
```


!!!
The test script was written with the aim of testing the configuration according to the instructions. If a cluster has strayed too far from the instructions, then the script may not be able to find errors correctly or at all.
!!!
