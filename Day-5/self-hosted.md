[![LinkedIn](https://img.shields.io/badge/Connect%20with%20me%20on-LinkedIn-blue.svg)](https://www.linkedin.com/in/rohit-rawat-7383091a7/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=for-the-badge&logo=github)](https://github.com/RohitRawat891997)
[![Docker](https://img.shields.io/badge/Docker-Profile-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/u/rohitrawat891997)

---

# ⚙️ Step-by-Step Flow (Self-Hosted Runner Job Execution)

## ✅ Step 1 — Runner Status Check karo

Runner install aur configure karne ke baad ensure karo:

```bash
./run.sh
```

Ya service mode me:

```bash
sudo ./svc.sh status
```

GitHub UI me jao:

```text
Repo ➜ Settings ➜ Actions ➜ Runners
```

👉 Status **Online** hona chahiye.

---

## ✅ Step 2 — Workflow YAML me self-hosted specify karo

Sabse important part 👇

GitHub ko batana padega ki job **self-hosted runner** pe run kare.

```yaml
name: Self Hosted Demo

on: push

jobs:
  build:
    runs-on: self-hosted
    steps:
      - run: echo "Running on self hosted runner"
```

👉 `runs-on: self-hosted` likhte hi job GitHub VM pe nahi, tumhare server pe execute hogi.

---

## ✅ Step 3 — Workflow Trigger karo

Workflow trigger karne ke multiple tarike:

### 🔹 Option 1: Code push

```bash
git push origin main
```

### 🔹 Option 2: Manual run

Agar `workflow_dispatch` use kiya hai:

```text
Actions ➜ Run Workflow

on:
  workflow_dispatch:

```

---

## ✅ Step 4 — Execution kaise hoti hai backend me?

Jab job start hoti hai:

```text
GitHub ➜ runner ko signal bhejta hai
Runner ➜ job download karta hai
Runner ➜ steps local server pe execute karta hai
Logs ➜ GitHub UI me upload hoti hain logs.
```

Matlab:

👉 Execution tumhare server pe ho rahi hai, GitHub sirf control kar raha hai.

---

## ✅ Step 5 — Server Terminal me kya dikhega?

Runner console me kuch aisa output dikhega:

```text
Listening for Jobs
Running job: build
```

Aur GitHub Actions UI me logs live show honge.

---

# 🧪 Real DevOps Example (Docker Build on Self-Hosted)

```yaml
name: Docker Self Hosted

on: push

jobs:
  docker-build:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v4
      - run: docker build -t myapp .
```

👉 Ye Docker build GitHub VM pe nahi — tumhare server pe hoga.

---

# 🧠 Important Concepts (Very Important)

## 🔥 Runner Labels

Agar multiple runners hain:

```yaml
runs-on: [self-hosted, linux]
```

👉 GitHub correct runner choose karega.

---

## 🔥 Runner Online hona zaroori

Agar runner offline hai:

```text
Job stuck in queue ❌
```

---

## 🔥 Runner Busy Scenario

1 runner + 3 jobs:

```text
Job1 ➜ Running
Job2 ➜ Queue
Job3 ➜ Queue
```

---

# 🚀 Full Execution Lifecycle (Memory Trick)

```text
Register Runner ➜ Runner Online
Workflow Trigger ➜ Job Assigned
Runner Pull Job ➜ Steps Execute
Logs Upload ➜ Job Complete
```

---

# 💎 Pro DevOps Tips (Real Production)

✅ Self-hosted runner ko **service mode** me chalao:

```bash
sudo ./svc.sh install
sudo ./svc.sh start
```

Server reboot ke baad bhi runner automatically start hoga.

---

✅ Runner pe required tools install hone chahiye:

* docker
* kubectl
* terraform
* ansible

Kyuki GitHub-hosted jaisa preinstalled environment nahi hota.

---

# 🔥 Common Mistake (Beginners karte hain)

❌ Runner register kar diya but workflow me:

```yaml
runs-on: ubuntu-latest
```

👉 Result: job GitHub-hosted pe run hogi.

Correct:

```yaml
runs-on: self-hosted
```

---


# 👨‍💻 Author

**Name:** Rohit Rawat<br>
**GitHub:** [https://github.com/RohitRawat891997](https://github.com/RohitRawat891997)<br>
**LinkedIn:** [https://www.linkedin.com/in/rohit-rawat-7383091a7/](https://www.linkedin.com/in/rohit-rawat-7383091a7/)

---
