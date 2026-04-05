# AWS CodeCommit Deep Understanding (Beginner Friendly Notes)

---

# 🧠 What is Version Control?

👉 Version control means:
Tracking changes in your code over time.

### 💡 Simple Meaning:

Your code has a history.

You can see:

* Who changed the code
* When it was changed
* What exactly was changed

---

# 🔄 Rollback Concept

👉 Rollback means:
Going back to a previous working version of your code.

### 💥 Why it matters:

If a bug breaks production:

* You can quickly restore the previous stable version

### 💡 Real DevOps example:

Production system breaks → rollback in minutes → system back online

---

# 🧰 Git in CodeCommit

👉 AWS CodeCommit uses Git internally.

### Meaning:

All Git commands work here:

* commit
* push
* pull
* branch

---

# ☁️ What is a Central Repository?

👉 Code is stored in two places:

* Local system (your laptop)
* Cloud (AWS CodeCommit)

### 💡 Why this is important:

* Backup of code
* Team collaboration
* No single point of failure

---

# 🎯 Benefits of CodeCommit

## 👥 Collaboration

Multiple developers can work on the same repository at the same time.

---

## 💾 Code Backup

If your laptop crashes:

* Your code is still safe in AWS

---

## 🔍 Auditing

You can track changes easily.

### 💡 Example:

Manager asks:

> “Who introduced this bug?”

Git history answers it clearly.

---

# 🔐 CodeCommit Features

## 🔒 Private Repositories

Your code is NOT public.
Only authorized users can access it.

---

## 📦 No Size Limit (Practically Scalable)

Large projects are supported easily.

---

## ⚙️ Fully Managed Service

No server setup required.
AWS manages everything.

---

## 🌍 High Availability

Service is highly reliable and rarely goes down.

---

## 🔐 AWS-Only Security

Access is controlled through AWS accounts only.

---

# 🔐 Security (VERY IMPORTANT)

## 👤 Authentication (Who are you?)

Used to verify identity.

### Methods:

* SSH Keys (secure login without password)
* HTTPS (username/password or IAM credentials)

---

## 🎯 Authorization (What can you do?)

Controlled using IAM policies:

* Read access
* Write access
* Admin access

---

## 🔒 Encryption

### At Rest:

Data stored in encrypted form using AWS KMS

### In Transit:

Data is encrypted using HTTPS or SSH

---

## 🔄 Cross-Account Access

One AWS account accessing another account’s repository.

### Solution:

* IAM Role
* AWS STS (AssumeRole)

---

## ⚠️ Security Warning

Never share:

* SSH keys ❌
* AWS access keys ❌

### 💥 Why?

Leak = full system compromise

---
## 📁 File Name

```
aws-codecommit-deep-understanding.md
```
# 🧠 FINAL MENTAL MODEL

Remember this pipeline like a flow:

```
Developer → CodeCommit → CodePipeline → CodeBuild → CodeDeploy → EC2/App
```

### Simple version:

Write → Store → Build → Test → Deploy → Run

---

# 📋 COPY BLOCK (Quick Revision)

```
Version Control = Track code changes over time
Rollback = Go back to previous version
CodeCommit = Git-based AWS repository

Security:
- Authentication = Who you are
- Authorization = What you can do
- Encryption = Data protection

Pipeline Flow:
Developer → CodeCommit → CodePipeline → CodeBuild → CodeDeploy → App
```

---

# 🚀 END OF NOTES
