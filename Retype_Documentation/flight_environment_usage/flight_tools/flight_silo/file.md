---
order: 80
label: Files
icon: dot-fill
---



### Viewing files

To list the files in a particular silo use the command `flight silo file list <silo>:` e.g.
```
[flight@chead1 ~]$ flight silo file list openflight:
OpenFOAM-v2212.tar.gz
motorBike.tar.gz
```

### Downloading files

To download a file from a silo, use the command `flight silo file pull <silo>:<filepath>` e.g.
```
[flight@chead1 ~]$ flight silo file pull openflight:motorBike.tar.gz
Pulling '/motorBike.tar.gz' into '/home/flight'...
File(s) downloaded to /home/flight/motorBike.tar.gz
```

### Uploading Files
To upload a file to a silo, use the command `flight silo file push`

```
[flight@chead1 ~]$ flight silo file push example.sh 
Local file '/home/flight/example.sh' copied to remote '/example.sh'
```

### Deleting Files

To delete a file, use the command `flight silo file delete`

```
[flight@chead1 ~]$ flight silo file delete example.sh 
Deleting remote file 'example.sh'...
Deleted remote file 'example.sh'
```
