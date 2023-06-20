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

---

#### `software pull <name> <version>`

Download a software binary from the default silo.
    - `--repo <silo>` - Instead of using the default silo, specify which one to delete from.
    - `--overwrite` - Overwrite local software if it exists.

---

#### `software push`

Upload a software binary to the default silo.
    - `--repo <silo>` - Instead of using the default silo, specify which one to delete from.
    - `--force` - Overwrite existing software in the silo if it exists.

---

#### `software search`

List the software binaries in the default silo.
    - `--repo <silo>` - Instead of using the default silo, specify which one to delete from.
