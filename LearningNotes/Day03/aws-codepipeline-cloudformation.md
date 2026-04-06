# AWS CodePipeline – Advanced Concepts (Clean Notes)

---

## 🔹 CodePipeline with CloudFormation (as Target)

CodePipeline ka use karke hum infrastructure ko automate karte hain using CloudFormation.

### 🔸 Action Modes (CloudFormation Actions)

Different modes define karte hain ke pipeline kya kare:

* **Create or Replace Change Set**
  → New changes prepare karta hai (but apply nahi karta)

* **Execute Change Set**
  → Prepared changes ko apply karta hai

* **Create or Update Stack**
  → Stack exist kare to update, warna create

* **Delete Stack**
  → Pura infrastructure remove

* **Replace Failed Stack**
  → Agar stack fail ho jaye to usay replace kare

---

## 🔹 Template Parameter Overrides

Kabhi kabhi tumhe CloudFormation template ke parameters dynamically change karne hote hain.

### 🔸 Static vs Dynamic

* **Static (Recommended)**
  → Fixed config file use hoti hai

* **Dynamic**
  → Runtime pe values change hoti hain using pipeline

---

## 🔸 JSON Example (Parameter Override)

```json
{
  "ParameterName": {
    "Fn::GetParam": [
      "ArtifactName",
      "config-file-name.json",
      "ParamName"
    ]
  }
}
```

### 🔍 Explanation:

* `ArtifactName` → Pipeline ka input artifact (e.g. S3 zip file)
* `config-file-name.json` → File jisme values stored hain
* `ParamName` → Specific parameter jo extract karna hai

👉 Ye config pipeline ke andar dynamically values inject karta hai.

⚠️ Important:

* Template ke andar **sab parameters defined hone chahiye**
* Agar parameter missing hua → pipeline fail

---

## 🔹 CodePipeline Best Practices

### 1️⃣ One Pipeline Strategy

* Ek CodePipeline + ek CodeDeploy
* Multiple deployment groups par **parallel deploy**

---

### 2️⃣ Parallel Actions (RunOrder)

* Same stage ke andar multiple actions run ho sakte hain
* `RunOrder` decide karta hai:

  * Same number → parallel
  * Different → sequential

---

### 3️⃣ Pre-Prod → Prod Strategy

* Always pehle deploy karo:

  * Dev → Pre-Prod → Production

👉 Direct production deploy = risk 💣

---

## 🔹 CodePipeline + EventBridge

EventBridge ka use hota hai pipeline events monitor karne ke liye.

### Use Cases:

* Failure detect karna
* Alerts bhejna
* Auto-recovery trigger karna

👉 Example:
Agar deploy fail ho → EventBridge → Lambda → Slack alert

---

## 🔹 Invoke Actions (Advanced Integrations)

### 🔸 Lambda

* Pipeline ke beech custom logic run kar sakte ho

👉 Example:

* Validation
* DB migration
* Security checks

---

### 🔸 Step Functions

* Complex workflows run karne ke liye

👉 Example:

* Multi-step approval process
* Conditional execution

---

## 🔹 Multi-Region CodePipeline

Large-scale systems ke liye multi-region deployment use hota hai.

### 🔸 Key Concepts:

* Different actions → different AWS regions
* Example:
  → Lambda deploy in multiple regions using CloudFormation

---

### 🔸 Artifact Stores

Har region ke liye alag S3 bucket required hota hai.

Example:

| Region       | Type | Bucket Name                    |
| ------------ | ---- | ------------------------------ |
| eu-west-1    | S3   | codepipeline-eu-west-1-xxxx    |
| eu-central-1 | S3   | codepipeline-eu-central-1-xxxx |

---

### 🔸 Important Rules:

* CodePipeline ko har bucket ka access hona chahiye
* Agar manually setup kar rahe ho → buckets khud create karo
* AWS automatically artifacts copy karta hai between regions

---

### 🔸 Cross-Region Tip

* Sirf **artifact name reference karo**
* AWS khud handle karega copying

---

## 🧠 Real World Flow (Simple)

1. Developer pushes code
2. CodePipeline trigger hota hai
3. Build stage (CodeBuild)
4. Test / validation (Lambda / Step Functions)
5. Deploy to Pre-Prod
6. Approval (optional)
7. Deploy to Production (multi-region)

---

## 🎯 Summary

* CodePipeline = CI/CD orchestrator
* CloudFormation = Infrastructure automation
* EventBridge = Monitoring + automation
* Lambda/StepFunctions = custom logic
* Multi-region = high availability systems

---