---
title: "Configure IAM and Monitor PM2 Logs with CloudWatch"
date: "2026-09-14"
weight: 3
chapter: false
pre: "<b> 5.3 </b>"
---

## Overview

In this chapter, we will **configure IAM and Amazon CloudWatch Logs** to collect and monitor logs from the backend running under **PM2 on Amazon EC2**.

Amazon CloudWatch Logs provides log storage and search on AWS. It helps us inspect backend activity, find error messages, and troubleshoot issues without opening an SSH session each time we need to view logs.

During deployment, we will perform the following tasks:

- Create an **IAM role** that allows EC2 to send logs to CloudWatch.
- Attach the IAM role to the **EC2 instance** running the backend.
- Install and configure **Amazon CloudWatch Agent** on EC2.
- Collect standard output and error logs from the **PM2** process.
- Verify and search logs in **CloudWatch Logs**.

---

## Deployment Architecture

In this model, **Amazon EC2** continues to host the backend. **PM2** manages the application process and writes standard output (`stdout`) and error output (`stderr`) to files on the server.

**Amazon CloudWatch Agent** runs on EC2, reads the PM2 log files, and sends their contents to **CloudWatch Logs**. File paths must match the user running PM2.

An **IAM role** attached to EC2 allows CloudWatch Agent to send logs using temporary credentials. Each component has the following role:

- **EC2 instance:** Hosts the backend and stores application log files.
- **PM2:** Manages the backend process and writes stdout and stderr logs.
- **IAM role:** Grants the AWS permissions required by CloudWatch Agent.
- **CloudWatch Agent:** Collects local logs and sends them to CloudWatch Logs.
- **CloudWatch Logs:** Centralizes logs in log groups and log streams for monitoring, searching, and troubleshooting.

The application log collection flow is:

```text
Backend → PM2 → Log files on EC2 → CloudWatch Agent → CloudWatch Logs
                                        ↑
                                  EC2 IAM role
```

Logs are organized in a backend **log group**, with **log streams** identifying the instance and output type. EC2 requires HTTPS connectivity to CloudWatch Logs in the selected Region to deliver data.

---

## Implementation Steps

The process of configuring IAM and collecting PM2 logs on EC2 consists of the following steps:

1. [Create an IAM Role](5.3.1-create_roleiam/)
2. [Attach an IAM Role to EC2](5.3.2-attachiamrole/)
3. [Configure CloudWatch Agent for EC2](5.3.3-configurepm2logs/)
