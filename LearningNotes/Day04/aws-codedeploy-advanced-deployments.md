# AWS CodeDeploy – Advanced Deployments (In-Depth Guide)

---

## 1. CodeDeploy – In-Place Deployment (Deep Dive)

### 🔹 What is In-Place Deployment?

In In-Place deployment:
👉 Same EC2 instance pe hi new version install hota hai

Old version → overwrite → new version

### 🔹 Line-by-Line Breakdown

#### • Use EC2 Tags or ASG to identify instances

* **EC2 Tags** = labels (e.g., `env=prod`, `app=web`)
* **ASG (Auto Scaling Group)** = group of EC2 instances

👉 CodeDeploy ko batana hota hai:

> "Kin servers pe deployment karna hai?"

Isliye tum:

* Tags use karte ho (flexible)
* ya ASG use karte ho (dynamic scaling)

📌 Real Example:
Tumhare paas 10 EC2 hain:

* 5 prod
* 5 dev

Tum tag lagate ho:

* `env=prod`

👉 CodeDeploy sirf prod pe deploy karega

---

#### • With Load Balancer: traffic stop → update → start

Flow:

1. Load Balancer traffic bhej raha hota hai
2. Deployment start hoti hai
3. Instance temporarily LB se hata diya jata hai
4. New code install hota hai
5. Instance wapas LB me add hota hai

👉 Why?
Taake users broken app na dekhein

📌 Real Life Analogy:
Lift repair ho rahi hai:

* Pehle lift band karo
* Repair karo
* Phir log use karein

---

## 2. CodeDeploy Hooks (Lifecycle Events)

### 🔹 What is Hook?

Hook = script jo deployment ke specific stage pe run hota hai

👉 Basically automation points

---

## 3. Deployment Hooks – Deep Explanation

### 🔹 BeforeInstall

👉 Deployment se pehle run hota hai

Use cases:

* Old version ka backup lena
* Files decrypt karna

📌 Example:
Tumhara app encrypted hai → deploy se pehle decrypt karna zaroori

---

### 🔹 AfterInstall

👉 Code install hone ke baad

Use cases:

* Config files set karna
* Permissions change karna

📌 Example:
`chmod 755 app` run karna

---

### 🔹 ApplicationStart

👉 App start karna

Use case:

* Service restart (nginx, node app)

📌 Example:
`systemctl restart nginx`

---

### 🔹 ValidateService

👉 Final verification

Use case:

* Check app properly run ho raha hai ya nahi

📌 Example:

* API call test karna
* Health endpoint `/health` hit karna

👉 Fail → deployment rollback

---

### 🔹 BeforeAllowTraffic

👉 Traffic aane se pehle last check

Use case:

* Health checks run karna

📌 Real DevOps Move:
Agar app crash ho raha hai:
👉 deployment fail kar do BEFORE users see it

---

## 4. Blue/Green Deployment (Advanced Understanding)

### 🔹 Manual Mode

* Tum khud 2 environments banate ho:

  * Blue (old)
  * Green (new)

* Tags se identify karte ho

👉 Full control but manual effort

---

### 🔹 Automatic Mode

* CodeDeploy khud:

  * New ASG create karta hai
  * Settings copy karta hai

👉 Less effort, more automation

---

## 5. Blue-Green Instance Termination

### 🔹 Problem:

Deployment successful ho gaya… ab old servers ka kya?

---

### 🔹 Option 1: Terminate

* Blue instances delete ho jate hain
* Wait time configurable (default: 1 hour)

👉 Use when:

* Confident ho deployment pe

---

### 🔹 Option 2: Keep Alive

* Blue instances chalti rehti hain
* LB se hata di jati hain

👉 Use when:

* Safety chahiye
* Quick rollback option

📌 Real Life:
Old shop band nahi karte… bas customers new shop me bhejte ho

---

## 6. Deployment Configurations

### 🔹 What is this?

Define karta hai:
👉 Kitni instances ek time pe update hongi

---

### 🔹 Predefined Configs

#### • AllAtOnce

* Sab ek sath update
* Fast but risky

#### • HalfAtATime

* 50% instances
* Balanced

#### • OneAtATime

* 1 instance
* Safe but slow

---

### 🔹 Custom Config

👉 Tum apni strategy define kar sakte ho

Example:

* 20% instances at a time

---

## 7. CodeDeploy Triggers

### 🔹 What is this?

Events ko notify karna via SNS

---

### 🔹 Examples

* DeploymentSuccess
* DeploymentFailure
* InstanceFailure

📌 Real DevOps Flow:
Deployment fail → SNS → Email/Slack alert 🚨

---

## 8. CodeDeploy – ECS Deployment (Deep Dive)

### 🔹 What happens?

* New ECS Task Definition deploy hoti hai
* New container image use hoti hai

---

### 🔹 Important Points

* Sirf Blue/Green supported
* Load Balancer required
* Agent required nahi hota

---

### 🔹 AppSpec.yml Role

Define karta hai:

* Kaunsa task version
* Kaunsa load balancer

---

### 🔹 Traffic Shifting

* Linear → gradual
* Canary → test + full
* AllAtOnce → instant

---

### 🔹 Test Listener (Advanced)

👉 Ek extra ELB listener use hota hai

* Green version pe test traffic bhejte ho
* Validate karte ho
* Phir production traffic shift hoti hai

---

## 9. ECS Deployment Hooks

👉 Yahan hooks = Lambda functions

### 🔹 AfterAllowTestTraffic

* Test traffic ke baad run hota hai

📌 Example:

* Lambda health check kare
* Fail → rollback trigger

---

## 10. CodeDeploy – Lambda Deployment

### 🔹 What happens?

* New Lambda version create hota hai
* Traffic alias ke through shift hoti hai

---

### 🔹 Important

* Agent required nahi
* AppSpec.yml me versions define hotay hain

---

## 11. Lambda AppSpec.yml (Understanding)

* **Name** → Lambda function name
* **Alias** → traffic pointer
* **CurrentVersion** → current live version
* **TargetVersion** → new version

👉 CodeDeploy:
Traffic ko gradually version 1 → version 2 shift karta hai

---

## 12. Rollbacks & Redeployments

### 🔹 Rollback kya hai?

👉 Previous working version pe wapas jana

---

### 🔹 Types

#### • Automatic

* Deployment fail
* CloudWatch alarm trigger

#### • Manual

* Tum manually rollback karo

---

### 🔹 Important Insight

Rollback:
👉 Old version restore nahi hota
👉 New deployment hota hai (clean process)

---

## 13. Troubleshooting (Real DevOps Pain Points)

---

### 🔴 Error: InvalidSignatureException

👉 Reason:

* EC2 time mismatch

👉 Fix:

* NTP sync karo

---

### 🔴 Deployment Fail Reasons

* Agent installed nahi
* IAM permissions missing
* Proxy issue
* Time mismatch

---

### 🔴 Health Constraint Error

👉 Meaning:

* Enough healthy instances nahi hain

---

### 🔴 ASG Edge Case

👉 Scenario:

* Deployment chal rahi hai
* New instance create hoti hai

👉 Problem:

* New instance old version le leti hai

👉 Solution:

* CodeDeploy auto follow-up deployment run karta hai

---

### 🔴 Blue/Green Failure (Allow Traffic Issue)

👉 Reason:

* ELB health check galat configured

👉 Fix:

* Health check path, port, timeout verify karo

---

## 14. Final Mental Model

CodeDeploy = Deployment Brain 🧠

* Hooks = checkpoints
* LB = traffic controller
* ASG = scaling engine
* AppSpec = instruction file

👉 Sab milke safe deployment system banate hain

---
