---
order: 90
label: Silos
icon: dot-fill
---

A silo is a storage space that is the same regardless of platform used. Even though a silo may appear as a directory in your cloud storage, it is highly recommended that a silo should **only** be managed by the command line tool.


### Creating and Adding Silos

To create a silo use the command `flight silo repo create`. This will take you through a series of questions:
   - Provider type - Which provider the silo should be created on. 
   - Silo name - What the name of the silo should be.
    
   &nbsp;After this point, any further questions depend on the chosen platform.
    
+++ AWS
   - Region - The region the silo should be created in.
   - Access key ID - The ID for a valid aws access key.
   - Secret access key - The secret key for a valid aws access key.
   
   More information about AWS access keys can be found [in the AWS documentation](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).
+++

You can add an already existing silo with the command `flight silo repo add`. All questions asked will be the same as for creation, except that the answers will be used to find an existing silo.

### Removing and Deleting Silos

If you no longer wish to have access to a silo on your machine, you can run the command `flight silo repo remove <name>`. This means that in order to access the silo again you would need to use the `add` command. 

A silo can be deleted with `flight silo repo delete <name>`. Unlike the `remove` command, the silo could not be re-added later as it is fully deleted along with all of its contents.


### Setting a default silo

If a default silo has been set, then commands that require a silo to be specified in the argument will use the default instead. Set a default with the command `flight silo set-default` e.g.
```
[flight@chead1 ~]$ flight silo set-default openflight
Default silo set to: openflight
```
