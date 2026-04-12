# 🧠 AWS CodeArtifact LAB - Step by Step DevOps Guide (Beginner Friendly)

---

# 🚀 1. Goal of This Lab

Is lab ka purpose hai:

👉 AWS CodeArtifact setup karna
👉 Packages (pip/npm) manage karna
👉 Upstream + external repos ka concept samajhna
👉 Secure dependency management practice karna

Simple words:

> “Hum apna private package manager cloud pe bana rahe hain”

---

# 🏗️ 2. Concept Samajh Lo (Before Steps)

## 📦 CodeArtifact kya karta hai?

* Python / Node.js packages store karta hai
* Dependencies manage karta hai
* Public repos (npm, PyPI) se packages fetch karta hai

---

## 🧠 Real DevOps Example

Socho tum ek company me ho:

* Har project ko same libraries chahiye
* Internet se baar baar download slow + risky hai

👉 Solution:
CodeArtifact = internal “company package store”

---

# 🧪 3. LAB SETUP (Step-by-Step)

---

## 🟢 STEP 1: Create Domain

👉 AWS Console → CodeArtifact → Domains

### Karo kya:

* Domain create karo
* Name: `my-company`

### Kyu?

👉 Domain = top-level container
👉 Jisme multiple repositories hoti hain

---

## 🟢 STEP 2: Create Repository

👉 Create Repository click karo

### Settings:

* Repository Name: `demo` (ya koi bhi)
* Domain: `my-company`

---

## 🌐 STEP 3: Enable Upstream Repository

Enable karo:

👉 External packages source

Example:

* PyPI (Python packages)
* npm (Node packages)

---

### Kyu important hai?

👉 Agar package tumhare repo me nahi hai:

* Upstream se fetch hoga
* Automatic caching ho jayegi

---

## 🔐 STEP 4: KMS Key Selection

Select:

👉 AWS managed key (default)

### Kyu?

* Encryption for packages
* Secure storage

---

## 🟢 STEP 5: Create Repository

Ab create click karo

---

# 🧠 4. WHAT YOU JUST CREATED

Ab tumhare paas:

* 🏢 Domain: `my-company`
* 📦 Repo: `demo`
* 🌍 External connection (PyPI/npm)
* 🔗 Upstream chain ready

---

# 🔗 5. Connection Flow (Important Mental Model)

```
Your Repo (demo)
        ↓
Upstream Repo
        ↓
External Repo (PyPI / npm)
```

👉 Matlab:
Agar local repo me package nahi mila → upstream → public repo

---

# 💻 6. CLOUDSHELL SETUP

## 🟢 STEP 6: Open CloudShell

AWS Console → CloudShell open karo

---

## 🟢 STEP 7: Login Command Run

Example command:

```bash id="cw83kd"
aws codeartifact login --tool pip --repository demo --domain my-company --domain-owner 771844493079 --region us-east-1
```

---

### ⚠️ Common Issue

* pip version issue
* pip3 missing

👉 Fix: use manual method below

---

# 🔐 7. AUTH TOKEN SETUP

## STEP 8: Export Token

CloudShell me run karo:

```bash id="xk91ab"
export CODEARTIFACT_AUTH_TOKEN=xxxxx
```

---

## STEP 9: Check Token

```bash
echo $CODEARTIFACT_AUTH_TOKEN
```

👉 Token temporary hota hai (12 hours)

---

## 🧠 Why this exists?

👉 Security reason:

* Direct access allowed nahi hota
* Temporary token authentication use hoti hai

---

# 📦 8. PACKAGE INSTALLATION

## STEP 10: Install Package

```bash id="pk44zz"
pip3 install requests
```

---

## 🧠 What happens internally?

1. pip checks local repo (CodeArtifact)
2. package nahi mila
3. upstream check hota hai
4. external PyPI se fetch hota hai
5. package cache ho jata hai repo me

---

## 🔁 RESULT

👉 Next time install fast ho jata hai
👉 Internet dependency reduce ho jati hai

---

# 📊 9. VERIFY (VERY IMPORTANT)

## Check Repo:

👉 CodeArtifact console open karo

Tumhe milega:

* demo repo
* installed packages list

---

## Check Upstream:

👉 Same package upstream repo me bhi visible ho sakta hai

---

# 🔄 10. VERSION TEST (IMPORTANT CONCEPT)

## Example:

```bash
pip3 install requests==2.25.0
```

👉 Specific version install hota hai

---

## 🧠 Why useful?

* Production stability
* No breaking changes

---

# 🔐 11. POLICY CONFIGURATION

## STEP 11: Repository Policy

Policy defines:

* Who can read packages
* Who can write packages

---

## Example Access Types:

* Read only
* Write access
* Admin access

---

## 🧠 Why important?

👉 Security control in enterprise systems

---

# 🏢 12. DOMAIN POLICY

Domain level control:

* All repos under domain
* Centralized permissions

---

## Example:

👉 Company rule:

* Only DevOps team can publish packages
* Developers can only read

---

# 🧹 13. CLEANUP (OPTIONAL)

You can delete:

* Repository
* Domain

---

## 🧠 Why cleanup matters?

* Cost control
* Resource hygiene
* Avoid clutter in AWS account

---

# 🚀 FINAL DEVOPS MINDSET

## CodeArtifact = Dependency Backbone

* Stores packages
* Controls versions
* Improves CI/CD speed

---

## Upstream = Smart fallback system

* If local fails → external source

---

## External connection = Internet bridge

* Public repositories access

---

# 🧠 SIMPLE ANALOGY

👉 CodeArtifact = Company warehouse
👉 Upstream = Branch warehouse
👉 External repo = Market (internet)

---

# 🧪 MINI REVISION DRILL

Try answer:

1. Why do we need upstream repos?
2. What happens if package is not found locally?
3. Why token expires after 12 hours?
4. Difference between domain and repository?

---

💡 Final Insight:

> “Good DevOps engineers don’t just run commands — they understand flow.”

---
