# AWS CodeBuild – Complete Guide (Clean Notes)

---

## 🔹 What is AWS CodeBuild?

AWS CodeBuild ek **fully managed build service** hai jo automatically:

* Source code leta hai
* Build karta hai
* Test karta hai
* Artifacts generate karta hai

👉 Tumhe servers manage nahi karne padte (no EC2 setup needed)

---

## 🔹 Supported Source Providers

CodeBuild multiple sources se code le sakta hai:

* AWS CodeCommit
* Amazon S3
* GitHub
* Bitbucket

---

## 🔹 Build Instructions (buildspec.yml)

Build ka pura process define hota hai:

* `buildspec.yml` file (recommended)
* ya manually AWS Console mein

👉 Best practice: always use **buildspec.yml (Infrastructure as Code mindset)**

---

## 🔹 Logs & Monitoring

### Logs Store:

* Amazon S3
* CloudWatch Logs

### Monitoring Tools:

* **CloudWatch Metrics**
  → Build success/failure track karna

* **EventBridge**
  → Failed builds detect karke automation trigger

* **CloudWatch Alarms**
  → Threshold-based alerts (e.g. 5 failures in 10 min)

---

## 🔹 CodeBuild Projects

Build project define karta hai:

* Source
* Environment
* Build instructions
* Output

👉 Ye project standalone bhi ho sakta hai
👉 Ya CodePipeline ke andar integrate bhi ho sakta hai

---

## 🔹 Supported Environments

CodeBuild multiple runtimes support karta hai:

* Java
* Python
* Node.js
* Ruby
* Go
* PHP
* .NET Core
* Android

### 🔸 Special Case: Docker

* Custom Docker image use kar sakte ho
* Apna environment fully control kar sakte ho

👉 Enterprise setups mein mostly custom Docker images use hote hain

---

## 🔹 How CodeBuild Works (Flow)

### Step-by-Step:

1. Source code fetch hota hai (GitHub / S3 / CodeCommit)
2. CodeBuild ek **temporary container** launch karta hai
3. `buildspec.yml` ke commands execute hote hain
4. Logs CloudWatch mein store hoti hain
5. Output (artifacts) S3 mein save hota hai
6. Optional: cache reuse hota hai (faster builds)

---

## 🔹 Key Components

* **Container**
  → Har build isolated environment mein run hota hai

* **Docker Image**
  → Prebuilt ya custom environment

* **Artifacts**
  → Final output (e.g. .jar, .zip)

* **Cache (S3)**
  → Dependencies store karke next builds fast banata hai

---

## 🔹 buildspec.yml (Deep Dive)

```yaml
version: 0.2

env:
  variables:
    JAVA_HOME: "/usr/lib/jvm/java-8-openjdk-amd64"

  parameter-store:
    LOGIN_PASSWORD: /CodeBuild/dockerLoginPassword

phases:
  install:
    commands:
      - echo "Entered install phase"
      - apt-get update -y
      - apt-get install -y maven

  pre_build:
    commands:
      - echo "Entered pre_build phase"
      - docker login -u User -p $LOGIN_PASSWORD

  build:
    commands:
      - echo "Entered build phase"
      - echo "Build started on $(date)"
      - mvn install

  post_build:
    commands:
      - echo "Entered post_build phase"
      - echo "Build completed on $(date)"

artifacts:
  files:
    - target/messageUtil-1.0.jar

cache:
  paths:
    - "/root/.m2/**/*"
```

---

## 🔍 Explanation (Senior-Level Breakdown)

### 🔸 version

* buildspec format version

---

### 🔸 env

* **variables**
  → Plain text variables

* **parameter-store**
  → Secure values from AWS SSM

* **secrets-manager**
  → Highly sensitive secrets

👉 NEVER hardcode passwords

---

### 🔸 phases

#### install

* Dependencies install hoti hain
  👉 Example: Maven, Node modules

---

#### pre_build

* Build se pehle setup
  👉 Example: Docker login

---

#### build

* Actual build process
  👉 Example: `mvn install`, `npm build`

---

#### post_build

* Final tasks
  👉 Example: packaging, notifications

---

### 🔸 artifacts

* Output files jo S3 mein upload hongi
  👉 Example: `.jar`, `.zip`

---

### 🔸 cache

* Dependencies cache hoti hain
  👉 Next build faster hota hai

---

⚠️ Important:

* `buildspec.yml` **root directory mein hona chahiye**

---

## 🔹 CodeBuild Inside VPC

### Default Behavior:

* CodeBuild container VPC ke bahar run hota hai
* Internal resources access nahi kar sakta

---

### VPC Configuration:

Agar tumhe internal access chahiye:

* VPC ID
* Subnet IDs
* Security Group IDs

---

### After Configuration:

CodeBuild access kar sakta hai:

* RDS (database)
* ElastiCache
* EC2 private services
* Internal Load Balancer

---

## 🔹 Real Use Cases

* Integration testing (DB ke sath)
* Internal APIs test karna
* Private services access
* Data processing inside VPC

---

## 🧠 Real-World Flow (Simple)

1. Developer pushes code
2. CodePipeline trigger hota hai
3. CodeBuild run hota hai
4. App build + test hoti hai
5. Artifact S3 mein store hota hai
6. Next stage: deploy

---

## 🎯 Summary

* CodeBuild = build engine
* buildspec.yml = brain of build
* Docker = environment control
* S3 = artifact storage
* CloudWatch = logs + monitoring
* VPC = secure internal access

---

  CodeBuild ek “serverless build machine” hai jo auto-scale karta hai aur DevOps ko simplify karta hai.
