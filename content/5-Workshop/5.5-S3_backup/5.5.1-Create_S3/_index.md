---
title: "Create an S3 Bucket"
date: "2026-09-14"
weight: 1
chapter: false
pre: "<b> 5.5.1 </b>"
---

## Overview

In this step, we will create an **S3 bucket** to store MongoDB data backup files. A bucket is a container for storing and managing files in Amazon S3, providing a dedicated location where backups can be accessed and used later.

Once created, the bucket will be ready to receive the data files generated in the next step.

---

## Implementation Steps

### Step 1: Open Amazon S3

- On the AWS Management Console home page, enter `S3` in the search bar and choose **S3** to open the service console.

![Open Amazon S3 from the console search bar](/images/myimage/5_5/5_5_1/image1.png)

### Step 2: Create a Bucket

- In the S3 console, choose **Create bucket**.

![Open the bucket creation page](/images/myimage/5_5/5_5_1/image2.png)

- Enter a bucket name and leave the remaining settings at their defaults.

![Enter the bucket name](/images/myimage/5_5/5_5_1/image3.png)

- Scroll down and choose **Create bucket**.

![Create the S3 bucket](/images/myimage/5_5/5_5_1/image4.png)
