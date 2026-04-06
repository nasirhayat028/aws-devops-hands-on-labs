# 🚀 AWS CodeBuild – Advanced Concepts (Environment, Security, Badges, Triggers, Test Reports)

## 🎯 Objective
Understand advanced AWS CodeBuild features including environment variables, security model, build badges, triggers, and test reporting.

---

## 🌍 1. CodeBuild – Environment Variables

### 🔹 Default Environment Variables (AWS Managed)
These are automatically provided by AWS CodeBuild.

Examples:
- AWS_DEFAULT_REGION
- CODEBUILD_BUILD_ARN
- CODEBUILD_BUILD_ID
- CODEBUILD_BUILD_IMAGE

👉 You don’t define these manually — AWS injects them at runtime.

---

### 🔹 Custom Environment Variables

These are defined by the developer.

#### 1. Static Variables
- Defined at build time
- Can be overridden using `start-build` API

Example:
```
ENVIRONMENT = Production
```

---

#### 2. Dynamic Variables

Fetched from secure AWS services:

- SSM Parameter Store
- AWS Secrets Manager

Example Mapping:

| Key              | Value                | Type        |
|------------------|---------------------|------------|
| AWS_DEFAULT_REGION | eu-west-2         | Default     |
| ENVIRONMENT      | Production          | Static      |
| MY_SECRET_TOKEN   | SSM Parameter Store | Dynamic     |
| SECRET_TOKEN     | Secrets Manager     | Dynamic     |

---

## 🔐 2. CodeBuild – Security Model

CodeBuild uses a **Service Role (IAM Role)** to access AWS resources on your behalf.

### 🔑 Responsibilities of Service Role:

- Access CodeCommit repositories
- Fetch parameters from SSM Parameter Store
- Retrieve secrets from Secrets Manager
- Upload artifacts to S3
- Write logs to CloudWatch Logs
- Encrypt data in transit and at rest
- Secure build outputs using KMS encryption (if configured)

---

### ⚠️ Key Insight

If a build fails randomly → 70% chance it's IAM permissions.

Think like a security engineer, not just a builder.

---

## 🏷️ 3. CodeBuild – Build Badges

### 📌 What is a Build Badge?
A dynamically generated status badge that shows the latest build result.

### 📍 Features:
- Public URL access
- Shows build status (Success / Failed / In Progress)
- Works with:
  - GitHub
  - Bitbucket
  - CodeCommit
- Badge is branch-specific

### 💡 Use Case:
- README dashboards
- Portfolio visibility
- CI/CD status tracking

---

## ⚡ 4. CodeBuild – Triggers

### 🔁 What triggers a build?

#### 1. CodeCommit Trigger
- Direct repository event triggers CodeBuild

#### 2. EventBridge Trigger
- AWS event-driven automation layer
- Flexible rule-based triggers

#### 3. Lambda Trigger
- Lambda function triggers CodeBuild manually or conditionally

#### 4. GitHub Webhook Trigger
- Push event → GitHub → CodeBuild

---

### 🧠 Flow Concept

```
GitHub / CodeCommit
        ↓
EventBridge / Webhook / Lambda
        ↓
CodeBuild Execution
```

---

## 🧪 5. CodeBuild – Test Reports

### 📌 What are Test Reports?
A structured way to collect and visualize test results from your build process.

---

### 🧾 Supported Formats:
- JUnit XML
- NUnit XML / NUnit3 XML
- TestNG XML
- Visual Studio TRX
- Cucumber JSON

---

### 🧱 How it works:

1. Run tests during build phase
2. Generate report file (XML/JSON)
3. Define Report Group in `buildspec.yml`
4. AWS CodeBuild stores and visualizes results

---

### 📌 Example Use Case:
- Unit tests
- Integration tests
- Functional tests
- API validation tests

---

### 💡 buildspec.yml integration idea:

```
reports:
  my-test-reports:
    files:
      - "**/*"
    base-directory: test-results
```

---

## 🚀 Key Takeaways

- Environment variables = AWS + custom + secure sources
- IAM roles are the backbone of CodeBuild security
- Build badges = visibility & trust signal
- Triggers = multiple event-driven entry points
- Test reports = observability for CI/CD quality

---

## 🧠 Final Mental Model

CodeBuild is not just a "build tool"

It is:

👉 Secure execution environment  
👉 Event-driven automation engine  
👉 Testing observability platform  
👉 CI/CD intelligence layer