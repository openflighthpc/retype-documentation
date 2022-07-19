---
icon: ":wc:"
order: -100
---


- Download the OpenFlight Azure template:

``` bash
$ curl -o cluster.json https://raw.githubusercontent.com/openflighthpc/openflight-compute-cluster-builder/master/templates/azure/cluster.json
```

- Generate base64 customdata string to set the default username to `flight` and add an SSH public key for authentication:

``` bash
$ DATA=$(cat << EOF
#cloud-config
system_info:
  default_user:
    name: flight
runcmd:
  - echo "ssh-rsa MySSHpublicKeyHere user@host" >> /home/flight/.ssh/authorized_keys
EOF
)
$ echo "$DATA" |base64 -w 0
I2Nsb3VkLWNvbmZpZwpzeXN0ZW1faW5mbwogIGRlZmF1bHRfdXNlcjoKICAgIG5hbWU6IGZsaWdodApydW5jbWQ6CiAgLSBlY2hvICJzc2gtcnNhIE15U1NIcHVibGljS2V5SGVyZSB1c2VyQGhvc3QiID4+IC9ob21lL2ZsaWdodC8uc3NoL2F1dGhvcml6ZWRfa2V5cwo=
```

!!!
The base64 value will differ from the above depending on the SSH key specified. It does not need to match the example output above.
!!!

- Create resource group for the cluster:

``` bash
$ az group create --name mycluster --location "UK South"
```

- Deploy a cluster (with a gateway and 2 nodes):
``` bash
$ az group deployment create --name mycluster --resource-group mycluster \
--template-file cluster.json \
--parameters sourceimage="SOURCE_IMAGE_PATH_HERE" \
clustername="mycluster" \
customdata="I2Nsb3VkLWNvbmZpZwpzeXN0ZW1faW5mbwogIGRlZmF1bHRfdXNlcjoKICAgIG5hbWU6IGZsaWdodApydW5jbWQ6CiAgLSBlY2hvICJzc2gtcnNhIE15U1NIcHVibGljS2V5SGVyZSB1c2VyQGhvc3QiID4+IC9ob21lL2ZsaWdodC8uc3NoL2F1dGhvcml6ZWRfa2V5cwo="
```

!!!
The above command can be modified to override the other parameters mentioned at the beginning of this page. The 3 parameters used in the above command are the minimum required to bring a cluster up
!!!

- Setup passwordless root SSH to all compute nodes from the gateway. This can be done by generating a public key with `ssh-keygen` and adding it to `/root/.ssh/authorized_keys` on the gateway and all other nodes.