---
order: 90
label: Launch a Desktop Session
icon: dot-fill
---


Users can launch a new session by using the `flight desktop start gnome` command. After launching the desktop, a message will be printed with connection details to access the new session:

```bash
Starting a 'gnome' desktop session:

   > ✅ Starting session

A 'gnome' desktop session has been started.

== Session details ==
      Name:
  Identity: 4549eae1-6f8b-4983-8057-99b378afcdd3
      Type: gnome
   Host IP: 20.68.202.163
  Hostname: chead1
      Port: 5901
   Display: :1
  Password: mkO3Zxjl
  Geometry: 1024x768

This desktop session is not directly accessible from outside of your
cluster as it is running on a machine that only provides internal
cluster access.  In order to access your desktop session you will need
to perform port forwarding using 'ssh'.

Refer to 'flight desktop show 4549eae1' for more details.

If prompted, you should supply the following password: mkO3Zxjl

```

Users need a VNC client to connect to the graphical desktop session - for a list of tested clients, see [Prerequisites](/USE/overview/prerequisites).

Users with Mac clients can use the URL provided in the command output to connect to the session; e.g. from the above example, simply enter `vnc://flight:L9Uysvi3@52.151.119.86:5902` into the Safari address bar. Linux and Windows users should enter the IP address and port number shown into their VNC client in the format `IP:port`. For example - for the output above, Linux and Windows client users would enter `52.151.119.86:5902` into their VNC client:

![](/images/vncclient.png)

A one-time randomized password is automatically generated automatically by OpenFlight Compute when a new session is started. Linux and Windows users may be prompted to enter this password when they connect to the desktop session.

Once connected to the graphical desktop, users can use the session as they would a local Linux machine:

![](/images/vncdesktop.png)