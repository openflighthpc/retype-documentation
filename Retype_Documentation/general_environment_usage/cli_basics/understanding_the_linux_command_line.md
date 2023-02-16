---
label: Understanding the Command Line Interface
order: 95
icon: dot
---

Almost all usage of the Flight system takes place via the Linux command line. For unfamiliar users here is a brief description of it.

```bash
[flight@chead1 (mycluster1) folder]$ echo Hello World!
Hello World!
```

- `flight` is the name of the user.
- `chead1` is the node the user is currently on.
- `(mycluster1)` is the name of the cluster being used.
- `folder` is the directory the user is currently in. If this is a `~` then that means you are in your home directory.
- `$` indicates whether the user is a root user or normal user (root users see a `#`).
- `echo Hello World!` is a command that prints out "Hello World!". This is where commands you type will go.

```bash
[username@node (clustername) folder]$ command
```

If some things that you see here are missing from your command line, you may not have activated [Flight](/flight_environment_usage/flight_overview/flight_system/#activating-the-flight-system).

Here is an example of a Linux Command Line Interface (CLI) without Flight enabled:

```bash
[username@node folder]$ command
```

