# AWS CodeDeploy – Complete Guide

## 1. What is AWS CodeDeploy?

AWS CodeDeploy ek fully managed deployment service hai jo applications ko automatically deploy karta hai.

Yeh tumhare code ko:

* EC2 instances
* On-premises servers
* AWS Lambda
* Amazon ECS

par safely aur efficiently deploy karta hai.

---

## 2. Why do we use CodeDeploy?

Manual deployment:

* Slow hoti hai
* Errors ka risk high hota hai
* Downtime create karti hai

CodeDeploy:

* Automation laata hai
* Downtime reduce karta hai
* Safe rollback provide karta hai

---

## 3. Core Concept

CodeDeploy ka main kaam hai:
👉 "New version of app ko safely production tak pohanchana"

---

## 4. Key Features

### 🔹 Automated Deployment

Application automatically deploy hoti hai without manual intervention.

### 🔹 Multiple Platform Support

* EC2 / On-prem
* Lambda
* ECS

### 🔹 Automated Rollback

Agar deployment fail ho jaye:

* Automatically previous version pe wapas aa jata hai
* CloudWatch alarms se trigger ho sakta hai

### 🔹 Gradual Deployment (Traffic Control)

Traffic ko slowly shift kiya jata hai taake risk kam ho.

### 🔹 AppSpec File

`appspec.yml` define karta hai:

* Kaunsa file kaha jayega
* Kaunsa script kab run hoga

---

## 5. CodeDeploy – EC2 / On-Premises

### Deployment Types

#### 🔹 In-Place Deployment

* Same server pe update hota hai
* Simple but risky (downtime possible)

#### 🔹 Blue/Green Deployment

* Naya environment (Green) create hota hai
* Traffic shift hoti hai
* Zero/low downtime

---

### Deployment Strategies

* **AllAtOnce**

  * Sab instances ek sath update
  * Fast but downtime high

* **HalfAtATime**

  * 50% instances update
  * Balanced approach

* **OneAtATime**

  * Ek ek karke update
  * Safe but slow

* **Custom**

  * Tum apni % define kar sakte ho

---

## 6. CodeDeploy Agent

Agent ek software hai jo target servers pe run karta hai.

### Requirements:

* EC2 pe install hona zaroori
* S3 se deployment bundle download karta hai
* IAM permissions honi chahiye

### Tip:

AWS Systems Manager se auto-install bhi kar sakte ho.

---

## 7. CodeDeploy – Lambda Deployments

Lambda mein CodeDeploy:
👉 Traffic shifting manage karta hai (versions ke beech)

### Strategies:

#### 🔹 Linear Deployment

* Har X minutes mein traffic increase hota hai
* Example:

  * 10% → 20% → 30% → ... → 100%

#### 🔹 Canary Deployment

* Pehle small traffic (e.g., 10%)
* Phir full 100%

#### 🔹 AllAtOnce

* Direct full traffic switch

---

## 8. CodeDeploy – ECS Deployments

ECS mein:

* New Task Definition deploy hoti hai
* Sirf **Blue/Green deployments** supported hain

### Strategies:

#### 🔹 Linear

Gradual traffic increase

#### 🔹 Canary

Small test → full rollout

#### 🔹 AllAtOnce

Instant switch

---

## 9. How CodeDeploy Works (Step-by-Step)

1. Developer code push karta hai (GitHub / S3)
2. CodeDeploy trigger hota hai
3. Deployment group identify hota hai
4. AppSpec file read hoti hai
5. Code instances pe deploy hota hai
6. Health checks run hoti hain
7. Success → continue
8. Failure → rollback

---

## 10. Real-World DevOps Example

### Scenario:

Tumhari company ka Node.js app EC2 pe run ho raha hai.

### Flow:

1. Developer GitHub pe code push karta hai
2. CodePipeline trigger hoti hai
3. CodeBuild app build karta hai
4. CodeDeploy:

   * New version EC2 pe deploy karta hai
   * Blue/Green deployment use hota hai
   * Traffic gradually shift hoti hai

👉 Result: Zero downtime deployment 🚀

---

## 11. Real-Life Analogy

Socho tum ek restaurant upgrade kar rahe ho:

* Old kitchen = Blue
* New kitchen = Green

Tum:

* Pehle new kitchen ready karte ho
* Thoda customers wahan bhejte ho
* Sab theek ho to full shift

👉 Yeh hi Blue/Green deployment hai

---

## 12. Interview Points (High Value)

* CodeDeploy supports EC2, Lambda, ECS
* Uses `appspec.yml`
* Requires agent for EC2 deployments
* Supports Blue/Green & In-place deployments
* Automated rollback with CloudWatch
* Traffic shifting strategies: Linear, Canary, AllAtOnce

---

## 13. Pro Tips (Senior Level Insight)

* Always use Blue/Green in production
* Combine with CodePipeline for full CI/CD
* Monitor using CloudWatch
* Use IAM roles properly (common interview trap)
* Never deploy directly without rollback strategy

---

## 14. Summary

AWS CodeDeploy ek powerful deployment service hai jo:

* Automation provide karta hai
* Downtime reduce karta hai
* Safe deployment enable karta hai

👉 DevOps pipeline ka critical part hai

