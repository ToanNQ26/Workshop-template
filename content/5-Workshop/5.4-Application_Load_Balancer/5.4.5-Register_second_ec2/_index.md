---
title: "Register the Second EC2 Instance"
date: "2026-09-14"
weight: 5
chapter: false
pre: "<b> 5.4.5 </b>"
---

## Overview

In this step, we will register the second backend EC2 instance with the **target group** used by the Application Load Balancer. This allows the ALB to distribute traffic across both instances, increasing capacity and improving fault tolerance.

---

## Implementation Steps

### Step 1: Open the Existing Target Group

- Open **Target Groups** in the Amazon EC2 console, as described in section **5.4.1**, and select the target group you created earlier.

![Open the existing target group](/images/myimage/5_4/5_4_5/image1.png)

### Step 2: Register the Second EC2 Instance

- Choose **Register targets** in the lower-right area of the page.

![Open the target registration page](/images/myimage/5_4/5_4_5/image2.png)

- Select the second EC2 instance you just launched, set the port to `80`, and choose **Include as pending below**.

![Select the second EC2 instance and port](/images/myimage/5_4/5_4_5/image3.png)

- Scroll down, review the pending target, and choose **Register pending targets**.

![Register the pending target](/images/myimage/5_4/5_4_5/image4.png)

- Wait for the health checks to complete, then verify that **both targets are Healthy**, as shown below.

![Verify that both targets are healthy](/images/myimage/5_4/5_4_5/image5.png)
