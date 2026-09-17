---
title: "Associate an Elastic IP Address"
date: "2026-07-10"
weight: 8
chapter: false
pre: "<b> 5.2.8 </b>"
---

## Overview

An Elastic IP address is a static public IPv4 address allocated to your AWS account. Associate it with EC2 to keep the website's address stable across instance stop/start cycles.

## Procedure

### Step 1: Allocate an Elastic IP Address

In the EC2 console, select the instance's Region:

1. Open **Network & Security → Elastic IPs**.

   ![Open Elastic IPs](/images/myimage/5_2_8/image1.png)

2. Choose **Allocate Elastic IP address**.

   ![Allocate an Elastic IP address](/images/myimage/5_2_8/image1.png)

3. Keep the default settings shown below.

   ![Default allocation settings](/images/myimage/5_2_8/image2.png)

4. Choose **Allocate**.

   ![Confirm allocation](/images/myimage/5_2_8/image2.png)

### Step 2: Associate the Address with EC2

1. Select the newly allocated Elastic IP address.

   ![Select the Elastic IP address](/images/myimage/5_2_8/image3.png)

2. Choose **Actions → Associate Elastic IP address**.
3. Select **Resource type: Instance**.
4. Select `WebServer` and the private IP of its primary network interface.
5. Choose **Associate**.

   ![Select the EC2 instance for association](/images/myimage/5_2_8/image4.png)

The previous automatically assigned public IPv4 address is replaced. An SSH session using the old address may disconnect; reconnect using the new one.

### Step 3: Verify Access

Open `http://ELASTIC_IP/` and test the API. An Elastic IP address does not configure HTTPS or change security group rules.

![Verify API access](/images/myimage/5_2_8/image5.png)

## Costs and Resource Management

AWS charges for public IPv4 addresses, including associated and unassociated Elastic IP addresses. **Disassociate** does not mean **Release**. At the end of the workshop, release the address only when the website and DNS no longer depend on it.

## Expected Outcomes

The EC2 instance has a static public IPv4 address.

## References

[AWS: Elastic IP addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)
