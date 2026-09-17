---
title: "Create an Application Load Balancer"
date: "2026-09-14"
weight: 2
chapter: false
pre: "<b> 5.4.2 </b>"
---

## Overview

In this step, we will create and configure an **Application Load Balancer (ALB)** to receive incoming traffic and distribute it across the backend EC2 instances. Once the second instance is registered later in this chapter, this setup will improve application availability and resilience.

---

## Implementation Steps

### Step 1: Open Load Balancers in the EC2 Console

Open the **Amazon EC2 console**. In the navigation pane, scroll down to **Load Balancing** and choose **Load Balancers**.

- Choose **Create load balancer**.

![Open the load balancer creation page](/images/myimage/5_4/5_4_2/image1.png)

### Step 2: Select the Load Balancer Type

- For this workshop, select **Application Load Balancer**.

![Select Application Load Balancer](/images/myimage/5_4/5_4_2/image2.png)

### Step 3: Configure the ALB

- Enter a name for the load balancer and configure the basic settings as shown below.

![Configure the ALB basic settings](/images/myimage/5_4/5_4_2/image3.png)

- Under **Network mapping**, select the VPC used by your backend EC2 instance and select the three subnets shown in the example.

![Configure network mapping](/images/myimage/5_4/5_4_2/image4.png)

- Under **Security groups**, keep the default selection and add the security group used by the backend EC2 instance you configured earlier.

![Select the security groups](/images/myimage/5_4/5_4_2/image5.png)

- Under **Listeners and routing**, select the target group created in section **5.4.1**. Leave the remaining settings at their defaults.

![Configure the listener and target group routing](/images/myimage/5_4/5_4_2/image6.png)

- Choose **Create load balancer**.

![Create the Application Load Balancer](/images/myimage/5_4/5_4_2/image7.png)
