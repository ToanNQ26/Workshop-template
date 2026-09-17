---
title: "Create an IAM Role"
date: "2026-09-10"
weight: 1
chapter: false
pre: "<b> 5.3.1 </b>"
---

## Overview

In this step, we will create an IAM role for EC2 to grant it permission to send logs to CloudWatch.

---

## Implementation Steps

### Step 1: Access the IAM Service

From your AWS Management Console home page, follow these steps:

- Enter "IAM" in the search bar at the top left.

![Access the IAM service](/images/myimage/5_3/5_3_1/image1.png)

- Click **IAM**, then select **Roles**.

![Create a role](/images/myimage/5_3/5_3_1/image2.png)

### Step 2: Create a Role for EC2

On the current page, click **Create role** at the top right of the screen.

- Select the entity and use case, then click **Next**.

![Create a role](/images/myimage/5_3/5_3_1/image3.png)

- Select the permissions policy, then click **Next**.

![Create a role](/images/myimage/5_3/5_3_1/image4.png)

- Enter a name, complete the configuration, scroll down, and click **Create role**.

![Create a role](/images/myimage/5_3/5_3_1/image5.png)
