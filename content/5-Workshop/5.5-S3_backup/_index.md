---
title: "Integrate Amazon S3 for Data Backups"
date: "2026-09-14"
weight: 5
chapter: false
pre: "<b> 5.5 </b>"
---

## Overview

In this section, we will use **Amazon S3** as a central location for storing application data backups. Keeping a copy of the data separate from the live database provides a source of data for recovery when needed.

The workflow consists of three steps: create an **S3 bucket**, export data from MongoDB collections using **MongoDB Compass**, and upload the exported files to S3. Together, these steps establish a manual data backup workflow for the workshop deployment.

---

## Deployment Architecture

The backup architecture consists of three main components: the **MongoDB database**, a **local computer running MongoDB Compass**, and **Amazon S3**. Data is exported from MongoDB to the local computer, then uploaded to S3 for storage separate from the database serving the application.

The backup data flow is:

```text
MongoDB Database
        │ Read data from each collection
        ▼
MongoDB Compass on the Local Computer
        │ Export Data — export the full collection
        ▼
Data Files Stored Locally
        │ Upload through the AWS Management Console
        ▼
Amazon S3 Bucket
        └ Store backup files as objects
```

In this workshop, the process is **performed manually**: export data from each collection you want to back up, then upload the resulting files to the bucket you created. When needed, you can download the files from S3 to your computer for use in importing the data back into MongoDB.

## Implementation Steps

1. [Create an S3 Bucket for Backups](5.5.1-create_s3/)
2. [Back Up Data with MongoDB Compass](5.5.2-create_backup/)
3. [Upload Backup Files to Amazon S3](5.5.3-upload_to_s3/)
