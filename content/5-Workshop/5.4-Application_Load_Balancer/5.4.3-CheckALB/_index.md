---
title: "Test the Application Load Balancer"
date: "2026-09-14"
weight: 3
chapter: false
pre: "<b> 5.4.3 </b>"
---

## Overview

In this section, we will verify that the ALB can forward requests to the backend before launching a second EC2 instance. Testing at this stage makes it easier to isolate and resolve configuration issues before expanding the deployment.

## Implementation Steps

### Step 1: Copy the ALB DNS Name

- Open **Load Balancers** in the Amazon EC2 console.
- Select the load balancer you just created. In this example, it is named `webtruyentranh`.

![Select the load balancer](/images/myimage/5_4/5_4_3/image1.png)

- Copy the **DNS name** of the ALB.

![Copy the ALB DNS name](/images/myimage/5_4/5_4_3/image2.png)

### Step 2: Test an API Request Through the ALB

- Use **Postman** or **Chrome** to send a request to the API endpoint configured as the target group's health check path. Build the URL using `http://`, your ALB DNS name, and the endpoint path. For example:

```text
http://webtruyentranh-306793996.ap-southeast-1.elb.amazonaws.com/stories
```

Replace the example DNS name with your own. This example uses `/stories`, the health check path configured in section **5.4.1**.

![Review the configured health check path](/images/myimage/5_4/5_4_1/image4.png)

- If the endpoint accepts **GET** requests, paste the URL into Chrome's address bar. For endpoints that require another HTTP method, use Postman to send the appropriate request.
- Check that the API returns the expected response through the ALB.

![Verify the API response through the ALB](/images/myimage/5_4/5_4_3/image3.png)
