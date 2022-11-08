---
order: 75
label: (AWS) Setting Up a Login Node
icon: dot
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

4. Configure region, software version (if unsure use the latest), and fulfillment option (if unsure use the default). Then click "Continue to Launch". **Make sure the region is the same for all nodes to be used in a cluster.**

![](/images/aws_continue_launch.png)

5. Click on "Usage Instructions" to see some instructions on how to get started, and a link to this documentation.

![](/images/aws_launch_usage.png)


6. Select the "Launch from Website" action.

![](/images/aws_launch_action.png)


7. Choose an instance type to use.

![](/images/aws_instance_type.png)


8. Choose VPC settings. **Remember what VPC was used to create this instance**, as it should also be used for any associated compute nodes.

![](/images/aws_vpc_settings.png)


9. Choose a subnet. **Remember what subnet was used to create this instance**, as it should also be used for any associated compute nodes.

![](/images/aws_subnet_settings.png)

10. It is recommended to use the seller's settings for a security group. If you have already created on these, use it again. Otherwise click "Create New Based On Seller Settings".

![](/images/aws_security_group.png)

11. Give your security group a name, and description, then configure the allowed IPs as necessary.

![](/images/aws_seller_settings.png)


12. Choose what key pair to use. *It is good practice for this to be the same on all nodes in a cluster.*

![](/images/aws_keypair_settings.png)

13. Click Launch

![](/images/aws_login_launched.png)

