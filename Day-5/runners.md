[![LinkedIn](https://img.shields.io/badge/Connect%20with%20me%20on-LinkedIn-blue.svg)](https://www.linkedin.com/in/rohit-rawat-7383091a7/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=for-the-badge&logo=github)](https://github.com/RohitRawat891997)
[![Docker](https://img.shields.io/badge/Docker-Profile-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/u/rohitrawat891997)

---

# ⚙️ Runner kya hota hai? (Basic Concept)

👉 Runner = wo machine (VM / Server) jahan tumhara workflow actually run hota hai.

Matlab:

```
Workflow = instructions
Runner = execution server
```

Jab bhi job start hoti hai:

➡️ GitHub runner ko command deta hai
➡️ Runner steps execute karta hai (build, test, deploy)

---

# 🧠 Types of Runners

GitHub Actions me mainly 2 types ke runners hote hain:

```
1️⃣ GitHub-hosted runners
2️⃣ Self-hosted runners
```

Ab dono ko deep samjhte hain.

---

# 🟢 1️⃣ GitHub-Hosted Runner

👉 Ye runners GitHub khud provide karta hai.

Example:

```yaml
runs-on: ubuntu-latest
```

GitHub background me:

* ek fresh VM banata hai
* job run karta hai
* job khatam ➜ VM delete

---

## 🔹 1. Job Execution Time

Matlab:

> Ek single job kitni der tak run kar sakti hai.

Typical limits:

* Free/Go plan: approx **6 hours max per job**

Agar job 6 hour se zyada chali:

❌ Automatically terminate ho jayegi.

---

## 🔹 2. Workflow Run Time

Poora workflow kitni der tak run ho sakta hai.

Example:

```
build ➜ test ➜ deploy
```

Total workflow duration bhi limited hoti hai (usually job limit se tied).

---

## 🔹 3. API Requests

GitHub-hosted runners GitHub API use karte hain:

* checkout repo
* artifacts upload
* logs send

GitHub rate limits apply karta hai.

👉 Agar heavy automation hai to API throttling ho sakti hai.

---

## 🔹 4. Concurrent Jobs

Kitni jobs ek time me parallel run hongi.

Example:

* Go plan me limited concurrency hoti hai.
* Paid plans me zyada parallel jobs milti hain.

Example mental model:

```
2 concurrent jobs allowed:
build1 ✅
build2 ✅
build3 ⏳ queue me wait
```

---

# 🟡 2️⃣ Self-Hosted Runner

👉 Ye runner tum apne server pe install karte ho.

Example:

* AWS EC2
* On-prem server
* Kubernetes node

Use case:

✅ Production deployment
✅ Private network access
✅ Custom tools installed

---

## 🔹 1. Job Execution Time

GitHub-hosted me limit hoti hai.

Self-hosted me:

👉 practically **no hard execution limit** (server resources pe depend).

Agar server powerful hai:

* long running build possible
* heavy DevSecOps scans possible

---

## 🔹 2. Workflow Run Time

Workflow duration bhi tum control karte ho.

GitHub VM destroy nahi karta — tumhara server hi run karta hai.

---

## 🔹 3. Job Queue Time

Queue time = job ko runner milne tak wait time.

Self-hosted me depend karta hai:

```
Kitne runners available hain?
```

Example:

```
1 runner
3 jobs
```

➡️ 2 jobs queue me wait karengi.

---

## 🔹 4. API Requests

Self-hosted runner bhi GitHub API use karta hai:

* logs send
* job status update

But:

👉 execution local hota hai, isliye API usage thoda different feel hota hai.

---

## 🔹 5. Job Matrix

Matrix strategy = ek job multiple variations me run karna.

Example:

```yaml
strategy:
  matrix:
    os: [ubuntu, windows]
```

Self-hosted me:

👉 har matrix job ko alag runner chahiye.

Agar sirf 1 runner hai:

```
matrix jobs sequential chalenge
```

Agar multiple runners:

```
parallel execution possible
```

---

## 🔹 6. Workflow Run Queue

Self-hosted me ek extra queue layer hoti hai:

```
GitHub Queue ➜ Runner Queue
```

Example:

* GitHub job send karta hai
* Runner busy hai
* Job local queue me wait karegi

---

## 🔹 7. Registering Self-Hosted Runners (Step-by-Step)

### ✅ Step 1 — Repo Settings

```
Repo ➜ Settings ➜ Actions ➜ Runners ➜ New Self-hosted Runner
```

---

### ✅ Step 2 — OS Select karo

Example:

```
Linux
```

GitHub tumhe commands dega.

---

### ✅ Step 3 — Server pe Install

```bash
mkdir actions-runner
cd actions-runner
curl -o actions-runner.tar.gz <download-url>
tar xzf actions-runner.tar.gz
```

---

### ✅ Step 4 — Configure Runner

```bash
./config.sh --url https://github.com/username/repo --token XXXXX
```

👉 Ye runner ko repo se link karega.

---

### ✅ Step 5 — Start Runner

```bash
./run.sh
```

Ya production me:

```bash
sudo ./svc.sh install
sudo ./svc.sh start
```

Ab workflow me use:

```yaml
runs-on: self-hosted
```

---

# 🚀 GitHub-Hosted vs Self-Hosted (Real DevOps Difference)
```
| Feature  | GitHub Hosted | Self Hosted   |
| -------- | ------------- | ------------- |
| Setup    | Zero          | Manual        |
| Limits   | Fixed         | Flexible      |
| Security | Shared infra  | Private infra |
| Cost     | Minutes based | Server cost   |
| Control  | Low           | Full control  |
```
---

# 🧠 Real DevOps Mental Model (Interview Level)

Socho:

```
GitHub-hosted = Taxi 🚕
Self-hosted   = Apni car 🚗
```

Taxi:

* ready
* fast
* but rules fixed

Apni car:

* full control
* maintenance tumhari

---

# 💎 Pro Tips (Company-Level Knowledge)

✅ Production deployment → mostly self-hosted runners
✅ Heavy Docker builds → self-hosted faster
✅ Secure infra access → self-hosted only
✅ Testing pipelines → GitHub-hosted best

---

# 👨‍💻 Author

**Name:** Rohit Rawat<br>
**GitHub:** [https://github.com/RohitRawat891997](https://github.com/RohitRawat891997)<br>
**LinkedIn:** [https://www.linkedin.com/in/rohit-rawat-7383091a7/](https://www.linkedin.com/in/rohit-rawat-7383091a7/)

---

