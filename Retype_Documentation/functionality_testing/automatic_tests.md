---
order: 0
label: 
icon: dot-fill
---

By performing the tests on the previous pages, it is possible to determine whether a cluster is functioning properly or not. However, there is also a set of automated tests that can determine the functionality of a system. 


The functionality test script can be found [here](https://github.com/openflighthpc/reference-evaluation/blob/main/function_tests.sh). It contains a series of automatic tests that run through a system and check the services evaluated in this section of the documentation except for Web Suite. Upon finding an issue, a message will be sent to the console with a rough description of the error, and what flight service is at fault. Depending on the error, the program may cease testing until the issue is fixed. 

### Usage Guide

1. To begin, copy the test script into the home directory of a user.
 
2. Run it with the command:

    ```
    bash function_tests.sh
    ```

There is 1 option that can be added to the script: verbosity. By default, all the necessary information will be written to the console, but that can be changed with the following:

- `--verbose` or `-v` makes the program output everything.

- `--chatty` or `-c` makes the program output more.

- `--quiet` or `-q` makes the program output less.

- `--silent` or `-s` makes the program output only errors.

As an example:
```
bash function_tests.sh -v
```


## Automatic Web Suite Testing