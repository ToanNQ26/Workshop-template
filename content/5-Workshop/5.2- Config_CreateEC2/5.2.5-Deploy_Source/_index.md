---
title: "Deploy the Source Code to EC2"
date: "2026-07-10"
weight: 5
chapter: false
pre: "<b> 5.2.5 </b>"
---

## Overview

Transfer the source code to EC2 and install the project dependencies.

## Procedure

### Step 1: Clone the Repository

On EC2, replace `YOUR_ACCOUNT` and `YOUR_REPOSITORY` with your repository details:

```bash
git clone https://github.com/YOUR_ACCOUNT/YOUR_REPOSITORY comic-website
cd comic-website
```

![Clone the repository](/images/myimage/5_2_5/image1.png)

> **Note:** If you do not have your own project, you can use my [Comic Website Project](https://github.com/ToanNQ26/AppTruyen_Be) to practice deploying an application to EC2.

### Step 2: Install Dependencies

```bash
npm install
```

`npm install` downloads the dependencies required by the project after you clone it from GitHub.

![Install dependencies](/images/myimage/5_2_5/image2.png)

### Step 3: Configure the Backend

Create a `.env` file in the backend directory using a text editor. Use the project's `.env.example` as a template for the required environment variables.

```bash
cd comic-website
nano .env
```

The backend must read these variables and load `.env`, for example through `dotenv`. If you use my project, follow the configuration shown below and replace the values with your own. Refer to `readme.md` for more information about the project.

![Configure the environment file](/images/myimage/5_2_5/image3.png)

Press `Ctrl+O`, then `Enter` to save the file, and `Ctrl+X` to exit.

## Expected Outcomes

The source code, dependencies, and backend configuration are ready for Nginx and PM2.

## References

[MongoDB Atlas: IP Access List](https://www.mongodb.com/docs/atlas/security/ip-access-list/)
