---
title: "Upload Backup Files to Amazon S3"
date: "2026-09-14"
weight: 3
chapter: false
pre: "<b> 5.5.3 </b>"
---

## Overview

In this step, we will upload the data files exported from **MongoDB Compass** to the **S3 bucket** created earlier. This transfers the backup files from the local computer to a central storage location in Amazon S3, where they can be accessed and downloaded when needed.

Once uploaded, the backup files will be stored as **objects** in the bucket, completing the workshop's data backup and storage workflow.

---

## Implementation Steps

### Step 1: Open the S3 Bucket

- Open the **Amazon S3 console** and select the bucket you created earlier.

![Select the bucket created for backups](/images/myimage/5_5/5_5_3/image1.png)

### Step 2: Upload the Backup Files

- Choose **Upload** in the center of the page, as shown below.

![Open the S3 upload page](/images/myimage/5_5/5_5_3/image2.png)

- Drag the folder containing your backup files into the S3 upload page.

![Add the folder containing the backup files](/images/myimage/5_5/5_5_3/image3.png)

- Choose **Upload** to upload the files to the bucket.

![Upload the backup files to S3](/images/myimage/5_5/5_5_3/image4.png)
