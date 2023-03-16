---
order: 40
label: Install Flight Web Suite
icon: dot
---

Flight web suite only needs to be installed on the head node. 


1. Swap to the head node (unless already on it).


2. Install the web suite:
    ```bash
    sudo yum install -y flight-web-suite 
    ```

3. Install extra packages:
    ```bash
    sudo yum install -y python-websockify xorg-x11-apps netpbm-progs 
    ```


4. Set the domain name to the hostname or ip address that Web-Suite will be accessed through. This also creates a self-certified certificate.
    ```bash
    flight web-suite set-domain <name/IP>
    ```

5. Go to the file `/opt/flight/opt/www/landing-page/default/content/data/environment.yaml` and change `name` to mycluster1. It will look something like this:
    ```
    environment:
    #   # Optional cluster (aka environment) name.  Defaults to an empty string if
    #   # not provided.
    name: "mycluster1"
    ```

6. Restart web suite to apply changes:
    ```bash
    flight web-suite restart
    ```

7. Enable flight web suite:
    ```bash
    flight web-suite enable
    ```
This means that flight web suite will start on boot

!!!
Using Flight Web Suite is explained [elsewhere in the documentation.](/flight_environment_usage/flight_web_suite/)
!!!

## Testing

If all was successful, then the following should be the case on the head node:

1. The command `flight web-suite` runs without errors

2. The domain is what it was set to during the instructions. E.g.
    ```
    [root@chead1 (mycluster1) ~]# flight web-suite get-domain
    my-domain-name
    ```

3. The Web-suite is active, this can be checked with the following command:
    ```
    flight service avail
    ```

4. The Web-Suite should function as described in [its documentation](/flight_environment_usage/flight_web_suite/).