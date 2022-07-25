---
order: 100
label: 
icon:
---



Your OpenFlight Compute gateway node can run graphical desktop sessions to support users who want to run interactive applications across the research environment. The system can support a number of different sessions simultaneously, and allow multiple remote participants to connect to the same session to support training and collaborative activities.

## Install Flight Desktop Types

Your OpenFlight Compute research environment supports many types of graphical session designed to provide interactive applications directly to users. To view the available types of session, use the command `flight desktop avail`:

```bash
[flight@chead1 (ivan1) ~]$ flight desktop avail
┌──────────┬──────────────────────────────────────────────────┬────────────┐
│ Name     │ Summary                                          │ State      │
├──────────┼──────────────────────────────────────────────────┼────────────┤
│ chrome   │ Full-screen Google Chrome browser session.       │ Unverified │
│          │                                                  │            │
│          │  > https://www.google.com/chrome/                │            │
│          │                                                  │            │
│ gnome    │ GNOME v3, a free and open-source desktop         │ Verified   │
│          │ environment for Unix-like operating systems.     │            │
│          │                                                  │            │
│          │  > https://www.gnome.org/                        │            │
│          │                                                  │            │
│ kde      │ KDE Plasma Desktop (KDE 4). Plasma is KDE's      │ Unverified │
│          │ desktop environment. Simple by default, powerful │            │
│          │ when needed.                                     │            │
│          │                                                  │            │
│          │  > https://kde.org/                              │            │
│          │                                                  │            │
│ terminal │ Preconfigured terminal for Flight HPC            │ Verified   │
│          │ environments.                                    │            │
│          │                                                  │            │
│ xfce     │ Xfce is a lightweight desktop environment for    │ Unverified │
│          │ UNIX-like operating systems. It aims to be fast  │            │
│          │ and low on system resources, while still being   │            │
│          │ visually appealing and user friendly.            │            │
│          │                                                  │            │
│          │  > https://xfce.org/                             │            │
│          │                                                  │            │
│ xterm    │ Minimal desktop environment with an xterm        │ Verified   │
│          │ terminal window.                                 │            │
│          │                                                  │            │
│          │ >                                                │            │
│          │ https://invisible-island.net/xterm/xterm.html    │            │
│          │                                                  │            │
└──────────┴──────────────────────────────────────────────────┴────────────┘
```

Application types that are `unverified` need to be prepared before they can be started. To prepare a new session type, use the command `flight desktop prepare <type>` (preparing will automatically install any required application and support files, if these dependencies have been installed manually then a desktop session can be checked for verfication with `flight desktop verify <type>`). Once enabled, users can start a new session using the command `flight desktop start <type>`.

!!!
The `prepare` command is only available to the `root` user as it requires installation of packages
!!!

!!!
Preparing a new session type only enables it for the machine that you run the command from, any other nodes will need to have the type enabled too.
!!!
