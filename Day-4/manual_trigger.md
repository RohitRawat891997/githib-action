[![LinkedIn](https://img.shields.io/badge/Connect%20with%20me%20on-LinkedIn-blue.svg)](https://www.linkedin.com/in/rohit-rawat-7383091a7/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=for-the-badge&logo=github)](https://github.com/RohitRawat891997)
[![Docker](https://img.shields.io/badge/Docker-Profile-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/u/rohitrawat891997)

---

# ⚙️ 1️⃣ Manual Workflow Trigger kya hota hai?

GitHub Actions me manual trigger ko bolte hain:

```yaml
workflow_dispatch
```

👉 Matlab:

> Developer khud button click karke workflow run karega.

Location:

```
GitHub Repo ➜ Actions ➜ Run workflow
```

---

# 🧩 2️⃣ Inputs kya hote hain?

Inputs = User se li hui values jab workflow manually run hota hai.

Example use cases:

✅ Deployment environment choose karna
✅ Docker image version dena
✅ Feature toggle ON/OFF
✅ Custom message pass karna

---

# 🔥 3️⃣ Step-by-Step Example (Basic Input)

```yaml
name: Manual Deploy

on:
  workflow_dispatch:
    inputs:
      environment:
        description: "Select Environment"
        required: true
        default: "dev"
```

### 🧠 Explanation:

| Field       | Meaning               |
| ----------- | --------------------- |
| description | UI me label           |
| required    | mandatory ya optional |
| default     | default value         |

---

## 🖥️ UI me kya dikhega?

Run workflow button click karoge:

```
environment: dev
```

User value change bhi kar sakta hai.

---

# ⚡ 4️⃣ Inputs ko Workflow me kaise use kare?

Syntax:

```yaml
${{ github.event.inputs.<name> }}
```

Example:

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying to ${{ github.event.inputs.environment }}"
```

👉 Jab user "prod" select karega:

```
Deploying to prod
```

---

# 🧪 5️⃣ Multiple Inputs Example (Real DevOps Style)

```yaml
on:
  workflow_dispatch:
    inputs:
      env:
        description: "Environment"
        required: true
        default: "dev"

      version:
        description: "App Version"
        required: true
        default: "v1.0"
```

Use inside workflow:

```yaml
run: |
  echo "Env: ${{ github.event.inputs.env }}"
  echo "Version: ${{ github.event.inputs.version }}"
```

---

# 🎯 6️⃣ Different Input Types (Advanced)

GitHub Actions me multiple input types hote hain.

---

## ✅ Choice Dropdown

```yaml
environment:
  type: choice
  options:
    - dev
    - staging
    - prod
```

👉 UI me dropdown ban jayega.

---

## ✅ Boolean (true/false)

```yaml
run_tests:
  type: boolean
  default: true
```

Use case:

```
Run tests before deploy? ✔️
```

---

## ✅ String (Default)

```yaml
tag:
  description: "Docker Tag"
```

---

# 🚀 7️⃣ Real Production DevOps Example

Ye ek realistic deployment workflow hai:

```yaml
name: Manual Deployment

on:
  workflow_dispatch:
    inputs:
      environment:
        type: choice
        description: "Select Env"
        options:
          - dev
          - prod
      image_tag:
        description: "Docker Tag"
        required: true

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: |
          echo "Deploying ${{ github.event.inputs.image_tag }}"
          echo "Target env ${{ github.event.inputs.environment }}"
```

---

# 🧠 8️⃣ Real Mental Model (Yaad rakhne ke liye)
---

Manual Workflow = Form Fill karna 📝

```text
User Button Click ➜ Inputs Fill ➜ Workflow Start ➜ Inputs use in pipeline
```

---

# 💎 9️⃣ Advanced DevOps Tips (Very Important)

### ✅ Production deployments mostly manual inputs se hote hain

Example:

```
env = prod
version = v2.1
```

---

### ✅ Conditional logic bhi laga sakte ho

```yaml
if: github.event.inputs.environment == 'prod'
```

👉 Prod deploy sirf specific condition me.

---

### ✅ Inputs + Secrets combo

```yaml
docker login -p ${{ secrets.DOCKER_PASS }}
```

---

# 🔥 BONUS — Pro Level Insight (Interview Killer)

3 tarah ke data pipeline me aate hain:

```text
inputs   ➜ user se
vars     ➜ repo config se
github   ➜ system metadata se
```

Aur real DevOps pipelines me tino ka combo use hota hai.

---

# 👨‍💻 Author

**Name:** Rohit Rawat<br>
**GitHub:** [https://github.com/RohitRawat891997](https://github.com/RohitRawat891997)<br>
**LinkedIn:** [https://www.linkedin.com/in/rohit-rawat-7383091a7/](https://www.linkedin.com/in/rohit-rawat-7383091a7/)

---
