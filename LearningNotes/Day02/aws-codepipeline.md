# 🚀 AWS CODEPIPELINE (Deep Dive Notes — Zero → Pro)

---

# 🔹 1. CodePipeline kya hai?

👉 Simple Definition:
CodePipeline ek **automation engine** hai jo tumhara pura CI/CD process automatically run karta hai.

👉 Simple words:
“Code likho → baaki sab automatic ho jaye”

---

# 🔹 2. Real-Life Analogy

Socho ek factory hai 🏭:

* Raw material aata hai (code)
* Machine process karti hai (build/test)
* Final product ready hota hai (deploy)

👉 CodePipeline = factory manager

---

# 🔹 3. High-Level Flow (MOST IMPORTANT)

Developer → Source → Build → Test → Deploy

---

# 🔥 Real DevOps Example (Node.js App)

1. Developer Git push karta hai
2. CodePipeline trigger hota hai
3. CodeBuild app build karta hai
4. Tests run hotay hain
5. CodeDeploy EC2 pe deploy karta hai

👉 Sab automatic 🔥

---

# 🔹 4. Pipeline ke Core Components

## 🧩 (1) Source Stage

👉 Code kahan se aa raha hai?

Options:

* CodeCommit
* GitHub
* S3
* Bitbucket

👉 Example:
Tum GitHub pe code push karte ho → pipeline start

---

## 🧩 (2) Build Stage

👉 Code ko executable banaya jata hai

Tools:

* CodeBuild
* Jenkins

👉 Example:

* Node.js app → Docker image banayi
* Java app → .jar file banayi

---

## 🧩 (3) Test Stage

👉 Code sahi kaam kar raha hai ya nahi?

Tools:

* CodeBuild
* AWS Device Farm

👉 Example:

* Unit tests run
* API test
* UI test

---

## 🧩 (4) Deploy Stage

👉 Code ko live environment me bhejna

Tools:

* CodeDeploy
* ECS
* S3
* Elastic Beanstalk

👉 Example:
App EC2 pe deploy ho jata hai

---

## 🧩 (5) Invoke Stage (Advanced)

👉 Additional automation

Tools:

* Lambda
* Step Functions

👉 Example:

* Deployment ke baad DB migration run karna

---

# 🔹 5. Stages kya hoti hain?

👉 Pipeline = stages ka collection

Example:

Source → Build → Test → Deploy

---

## 🔥 Important:

👉 Har stage me:

* Sequential actions (step by step)
* Parallel actions (same time)

---

## 💡 Example:

Test Stage me:

* Unit tests
* Integration tests

👉 Dono parallel run ho sakte hain

---

# 🔹 6. Manual Approval (Production Safety 🔥)

👉 Pipeline automatically chalti hai
👉 BUT production pe deploy se pehle stop ho sakti hai

---

## 💡 Example:

1. Code build ho gaya
2. Test pass
3. STOP ✋ (manual approval)

👉 Senior dev approve karega → tab deploy hoga

---

# 🔹 7. Artifacts (VERY IMPORTANT 🔥)

## 🔥 Concept:

👉 Har stage output banati hai
👉 Us output ko next stage use karta hai

---

## 🧠 Simple words:

Artifact = “processed file”

---

## 💡 Example Flow:

1. Source:

   * Code aaya → artifact bana (zip)

2. Build:

   * Code compile hua → new artifact (build output)

3. Deploy:

   * Ye artifact server pe chala gaya

---

## ⚙️ Storage:

👉 Artifacts S3 bucket me store hote hain

---

## 🧠 Analogy:

> Factory me har stage ka output next machine ko diya jata hai

---

# 🔹 8. Visual Flow (MENTAL MODEL)

Developer → CodeCommit → CodePipeline
→ CodeBuild → CodeDeploy → Live App

👉 Beech me S3 = storage (artifacts)

---

# 🔹 9. Troubleshooting (REAL ENGINEER SKILL 🔥)

Pipeline fail ho gayi? 😈

---

## 🧩 Step 1: Check Stage Failure

👉 Console me dekho:

* Kaunsa stage fail hua?
* Build? Test? Deploy?

---

## 🧩 Step 2: Event Monitoring

👉 Use:
EventBridge / CloudWatch

---

## 💡 Example:

* Pipeline failed → notification aayi
* Stage cancelled → alert mila

---

## 🧩 Step 3: IAM Permissions Check

👉 Most common issue ❗

👉 Problem:
Pipeline kuch action perform nahi kar pa rahi

👉 Reason:
IAM role ke paas permission nahi

---

## 💡 Example:

* CodeDeploy fail
* Reason: EC2 access allowed nahi

---

## 🧩 Step 4: Audit Logs

👉 Use:
CloudTrail

👉 Purpose:

* Kisne kya action kiya?
* API calls track karna

---

# 🔥 FINAL MENTAL MODEL

CodePipeline =

👉 “Automation Brain of DevOps”

---

## Flow:

Code → Build → Test → Deploy
(Everything automatic)

---

## Supporting Services:

* CodeCommit → code store
* CodeBuild → build/test
* CodeDeploy → deploy
* S3 → artifacts

---

# 🧠 SELF TEST (MANDATORY)

Without notes, explain:

1. Pipeline me stages kya hoti hain?
2. Artifact kya hota hai?
3. Manual approval kyun use hota hai?
4. Pipeline fail ho to kya check karte ho?

---

# 🚀 PRACTICAL TASK

👉 Design karo:

“Node.js app CI/CD pipeline”

Include:

* Source (GitHub)
* Build (CodeBuild)
* Deploy (EC2)

---

