---
title : "Workshop"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

# A Detailed Guide to Building the Infrastructure for a Comic-Reading Website

#### Workshop Overview

The workshop is organized into five main chapters, from 5.1 to 5.5, with detailed hands-on exercises numbered 5.x.y as listed below:

> [!NOTE]
>
> * Website Demo: [Web Demo](https://webtruyenbyquoctoan.netlify.app/)
> * [Backend](https://github.com/ToanNQ26/AppTruyen_Be)
> * [Frontend](https://github.com/ToanNQ26/AppTruyen_Fe)

---

#### Workshop Chapters:

1. [5.1. Preparation](5.1-prepare/)

2. [5.2. Launching and Configuring an EC2 Server](5.2-config_createec2/)
   * [5.2.1. Launch an EC2 Instance](5.2-config_createec2/5.2.1-createec2/)
   * [5.2.2. Configure the Security Group](5.2-config_createec2/5.2.2-config_security_group/)
   * [5.2.3. Connect to EC2 via SSH](5.2-config_createec2/5.2.3-connect_ssh/)
   * [5.2.4. Set Up the Server Environment](5.2-config_createec2/5.2.4-setup_server/)
   * [5.2.5. Deploy the Source Code to EC2](5.2-config_createec2/5.2.5-deploy_source/)
   * [5.2.6. Install and Configure Nginx](5.2-config_createec2/5.2.6-configure_nginx/)
   * [5.2.7. Run and Manage the Application](5.2-config_createec2/5.2.7-run_application/)
   * [5.2.8. Configure an Elastic IP](5.2-config_createec2/5.2.8-configure_elastic_ip/)

3. [5.3. Configuring IAM and Monitoring PM2 Logs with CloudWatch](5.3-iam-couldwatch/)
   * [5.3.1. Create an IAM Role](5.3-iam-couldwatch/5.3.1-create_roleiam/)
   * [5.3.2. Attach the IAM Role to EC2](5.3-iam-couldwatch/5.3.2-attachiamrole/)
   * [5.3.3. Configure the CloudWatch Agent on EC2](5.3-iam-couldwatch/5.3.3-configurepm2logs/)

4. [5.4. Configuring an Application Load Balancer](5.4-application_load_balancer/)
   * [5.4.1. Create a Target Group](5.4-application_load_balancer/5.4.1-create_target_group/)
   * [5.4.2. Create an Application Load Balancer](5.4-application_load_balancer/5.4.2-create_application_load_balancer/)
   * [5.4.3. Test the ALB](5.4-application_load_balancer/5.4.3-checkalb/)
   * [5.4.4. Create a Second EC2 Server](5.4-application_load_balancer/5.4.4-create_second_ec2/)
   * [5.4.5. Register the Second EC2 Server with the Target Group](5.4-application_load_balancer/5.4.5-register_second_ec2/)

5. [5.5. Integrating S3](5.5-s3_backup/)
   * [5.5.1. Create an S3 Bucket for Backup Storage](5.5-s3_backup/5.5.1-create_s3/)
   * [5.5.2. Back Up Data Using MongoDB Compass](5.5-s3_backup/5.5.2-create_backup/)
   * [5.5.3. Upload Backup Files to Amazon S3](5.5-s3_backup/5.5.3-upload_to_s3/)
