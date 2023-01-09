---
order: 100
label: '2\. Setting Up Compute Nodes'
icon: dot-fill
---



Setting up computes nodes is done slightly differently than a login node. In this example 2 compute nodes are setup, but it could be any non-zero number of compute nodes.

1. Go to the Openstack instances page.

![](/images/openstack_instances.png)

2. Click "Launch Instance", and the instance creation window will pop up.

3. Fill in the instance name, and leave the number of instances as 2, then click next.

![](/images/openstack_instance_details_count2.png)

4. Choose the desired image to use by clicking the up arrow at the end of its row. It will be displayed in the "Allocated" section when selected. 

![](/images/openstack_instance_source.png)

5. Choose the desired instance size by clicking the up arrow at the end of its row. It will be displayed in the "Allocated" section when selected.

![](/images/openstack_instance_flavours.png)

6. Choose a network in the same way as an image or instance size. Note that **this should be the same network as the login node**.

![](/images/openstack_instance_network.png)

7. Choose a security group in the same way as an image or instance size. Note that **this should be the same network as the login node**.

![](/images/openstack_instance_security.png)

8. Choose the keypair in the same way as an image or instance size. 

![](/images/openstack_instance_keypair.png)



9. In the "Configuration" section, there is a "Customisation Script" section with a text box. This will be used to set custom data.

![](/images/openstack_instance_configuration.png)


&ensp;&ensp;&ensp;&ensp;a. Copy this cloud init script into the text box, making sure to change the parts in <> brackets:


```
	#cloud-config
	write_files:
	  - content: |
          SERVER=<private ip of login node>
	    path: /opt/flight/cloudinit.in
	    permissions: '0644'
	    owner: root:root
	users:
	  - name: root
	    ssh_authorized_keys:
	      - <Content of ~/.ssh/id_alcescluster.pub from root user on login node>
```

&ensp;&ensp;&ensp;&ensp;b. To get the information necessary for the cloud init script. Go to the "Instances" page in the "Compute" section. The login node created on the previous page should be visible, use its private IP.

&ensp;&ensp;&ensp;&ensp;c. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

&ensp;&ensp;&ensp;&ensp;d. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/) and open the file `~/.ssh/id_alcescluster.pub`, copy the contents to the cloud init script.


10. When all options have been selected, press the "Launch Instance" button to launch. If the button is greyed out, then a mandatory setting has not been configured.

![](/images/openstack_instance_ready.png)

