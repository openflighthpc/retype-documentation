---
order: 100
label: '1\. Setting Up a Login Node'
icon: dot-fill
---

Before setting up a cluster, there are several required prerequisites:
- A flight solo image imported to openstack
- The following set up on Openstack:
	- Your own keypair
	- A network
	- A router
	- A security group that allows traffic through ports 22, 80, 8888, 443 and 5900-5903

This documentation includes instructions for [importing an image to Openstack](/cluster_build_methods/get_flight_solo/openstack_setup_solo/), and guides for setting up the other prerequisites can be found in the [Openstack documentation](https://docs.openstack.org/zed/)


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

+++ Use Existing

14. Open the IP Address drop down menu.

![](/images/openstack_manage_ips_dropdown.png)

15. Select one of the IP Addresses.

+++ Allocate New

14. Click the "+" next to the dropdown arrow to open the allocation menu.

![](/images/openstack_manage_ips_new.png)

15. Click "Allocate IP". 

!!!
If all available IPs have already been allocated, use an existing one instead.
!!!

+++

16. Click "Associate" to finish associating an IP.