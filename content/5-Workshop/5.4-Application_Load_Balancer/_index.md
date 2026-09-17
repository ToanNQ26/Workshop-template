---
title: "Configure an Application Load Balancer"
date: "2026-09-14"
weight: 4
chapter: false
pre: "<b> 5.4 </b>"
---

## Overview

In this chapter, we will configure an **Application Load Balancer (ALB)** to receive requests and route them to the comic website backend running on Amazon EC2. With multiple EC2 instances running the application, the ALB **distributes incoming traffic** and routes requests to healthy instances when an instance fails.

## Deployment Architecture

Users access the application through the **ALB DNS name** on port `80`. The ALB forwards requests to EC2 instances in a target group on port `80`. On each instance, Nginx acts as a reverse proxy, forwarding requests to the Node.js backend running at `127.0.0.1:8080` under PM2.

```text
User / Browser
        │ Sends an HTTP request to the ALB DNS name
        ▼
Application Load Balancer — HTTP:80 listener
        │ Applies a forwarding rule for the target group
        │ Selects an EC2 instance to handle the request
        ▼
EC2 — Nginx:80
        │ Forwards the request through the reverse proxy
        ▼
Node.js Backend — 127.0.0.1:8080
        │ Processes the request and returns a response
        ▼
Response → Nginx → ALB → User
```

The ALB uses **health checks** to determine which instances are ready to receive traffic. To continue serving requests if an instance fails, the target group needs at least **two EC2 instances running the same application**, with at least one remaining **Healthy**.

## Implementation Steps

1. [Create a Target Group](5.4.1-create_target_group/)
2. [Create an Application Load Balancer](5.4.2-create_application_load_balancer/)
3. [Test the Application Load Balancer](5.4.3-checkalb/)
4. [Launch a Second EC2 Instance](5.4.4-create_second_ec2/)
5. [Register the Second EC2 Instance](5.4.5-register_second_ec2/)
