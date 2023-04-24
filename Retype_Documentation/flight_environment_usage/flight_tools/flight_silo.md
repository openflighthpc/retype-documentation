---
order: 80
label: Flight Silo
icon: dot
---

Flight Silo allows users to connect to "silos" - cloud storage systems designed primarily to distribute software and projects, with more general file storage also available. Silo comes pre-installed as part of the User Suite included with Flight Solo.

## Setting up
Use `flight silo type avail` to list available types. e.g.
```
[flight@chead1 ~]$ flight silo type avail
┌──────┬───────────────────────────────┬──────────┐
│ Name │ Description                   │ Prepared │
├──────┼───────────────────────────────┼──────────┤
│ aws  │ Amazon Simple Storage Service │ false    │
└──────┴───────────────────────────────┴──────────┘
```
!!! 
Types are not prepared by default. To prepare a type you must [become a root user](/general_environment_usage/cli_basics/becoming_the_root_user/), and then do `flight silo type prepare <type>`. e.g.
```
[root@chead1 ~]# flight silo type prepare aws
Preparing...
Type aws prepared for use
```
!!!
Types are the backend providers of storage, each type can hold multiple silos. These can be listed with the command `flight silo repo list`. e.g.
```
[flight@chead1 ~]$ flight silo repo list
┌────────────┬───────────────────────────────────┬──────────┬─────────┐
│ Name       │ Description                       │ Platform │ Public? │
├────────────┼───────────────────────────────────┼──────────┼─────────┤
│ openflight │ Openflight software and resources │ aws      │ true    │
└────────────┴───────────────────────────────────┴──────────┴─────────┘
```

## Viewing and accessing files

To list the files in a particular repo use the command `flight silo file list <repo>:` e.g.
```
[flight@chead1 ~]$ flight silo file list openflight:
OpenFOAM-v2212.tar.gz
motorBike.tar.gz
```

To pull a file from a repo, use the command `flight silo file pull <repo>:<filepath>` e.g.
```
[flight@chead1 ~]$ flight silo file pull openflight:motorBike.tar.gz
Pulling '/motorBike.tar.gz' into '/home/flight'...
File(s) downloaded to /home/flight/motorBike.tar.gz
```

## More information

These commands and a summary of each of them can be viewed with `flight silo help`, using the `--help` argument on a particular command will give more information about it. e.g.
```
[flight@chead1 ~]$ flight silo repo list --help
  SYNOPSIS:

    flight silo repo list

  DESCRIPTION:

    List available existing silos

```
