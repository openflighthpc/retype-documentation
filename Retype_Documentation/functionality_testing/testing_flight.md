---
order: 90
label: Flight
icon: dot-fill
---

The Flight User Suite serves as an entrypoint to the various system commands. To test it's functionality:

1. Check whether flight is started or not with this command:
    ```
    flight
    ```
    This should show a list of available flight commands, that will look like this:
    ```
    [flight@chead1 (mycluster1) ~]$ flight
      'o`
     'ooo`                                                        
     `oooo`                                                       
      `oooo`         'o`
        `ooooo`  `ooooo
           `oooo:oooo`
              `v  -[ alces flight ]- 

    Usage: flight COMMAND [[OPTION]... [ARGS]]
    Perform high performance computing management activities.

    Commands:
      flight config           Configure a global HPC environment setting.
      flight desktop          Manage interactive GUI desktop sessions.
      flight env              Manage and access HPC application ecosystems.
      flight help             Display help and usage information.
      flight howto            View user guides for your HPC environment.
      flight info             Brief help about your HPC environment.
      flight job              Generate and submit jobs from predefined templates.
      flight landing-page     Flight WWW landing page.
      flight profile          Manage node provisioning.
      flight service          Manage HPC environment services.
      flight set              Configure an HPC environment setting.
      flight shell            Enter a shell-like sandbox for a Flight command.
      flight start            Activate your HPC environment.
      flight stop             Deactivate your HPC environment.
      flight web-suite        Manage web-suite services.
      flight www              Manage the HTTPs server and SSL certificates.

    For more help on a particular command run:
      flight COMMAND help

    Please report bugs to <flight@openflighthpc.org>
    OpenFlight home page: <https://openflighthpc.org/>

    ```
    
    Any other output suggests that flight is not functioning properly. 

### More Information

If Flight is not functioning, it may be worth checking the [Flight Basics](/hpc_environment_usage/flight_overview/what_is_flight_user_suite/) section.




