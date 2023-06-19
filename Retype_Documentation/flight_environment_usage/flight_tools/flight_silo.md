---
order: 80
label: Flight Silo
icon: dot
---

Flight Silo allows users to connect to "silos" - cloud storage systems designed primarily to distribute software and projects, with more general file storage also available. Silo comes pre-installed as part of the User Suite included with Flight Solo.

## Setting up
Use `flight silo type avail` to list available platform types. e.g.
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
Types are the backend providers of storage, and each type can hold multiple silos. These can be listed with the command `flight silo repo list`. e.g.
```
[flight@chead1 ~]$ flight silo repo list
┌────────────┬───────────────────────────────────┬──────────┬─────────┐
│ Name       │ Description                       │ Platform │ Public? │
├────────────┼───────────────────────────────────┼──────────┼─────────┤
│ openflight │ Openflight software and resources │ aws      │ true    │
└────────────┴───────────────────────────────────┴──────────┴─────────┘
```

## Managing Silos

A silo is a storage space that is the same regardless of platform used. Despite appearing to be a directory, it is highly recommended that silos be managed only with the `flight silo` command line tool.


To create a silo use the command `flight silo repo create`. This will take you through a series of questions:
   - Provider type - Which provider the silo should be created on. 
   - Silo name - What the name of the silo should be.
    
   &nbsp;After this point, any further questions depend on the chosen platform.
    
+++ AWS
   - Region - The region the silo should be created in.
   - Access key ID - The ID for a valid aws access key.
   - Secret access key - The secret key for a valid aws access key.
   
   More information about AWS access keys can be found [in the aws documentation](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).
+++

You can add an already existing silo with the command `flight silo repo add`. All questions asked will be the same as for creation, except that the answers will be used to find an existing silo.

### Removing and Deleting Silos

If you no longer wish to have access to a silo on your machine, you can run the command `flight silo repo remove <name>`. This means that in order to access the silo again you would need to use the `add` command. 

A silo can be deleted with `flight silo repo delete <name>`. Unlike the `remove` command, the silo could not be re-added later as it is fully deleted along with all of its contents.


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
