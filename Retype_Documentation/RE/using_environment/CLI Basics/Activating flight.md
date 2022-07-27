---
label: Activating Flight
order: 89
icon: 
---

When connecting to a new session you may be shown this:

```bash
Welcome to gateway1, based on CentOS Linux 7.9.2009.

This cluster provides an Alces Flight Direct HPC environment.

'flight start' - activate Flight Direct now
'flight info'  - get some brief help about Flight Direct
'flight set'   - change login defaults (see 'flight info' for details)

[flight@chead1 ~]$
```

Many of the utilities demonstrated in this documentation are not available on a normal linux command line. To make the most of your HPC enable Flight Direct with the command `flight start`.

```bash
[flight@chead1 ~]$ flight start
  'o`
 'ooo`                                       Welcome to gateway1
 `oooo`
  `oooo`         'o`                    Flight Direct r2022.4
    `ooooo`  `ooooo            Based on CentOS Linux 7.9.2009
       `oooo:oooo`
          `v  -[ alces flight ]-

TIPS:

'flight help'           - get help on available commands
'flight env'            - manage software package ecosystems
'flight desktop'        - manage interactive GUI desktop sessions

Flight Direct is now active.
[flight@chead1 (gateway1) ~]$
```

Enabling Flight Direct needs to be done every single time you log in. However, it can be set to always on with the command `flight set always on`.

This and other settings can be changed at any time. Run the command `flight help` for more information.