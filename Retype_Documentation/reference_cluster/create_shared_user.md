---
order: 10
label: Create Shared User
icon: dot-fill
---

step 9 create shared user

create an identical user on 3 nodes

useradd -d /home/flight -u 1234 flight

created a user called flight

passwd flight




now on other nodes

useradd -d /home/flight -u 1234 flight -M
