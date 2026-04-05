# AWS CI/CD Tools Breakdown (Simple DevOps Guide)

---

# 🧠 What is CI/CD?

👉 Simple meaning:
Code write karo → test karo → deploy karo → automatically repeat hota rahe

```
CI/CD = Automating software delivery pipeline
```

---

# 🧰 AWS CI/CD TOOLCHAIN (Step by Step)

---

# 📦 AWS CodeCommit – Code Storage

## 🧠 Meaning:

AWS ka Git repository service (like GitHub)

---

## 💡 Example:

* Tum apna Node.js code push karte ho
* Code safely AWS mein store ho jata hai

---

## ⚙️ DevOps Role:

* Single source of truth
* Pipeline ka starting point

---

# 🔁 AWS CodePipeline – Automation Engine

## 🧠 Meaning:

Pipeline ka boss / orchestrator

---

## 💡 Example Flow:

```
CodeCommit → CodeBuild → CodeDeploy → Elastic Beanstalk
```

---

## 🧠 Memory Hook:

CodePipeline = manager jo sab tools ko connect karta hai

---

# 🏗️ AWS CodeBuild – Build & Test

## 🧠 Meaning:

Code ko build aur test karta hai

---

## 💡 Example:

* npm install
* npm test
* Docker image build

---

## ⚙️ DevOps Role:

* Agar test fail → pipeline stop
* Quality gate enforce karta hai

---

# 🚀 AWS CodeDeploy – Deployment Service

## 🧠 Meaning:

Code ko real server (EC2) par deploy karta hai

---

## 💡 Example:

* EC2 instance update
* Application new version deploy

---

## ⚙️ Deployment Strategies:

* Rolling updates
* Blue/Green deployment

---

# 🧩 AWS CodeStar – All-in-One Dashboard

## 🧠 Meaning:

Complete project management UI

---

## 💡 Example:

* Git repository
* CI/CD pipeline
* Monitoring
  All in one place

---

# 📦 AWS CodeArtifact – Package Manager

## 🧠 Meaning:

Private package registry

---

## 💡 Example:

* npm packages
* Python libraries
* Maven dependencies

---

# 🤖 AWS CodeGuru – AI Code Review

## 🧠 Meaning:

Machine Learning based code reviewer

---

## 💡 Example:

* Memory leak detection
* Performance improvements suggestions

---

# 🧠 FINAL PIPELINE MODEL

```
CodeCommit → CodePipeline → CodeBuild → CodeDeploy → App
                    ↓
               CodeGuru (AI review)
```

---

# 📋 COPY BLOCK (Quick Revision)

```
CodeCommit = stores code (Git repo)
CodePipeline = automates workflow
CodeBuild = builds + tests code
CodeDeploy = deploys to servers
CodeArtifact = stores packages
CodeGuru = AI code review tool

CI/CD Flow:
Code → Build → Test → Deploy → Monitor
```

---

# 🧠 FINAL MENTAL MODEL

👉 CI/CD is not tools — it's a system

Tools are just parts of one machine:

* Store
* Build
* Test
* Deploy
* Improve

---

# 🚀 END OF NOTES
