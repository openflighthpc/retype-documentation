---
order: 80
label: "Installation Method 2: Slightly Less Quick"
icon: dot
---
Installation Method 2: Slightly Less Quick
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each tool in the user suite is also available through the repositories and can be installed one at a time.

.. tabs::

    .. group-tab:: CentOS 7

        - Install the Flight Runway RPM::

            [flight@gateway1 ~]$ sudo yum install flight-runway

        - Install Flight Env RPM::

            [flight@gateway1 ~]$ sudo yum install flight-env

        - Install Flight Desktop RPM::

            [flight@gateway1 ~]$ sudo yum install flight-desktop

        - Install Flight Starter RPM::

            [flight@gateway1 ~]$ sudo yum install flight-starter

    .. group-tab:: CentOS 8

        - Install the Flight Runway RPM::

            [flight@gateway1 ~]$ sudo dnf install flight-runway

        - Install Flight Env RPM::

            [flight@gateway1 ~]$ sudo dnf install flight-env

        - Install Flight Desktop RPM::

            [flight@gateway1 ~]$ sudo dnf install flight-desktop

        - Install Flight Starter RPM::

            [flight@gateway1 ~]$ sudo dnf install flight-starter

    .. group-tab:: Ubuntu 18.04

        - Install Flight Runway deb::

            flight@gatewat1:~$ sudo apt-get install flight-runway

        - Install Flight Env deb::

            flight@gatewat1:~$ sudo apt-get install flight-env

        - Install Flight Desktop deb::

            flight@gatewat1:~$ sudo apt-get install flight-desktop

        - Install Flight Starter deb::

            flight@gatewat1:~$ sudo apt-get install flight-starter

    .. group-tab:: Ubuntu 20.04

        - Install Flight Runway deb::

            flight@gatewat1:~$ sudo apt-get install flight-runway

        - Install Flight Env deb::

            flight@gatewat1:~$ sudo apt-get install flight-env

        - Install Flight Desktop deb::

            flight@gatewat1:~$ sudo apt-get install flight-desktop

        - Install Flight Starter deb::

            flight@gatewat1:~$ sudo apt-get install flight-starter


.. note:: After installation, either reboot your system or logout and back in again to expose the ``flight`` command to the shell
