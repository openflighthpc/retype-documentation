---
order: 10
label: Create Shared User
icon: dot-fill
---

There are other ways of doing it, but in this documentation we will create a shared user by making the exact same user on every node.

Add a user named flight on the head node

```bash
useradd -d /home/flight -u 1234 flight 
```

Set the new user's password:
```bash
passwd flight
```

On compute nodes do:

```bash
useradd -d /home/flight -u 1234 flight -M
```

Set the new user's password:
```bash
passwd flight
```


Repeat this on every other comput node.
