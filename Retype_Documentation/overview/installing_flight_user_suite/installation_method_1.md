---
order: 90
label: "Installation Method 1: Quick"
icon: dot
---
Installation Method 1: Quick
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The quickest and simplest way to get up and running with the user suite is to simply install the group package for the tools. This will ensure that compatible versions of all the tools are installed.

.. tabs::

    .. group-tab:: CentOS 7

        - Install the user suite RPM::

            [flight@gateway1 ~]$ sudo yum install flight-user-suite

    .. group-tab:: CentOS 8

        - Install the user suite RPM::

            [flight@gateway1 ~]$ sudo dnf install flight-user-suite

    .. group-tab:: Ubuntu 18.04

        - Install the user suite deb::

            flight@gateway1:~$ sudo apt-get install flight-user-suite

    .. group-tab:: Ubuntu 20.04

        - Install the user suite deb::

            flight@gateway1:~$ sudo apt-get install flight-user-suite


.. note:: After installation, either reboot your system or logout and back in again to expose the ``flight`` command to the shell
