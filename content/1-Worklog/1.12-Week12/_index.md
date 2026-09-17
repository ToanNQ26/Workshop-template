---
title: "Week 12 Worklog"
date: "2026-10-05"
weight: 12
chapter: false
pre: "<b> 1.12 </b>"
---


### Week 12 Objectives:

* Learn about Amazon Elastic IP and the use of static IP addresses for EC2 instances.
* Study the Security Group design between the Application Load Balancer and EC2 instances in a Target Group.
* Learn how IAM Roles grant EC2 access to AWS services without storing access keys on the server.
* Research Amazon CloudWatch Agent, CloudWatch Logs, Log Groups, and Log Streams for collecting logs from multiple EC2 instances.
* Learn about Amazon S3 data-protection features, including Block Public Access, encryption, Versioning, and Lifecycle Rules.
* Consolidate the required AWS services and prepare a phased infrastructure implementation plan for the project.

### Tasks to be completed this week:

| Day | Task | Start Date | Completion Date | Resources |
| --- | ---- | ---------- | --------------- | --------- |
| 2 | Learn how to allocate, associate, and release an Elastic IP for EC2 | 05/10/2026 | 05/10/2026 | https://docs.aws.amazon.com/AWSEC2/ |
| 3 | Study Security Groups for ALB and EC2 and restrict traffic between the components | 06/10/2026 | 06/10/2026 | https://docs.aws.amazon.com/elasticloadbalancing/ |
| 4 | Learn about IAM Roles, Instance Profiles, and least-privilege permissions for EC2 | 07/10/2026 | 07/10/2026 | https://docs.aws.amazon.com/IAM/ |
| 5 | Research the CloudWatch Agent and the organization of Log Groups and Log Streams for multiple EC2 instances | 08/10/2026 | 08/10/2026 | https://docs.aws.amazon.com/AmazonCloudWatch/ |
| 6 | Learn about Block Public Access, encryption, Versioning, and Lifecycle Rules in Amazon S3 | 09/10/2026 | 09/10/2026 | https://docs.aws.amazon.com/s3/ |
| 7 | Consolidate the findings and plan how to apply the AWS services during each project phase | 10/10/2026 | 10/10/2026 | https://docs.aws.amazon.com/ |

### Week 12 Achievements:

* Understood the purpose, association process, and cost considerations of using Elastic IP with EC2.
* Defined the Security Group rules required for the ALB to route requests to EC2 without exposing unnecessary ports.
* Understood how IAM Roles provide temporary credentials to EC2 and reduce the risks associated with long-term access keys.
* Learned how the CloudWatch Agent sends logs from multiple EC2 instances to CloudWatch Logs and separates their sources with Log Streams.
* Understood how Block Public Access, encryption, Versioning, and Lifecycle Rules protect and manage backup data in S3.
* Completed the AWS research notes and implementation plan for the following project weeks.
