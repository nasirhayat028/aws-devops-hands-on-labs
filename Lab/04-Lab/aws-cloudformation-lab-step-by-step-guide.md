# 🧠 AWS CloudFormation LAB - Step by Step DevOps Guide

---

# 🚀 1. Goal of This Lab

Is lab ka purpose hai:

👉 CloudFormation ka practical use samajhna
👉 Ready-made templates explore karna
👉 Apna custom infrastructure code likhna
👉 Stack create karna

Simple words:

> “Hum infrastructure ko code se create karna seekh rahe hain”

---

# 🌍 2. Region Selection (VERY IMPORTANT)

## 📌 Step 1: Region select karo

👉 Use: `us-east-1 (N. Virginia)`

---

## 🧠 Kyu ye region?

* AWS ka default aur most supported region
* New features yahan sabse pehle aate hain
* Learning aur labs ke liye best
* Cheap aur stable

---

# 🧪 3. PART 1 - Ready-made Template Explore Karna

---

## 🟢 STEP 2: CloudFormation Console Open

👉 AWS Console → CloudFormation → Stacks

---

## 🟢 STEP 3: Create Stack

👉 Click “Create Stack”

---

## 🟢 STEP 4: Template Selection

Option milega:

👉 “Prepare Template”

Select karo:

* Use a sample template

---

## 🟢 STEP 5: Choose Template

👉 List me se select karo:

* WordPress Blog (ya koi bhi)

---

## 🧠 Kyu ye step?

👉 Samajhne ke liye:

* Real production architecture kaisa hota hai
* Multiple services kaise connect hoti hain

---

## 🟢 STEP 6: Open in Application Composer

👉 Click “View in Application Composer”

---

## 🧠 Yahan kya dekho?

### Canvas View:

👉 Visual diagram milega:

* EC2 instances
* Database
* Load Balancer
* Networking

---

### Template View:

👉 YAML / JSON code milega

---

## 🔍 Learning Focus

* Resources ka structure
* Kaun si service kis se connected hai
* Kaise large infra define hota hai

---

## ⚠️ IMPORTANT

👉 Is template ko deploy nahi karna

### Kyu?

❌ Cost high ho sakti hai
❌ Multiple resources create ho jate hain

---

# 🧪 4. PART 2 - Apna Custom Template Use Karna

---

## 🟢 STEP 7: Create Stack Again

👉 Phir se “Create Stack” pe jao

---

## 🟢 STEP 8: Use Your Own Template

👉 Option select karo:

* Upload a template file

---

## 🟢 STEP 9: Upload File

File name:

```id="file1"
0-just-ec2.yml
```

---

## 📄 Template Code

```yaml id="code1"
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0a3c3a20c096f377
      InstanceType: t2.micro
```

---

# 🧠 5. Code Explanation (Line by Line)

---

## 🔹 Resources

👉 Yahan hum define karte hain kya create karna hai

---

## 🔹 MyInstance

👉 Ye resource ka logical naam hai
👉 Tum kuch bhi naam rakh sakte ho

---

## 🔹 Type

```yaml id="code2"
AWS::EC2::Instance
```

👉 AWS ko batata hai:

* EC2 instance create karna hai

---

## 🔹 Properties

👉 Configuration of EC2

---

### AvailabilityZone

```yaml id="code3"
us-east-1a
```

👉 Specific data center location

---

### ImageId

```yaml id="code4"
ami-0a3c3a20c096f377
```

👉 OS template (AMI)

Example:

* Ubuntu
* Amazon Linux

---

### InstanceType

```yaml id="code5"
t2.micro
```

👉 Server size

* Free tier eligible
* Low cost

---

# 🚀 6. Deploy the Stack

---

## 🟢 STEP 10: Stack Name

👉 Name do:

```id="code6"
demo-stack
```

---

## 🟢 STEP 11: Create Stack

👉 Baaki sab default rehne do
👉 Click “Create”

---

# 🔄 7. What Happens Internally?

👉 CloudFormation:

1. Template read karta hai
2. EC2 create karta hai
3. Configuration apply karta hai
4. Stack status update karta hai

---

# 📊 8. Verify

👉 CloudFormation → Stack status check karo

Expected:

* CREATE_COMPLETE

---

👉 EC2 Console check karo:

* Instance running hoga

---

# ⚠️ 9. Common Mistakes

❌ Wrong AMI ID → instance fail
❌ Wrong AZ → error
❌ YAML indentation error

---

# 🧹 10. Cleanup (IMPORTANT)

👉 Stack delete karo

---

## 🧠 Kyu?

* Cost avoid karne ke liye
* Resources clean rakhne ke liye

---

# 🧠 FINAL DEVOPS UNDERSTANDING

---

## 💡 Tumne kya seekha?

* CloudFormation ka real use
* Ready templates explore karna
* Apna infra code likhna
* Stack create aur manage karna

---

## 🔥 Mental Model

👉 Template = Blueprint
👉 Stack = Live Infra

---

## 🚀 Real World Use

* Production infra setup
* CI/CD automation
* Disaster recovery (recreate infra anytime)

---

# 🧪 MINI CHALLENGE

1. InstanceType change karo (t2.small)
2. New stack deploy karo
3. Difference observe karo

---

💡 Final Insight:

> “Jo engineer infra ko code se control karta hai… wahi real DevOps engineer hai.”

---
