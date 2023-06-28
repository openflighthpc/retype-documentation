---
order: 80
label: Files
icon: dot-fill
---

Files can be stored on silos, and use a normal file structure with directories and files, except that the top level directory is the silo. This page describes several commands associated with files in silos which are run in the format `flight silo <command> --<option>`. 

---

### `file list <silo>:`

List the files in a silo. If no silo is specified then the default will be used. 
e.g.
```
[flight@chead1 ~]$ flight silo file list exampleSilo:
file.sh
```
e.g.2
```
[flight@chead1 ~]$ flight silo file list
file.sh
```

---

### `file pull <silo>:<filepath>`

Download a file from a silo. If no silo is specified then the default will be used. 

   - `--recursive` - Downloads a whole directory and all of its contents. You must specify a directory rather than a file.

e.g.

```
[flight@chead1 ~]$ flight silo file pull exampleSilo:file.sh
Pulling '/file.sh' into '/home/flight'...
File(s) downloaded to /home/flight/file.sh
```
e.g.2
```
[flight@chead1 ~]$ flight silo file pull dir/file2.sh
Pulling '/file2.sh' into '/home/flight'...
File(s) downloaded to /home/flight/file2.sh
```

---

### `file push <source> <silo>:<destination>`

Upload a file to a silo.If no silo is specified then the default will be used. 
   - `--recursive` - Uploads a whole directory and all of its contents. You must specify a directory rather than a file.
   - `--make-parent` - Create parent directories if they don't exist.

e.g.
```
[flight@chead1 ~]$ flight silo file push example.sh 
Local file '/home/flight/example.sh' copied to remote '/example.sh'
```
e.g. 2
```
[flight@chead1 ~]$ flight silo file push dir/subdir/example.sh --make-parent
Local file '/home/flight/example.sh' copied to remote '/dir/subdir/example.sh' 
```

---

### `file delete <silo>:<destination>`

Delete a file in a silo. If no silo is specified then the default will be used. 

   - `--recursive` - Deletes a whole directory and all of its contents. You must specify a directory rather than a file.

```
[flight@chead1 ~]$ flight silo file delete example.sh 
Deleting remote file 'example.sh'...
Deleted remote file 'example.sh'
```
