---
title: "Launch a Second EC2 Instance"
date: "2026-09-14"
weight: 4
chapter: false
pre: "<b> 5.4.4 </b>"
---

## Overview

In this step, we will create an **Amazon Machine Image (AMI)** from the existing backend EC2 instance and use it to launch a second instance. Adding another backend instance will increase the deployment's capacity and improve fault tolerance once it is registered with the load balancer.

---

## Implementation Steps

### Step 1: Create an AMI from the Existing EC2 Instance

- Open the **Amazon EC2 console**, choose **Instances**, and select the existing backend instance.
- Choose **Actions → Image and templates → Create image**.

![Create an AMI from the backend instance](/images/myimage/5_4/5_4_4/image1.png)

- Enter an image name and leave the remaining settings at their defaults.

![Enter the AMI name](/images/myimage/5_4/5_4_4/image2.png)

- Scroll down and choose **Create image**.

![Submit the image creation request](/images/myimage/5_4/5_4_4/image3.png)

### Step 2: Launch a Second EC2 Instance from the AMI

- In the EC2 navigation pane, scroll down to **Images** and choose **AMIs**.

![Open the AMIs page](/images/myimage/5_4/5_4_4/image4.png)

- Select the AMI you just created and choose **Launch instance from AMI**.

![Launch an instance from the new AMI](/images/myimage/5_4/5_4_4/image5.png)

- Configure the instance by following the instructions in section **5.2.1**.

![Configure the second EC2 instance](/images/myimage/5_4/5_4_4/image6.png)

> **Note:** For **Network settings**, use the configuration shown below to follow the workshop setup. Place the new instance in the **same VPC** as the first instance, but in a **different subnet**.

![Configure the VPC and subnet for the second instance](/images/myimage/5_4/5_4_4/image7.png)

- Choose **Launch instance** on the right.
