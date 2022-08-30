---
order: 80
label: Resizing the desktop to fit your screen
icon: dot
---



### Specifying a size with the flight desktop tool

When launching a graphical desktop session using the ``flight desktop`` utility, a session resolution can be specified using the ``--geometry <size>`` option. For example, to launch a ``gnome`` desktop session with a resolution of 1920x1080 pixels, use the command:

```bash
[flight@gateway1(mycluster1) ~]$ flight desktop start --geometry 1920x1080 gnome
```

By default, your graphical desktop session will launch with a compatibility resolution of 1024x768. Users can resize the desktop to fit their screens using the Linux ``xrandr`` command, run from within the graphical desktop session.

To view the available screen resolutions, start a terminal session on your graphical desktop by navigating to the ``Applications`` menu in the top left-hand corner of the screen, then selecting the ``Terminal`` under the ``System tools`` menu.

![](https://use.openflighthpc.org/_images/startingterminal.png)

The ``xrandr`` command will display a list of available resolutions supported by your desktop:

```bash
[flight@gateway1(mycluster1) ~]$ xrandr
Screen 0: minimum 32 x 32, current 1024 x 768, maximum 32768 x 32768
VNC-0 connected primary 1024x768+0+0 0mm x 0mm
   1920x1200     60.00
   1920x1080     60.00
   1600x1200     60.00
   1680x1050     60.00
   1400x1050     60.00
   1360x768      60.00
   1280x1024     60.00
   1280x960      60.00
   1280x800      60.00
   1280x720      60.00
   1024x768      60.00*
   800x600       60.00
   640x480       60.00
```
To set a new resolution, run the `xrandr` command again with the `-s <resolution>` argument;

- e.g. to change to 1280x1024, enter the command `xrandr -s 1280x1024`

Your graphical desktop session will automatically resize to the new resolution requested. Use your local VNC client application to adjust the compression ratio, colour depth and frame-rate sessions in order to achieve the best user-experience for the desktop session.