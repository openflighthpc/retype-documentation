---
order: 80
label: Configuring Web Suite
icon: dot-fill
---


## System Prerequisites

In order to authenticate the user in the web interface, the following must be true:
- User has a password (can be set with the `passwd` command or through other user management software that is
setup on the system)
- Ports 80 & 443 on the gateway must be accessible (allowed through both the system firewall and cloud security
group)
- SSH password authentication must be enabled (can be set in `/etc/ssh/sshd_config` in CentOS or through
other access management software that is setup on the system)

## Certificate Preparation

To secure the server connections, it is recommended to generate a certificate to be used by the web suite. The Flight
Web Suite comes with tools that can generate either a “self-signed” or LetsEncrypt certificate. Alternatively, a certificate that has been created outside of the web suite can be used to secure the server.


 
+++ Self-Signed

A self-signed certificate, whilst not usually trusted by browsers, does still provide extra security to the web server over
HTTP communication.
A self-signed certificate is automatically created when installing the packages from the repo.
To generate and install the self-signed certificates, simply:
```bash
flight www cert-gen --cert-type self-signed --domain $(hostname -f)
```
After this has run, changes are applied on a service restart:
```bash
flight web-suite restart
```
+++ Lets Encrypt

To generate and install a Lets Encrypt certificate, run the following (replacing the domain and email with appropriate
values):
```bash
flight www cert-gen --cert-type lets-encrypt --domain gateway1.mycluster1.example.com --email user@example.com
```

!!!
Ensure that the domain/IP is publicly accessible in order for certificate generation to work
!!!

After this has run, changes are applied on a service restart:
```bash
flight web-suite restart
```
+++ External Certificate

Externally generated certificates can be used by placing them in `/opt/flight/etc/www/ssl/`, the files that
should be in there are:
- `fullchain.pem`: The full certificate (recommended permissions are 644 root:root)
- `key.pem`: The private key for the certificate (recommended permissions are 644 root:root)
After placing the certificates in place, the HTTPS server can be enabled with:

```bash
flight web-suite restart
```
+++