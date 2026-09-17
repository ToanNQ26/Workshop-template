---
title: "Configure the Security Group"
date: "2026-07-10"
weight: 2
chapter: false
pre: "<b> 5.2.2 </b>"
---

## Overview

After launching the EC2 instance, configure its **security group** to control inbound and outbound traffic.

A security group acts as a **virtual firewall** for an EC2 instance. Its rules specify which incoming and outgoing traffic is allowed.

For this project, you will configure the security group to:

- Allow **SSH** access for instance administration.
- Allow users to access the website over **HTTP**.
- Allow users to access the website over **HTTPS** once SSL/TLS is configured.
- Restrict the source IP addresses allowed to access each port.

---

## Procedure

### Step 1: Select the EC2 Instance

In the **AWS Management Console**:

- Open the **EC2** console.
- Select **Instances**.
- Select the instance launched in the previous section, then scroll down to the details pane shown below.

![Select the EC2 instance](/images/myimage/5_2-2/image1.png)

---

### Step 2: Identify the Associated Security Group

In the instance details pane:

- Select the **Security** tab.
- Locate **Security groups**.
- Select the security group associated with the instance.

![Identify the security group](/images/myimage/5_2-2/image2.png)

The associated security group contains the rules that control inbound and outbound traffic for the instance. Configure these rules as described below to support this project's requirements.

---

### Step 3: Edit the Inbound Rules

Open the security group details:

- Select the security group shown in Step 2, such as `launch-wizard-4`.
- If the console displays the security group list, select its **Security group ID**. The example below uses `sg-0505ab841db0cbd9f`.

Inbound rules specify which incoming connections are allowed to reach the EC2 instance.

![Inbound rules](/images/myimage/5_2-2/image3.png)

To modify these rules, choose **Edit inbound rules**.

![Edit inbound rules](/images/myimage/5_2-2/image4.png)

### Step 4: Allow SSH Access

First, add a rule to allow SSH connections to the instance.

- Choose **Add rule**.

Configure the rule as follows:

| Type | Protocol | Port range | Source |
| --- | --- | --- | --- |
| SSH | TCP | 22 | My IP |

![Configure the SSH rule](/images/myimage/5_2-2/image5.png)

SSH uses port **22** to provide remote access for administering the instance from your local computer.

For **Source**, select:

`My IP`

The console automatically detects the current public IP address of the computer accessing the AWS Management Console.

> **Note:** Avoid setting the SSH source to `0.0.0.0/0` unless required. This permits connection attempts to port 22 from any IPv4 address on the internet.

---

### Step 5: Allow HTTP Traffic

Add an HTTP rule to allow users to access the website from their browsers.

Use the following settings:

| Type | Protocol | Port range | Source |
| --- | --- | --- | --- |
| HTTP | TCP | 80 | Anywhere IPv4 |

![Configure the HTTP rule](/images/myimage/5_2-2/image6.png)

Port **80** is the default port for HTTP.

For **Source**, select:

`Anywhere IPv4`

This corresponds to the CIDR block:

`0.0.0.0/0`

The rule allows incoming HTTP traffic from any IPv4 address, enabling internet users to access the website running on the EC2 instance.

---

### Step 6: Allow HTTPS Traffic

If the website uses SSL/TLS, allow incoming HTTPS connections.

Add the following rule:

| Type | Protocol | Port range | Source |
| --- | --- | --- | --- |
| HTTPS | TCP | 443 | Anywhere IPv4 |

![Configure the HTTPS rule](/images/myimage/5_2-2/image7.png)

Port **443** is the default port for HTTPS.

HTTPS encrypts traffic between the user's browser and the web server, protecting data in transit.

> **Note:** If the project does not yet use HTTPS, you can add this rule later when configuring the domain and SSL/TLS.

---

### Step 7: Review and Save the Inbound Rules

After adding the required rules, the security group should include the following, as shown below:

| Type | Protocol | Port | Source | Purpose |
| --- | --- | --- | --- | --- |
| SSH | TCP | 22 | My IP | Remote server administration |
| HTTP | TCP | 80 | 0.0.0.0/0 | Website access over HTTP |
| HTTPS | TCP | 443 | 0.0.0.0/0 | Website access over HTTPS |

![Review the inbound rules](/images/myimage/5_2-2/image8.png)

Review the configuration, then choose **Save rules** to apply the changes.

---

## Configure Outbound Rules

### Step 8: Review the Outbound Rules

To review or modify the outbound rules:

- Select the **Outbound rules** tab.
- Choose **Edit outbound rules**.

![Outbound rules](/images/myimage/5_2-2/image9.png)

Outbound rules control traffic initiated by the EC2 instance to other destinations.

By default, a security group typically includes the following rule:

| Type | Protocol | Port range | Destination |
| --- | --- | --- | --- |
| All traffic | All | All | 0.0.0.0/0 |

This rule allows the EC2 instance to connect to the internet.

For this project, you can retain the default outbound rule.

---

## Verify the Security Group

### Step 9: Verify the Applied Configuration

After completing the configuration, return to the EC2 instance:

- Select the instance.
- Open the **Security** tab.
- Review the security group you configured.

![Verify the configured security group](/images/myimage/5_2-2/image10.png)

Confirm that all required inbound rules have been added successfully.

---

## Security Considerations

Security groups are an important part of protecting EC2 instances.

When configuring a security group:

- Allow access only to the ports required by the application.
- Avoid exposing SSH port `22` to the entire internet unless required.
- Restrict SSH access to the administrator's public IP address.
- Do not expose database ports directly to the internet unless public access is required.
- Ports `80` and `443` can accept traffic from the internet when the instance hosts a public website.
- Review the rules regularly and remove those that are no longer needed.

> **Note:** Restricting ports and source IP addresses reduces the server's attack surface and limits unwanted access from the internet.

---

## Expected Outcomes

After completing this section, you will have:

- Identified the security group associated with the EC2 instance.
- Allowed SSH connections on port **22**.
- Allowed HTTP traffic on port **80**.
- Allowed HTTPS traffic on port **443**.
- Reviewed the instance's outbound rules.
- Restricted SSH access to the administrator's public IP address.
- Configured the instance's basic network access controls.

The EC2 instance is now ready for SSH access and server environment setup.

