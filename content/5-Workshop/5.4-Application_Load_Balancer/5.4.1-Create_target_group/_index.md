---
title: "Create a Target Group"
date: "2026-09-14"
weight: 1
chapter: false
pre: "<b> 5.4.1 </b>"
---

## Overview

In this step, we will create a **target group** for the backend EC2 instance. The Application Load Balancer will use this target group to route requests to the application.

---

## Implementation Steps

### Step 1: Open Target Groups in the EC2 Console

Open the **Amazon EC2 console**. In the navigation pane, scroll down to **Load Balancing** and choose **Target Groups**.

![Open Target Groups in the EC2 console](/images/myimage/5_4/5_4_1/image1.png)

### Step 2: Configure the Target Group

Choose **Create target group**.

- Select **Instances** as the target type (the default), then enter a name for the target group.

![Select the target type and enter a target group name](/images/myimage/5_4/5_4_1/image2.png)

- Configure **Protocol**, **Port**, **IP address type**, **VPC**, and **Protocol version** as shown below.

![Configure the target group connection settings](/images/myimage/5_4/5_4_1/image3.png)

> **Note:** Select the same VPC as the EC2 instance you configured for the backend earlier.

- Set the **Health check path** to an API endpoint in your application, such as `/home`. If you are following along with the sample project, use the configuration shown below.

![Configure the health check path](/images/myimage/5_4/5_4_1/image4.png)

- Choose **Next** to continue.

### Step 3: Select the Backend EC2 Instance

- Select the EC2 instance you configured for the backend. If needed, return to the **Instances** page in the EC2 console to confirm which instance to use.

![Select the backend EC2 instance](/images/myimage/5_4/5_4_1/image5.png)

- Enter the port on which the instance will receive traffic, then choose **Include as pending below**. The instance should appear in the pending targets list, as shown below.

![Add the instance to the pending targets list](/images/myimage/5_4/5_4_1/image6.png)

- Continue to the final review step.

### Step 4: Review and Create the Target Group

- Verify that the settings match your intended configuration, then choose **Create target group**.

![Review and create the target group](/images/myimage/5_4/5_4_1/image7.png)
