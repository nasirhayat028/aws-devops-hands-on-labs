# 🚀 AWS CI/CD Lab: CodeBuild + CodePipeline

## 🎯 Objective
Build an automated CI/CD pipeline using AWS CodeBuild and CodePipeline that triggers builds/tests on every GitHub commit.

---

## 🧱 Phase 1: AWS CodeBuild Setup

### 1. Create CodeBuild Project
- Open AWS Console → CodeBuild
- Click **Create project**

---

### 2. Source Configuration
- Source Provider: GitHub
- Connect GitHub account to AWS
- Select your repository
- Enable:
  - Rebuild every time code is pushed

---

### 3. Environment Setup
- Operating System: Ubuntu
- Runtime: Standard
- Image:
  aws/codebuild/standard:7.0

---

### 4. Service Role
- Create new role:
  CodeBuildDemoServiceRole

---

### 5. Additional Settings (Optional)
- Timeout settings
- VPC configuration (if needed)
- Logs (CloudWatch)

---

### 6. Build Specification
Select:
- Use buildspec file

⚠️ IMPORTANT:
Your repo must include this file in root:

buildspec.yml

---

### Example buildspec.yml

```yml
version: 0.2

phases:
  install:
    runtime-versions:
      nodejs: 18
  build:
    commands:
      - echo "Installing dependencies"
      - npm install
      - npm run build

artifacts:
  files:
    - '**/*'
```

---

### 7. Trigger Behavior
- Every GitHub push automatically triggers build

---

## 🧱 Phase 2: CodePipeline Setup

### 1. Disable Auto Build in CodeBuild
- Uncheck:
  Rebuild every code change

(We shift control to CodePipeline)

---

### 2. Create Pipeline
- Go to AWS CodePipeline → Create Pipeline

---

## 🟦 Stage 1: Source
- Provider: GitHub
- Select repo + branch (main/master)

---

## 🟨 Stage 2: Test (CodeBuild)

- Action Name: CodeBuildTest
- Provider: AWS CodeBuild
- Region: same as pipeline
- Project: myFirstBuild
- Build Type: Single build
- Output Artifact: OutputOfTest

---

## 🟥 Stage 3: Deploy (Optional)
Can be added later:
- Elastic Beanstalk
- EC2 deployment
- S3 static hosting

---

## ⚠️ Issue Faced

Pipeline failed multiple times due to missing IAM permissions.

### Fix:
Attach this policy to pipeline role:

AWSCodeBuildDeveloperAccess

---

## 🧠 Key Learnings

- CodeBuild = build + test engine
- CodePipeline = orchestration layer
- GitHub = source trigger
- IAM roles are critical for permissions
- buildspec.yml controls build lifecycle

---

## 🚀 Final Flow

GitHub Push
   ↓
CodePipeline
   ↓
CodeBuild (Test/Build)
   ↓
Deploy 