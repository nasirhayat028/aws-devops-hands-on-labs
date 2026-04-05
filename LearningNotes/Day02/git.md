GIT HANDS-ON NOTES

---

# 🔹 1. Git kya hai?

Git ek **Version Control System (VCS)** hai.

👉 Simple words:
Git tumhari files ka **history manager** hai.

👉 Real-life example:

* Tum code likhte ho
* Galti ho gayi ❌
* Git → tumhe pichla version wapas la deta hai ✅

---

# 🔹 2. Git vs GitHub

## Git:

* Local tool (tumhare system pe)
* Version control karta hai

## GitHub:

* Cloud platform (internet pe)
* Code store + share + collaborate

👉 Flow:
Laptop (Git) → Push → GitHub (remote storage)

---

# 🔹 3. Basic Git Workflow (Core Mental Model)

Working Directory → Staging Area → Repository

1. Working Directory:

   * Jahan tum files edit karte ho

2. Staging Area:

   * Files ready for commit

3. Repository:

   * Final saved version (history)

---

# 🔹 4. Git Setup (First Time)

git config --global user.name "Your Name"
git config --global user.email "[your@email.com](mailto:your@email.com)"

👉 Purpose:
Git ko batana ke commits kisne kiye

---

# 🔹 5. Repository Initialize karna

git init

👉 Ye kya karta hai?

* Folder ko Git repository bana deta hai
* .git folder create hota hai (hidden)

---

# 🔹 6. File Tracking Start karna

git status

👉 Batata hai:

* Kaunsi files new hain
* Kaunsi modified hain

---

git add filename.txt
git add .

👉 Purpose:

* Files ko staging area me bhejna

---

# 🔹 7. Commit (Snapshot lena)

git commit -m "Added first file"

👉 Commit kya hai?

* Tumhare project ka ek **snapshot (photo)**

👉 Important:
Har commit = ek checkpoint

---

# 🔹 8. Commit History dekhna

git log

👉 Shows:

* All commits
* Author
* Time
* Message

---

# 🔹 9. GitHub se connect karna

git remote add origin <repo-url>

👉 origin = GitHub repo ka naam (default)

---

git push -u origin main

👉 Purpose:

* Local code → GitHub pe upload

---

# 🔹 10. Clone (Repo copy karna)

git clone <repo-url>

👉 Ye kya karta hai?

* GitHub repo → local system pe laata hai

---

# 🔹 11. Branching (Most Important 🔥)

👉 Branch kya hai?

* Alag working line (safe experimentation)

---

git branch

👉 Sab branches show karta hai

---

git branch feature-login

👉 New branch create

---

git checkout feature-login

👉 Branch switch

---

Shortcut:
git checkout -b feature-login

👉 Create + switch ek sath

---

# 🔹 12. Merge (Branches ko jorna)

git checkout main
git merge feature-login

👉 Purpose:

* Feature branch ka code → main branch me lana

---

# 🔹 13. Pull (Latest code lana)

git pull origin main

👉 GitHub → local system

---

# 🔹 14. Real Workflow (Professional DevOps Flow)

1. main branch (stable code)
2. New feature branch create
3. Code likho + commit karo
4. Push to GitHub
5. Pull Request (PR) create
6. Code Review
7. Merge to main

---

# 🔹 15. Pull Request (PR) kya hota hai?

👉 Simple:
"Please mera code review karo aur merge karo"

👉 Use case:
Team collaboration

---

# 🔹 16. Important Best Practices

✅ Direct main branch pe kaam na karo
✅ Small commits likho (clear message)
✅ Meaningful commit messages likho
✅ Har feature ke liye alag branch

---

# 🔹 17. Common Commands Summary

git init
git status
git add .
git commit -m "message"
git branch
git checkout -b branch-name
git merge branch-name
git push
git pull
git clone

---

# 🔥 FINAL MENTAL MODEL

Git = Time Machine + Collaboration Tool

Tum:

* Code likhte ho
* Save karte ho (commit)
* Branch banate ho
* Test karte ho
* Merge karte ho

👉 Result:
Safe, trackable, team-friendly development

---