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


4. Set the domain name. This is for use with certificate generation. Setting the domain name as the ip address of the head node means that changing pages doesn't log the user out.
  ```bash
  flight web-suite set-domain 18.170.36.50
  ```

5. Go to the file `/opt/flight/opt/www/landing-page/default/content/data/environment.yaml` and change `name` to mycluster1. It will look something like this:
  ```
  environment:
  #   # Optional cluster (aka environment) name.  Defaults to an empty string if
  #   # not provided.
    name: "mycluster1"
  ```

6. Create a self-signed certificate to secure the connection.
  ```bash
  flight www cert-gen --cert-type self-signed --domain $(hostname -f)
  ```

7. Restart web suite to apply changes:
  ```bash
  flight web-suite restart
  ```

8. Enable flight web suite:
  ```bash
  flight web-suite enable
  ```
This means that flight web suite will start on boot

!!!
Using Flight Web Suite is explained [elsewhere in the documentation.](/hpc_environment_usage/flight_web_suite/what_is_web_suite/)
!!!