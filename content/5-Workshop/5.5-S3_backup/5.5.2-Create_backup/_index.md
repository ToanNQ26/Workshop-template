---
title: "Back Up Data with MongoDB Compass"
date: "2026-09-14"
weight: 2
chapter: false
pre: "<b> 5.5.2 </b>"
---

## Overview

In this step, we will use **MongoDB Compass** to export all data from individual **collections** in the application database and save it as files on the local computer. Repeat the process for each collection you want to back up to prepare the files for upload to Amazon S3.

This exercise focuses on **backing up data with the Export Data feature** in MongoDB Compass. The exported files will be uploaded to S3 in the next section.

---

## Implementation Steps

### Step 1: Connect to the Database and Export Data with MongoDB Compass

- Open **MongoDB Compass** and connect to the database.

![Connect to the database using MongoDB Compass](/images/myimage/5_5/5_5_2/image1.png)

- Select the collection you want to back up, then choose **Export Data → Export the full collection**.

![Export all data from the selected collection](/images/myimage/5_5/5_5_2/image2.png)

- Repeat the export process until you have saved the data from all collections you want to back up.
