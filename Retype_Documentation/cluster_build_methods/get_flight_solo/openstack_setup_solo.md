---
order: 
label: Import Flight Solo Image to Openstack
icon: dot
---

Several different cloud hosting services can use the downloaded Flight Solo image. This page shall describe how to do it with Openstack.

First, go to the Images section of OpenStack, and press the create image button.

![](/images/openstack_images.png)


A window with image details will appear. Select the format `Raw`, and upload the flight solo [file](/cluster_build_methods/what_is_flight_solo/#where-can-i-download-flight-solo).


![](/images/image_create_details.png)


Fill in any desired settings, or if unsure leave it blank and the defaults will be used. When all the information needed to create an image has been written into the form, the `Create image` button will become available, hit it to create the image.

!!!
The image may take some time to load.
!!!


