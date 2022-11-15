---
order: 100
label: Setting Up a Login Node
icon: dot-fill
---

To set up a cluster, you will need a Flight Solo Image, which can either be from Amazon Marketplace, or imported as a file.

+++ Marketplace

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

+++ Imported


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




+++
