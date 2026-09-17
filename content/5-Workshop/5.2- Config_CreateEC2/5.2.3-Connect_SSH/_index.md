---
title: "Connect to EC2 Using SSH"
date: "2026-07-10"
weight: 3
chapter: false
pre: "<b> 5.2.3 </b>"
---

## Overview

SSH (Secure Shell) provides encrypted remote access for administering EC2 from your local computer. Use OpenSSH and the private key downloaded in Section 5.2.1.

## Procedure

### Step 1: Check Connection Prerequisites

The instance must be **Running**, have passed its status checks, and have a public IPv4 address. Its security group must allow TCP port **22** from **My IP**. The subnet must route `0.0.0.0/0` to an internet gateway.

Select the instance in the EC2 console and copy its **Public IPv4 address**. Replace `PUBLIC_IP` in the commands with this address.

![Copy the public IPv4 address](/images/myimage/5_2_3/image1.png)

### Step 2: Prepare the SSH Client

On your local computer, open PowerShell or Terminal and run `ssh -V`. If SSH is unavailable on Windows, install **OpenSSH Client** through Optional features.

Store `WebServer-Key.pem` in a private folder. On Windows, restrict read access to your account through **Properties → Security → Advanced**. On Linux/macOS, run from the key directory:

```bash
chmod 400 WebServer-Key.pem
```

### Step 3: Connect to the Server

Run on your local computer from the key directory:

```bash
ssh -i "WebServer-Key.pem" ec2-user@PUBLIC_IP
```

`ec2-user` is the default username for Amazon Linux 2023. On the first connection, verify the instance's host key fingerprint before entering `yes`.

![Connect using SSH](/images/myimage/5_2_3/image2.png)

### Step 4: Verify the SSH Session

Run these commands **on EC2**:

```bash
whoami
cat /etc/os-release
pwd
```

Confirm the username is `ec2-user` and the operating system is Amazon Linux 2023. Run `exit` to close the session.

## Troubleshooting

| Error | What to check |
| --- | --- |
| Connection timed out | Public IP, SSH rule, routing, and network ACL. |
| Permission denied (publickey) | Username and private key matching the instance's key pair. |
| Unprotected private key file | Restrict access to the private key. |
| Host key verification failed | Verify the instance and fingerprint before updating the saved host entry. |

## Expected Outcomes

You have established an SSH session and can configure the server.

## References

[AWS: Connect to your Linux instance using SSH](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-to-linux-instance.html)


