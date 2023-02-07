---
order: 90
label: '2\. Make a Compute Node'
icon: dot
---


Setting up compute nodes is done slightly differently than a login node. In this example 2 compute nodes are setup, but it could be any non-zero number of compute nodes.

+++ AWS Marketplace



1. Go to the EC2 instance setup page through marketplace.

a. Find the Flight Solo image [here](https://alces-flight.com/solo/aws) or by searching the marketplace for "Flight Solo".

!!!
The image, along with this documentation is open-source, and freely available to use. However if more help is needed, the developers of Flight Solo offer paid additional support.
!!!

b. Click "Continue to Subscribe"

![](/images/aws_continue_subscribe.png)


c. Read the terms and conditions, then click "Continue to Configuration"

![](/images/aws_continue_configure.png)

d. Configure region, software version (if unsure use the latest), and fulfillment option (if unsure use the default). Then click "Continue to Launch". **Make sure the region is the same for all nodes to be used in a cluster.**

![](/images/aws_continue_launch.png)

e. Click on "Usage Instructions" to see some instructions on how to get started, and a link to this documentation.

![](/images/aws_launch_usage.png)


f. Select the "Launch from EC2" action

![](/images/aws_launch_action_ec2.png)

g. Click "Launch" to go to the EC2 instance setup page.


![](/images/aws_ec2.png)

## Configuring Settings

2. Set the instance name and number of instances.

![](/images/aws_ec2_num_instances.png)

3. Confirm that the region(top right, next to username) **is the same as the region the login node was created in.** 

![](/images/aws_region.png)

4. In the "Application and OS Images" section, confirm that Flight Solo is the selected AMI.

![](/images/aws_ec2_appandOS.png)


5. In the "Instance type" section, choose the required instance size.

![](/images/aws_ec2_instance_type.png)

6. In the "Keypair" section, select a keypair to use. *It is good practice to use the same keypair for the login and compute nodes.*

![](/images/aws_ec2_keypair.png)


7. In the "Network settings" section, **select the same network, subnet, and security group as the login node.**

![](/images/aws_ec2_security.png)

&ensp;&ensp;&ensp;&ensp;a. To change the network and subnet, click the "Edit" button, and then use the drop downs to find the correct network and subnet.

![](/images/aws_ec2_security_edit.png)


8. In the "Configure Storage" section, allocate as much memory as needed. 8GB is the minimum required for Flight Solo, so it is likely the compute nodes will not need much more than that, as the login node hosts most data.

![](/images/aws_ec2_storage.png)

9. In the "Advanced details" section there are many settings, but at the bottom is a text box labeled "User data". 

![](/images/aws_ec2_userdata.png)


&ensp;&ensp;&ensp;&ensp;a. Copy this cloud init script into the user data section, making sure to change the parts in <> brackets:


    
	#cloud-config
	write_files:
	  - content: |
          SERVER=<private ip of login node>
	    path: /opt/flight/cloudinit.in
	    permissions: '0644'
	    owner: root:root
	users:
	  - default    
	  - name: root
	    ssh_authorized_keys:
	      - <Content of ~/.ssh/id_alcescluster.pub from root user on login node>
    
    
&ensp;&ensp;&ensp;&ensp;b. To get the information necessary for the cloud init script. Go to the [EC2 console](https://eu-west-2.console.aws.amazon.com/ec2/v2/home?region=eu-west-2#Instances:). 
Make sure your region is set to the one used for login and compute nodes.

&ensp;&ensp;&ensp;&ensp;c. Select the created login node to see more details about it, including the private ip.

![](/images/aws_ec2_console.png)

&ensp;&ensp;&ensp;&ensp;d. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

&ensp;&ensp;&ensp;&ensp;e. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/) and open the file `~/.ssh/id_alcescluster.pub`, copy the contents to the cloud init script.

10. Back on the compute node creation page, click "Launch Instance".

!!!
Repeat this process for any other types of nodes that need to be added to the cluster.
!!!





+++ AWS Imported

1. Go the EC2 instance [console](https://eu-west-2.console.aws.amazon.com/ec2/home?region=eu-west-2#Instances:v=3;$case=tags:true%5C,client:false;$regex=tags:false%5C,client:false)

![](/images/aws_ec2_console_overview.png)

a. Click "Launch Instance" to go to the EC2 instance setup page.


![](/images/aws_ec2.png)

## Configuring Settings

2. Set the instance name and number of instances.

![](/images/aws_ec2_num_instances.png)

3. Confirm that the region(top right, next to username) **is the same as the region the login node was created in.** 

![](/images/aws_region.png)

4. In the "Application and OS Images" section choose the "My AMIs" tab and select your imported solo AMI.

![](/images/aws_ec2_appandOS_myami.png)


5. In the "Instance type" section, choose the required instance size.

![](/images/aws_ec2_instance_type.png)

6. In the "Keypair" section, select a keypair to use. *It is good practice to use the same keypair for the login and compute nodes.*

![](/images/aws_ec2_keypair.png)


7. In the "Network settings" section, **select the same network, subnet, and security group as the login node.**

![](/images/aws_ec2_security.png)

&ensp;&ensp;&ensp;&ensp;a. To change the network and subnet, click the "Edit" button, and then use the drop downs to find the correct network and subnet.

![](/images/aws_ec2_security_edit.png)


8. In the "Configure Storage" section, allocate as much memory as needed. 8GB is the minimum required for Flight Solo, so it is likely the compute nodes will not need much more than that, as the login node hosts most data.

![](/images/aws_ec2_storage.png)

9. In the "Advanced details" section there are many settings, but at the bottom is a text box labeled "User data". 

![](/images/aws_ec2_userdata.png)


&ensp;&ensp;&ensp;&ensp;a. Copy this cloud init script into the user data section, making sure to change the parts in <> brackets:


    
	#cloud-config
	write_files:
	  - content: |
          SERVER=<private ip of login node>
	    path: /opt/flight/cloudinit.in
	    permissions: '0644'
	    owner: root:root
	users:
	  - default    
	  - name: root
	    ssh_authorized_keys:
	      - <Content of ~/.ssh/id_alcescluster.pub from root user on login node>
    
    
&ensp;&ensp;&ensp;&ensp;b. To get the information necessary for the cloud init script. Go to the [EC2 console](https://eu-west-2.console.aws.amazon.com/ec2/v2/home?region=eu-west-2#Instances:). 
Make sure your region is set to the one used for login and compute nodes.

&ensp;&ensp;&ensp;&ensp;c. Select the created login node to see more details about it, including the private ip.

![](/images/aws_ec2_console.png)

&ensp;&ensp;&ensp;&ensp;d. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

&ensp;&ensp;&ensp;&ensp;e. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/) and open the file `~/.ssh/id_alcescluster.pub`, copy the contents to the cloud init script.

10. Back on the compute node creation page, click "Launch Instance".

!!!
Repeat this process for any other types of nodes that need to be added to the cluster.
!!!


+++ Openstack


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
  - default
  - name: root
    ssh_authorized_keys:
      - <Content of ~/.ssh/id_alcescluster.pub from root user on login node>
```

&ensp;&ensp;&ensp;&ensp;b. To get the information necessary for the cloud init script. Go to the "Instances" page in the "Compute" section. The login node created on the previous page should be visible, use its private IP.

&ensp;&ensp;&ensp;&ensp;c. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

&ensp;&ensp;&ensp;&ensp;d. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/) and open the file `~/.ssh/id_alcescluster.pub`, copy the contents to the cloud init script.


10. When all options have been selected, press the "Launch Instance" button to launch. If the button is greyed out, then a mandatory setting has not been configured.

![](/images/openstack_instance_ready.png)

+++ Azure

+++