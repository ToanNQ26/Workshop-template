---
title: "Preparation"
date: "2026-07-10"
weight: 1
chapter: false
pre: "<b> 5.1 </b>"
---


### Requirements

Before designing and deploying infrastructure for the **Comic Website on AWS**, prepare the necessary accounts, tools, source code, and development environment.

The preparation requirements are listed below:

---

### 1. AWS Account

An **AWS (Amazon Web Services) account** is required to create and manage the cloud resources used in this workshop.

During deployment, you will use your AWS account to work with services such as:

- **Amazon EC2**: Launch servers to deploy the application.
- **Amazon S3**: Store data and static assets when needed.
- **Amazon CloudWatch**: Monitor system activity.
- **AWS IAM**: Manage access permissions for AWS resources.
- Other AWS services added as the system is developed.

> **Note:** Avoid using the root account for routine deployment tasks. Use an IAM user or IAM role with appropriate permissions.

---

### 2. Complete Tasks to Receive AWS Credits (Optional)

As part of the internship program, complete the assigned tasks to receive **AWS Credits**.

AWS Credits help cover the costs of creating and operating AWS resources during the workshop.

Before deployment, check:

- Whether AWS Credits have been added to your account.
- Your available credit balance.
- The expiration date of the credits.
- Which services are eligible for credits.
- Your costs throughout the deployment process.

> **Recommendation:** Set up **AWS Budgets** and cost alerts to reduce the risk of unexpected AWS resource costs.

---

### 3. Existing Website Project

This workshop requires an **existing website project** to deploy on AWS infrastructure.

The project should include at least:

- A website frontend.
- A backend that provides REST APIs.
- A database or a database connection.
- An environment variable configuration file.
- Source code managed with Git.
- The ability to run successfully in a local environment before deployment to AWS.

The project used in this workshop is a **Comic Website**, consisting of a frontend, backend, and database.

If you do not have your own project, you can use the sample project provided below for practice:

**Project Source Code:**  
[Comic Website - GitHub](LINK_GITHUB_PROJECT_CUA_BAN)

> **Note:** Replace `LINK_GITHUB_PROJECT_CUA_BAN` with your project's GitHub URL before finalizing the report.

Before continuing, make sure the project runs correctly on your personal computer. This helps distinguish application errors from errors caused by AWS infrastructure configuration.

---

### 4. Google Chrome Browser

Install **Google Chrome** to access and manage the platforms used in this workshop, such as:

- AWS Management Console.
- MongoDB Atlas.
- GitHub.
- The deployed website.
- Other management and testing tools.

Use a recent version of Google Chrome to ensure compatibility with the AWS Management Console and modern web services.

---

### 5. Node.js (Skip This Step if You Already Have the Project Source Code)

Install **Node.js** on your personal computer to run and test the project before deployment.

You can check the Node.js version with:

```bash
node --version
```

Check the npm version:

```bash
npm --version
```

Node.js and npm are used to:

- Run the backend locally.
- Install the required packages.
- Build the project.
- Test the application before deployment.
- Identify and resolve errors during development.

> **Recommendation:** Use a Node.js LTS version or a version compatible with your project.

---

### 6. MongoDB Atlas Account

The system uses **MongoDB Atlas** as its database, so prepare a MongoDB Atlas account.

After registering an account, complete these basic steps:

1. Create a MongoDB project.
2. Create a database cluster.
3. Create a database user.
4. Configure Network Access.
5. Obtain the MongoDB connection string.
6. Add the connection string to the backend's environment variables.

Example:

```env
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>/<database>
```

> **Note:** Do not upload usernames, passwords, connection strings, or other sensitive information directly to GitHub.

If your project already has a MongoDB Atlas cluster, you can continue using it. Check the Network Access configuration before deploying the backend to AWS.

---

### 7. Personal Computer

Prepare a desktop computer or laptop with basic specifications to complete this workshop.

Suggested specifications:

| Component | Requirement |
|---|---|
| CPU | Intel Core i3 / AMD Ryzen 3 or equivalent or higher |
| RAM | At least 8 GB |
| Storage | At least 10 GB of free space |
| Operating system | Windows 10/11, Linux, or macOS |
| Internet | Stable internet connection |
| Browser | Google Chrome |
| Node.js | A version compatible with the project |

This workshop mainly involves deploying and operating resources on AWS, so your personal computer does not need particularly high specifications.

Your personal computer is mainly used to:

- Edit source code.
- Run the application locally.
- Access the AWS Management Console.
- Connect to the EC2 server through SSH.
- Manage source code.
- Test the system after deployment.

---

### 8. Supporting Tools

In addition to the main requirements, prepare tools to support development and deployment:

- **Visual Studio Code** or an equivalent IDE to edit source code.
- **Git** to manage source code versions.
- **GitHub** to host source code.
- **Postman** to test REST APIs.
- **PowerShell / Terminal** to run commands.
- **SSH Client** to connect to the EC2 server.

You can check Git with:

```bash
git --version
```

---

### 9. Expected Outcomes

After completing the preparation steps, ensure that:

- You have an AWS account and can access the AWS Management Console.
- You have completed the required tasks to receive AWS Credits.
- You have enough AWS Credits for the practical exercises.
- Your computer meets the basic specifications.
- Google Chrome is installed.
- Node.js and npm are installed.
- You have a MongoDB Atlas account.
- You have a database cluster for the project.
- You have Git and GitHub to manage source code.
- You have a website project to deploy.
- The project runs successfully in your local environment.
- You can use the provided sample project if you do not have your own.

> **Note:**  
> If you already have a complete project that runs reliably in your local environment, you can **skip installation and configuration steps for development tools and services that are already set up**, such as Node.js, npm, Git, GitHub, and MongoDB Atlas.  
>
> However, make sure the project works correctly before continuing with deployment to AWS.

After completing these requirements, proceed to the next step to begin **designing and deploying infrastructure for the Comic Website on AWS**.
