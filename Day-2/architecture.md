
[![LinkedIn](https://img.shields.io/badge/Connect%20with%20me%20on-LinkedIn-blue.svg)](https://www.linkedin.com/in/rohit-rawat-7383091a7/)
[![GitHub](https://img.shields.io/github/stars/AmanPathak-DevOps.svg?style=social)](http://github.com/RohitRawat891997)
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)](https://app.docker.com/accounts/rohitrawat891997)

---

# ⚙️ GitHub Actions Architecture (High-Level Flow)

👉 Jab repo me koi **event** hota hai (push, PR, schedule etc.)
➡️ **Workflow** trigger hota hai
➡️ Workflow ke andar multiple **Jobs** run hote hain
➡️ Jobs ke andar **Steps** aur **Actions** execute hote hain
➡️ Ye sab **Runner** machine pe run hota hai

Simple flow:

```
Event ➜ Workflow ➜ Jobs ➜ Steps/Actions ➜ Runner
```

Ab ek-ek component ko deep samjhte hain.

---

# 🧩 1. Workflows (Brain of GitHub Actions)

### 🔹 Workflow kya hota hai?

Workflow ek YAML file hoti hai jo define karti hai:

* Kab pipeline chalegi
* Kya tasks honge
* Kis environment me run hoga

📁 Location:

```
.github/workflows/
```

Example:

```yaml
name: CI Pipeline

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello DevOps"
```

### 🧠 Real Concept:

Workflow = **poori automation script**

Jaise:

* Code build
* Testing
* Docker build
* Deployment

👉 Production pipelines me multiple workflows hote hain:

* ci.yml
* deploy.yml
* security-scan.yml

---

# 🧩 2. Events (Trigger System)

### 🔹 Event kya hai?

Event wo signal hai jo workflow start karta hai.

Matlab:

> “Kab automation chalni chahiye?”

### 🔥 Common Events:

| Event             | Meaning            |
| ----------------- | ------------------ |
| push              | Code push hua      |
| pull_request      | PR create/update   |
| schedule          | Cron job           |
| workflow_dispatch | Manual trigger     |
| release           | Release create hui |

Example:

```yaml
on:
  push:
    branches: [ main ]
```

👉 Matlab:

* Jab main branch me push hoga tab workflow chalega.

### 🧠 DevOps Insight:

Events automation ka **entry point** hote hain.

Real companies use:

* PR pe testing
* Nightly security scan
* Release pe deployment

---

# 🧩 3. Jobs (Logical Blocks)

### 🔹 Job kya hota hai?

Workflow ke andar ek independent unit of work.

Har job:

* alag runner pe run hoti hai
* parallel bhi run ho sakti hai

Example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

  test:
    runs-on: ubuntu-latest
```

### 🧠 Think Like This:

Workflow = Project
Jobs = Departments

Example:

* build job
* test job
* deploy job

---

### 🔥 Job Dependency

```yaml
deploy:
  needs: build
```

👉 Deploy tabhi chalega jab build successful ho.

Real CI/CD pipeline exactly isi tarah design hoti hai.

---

# 🧩 4. Actions (Reusable Automation Blocks)

### 🔹 Action kya hota hai?

Action ek ready-made script ya automation component hota hai.

Matlab:

> Pre-built DevOps tools inside GitHub Actions.

Example:

```yaml
- uses: actions/checkout@v4
```

Ye action automatically:

✅ repo clone karta hai runner me.

---

### 🔥 Types of Actions:

## 1️⃣ Official Actions

* checkout
* setup-node
* setup-java

## 2️⃣ Community Actions

Docker build, Terraform deploy, SonarQube scan etc.

## 3️⃣ Custom Actions

Tum khud bhi bana sakte ho.

---

### 🧠 Real DevOps Example:

```yaml
- uses: docker/build-push-action@v5
```

Ye pura Docker build aur push automate kar deta hai.

👉 Matlab tumhe shell scripting likhne ki need nahi.

---

# 🧩 5. Runner (Execution Machine)

### 🔹 Runner kya hota hai?

Runner ek server ya VM hota hai jahan workflow actually execute hota hai.

GitHub Actions ka **execution engine**.

---

### 🖥️ Types of Runner:

## ✅ GitHub Hosted Runner

```yaml
runs-on: ubuntu-latest
```

GitHub automatically VM create karta hai.

Pros:

* Easy
* No infra management

---

## 🏢 Self-Hosted Runner

Tum apne server pe runner install karte ho.

Example use cases:

* Production deployment
* Private network
* Heavy workloads

---

### 🧠 Real Production Insight:

Companies self-hosted runners use karti hain because:

* Secrets safe
* Internal servers access
* Custom tools installed

---

# 🧠 Full Mental Model (Important for Interview)

Socho pipeline ka flow:

```
Developer push code ➜ Event trigger ➜ Workflow start
    ➜ Jobs run ➜ Actions execute ➜ Runner machine process karta hai
```

👉 Ye pura system ek **CI/CD automation engine** ban jata hai.

---

# 🔥 Real DevOps Example (Complete Structure)

```yaml
name: DevOps Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: mvn clean package

  docker:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - run: docker build -t myapp .
```

---

# 🚀 Deep Real-Life Analogy (Yaad rakhne ke liye)

GitHub Actions = Restaurant 🍽️

| Component | Real Meaning   |
| --------- | -------------- |
| Event     | Customer order |
| Workflow  | Recipe         |
| Jobs      | Cooking stages |
| Actions   | Kitchen tools  |
| Runner    | Chef/kitchen   |

---

# 💎 Pro DevOps Tips (Advanced Level)

### ✅ Multiple jobs parallel run karao → pipeline fast hogi

### ✅ Self-hosted runner use karo production deploy ke liye

### ✅ Actions ko reuse karo → DRY principle

### ✅ Secrets GitHub Secrets me rakho (never hardcode)

---
# 👨‍💻 Author

**Name:** Rohit Rawat<br>
**GitHub:** [https://github.com/RohitRawat891997](https://github.com/RohitRawat891997)<br>
**LinkedIn:** [https://www.linkedin.com/in/rohit-rawat-7383091a7/](https://www.linkedin.com/in/rohit-rawat-7383091a7/)

---

