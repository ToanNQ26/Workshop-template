---
title: "Proposal"
date: "2026-09-16"
weight: 2
chapter: false
pre: "<b> 2. </b>"
---

# Building a Load-Balanced AWS Infrastructure for Web Truyện Tranh

## 1. Project Overview

**Web Truyện Tranh** is an online comic-reading platform with a React frontend, a Node.js/Express backend, MongoDB Atlas as its database, and Cloudinary for storing and delivering comic images.

This proposal focuses on building the backend infrastructure on Amazon Web Services to improve availability, distribute traffic, centralize monitoring, and protect backup data.

The Node.js/Express backend is deployed on **two Amazon EC2 instances**. On each instance, **PM2** manages the application at `127.0.0.1:8080`, while **Nginx** receives requests on port 80 and forwards them to the backend as a reverse proxy.

An **Application Load Balancer (ALB)** provides a common backend entry point and distributes user requests to healthy EC2 instances in a **Target Group**. Periodic health checks ensure that the ALB routes traffic only to targets marked `Healthy`.

An **Elastic IP** is attached to the primary server to provide a stable address for administration and direct testing. **AWS IAM** grants EC2 access to required AWS services without storing access keys on the servers.

**Amazon CloudWatch** collects and centralizes application logs from both EC2 instances for monitoring and troubleshooting. **Amazon S3** stores MongoDB backups, adding a data-protection layer independent of the live database.

The frontend remains on Netlify, primary data remains in MongoDB Atlas, and comic images remain in Cloudinary. Reusing these stable components keeps the project focused on backend infrastructure and reduces the risks of migrating the entire system at once.

### Project Objectives

The project aims to build a stable AWS backend infrastructure that distributes traffic across multiple servers and maintains service when one server fails.

- Deploy the Node.js/Express backend on two Amazon EC2 instances.
- Use an ALB as a common entry point and distribute requests between the instances.
- Use a Target Group and health checks to route traffic only to healthy servers.
- Centralize application logs in CloudWatch for monitoring and troubleshooting.
- Use IAM Roles so EC2 can access services without locally stored access keys.
- Store MongoDB backups in S3 to support data recovery.
- Retain Netlify, MongoDB Atlas, and Cloudinary to reduce the migration scope.
- Establish a foundation for adding HTTPS, Route 53, and Auto Scaling later.

---

## 2. Problem Statement

### 2.1. Current State

The system already has a frontend, backend, database, and image-storage service. However, running the backend on one server creates a single point of failure. Requests are not distributed, logs are scattered, and backups are not managed in an independent repository.

The infrastructure must:

- Keep the backend available when one server fails.
- Distribute traffic across multiple servers.
- Maintain a stable administrative IP for the primary server.
- Route requests only to healthy servers.
- Manage AWS permissions securely according to least privilege.
- Collect logs centrally for troubleshooting.
- Store MongoDB backups outside the operational database.

### 2.2. Problems, Solutions, and Benefits

| Problem | Service or solution | Rationale and benefit |
|---|---|---|
| One backend server creates a single point of failure and limits capacity | **Two Amazon EC2 instances** | EC2 provides control over the OS, Node.js, PM2, and Nginx. Two instances maintain service during one-instance failures and enable horizontal scaling. |
| Public IPv4 may change after stopping and restarting EC2 | **Elastic IP** | Provides a static address for administration, SSH, and direct testing. It does not replace the ALB's public endpoint. |
| No common traffic entry point or distribution mechanism | **Application Load Balancer** | Accepts HTTP on port 80, distributes requests to healthy EC2 instances, and provides one DNS name. |
| Unhealthy servers must be removed from traffic | **Target Group** | Registers both instances, performs health checks, and exposes only `Healthy` targets to the ALB. |
| Access keys should not be stored on EC2 | **AWS IAM Role** | Supplies temporary credentials, restricts permissions, and reduces secret-exposure risk. |
| PM2 logs are isolated on each instance | **Amazon CloudWatch** | Sends output/error logs to a shared Log Group, separated by instance ID, avoiding the need to SSH into each server. |
| An independent MongoDB Atlas backup is required | **Amazon S3** | Offers high durability, encryption, versioning, and lifecycle policies for JSON exports or `mongodump` archives. |
| Node.js should not be directly exposed to the Internet | **Nginx and Security Groups** | Nginx forwards port 80 traffic to `127.0.0.1:8080`; Security Groups restrict sources and keep port 8080 private. |

### 2.3. Overall Benefits

- Reduces reliance on a single backend server.
- Automatically distributes requests among healthy EC2 instances.
- Centralizes logs and simplifies incident detection.
- Avoids long-term credentials on servers.
- Provides an independent backup for recovery.
- Retains Netlify, Cloudinary, and MongoDB Atlas, reducing the scope of change.

---

## 3. Solution Architecture

### 3.1. Overall Architecture Diagram

![Architecture diagram](/images/myimage/sodo1.png)

### 3.2. Architecture Components

| Component | Main configuration | Role |
|---|---|---|
| Amazon EC2 | Two Amazon Linux 2023 instances in different Availability Zones | Runs Node.js/Express, PM2, and Nginx |
| Elastic IP | Attached to the primary EC2 instance | Stable IP for administration and direct testing |
| Application Load Balancer | Internet-facing, HTTP:80 listener | Common entry point and request distribution |
| Target Group (in ALB) | Instances, HTTP:80, HTTP1 | Manages both EC2 instances and health checks |
| IAM Role | Attached to EC2, least privilege | Grants CloudWatch and S3 access without local access keys |
| Amazon CloudWatch | Log Group `/webtruyen/backend` | Stores output/error logs by instance ID |
| Amazon S3 | Private bucket, Block Public Access | Stores MongoDB backups and applies lifecycle policies |
| MongoDB Atlas | Shared database | Stores primary application data |
| Netlify | Existing frontend platform | Delivers the React application, provider proxy for dns alb |
| Cloudinary | Existing image service | Stores and delivers comic images |

### 3.3. Request Flow

1. The frontend sends an API request to the ALB DNS name.
2. The ALB's HTTP:80 listener forwards it to the `webtruyentranh` Target Group.
3. The Target Group selects one of the two `Healthy` EC2 instances.
4. Nginx receives the request on port 80 and proxies it to Node.js at `127.0.0.1:8080`.
5. The backend processes the request and accesses MongoDB Atlas or Cloudinary as needed.
6. The response returns to the user through Nginx and the ALB.

### 3.4. Health Checks and Failure Handling

The Target Group performs HTTP health checks against `/stories` on port 80. A successful response marks the target as `Healthy`.

If an EC2 instance repeatedly fails health checks, the ALB stops sending requests to it and continues serving traffic through the remaining healthy target.

### 3.5. Logging and Backup Flow

- The CloudWatch Agent reads PM2 logs on each EC2 instance and sends them to `/webtruyen/backend`.
- Log streams use the instance ID and log type (`out` or `error`) to identify their source.
- MongoDB data is periodically exported as JSON or a `mongodump` archive and uploaded to S3.
- Backups must be test-restored periodically; uploading them without testing recovery does not prove that the backup process works.

---

## 4. Technical Implementation

### 4.1. EC2, PM2, and Nginx

- Launch Amazon Linux 2023 EC2 instances in the ALB's VPC.
- Install Node.js, npm, PM2, and Nginx.
- Deploy the backend and configure environment variables.
- Run Node.js on port 8080 with PM2.
- Configure Nginx on port 80 to proxy to `http://127.0.0.1:8080`.
- Save the PM2 configuration so the application starts with the operating system.

### 4.2. Elastic IP and Security Groups

- Allocate an Elastic IP and attach it to the primary EC2 instance.
- Allow Internet HTTP:80 traffic in the ALB Security Group.
- Allow HTTP:80 from the ALB Security Group in the EC2 Security Group.
- Restrict SSH:22 to required administrative IP addresses.
- Do not expose port 8080 to the Internet.

### 4.3. Target Group and ALB

- Create an `Instances` Target Group using `HTTP:80` and `HTTP1`.
- Set the health check protocol to `HTTP` and path to `/stories`.
- Create an `Internet-facing` ALB across at least two subnets in two Availability Zones.
- Create an `HTTP:80` listener whose default action forwards to `webtruyentranh`.
- Verify that the ALB DNS name returns a successful response.

### 4.4. Second EC2 Instance

- Create an AMI from the validated EC2 configuration.
- Launch a second EC2 instance from the AMI in another Availability Zone.
- Verify environment variables, PM2, Nginx, and MongoDB Atlas connectivity.
- Register both instances with the Target Group on port 80 and wait until both are `Healthy`.
- Do not keep sessions or business files only on local disks if the instances must be interchangeable.

### 4.5. IAM and CloudWatch

- Create an IAM Role with EC2 as its trusted entity.
- Attach `CloudWatchAgentServerPolicy`.
- If EC2 uploads backups to S3, add a dedicated policy allowing only necessary operations on the correct bucket and prefix.
- Attach the role to both EC2 instances; do not create long-term access keys on them.
- Install CloudWatch Agent and specify the actual PM2 log paths.
- Use Log Group `/webtruyen/backend` and stream names `{instance_id}/out` and `{instance_id}/error`.
- Load the configuration, confirm the agent is `running`, generate test requests, and verify the resulting logs.

### 4.6. S3 Data Backup

- Create a private S3 bucket and enable Block Public Access.
- Enable default object encryption.
- Organize objects by date, for example `mongodb-backups/2026-09-16/`.
- Export data with MongoDB Compass or `mongodump` and upload it to S3.
- Configure a Lifecycle Rule for older backups.
- Perform a test restore in a testing environment.

### 4.7. Acceptance Testing

- The ALB DNS name returns HTTP 200.
- Both targets have a `Healthy` status.
- Stopping the backend on one instance does not interrupt the system.
- Logs from both instances appear in CloudWatch.
- A backup downloaded from S3 is successfully test-restored.
- Port 8080 is not directly accessible from the Internet.

---

## 5. Implementation Roadmap and Milestones

The project is expected to take **at least eight weeks, equivalent to approximately two months or 40 working days**, from the agreed start date. This roadmap covers AWS infrastructure deployment for the existing backend. These milestones are estimates rather than confirmation of completed work; exact dates will be updated when the schedule is finalized.

| Phase | Week 1 | Week 2 | Week 3 | Week 4 | Week 5 | Week 6 | Week 7 | Week 8 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1. Assessment and design | ● | ● | | | | | | |
| 2. Base EC2 deployment | | ● | ● | | | | | |
| 3. Load balancer configuration | | | ● | ● | | | | |
| 4. Add the second EC2 instance | | | | ● | | | | |
| 5. Permissions and monitoring | | | | | ● | | | |
| 6. Data backup setup | | | | | ● | ● | | |
| 7. Restore testing | | | | | | ● | | |
| 8. Testing, optimization, and technical acceptance | | | | | | ● | ● | |
| 9. Documentation and handover | ● | ● | ● | ● | ● | ● | ● | ● |

**Legend:** ● indicates an active week. Documentation and deployment evidence are updated throughout. The final week is reserved for handover, retesting, and resolving outstanding issues.

---

## 6. Estimated Budget

Actual costs depend on instance types, operating hours, log and backup volumes, and network traffic.

| Item | Cost basis | Cost-control measure |
|---|---|---|
| Amazon EC2 | Two instances multiplied by operating hours | Select small instances appropriate for the workload; stop non-continuous practice environments when unused |
| EBS and AMI snapshots | Monthly volume and snapshot storage | Delete experimental AMIs and snapshots when no longer required |
| Elastic IP/Public IPv4 | Number of addresses and usage duration | Retain only necessary addresses and release unused ones |
| Application Load Balancer | Operating hours and Load Balancer Capacity Units | Monitor traffic; ALB may be a significant expense for a small system |
| Amazon CloudWatch | Log ingestion, storage, and queries | Set a retention period instead of `Never expire` when permanent retention is unnecessary |
| Amazon S3 | Storage, requests, and retrieval | Use Lifecycle Rules and avoid duplicate backups |
| Data transfer | Internet egress and cross-region traffic | Keep AWS resources in the same Region where possible |
| MongoDB Atlas, Netlify, Cloudinary | Existing plans | No migration cost within this proposal's scope |

For an accurate figure, enter the actual configuration in AWS Pricing Calculator using the Singapore Region, selected EC2 types, operating hours, and expected usage. An AWS Budget and cost alerts should also be configured.

---

## 7. Risk Assessment

| Risk | Impact | Mitigation |
|---|---|---|
| Both instances are created from a faulty configuration | High | Test the AMI before replication, manage versions, and prepare rollback |
| Health check returns HTTP 200 while critical functionality fails | High | Build a dedicated `/health` endpoint; use `/stories` only for initial testing |
| MongoDB Atlas rejects a new EC2 connection | High | Update Network Access carefully without allowing a broader range than required |
| Sessions or local files are not synchronized | High | Use stateless sessions or shared storage |
| Ports 80, 22, or 8080 are exposed too broadly | High | Expose ALB port 80; allow EC2 port 80 only from the ALB; restrict SSH by IP; keep 8080 private |
| IAM Role permissions are excessive | High | Separate policies by task, restrict bucket/prefix, and review permissions periodically |
| Rapid log growth creates costs | Medium | Set retention and remove unnecessary logs |
| S3 backups become public or cannot be restored | High | Enable Block Public Access, encryption, least privilege, and test restores |
| Unused resources continue generating costs | Medium | Apply tags, create an AWS Budget, and remove experimental resources |
| EC2 replacement is not automated | Medium | Add a Launch Template and Auto Scaling Group later |
| HTTP leaves data in transit unencrypted | High | Add a domain, AWS Certificate Manager, and an HTTPS:443 listener before production |

---

## 8. Expected Results

- The backend runs on two EC2 instances, reducing dependence on one server.
- Users access the API through one ALB DNS name.
- Requests go only to targets with a `Healthy` status.
- The ALB stops sending traffic to failed targets.
- Node.js listens internally at `127.0.0.1:8080`.
- Nginx receives port 80 traffic and forwards it to the application.
- Each instance's output and error logs are centralized in CloudWatch.
- EC2 accesses CloudWatch and S3 through an IAM Role rather than local access keys.
- MongoDB backups are stored in a private S3 bucket.
- A tested recovery procedure is available.
- The architecture can later support HTTPS, Auto Scaling, Route 53, and automated deployment.

Minimum acceptance criteria:

- Both targets are `Healthy`.
- The endpoint through the ALB returns HTTP 200.
- The system remains available when one backend is stopped.
- Both instances' logs appear in CloudWatch.
- An S3 backup is successfully test-restored.
- Port 8080 cannot be reached directly from the Internet.

---

## Conclusion

The solution uses **Amazon EC2, Elastic IP, Application Load Balancer, Target Group, AWS IAM, Amazon CloudWatch, and Amazon S3** to provide load distribution, centralized monitoring, and backups for the Web Truyện Tranh backend.

The design retains Netlify, MongoDB Atlas, and Cloudinary to reuse stable components. It addresses the backend's single point of failure, unstable administrative address, missing load balancing and health checks, permission management, scattered logs, and data backups.

- Amazon EC2 runs the backend.
- Elastic IP provides a stable administrative address.
- Application Load Balancer receives and distributes requests.
- Target Group manages EC2 instances and health checks.
- AWS IAM controls service permissions.
- Amazon CloudWatch centralizes logs and monitoring.
- Amazon S3 stores MongoDB backups.

This foundation can be extended with HTTPS, Route 53, and an Auto Scaling Group when the system moves into production.
