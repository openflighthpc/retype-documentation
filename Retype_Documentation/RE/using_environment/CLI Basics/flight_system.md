---
order: 90
label: Flight System
icon: dot
---


# Flight System




## Activating the Flight System


The Flight User Suite sits unobtrusively on the research environment with the `flight` command serving as an entrypoint to the various system commands.

This provides some quick tips to activating the system and finding out more about the flight system (`flight info`).

To load the system, simply run `flight start` (which, when first run, will generate some login keys for allowing passwordless login to compute nodes)


![](/images/flight_start.png)

!!!
The flight system can be set to automatically start on login for the user by running `flight set always on`
!!!

## Customising the Environment

### Setting the Research Environment Name

To identify the research environment that's being worked on, a cluster name can be specified and displayed in the prompt when the Flight System is active. 

A cluster name can be specified as follows:

```bash
[flight@gateway1 ~]$ flight config set cluster.name scooby
```

Note that for the name change to take effect you must start a new terminal session or stop/start Flight.