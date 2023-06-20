---
order: 70
label: Software
icon: dot-fill
---

Software in the context of Flight Silo is software binaries that can be compiled in advance, and then kept in a silo so that they can be accessed from any number of machines without needing to be recompiled. This page describes several commands associated with software which are run in the format `flight silo <command> --<option>`. 

!!!
Software are made to appear less like files in a directory and more like a list of accessible software. They do not have directories and can be managed by version number.
!!!

---

#### `software delete <name> <version>`

Delete a software binary from the default silo.
    - `--repo <silo>` - Instead of using the default silo, specify which one to delete from.

e.g.
```
[flight@chead1 ~]$ flight silo software delete exampl 0.0
Deleting software 'exampl' version '0.0'...
Deleted software 'exampl' version '0.0'.
```

---

#### `software pull <name> <version>`

Download and extract a software binary from the default silo.
    - `--repo <silo>` - Instead of using the default silo, specify which one to delete from.
    - `--overwrite` - Overwrite local software if it exists.

e.g.
```
[flight@chead1 ~]$ flight silo software pull exampl 0.0
Downloading software 'exampl' version '0.0'...
Extracting software to '/home/flight/.local/share/flight/silo/software'...
Extracted software 'exampl' version '0.0 to '/home/flight/.local/share/flight/silo/software'...
```

---

#### `software push`

Upload a software binary to the default silo.
    - `--repo <silo>` - Instead of using the default silo, specify which one to delete from.
    - `--force` - Overwrite existing software in the silo if it exists.

e.g.
```
[flight@chead1 ~]$ flight silo software push OpenFOAM-v2212.tar.gz exampl 0.0
Uploading software 'exampl' version '0.0'...
Uploaded software 'exampl' version '0.0'.

```

---

#### `software search <name>`

List the software binaries in the default silo. If no name is given, then all software will be displayed.
    - `--repo <silo>` - Instead of using the default silo, specify which one to delete from.

e.g.
```
[flight@chead1 ~]$ flight silo software search exampl
┌────────┬─────────┬────────┐
│ Name   │ Version │ Size   │
├────────┼─────────┼────────┤
│ exampl │ 0.0     │ 500 MB │
└────────┴─────────┴────────┘
```

e.g.2
```
[flight@chead1 ~]$ flight silo software search
Showing latest 5 versions...
┌────────┬─────────┐
│ Name   │ Version │
├────────┼─────────┤
│ exampl │ 0.0     │
└────────┴─────────┘
```