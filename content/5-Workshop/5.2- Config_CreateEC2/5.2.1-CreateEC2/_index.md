---
title: "Launch an EC2 Instance"
date: "2026-07-10"
weight: 1
chapter: false
pre: "<b> 5.2.1 </b>"
---

## Overview

In this section, you will launch an **Amazon EC2 instance** to host the website application.

Amazon EC2 (Elastic Compute Cloud) provides virtual servers on AWS. Once the instance is available, you can connect to it, set up the runtime environment, and deploy the application's source code.

---

## Procedure

### Step 1: Open the EC2 Console

- Sign in to the **AWS Management Console**.
- Enter `EC2` in the search bar.
- Select **EC2** from the search results.

![Open the EC2 console](/images/myimage/5_2/01-ec2-service.png)

---

### Step 2: Start the Instance Launch Wizard

In the **Amazon EC2** console:

- Select **Instances** in the left navigation pane.
- Choose **Launch instances** to begin configuring a new instance.

![Choose Launch instances](/images/myimage/5_2/02-ec2-service.png)

---

### Step 3: Name the Instance

Under **Name and tags**, enter a name for the EC2 instance.

For example:

`WebServer`

An instance name makes it easier to identify and manage the server, especially when your AWS account contains multiple EC2 instances.

![Name the EC2 instance](/images/myimage/5_2/03-ec2-service.png)

---

### Step 4: Select an Amazon Machine Image (AMI)

Under **Application and OS Images (Amazon Machine Image)**, select the operating system image for the instance.

For this project, use:

- **Amazon Linux**
- **Amazon Linux 2023 AMI**
- **Architecture:** 64-bit (x86)

Amazon Linux is an operating system provided by AWS and optimized for workloads running on AWS.

![Select the Amazon Linux AMI](/images/myimage/5_2/04-ec2-service.png)

---

### Step 5: Select an Instance Type

Under **Instance type**, select the compute configuration for the instance.

For this project, choose:

`t3.micro`

The instance type determines the compute resources available to the server, including CPU and memory, and its performance characteristics.

For a workshop website with light traffic, this configuration is suitable for deploying and testing the application while keeping AWS costs low.

![Select the instance type](/images/myimage/5_2/05-ec2-service.png)

---

### Step 6: Create a Key Pair

A **key pair** is used to authenticate SSH connections from your local computer to the EC2 instance.

Under **Key pair (login)**:

- Choose **Create new key pair**.

![Choose Create new key pair](/images/myimage/5_2/06-ec2-service.png)

Configure the key pair as follows:

- **Key pair name:** `WebServer-Key`
- **Key pair type:** RSA
- **Private key file format:** `.pem`

Choose **Create key pair**.

The `.pem` private key file will be downloaded to your computer.

> **Note:** Store the `.pem` private key securely. You will need it to authenticate SSH connections to the instance. Do not share the private key or commit it to GitHub or a public repository.

---

### Step 7: Configure Network Settings

Under **Network settings**, configure the instance's basic networking options.

You can use the following settings:

- **VPC:** Default VPC.
- **Subnet:** No preference.
- **Auto-assign Public IP:** Enable.

![Configure network settings](/images/myimage/5_2/07-ec2-service.png)

Enabling **Auto-assign Public IP** assigns a public IPv4 address to the instance so you can connect to the server over the internet.

Under **Firewall**, you can create a new **security group**.

For now, configure the basic settings needed to launch the instance. You will configure the security group in detail in the next section.

---

### Step 8: Configure Storage

Under **Configure storage**, specify the instance's storage capacity.

For example:

- **Volumes:** 1
- **Size:** 8 GiB
- **Volume type:** gp3

![Configure storage](/images/myimage/5_2/08-ec2-service.png)

Adjust the storage capacity to meet your project's requirements.

For a small website project, this capacity may be sufficient for the runtime environment, dependencies, and application source code.

---

### Step 9: Review the Configuration and Launch the Instance

Review your configuration before launching the instance, using the **Summary** panel and the settings you selected:

![Review the instance configuration](/images/myimage/5_2/09-ec2-service.png)

- Instance name.
- Amazon Machine Image (AMI).
- Instance type.
- Key pair.
- Network settings.
- Security group.
- Storage.

Once you have confirmed the settings, choose **Launch instance**.

![Launch the EC2 instance](/images/myimage/5_2/10-ec2-service.png)

---

### Step 10: Check the Instance State

After the launch request completes:

- Select **Instances** in the left navigation pane.
- Locate the instance you just launched.
- Check its instance state and status checks.

![EC2 instance list](/images/myimage/5_2/11-ec2-service.png)

Wait until the instance shows:

- **Instance state:** Running.
- **Status check:** 3/3 checks passed, as shown in the workshop example.

The instance is now ready to use.

---

### Step 11: Review the Instance Details

Select the instance to view its details.

Key information includes:

- **Instance ID:** The unique identifier of the EC2 instance.
- **Instance state:** The instance's current lifecycle state.
- **Instance type:** The instance's compute configuration.
- **Public IPv4 address:** The instance's public IP address.
- **Private IPv4 address:** The IP address used within the VPC.
- **Public IPv4 DNS:** The instance's public DNS hostname.
- **Availability Zone:** The Availability Zone where the instance is running.

![EC2 instance details](/images/myimage/5_2/12-ec2-service.png)

> **Note:** An automatically assigned public IPv4 address can change when you stop and then start the instance. In a later step, you will associate an **Elastic IP address** with the instance to provide a static public IPv4 address.

---

## Expected Outcomes

After completing this section, you will have:

- Launched an **Amazon EC2 instance**.
- Selected **Amazon Linux** as the instance's operating system.
- Created a **key pair** for SSH authentication.
- Configured basic networking and storage.
- Confirmed that the instance is in the **Running** state.
- Prepared the server for further configuration and application deployment.

In the next section, you will configure the **security group** to control inbound and outbound traffic for the EC2 instance.

