---
order: 80
label: 'c\. Configure Web Suite'
icon: dot
---

Only on the login node:

1. Set the domain name to the hostname or ip address that Web-Suite will be accessed through. This also creates a self-certified certificate.
    ```bash
    flight web-suite set-domain <name/IP>
    ```

2. Restart web suite to apply changes:
    ```bash
    flight web-suite restart
    ```
