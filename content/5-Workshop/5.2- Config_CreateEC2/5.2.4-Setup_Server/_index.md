---
title: "Set Up the Server Environment"
date: "2026-07-10"
weight: 4
chapter: false
pre: "<b> 5.2.4 </b>"
---

## Overview

Install Git, Node.js, npm, and PM2 on Amazon Linux 2023. Run all commands **on EC2 through SSH**.

## Procedure

### Step 1: Update the System and Install Git

```bash
sudo dnf upgrade -y
sudo dnf install -y git
git --version
```

If the update requires a reboot, run `sudo reboot`, wait for the instance to become ready, and reconnect.

### Step 2: Install Node.js and npm

This example uses Node.js 24. Check `engines` in `package.json` and the project documentation for compatibility.

```bash
sudo dnf install -y nodejs24 nodejs24-npm
node -v
npm -v
```

If multiple versions are installed, use `sudo alternatives --config node` to select the default and check again. MongoDB Server is unnecessary on EC2 because the project uses MongoDB Atlas.

### Step 3: Install PM2

Install PM2 globally to make the `pm2` command available on the server:

```bash
sudo npm install -g pm2
pm2 -v
```

`-g` installs the package globally; `sudo` allows writing to the system installation directory. After installation, run application management commands as `ec2-user`, as described in [Section 5.2.7 – Run and Manage the Application](../5.2.7-run_application/).

After completing the installation, check the installed versions:

```bash
node -v
pm2 -v
git -v
```

## Expected Outcomes

Git, Node.js, npm, and PM2 are ready.

## References

[AWS: Node.js in Amazon Linux 2023](https://docs.aws.amazon.com/linux/al2023/ug/nodejs.html)




