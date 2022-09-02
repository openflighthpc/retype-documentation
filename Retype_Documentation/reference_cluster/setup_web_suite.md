---
order: 40
label: Install Flight Web Suite
icon: dot-fill
---

Flight web suite only needs to be installed on the head node. Swap to the head node (unless already on it).


Install the web suite:

```bash
sudo yum install flight-web-suite -y
```

Install extra packages:
```bash
sudo yum install python-websockify xorg-x11-apps netpbm-progs -y
```

Find your ip:

```bash
curl ifconfig.co
```

Set the domain name. This is for use with certificate generation.

```bash
flight web-suite set-domain 18.170.36.50
```

Go to the file `/opt/flight/opt/www/landing-page/default/content/data/environment.yaml` and change name to mycluster1. It will look something like this:
```
environment:
#   # Optional cluster (aka environment) name.  Defaults to an empty string if
#   # not provided.
  name: "mycluster1"

```

Create a self-signed certificate to secure the connection.

```bash
flight www cert-gen --cert-type self-signed --domain $(hostname -f)
```

Restart web suite to apply changes:
```bash
flight web-suite restart
```

Go to your browser, and copy the hostname (in this case `18.170.36.50`) into the search bar.

You may be warned about the security risk of proceeeding to the website like this:

![](/images/security_risk.png)


Continue through it to reach the flight web suite.



Back on the console, you may want to enable flight web suite:
```bash
flight web-suite enable
```
This means that flight web suite will start on boot

