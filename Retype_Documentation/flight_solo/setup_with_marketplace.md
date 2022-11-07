---
order: 70
label: Setting Up with AWS Marketplace
icon: dot-fill
---

The Flight Solo image can also be found on AWS Marketplace. This allows for users of Amazon Web Services to get started without downloading anything.

1. Find the Flight Solo image [here](https://aws.amazon.com/marketplace/pp/prodview-q5u533n6b34oc) or by searching the marketplace for "Flight Solo".

!!!
The image, along with this documentation is open-source, and freely available to use. However if more help is needed, the developers of Flight Solo offer paid additional support.
!!!

2. Click "Continue to Subscribe"

![](/images/aws_continue_subscribe.png)


3. Read the terms and conditions, then click "Continue to Configuration"

![](/images/aws_continue_configure.png)

4. Configure region, software version (if unsure use the latest), and fulfillment option (if unsure use the default). Then click "Continue to Launch". Make sure the region is the same for all nodes to be used in a cluster.

![](/images/aws_continue_launch.png)

5. Click on "Usage Instructions" to see some instructions on how to get started, and a link to this documentation.

![](/images/aws_launch_usage.png)


+++ Launch a login node

## For a login node

6. Select the "Launch from Website" action.

![](/images/aws_launch_action.png)


7. Choose an instance type to use.

![](/images/aws_instance_type.png)


8. Choose VPC settings. Remember what VPC was used to create this instance, as it should also be used for any associated compute nodes.

![](/images/aws_vpc_settings.png)


9. Choose a subnet. Remember what subnet was used to create this instance, as it should also be used for any associated compute nodes.

![](/images/aws_subnet_settings.png)

10. It is recommended to use the seller's settings for a security group. If you have already created on these, use it again. Otherwise click "Create New Based On Seller Settings".

![](/images/aws_security_group.png)

11. Give your security group a name, and description, then configure the allowed IPs as necessary.

![](/images/aws_seller_settings.png)


12. Choose what key pair to use. It is good practice for this to be the same on all nodes in a cluster.

![](/images/aws_keypair_settings.png)

13. Click Launch

![](/images/aws_login_launched.png)



+++ Launch a compute node

## For compute nodes

6. Select the "Launch from EC2" action

![](/images/aws_launch_action_ec2.png)

7. Click "Launch" to go to the EC2 instance setup page.

![](/images/aws_ec2.png)

8. Set the instance name and number of instances.

9. Confirm that the region(top right, next to username) is the same as the region the login node was created in. 

![](/images/aws_region.png)


10. In the "Application and OS Images" section, confirm that Flight Solo is the selected AMI.

![](/images/aws_ec2_appandOS.png)

11. In the "Instance type" section, choose the required instance size.

![](/images/aws_ec2_instance_type.png)

12. In the "Keypair" section, select a keypair to use. It is good practice to use the same keypair for the login and compute nodes.

![](/images/aws_ec2_keypair.png)

13. In the "Network settings" section, select the same security group that was used for the login node. Note that you will need to click "Edit" to change the subnet and/or VPC.

![](/images/aws_ec2_security.png)


14. In the "Configure Storage" section, allocate as much memory as needed. 8GB is the minimum required for Flight Solo, so it is likely the compute nodes will not need much more than that, as the login node hosts most data.

![](/images/aws_ec2_storage.png)

15. In the "Advanced details" section there are many settings, but at the bottom is a text box labeled "User data". 

    ![](/images/aws_ec2_userdata.png)

    Copy this cloud init script into the user data section, making sure the change the parts in <> brackets:
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
    
16. To get the information necessary for the cloud init script. Go to the [EC2 console](https://eu-west-2.console.aws.amazon.com/ec2/v2/home?region=eu-west-2#Instances:). Make sure your region is set to the one used for login and compute nodes.

17. Select the created login node to see more details about it, including the private ip.

![](/images/aws_ec2_console.png)

18. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

19. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/)  and open the file `~/.ssh/id_alcescluster.pub`, copy the contents to the cloud init script.

20. Back on the compute node creation page, click "Launch Instance".

+++