---
order: 100
label: '1\. Make a Login Node'
icon: dot
---

+++ AWS Marketplace

To set up a cluster, you will need a Flight Solo Image, which can either be from Amazon Marketplace, or [imported as a file](/cluster_build_methods/aws/import_solo_aws/).


1. Find the Flight Solo image [here](https://alces-flight.com/solo/aws) or by searching the marketplace for "Flight Solo".

!!!
The image, along with this documentation is open-source, and freely available to use. However if more help is needed, the developers of Flight Solo offer paid additional support.
!!!

2. Click "Continue to Subscribe"

![](/images/aws_continue_subscribe.png)


3. Read the terms and conditions, then click "Continue to Configuration"

![](/images/aws_continue_configure.png)

4. Configure region, software version (if unsure use the latest), and fulfillment option (if unsure use the default). Then click "Continue to Launch". **Make sure the region is the same for all nodes to be used in a cluster.**

![](/images/aws_continue_launch.png)

5. Click on "Usage Instructions" to see some instructions on how to get started, and a link to this documentation.

![](/images/aws_launch_usage.png)


6. Select the "Launch from Website" action.

![](/images/aws_launch_action.png)


7. Choose an instance type to use.

![](/images/aws_instance_type.png)


8. Choose VPC settings. **Remember what VPC was used to create this instance**, as it should also **be used for any associated compute nodes.**

![](/images/aws_vpc_settings.png)


9. Choose a subnet. **Remember what subnet was used to create this instance**, as it should also **be used for any associated compute nodes.**

![](/images/aws_subnet_settings.png)

10. A security group is needed to associate with all nodes on the cluster. It is recommended to use a security group with rules limiting traffic through:
    - HTTP
    - HTTPS
    - SSH
    - Port 8888
    - Ports 5900 - 5903
    - All traffic from within the security group should be allowed. (This rule can only be added after creation)


    If you already have a security group which does this, use it here and **make sure to use it again for the compute nodes.** Otherwise, a security group can be made from the launch page, or through the [security groups page](https://eu-west-2.console.aws.amazon.com/ec2/home?region=eu-west-2#SecurityGroups:)

    
    The seller's settings (shown below) can be used as a reference for creating a security group.

![](/images/aws_seller_settings.png)

&ensp;&ensp;&ensp;&ensp;Describing exactly how to create a security group is out of scope for this documentation, but covered by the [AWS documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html?icmpid=docs_ec2_console#creating-security-group). 

&ensp;&ensp;&ensp;&ensp;However, here is an example security group that might be used for a Flight Solo cluster:

![](/images/aws_security_group_example.png)

&ensp;&ensp;&ensp;&ensp;After a security group has been made, click "Select existing security group" select it from the drop down menu.

![](/images/aws_security_group.png)

12. Choose what key pair to use. *It is good practice for this to be the same on all nodes in a cluster.*

![](/images/aws_keypair_settings.png)

13. Click Launch

![](/images/aws_login_launched.png)






+++ AWS Imported

To set up a cluster, you will need a Flight Solo Image, which can either be from Amazon Marketplace, or [imported as a file](/cluster_build_methods/aws/import_solo_aws/).


1. Go the EC2 instance [console](https://eu-west-2.console.aws.amazon.com/ec2/home?region=eu-west-2#Instances:v=3;$case=tags:true%5C,client:false;$regex=tags:false%5C,client:false)

![](/images/aws_ec2_console_overview.png)
2. Click "Launch" to go to the EC2 instance setup page.

![](/images/aws_ec2.png)

3. Set the number of instances to 1, and name of instance to something descriptive.

![](/images/aws_ec2_single_instance.png)

4. Confirm that the region(top right, next to username) is correct.

![](/images/aws_region.png)

5. In the "Application and OS Images" section choose the "My AMIs" tab and select your imported solo AMI.

![](/images/aws_ec2_appandOS_myami.png)

6. In the "Instance type" section, choose the required instance size.

![](/images/aws_ec2_instance_type.png)

7. In the "Keypair" section, select a keypair to use. *It is good practice to use the same keypair for the login and compute nodes.*

![](/images/aws_ec2_keypair.png)

8. In the "Network settings" sections, click the "Edit" button to set the network and subnet. **Remember what these are**, as they should be the same **for any associated compute nodes.**


![](/images/aws_ec2_security.png)


![](/images/aws_ec2_security_edit.png)


9. Another thing needed is a security group to associate with all nodes on the cluster. It is recommended to use a security group with rules limiting traffic through:
    - HTTP
    - HTTPS
    - SSH
    - Port 8888
    - Ports 5900 - 5903
    - All traffic from within the security group should be allowed. (This rule can only be added after creation)


    If you already have a security group which does this, use it here and **make sure to use it again for the compute nodes.** Otherwise, a security group can be made from the launch page, or through the [security groups page](https://eu-west-2.console.aws.amazon.com/ec2/home?region=eu-west-2#SecurityGroups:)

    

&ensp;&ensp;&ensp;&ensp;Describing exactly how to create a security group is out of scope for this documentation, but covered by the [AWS documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html?icmpid=docs_ec2_console#creating-security-group). 

&ensp;&ensp;&ensp;&ensp;However, here is an example security group that might be used for a Flight Solo cluster:

![](/images/aws_security_group_example.png)

&ensp;&ensp;&ensp;&ensp;After a security group has been made, click "Choose Existing" select it from the drop down menu.





9. In the "Configure Storage" section, allocate as much memory as needed. 8GB is the minimum required for Flight Solo, so it is likely the compute nodes will not need much more than that, as the login node hosts most data.

![](/images/aws_ec2_storage.png)


10. Finally, click "Launch Instance".



+++ Openstack



Before setting up a cluster, there are several required prerequisites:
- A flight solo image imported to openstack
- The following set up on Openstack:
	- Your own keypair
	- A network
	- A router
	- A security group that allows traffic through ports 22, 80, 8888, 443 and 5900-5903

This documentation includes instructions for [importing an image to Openstack](/cluster_build_methods/openstack/openstack_setup_solo/), and guides for setting up the other prerequisites can be found in the [Openstack documentation](https://docs.openstack.org/zed/)


To set up a cluster:

1. Go to the Openstack instances page.

![](/images/openstack_instances.png)

2. Click "Launch Instance", and the instance creation window will pop up.

3. Fill in the instance name, and leave the number of instances as 1, then click next.

![](/images/openstack_instance_details.png)

4. Choose the desired image to use by clicking the up arrow at the end of its row. It will be displayed in the "Allocated" section when selected. 

![](/images/openstack_instance_source.png)

5. Choose the desired instance size by clicking the up arrow at the end of its row. It will be displayed in the "Allocated" section when selected.

![](/images/openstack_instance_flavours.png)

6. Choose a network in the same way as an image or instance size. Note that **all nodes in a cluster must be on the same network**.

![](/images/openstack_instance_network.png)

7. Choose a security group in the same way as an image or instance size. Note that **all nodes in a cluster must be in the same security group**.

![](/images/openstack_instance_security.png)

8. Choose the keypair in the same way as an image or instance size. 

![](/images/openstack_instance_keypair.png)


9. When all options have been selected, press the "Launch Instance" button to launch. If the button is greyed out, then a mandatory setting has not been configured.

![](/images/openstack_instance_ready.png)

10. Go to the "Instances" page in the "Compute" section. The created node should be there and be finishing or have finished creation.

![](/images/openstack_associate_ip.png)


11. Click on the down arrow at the end of the instance row. This will bring up a drop down menu. 

12. Select "Associate Floating IP", this will make the ip management window pop up.

![](/images/openstack_manage_ips.png)

13. Associate a floating IP, either by using an existing one or allocating a new one.

To Use Existing

14. Open the IP Address drop down menu.

![](/images/openstack_manage_ips_dropdown.png)

15. Select one of the IP Addresses.

To Allocate New

14. Click the "+" next to the dropdown arrow to open the allocation menu.

![](/images/openstack_manage_ips_new.png)

15. Click "Allocate IP". 

!!!
If all available IPs have already been allocated, use an existing one instead.
!!!



16. Click "Associate" to finish associating an IP.

+++
