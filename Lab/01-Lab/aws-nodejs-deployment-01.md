# AWS First Deployment Journey – Node.js App (Beginner Friendly Guide)

## 🧠 Overview

This guide explains step-by-step how a simple Node.js application was deployed on AWS using:

* AWS Elastic Beanstalk
* EC2 instances (managed by Beanstalk)
* AWS CodePipeline
* GitHub integration
* IAM permissions fix

This is written in very simple English so anyone can follow and deploy the same app.

---

# 🚀 Step 1: Create AWS Account

### What I did:

* Created a new AWS account
* Set up billing information
* Configured account preferences

### Why this is important:

AWS needs billing + identity setup before using any services.

---

# 👤 Step 2: Create IAM User (Access Setup)

### Steps:

1. Go to AWS Console
2. Search: **IAM**
3. Click **Users → Create user**
4. Enter username
5. Enable **Programmatic access (if needed)**
6. Attach policies:

   * AdministratorAccess (for learning purpose)

### Result:

You now have a user with permissions to manage AWS services.

---

# 🌐 Step 3: Deploy First Node.js App using Elastic Beanstalk

### Steps:

1. Go to AWS Console
2. Search: **Elastic Beanstalk**
3. Click **Create Application**
4. Enter:

   * Application name: `node-app`
5. Select platform:

   * Node.js
6. Click **Create environment**

---

## 🖥️ Step 3.1: Create Environment

You created two environments:

* **Dev Environment** → for testing
* **Prod Environment** → for production

### AWS automatically created:

* EC2 instance
* Security groups
* Load balancer

---

# ⚙️ Step 4: Deploy Code to Elastic Beanstalk

### Steps:

1. Zip your Node.js app
2. Upload it in Elastic Beanstalk
3. Click **Deploy**

### Result:

Your app becomes live on AWS URL.

---

# 🔗 Step 5: Setup CI/CD using AWS CodePipeline

### Steps:

1. Search: **CodePipeline**
2. Click **Create pipeline**
3. Pipeline name: `nodejs-pipeline`
4. Source provider:

   * GitHub
5. Connect GitHub account
6. Select repository (Node.js app)

---

# 🏗️ Step 6: Build Pipeline Stages

Pipeline includes:

### 1. Source Stage

* Pulls code from GitHub

### 2. Build Stage

* Builds application

### 3. Deploy Stage

* Deploys to Elastic Beanstalk / EC2

---

# ❌ Issue Faced (Important Learning)

### Problem:

Pipeline failed with permission error:

> “Pipeline does not have access to create EC2 instance”

---

# 🔐 Step 7: Fix IAM Permission Issue

### Solution:

1. Go to IAM
2. Open pipeline service role
3. Attach permission:

   * EC2FullAccess
   * ElasticBeanstalkFullAccess

### Result:

Pipeline got permission to create and manage resources.

---

# ✅ Step 8: Successful Deployment

After fixing permissions:

* Pipeline ran successfully
* EC2 instance was created
* Node.js app deployed
* Application became live

---

# 🧠 Final Outcome

You successfully built your first full DevOps workflow:

```
GitHub → CodePipeline → Elastic Beanstalk → EC2 → Live App
```

---

# 📌 Key Learning

* AWS services work together like a system
* IAM permissions are critical (most common failure point)
* Elastic Beanstalk simplifies EC2 management
* CodePipeline automates deployment flow

---

**End of Notes 🚀**
