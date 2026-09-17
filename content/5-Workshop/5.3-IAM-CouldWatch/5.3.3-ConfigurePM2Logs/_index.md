---
title: "Configure CloudWatch Agent for EC2"
date: "2026-09-10"
weight: 3
chapter: false
pre: "<b> 5.3.3 </b>"
---

## Overview

In this step, we will configure the EC2 server to send PM2 logs to CloudWatch.

---

## Implementation Steps

### Step 1: Connect to the EC2 Server Using SSH

Use SSH to connect to the server. If you need a reminder, refer to step 5.2.3.

- After connecting successfully, run the following command to obtain root privileges:

```bash
sudo -i
```

### Step 2: Configure Log Delivery for EC2

Follow the instructions below:

- Run `pm2 describe webtruyen_be` in the terminal connected to EC2 and note the **out log path** and **error log path** values.

![Configure log delivery for EC2](/images/myimage/5_3/5_3_3/image1.png)

- Run `sudo dnf install amazon-cloudwatch-agent -y` to install the agent on EC2. You can omit `sudo` if you followed step 1.

![Configure log delivery for EC2](/images/myimage/5_3/5_3_3/image2.png)

- Run `sudo nano /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json` to create the configuration file, then paste the following content into the file and save it:

```json
{
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/root/.pm2/logs/webtruyen-be-out.log",
            "log_group_name": "/webtruyen/backend",
            "log_stream_name": "{instance_id}/out"
          },
          {
            "file_path": "/root/.pm2/logs/webtruyen-be-error.log",
            "log_group_name": "/webtruyen/backend",
            "log_stream_name": "{instance_id}/error"
          }
        ]
      }
    }
  }
}
```

![Configure log delivery for EC2](/images/myimage/5_3/5_3_3/image3.png)

- Run `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -s -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json` to start the agent.

![Configure log delivery for EC2](/images/myimage/5_3/5_3_3/image4.png)

- Finally, run `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a status -m ec2` to check the status. If it shows `running`, the configuration is successful.

![Configure log delivery for EC2](/images/myimage/5_3/5_3_3/image5.png)

From now on, to view logs, go to **CloudWatch → Log Management → Select the log group you just created → View logs**.

![Result](/images/myimage/5_3/5_3_3/image6.png)
