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

- `--silent` or `-s` makes the program output only errors.

- `--quiet` or `-q` makes the program also output the section being tested, e.g. SLURM tests.

- `--chatty` or `-c` makes the program also output the individual tests being run e.g. Test 1: activation. This is the default level.

- `--verbose` or `-v` makes the program also output orange warning and green success messages.


As an example:
```
bash function_tests.sh -v
```


## Automatic Web Suite Testing

The aforementioned functionality test script does not cover the flight web suite since it is a browser based application. However, there is another way to test it.

### Selenium IDE

Selenium is a web automation tool, specifically designed for testing web applications. There are several different versions, but the one used here is [Selenium IDE](https://www.selenium.dev/selenium-ide/).

1. Get the Selenium IDE browser extension from https://www.selenium.dev/selenium-ide/ 

2. Get a local copy of the flight web tests from [here](https://github.com/openflighthpc/reference-evaluation/blob/main/auto-web-tests.side).

3. After it has been added to your browser, open it, it should look like this:

![](/images/selenium_open.png)

4. Select "Open an existing project" and open the file mentioned in step 2. It should look like this:

![](/images/selenium_file_opened.png)

5. Click on the arrow next to the "Tests" button.

![](/images/selenium_tests_button.png)

6. From the drop down menu, select "Test suites"

![](/images/selenium_tests_dropdown.png)

7. Click on "Web-Suite-Tests" and then select "1-login-test" from below.

![](/images/selenium_suite.png)

8. Select the "Enter Username" field, and in the "Value" field, change it from "username" to your web-suite username.

9. Select the "Enter Password" field, and in the "Value" field, change it from "password" to your web-suite password.

10. Change the URL to the domain name set when starting Web-Suite.

![](/images/selenium_url.png)

11. Finally, click "Run All tests in suite"

![](/images/selenium_run_all.png)


All tests will run, and any errors will be highlighted in red.