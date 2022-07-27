---
order: 85
label: Port Forwarding with a Desktop Session
---

Depending on your connection to the HPC you may see this message when starting a desktop session:

```bash
This desktop session is not directly accessible from outside of your
cluster as it is running on a machine that only provides internal
cluster access.  In order to access your desktop session you will need
to perform port forwarding using 'ssh'.
```

For example in the following:

```bash
[flight@chead1 (your_cluster) ~]$ flight desktop start gnome
Starting a 'gnome' desktop session:

   > ✅ Starting session

A 'gnome' desktop session has been started.

== Session details ==
      Name:
  Identity: dd8acf76-1494-4c88-adb1-a8bbd405d965
      Type: gnome
   Host IP: 20.68.202.163
  Hostname: chead1
      Port: 5903
   Display: :3
  Password: WB3gUQMW
  Geometry: 1024x768

This desktop session is not directly accessible from outside of your
cluster as it is running on a machine that only provides internal
cluster access.  In order to access your desktop session you will need
to perform port forwarding using 'ssh'.

Refer to 'flight desktop show dd8acf76' for more details.

If prompted, you should supply the following password: WB3gUQMW
```

By running the command `flight desktop show <name>` we can see more information

```bash
[flight@chead1 (your_cluster) ~]$ flight desktop show dd8acf76

== Session details ==
      Name:
  Identity: dd8acf76-1494-4c88-adb1-a8bbd405d965
      Type: gnome
   Host IP: 20.68.202.163
  Hostname: chead1
      Port: 5903
   Display: :3
  Password: WB3gUQMW
  Geometry: 1024x768

This desktop session is not directly accessible from outside of your
cluster as it is running on a machine that only provides internal
cluster access.  In order to access your desktop session you will need
to perform port forwarding using 'ssh':

  ssh -L 5903:20.68.202.163:5903 flight@

Once the ssh connection has been established, depending on your
client, you can connect to the session using one of:

  vnc://flight:WB3gUQMW@localhost:5903
  localhost:5903
  localhost:3

If, when connecting, you receive a warning as follows, try again with
a different port number, e.g. 5904, 5905 etc.:

  channel_setup_fwd_listener_tcpip: cannot listen to port: 5903

If prompted, you should supply the following password: WB3gUQMW
```
+++Windows

On Windows, the desktop environment can still be connected like so:

1. Begin your environment as demonstrated on the previous page. 

2. Note down the IP address, port number and password.

3. Open PuTTy, or get it from the [Prerequisites](/USE/overview/prerequisites) page and then open it.

4. Load one of your saved sessions or save a new session with your log in details.

![](/images/putty_load_session.png)

5. Find the "Category:" section on the left of the window

    a. Scroll down to "Connection" and expand it.
    b. Scroll down to "SSH" and expand it.
    c. Click on the "Tunnels page.

![](/images/tunnels_page.png)

6. Input the source port (a local port) and destination which is `IP address:port number` of the desktop environment that was started.

![](/images/source_and_destination.png)

7. After inputting the information, click "Add" and the details will move to a box above.

![](/images/tunnels_add_button.png)

8. Scroll back to the top of the "Category:" section, and click on "Session"

![](/images/save_session.png)

9. Save the session and then click open to run the command line interface and log in.

11. Open your VNC client, and type `localhost:XXXXX` where `XXXX` is the source port number you entered earlier.

![](/images/vnc_client_local.png)

12. Click "Connect", and if prompted enter the password you noted down.
+++ Linux/Mac

On Linux or Mac remotely connecting to the desktop environment is easier than on Windows.

Note that in the above code block there is mentioned a command.

`ssh -L 5903:20.68.202.163:5903 flight@`

By running `flight desktop show <name>` the flight environment will also give you a command to use for port forwarding. After running the command continue with your VNC client as normal.

+++