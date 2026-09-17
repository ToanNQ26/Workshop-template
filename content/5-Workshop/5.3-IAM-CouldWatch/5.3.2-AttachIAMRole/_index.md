---
title: "Attach an IAM Role to EC2"
date: "2026-09-10"
weight: 2
chapter: false
pre: "<b> 5.3.2 </b>"
---

## Overview

In this step, we will configure the EC2 server to send logs to CloudWatch and attach the role created earlier to grant the server permission to send logs.

---

## Implementation Steps

### Step 1: Access the EC2 Instance

Access your EC2 instance. If you need a reminder, refer to the steps in section 5.2. Once you have opened the EC2 instance:

- At the top right of the instance page, select **Actions → Security → Modify IAM role**.

![Attach a role to EC2](/images/myimage/5_3/5_3_2/image1.png)

- On the **Modify IAM role** page, select the role created earlier in the **IAM role** field.

![Attach a role to EC2](/images/myimage/5_3/5_3_2/image2.png)

Finally, click **Update IAM role**.
