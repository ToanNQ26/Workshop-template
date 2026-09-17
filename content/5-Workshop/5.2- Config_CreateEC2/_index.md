---
title: "EC2 Configuration and Instance Creation"
date: "2026-07-10"
weight: 2
chapter: false
pre: "<b> 5.2 </b>"
---

## Overview

In this chapter, we will perform **initialization and configuration of Amazon EC2 instances** to deploy the Project Website to the AWS environment.

Amazon EC2 (Elastic Compute Cloud) is a service that provides virtual servers on the AWS platform. EC2 will be used as the primary compute server to run the application and handle user requests over the Internet.

During the deployment process, we will execute the following key tasks:

- Launch an **EC2 Instance**.
- Configure a **Security Group** to control inbound and outbound network traffic to the server.
- Connect to the EC2 instance via **SSH**.
- Install necessary tools and runtime environments to execute the Project.
- Deploy the Project's Source Code to the EC2 instance.
- Install and configure **Nginx** as the Web Server/Reverse Proxy.
- Launch the Project on the EC2 instance.
- Configure an **Elastic IP** to maintain a static public IPv4 address for the server.
- Verify website accessibility from the Internet.

---

## Deployment Architecture

In this model, **Amazon EC2** serves as the application server. Users can send requests from the Internet to the server using a Public IP address.

**Security Group** functions as a virtual firewall layer to control which connections are permitted to access the EC2 instance, such as:

- **SSH (Port 22):** Used for remote server administration.
- **HTTP (Port 80):** Allows users to access the Website using the HTTP protocol.
- **HTTPS (Port 443):** Used when the Website is configured with SSL/TLS certificates.

Additionally, we will use **Elastic IP** to associate a static public IPv4 address with the EC2 Instance. This ensures that the server's IP address remains constant even after the Instance is stopped and restarted.

---

## Implementation Steps

The EC2 server configuration and deployment process is organized into the following steps:

1. [Launch EC2 Instance](5.2.1-createec2/)
2. [Configure Security Group](5.2.2-config_security_group/)
3. [Establish SSH Connection to EC2](5.2.3-connect_ssh/)
4. [Set Up Server Environment](5.2.4-setup_server/)
5. [Deploy Source Code to EC2](5.2.5-deploy_source/)
6. [Install and Configure Nginx](5.2.6-configure_nginx/)
7. [Launch Project on EC2](5.2.7-run_application/)
8. [Configure Elastic IP](5.2.8-configure_elastic_ip/)

> **Note:** The names and paths of the sections above may be modified according to the directory structure of your report project.

