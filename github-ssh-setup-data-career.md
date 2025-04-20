# GitHub SSH Configuration for Multi-Account Workflow (VS Code + GitKraken)

As part of my portfolio and professional setup as a **Data Scientist / Data Analyst / Machine Learning Engineer**, I implemented a secure SSH-based Git workflow for managing **multiple GitHub accounts**. This is crucial when maintaining separate profiles for personal projects, freelance work, or open-source contributions.

This document explains how I securely push code to a secondary GitHub account using SSH while continuing to develop, commit, and push seamlessly in **VS Code**—a workflow that also integrates well with GitKraken for version control visualization.

---

## ✅ Objective

Set up Git to:

- Authenticate with **two GitHub accounts** using **separate SSH keys**.
- Enable **VS Code** to handle Git operations without interference or conflict between accounts.
- Use **GitKraken** as a visual Git manager for clarity and productivity.
- Ensure that selected repositories push code only to **Account B**, used here to showcase my portfolio projects.

---

## 🔐 SSH Key Generation

I created a **dedicated SSH keypair** for GitHub Account B (my public portfolio account):

```bash
ssh-keygen -t ed25519 -C "your-email@example.com" -f ~/.ssh/id_ed25519_accountB
```

Public key was added to GitHub under:
```
GitHub → Settings → SSH and GPG Keys → New SSH Key
```

---

## ⚙️ SSH Configuration for Account Separation

To separate authentication between accounts, I configured a custom SSH host alias:

```bash
# ~/.ssh/config

# Default GitHub (Account A - personal/private work)
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_accountA

# GitHub Account B (public portfolio + recruiter-visible)
Host github-accountB
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_accountB
```

---

## 🔄 Pointing a Repo to the Right GitHub Account

Inside my project folder (`notion-gpt-api`), I redirected Git operations to use the correct account:

```bash
git remote set-url origin git@github-accountB:vishant-raz/notion-gpt-api.git
```

Confirmed using:

```bash
git remote -v
# Output:
# origin  git@github-accountB:vishant-raz/notion-gpt-api.git (fetch)
# origin  git@github-accountB:vishant-raz/notion-gpt-api.git (push)
```

---

## 🧪 Verification Process

### SSH Auth Test:
```bash
ssh -T git@github-accountB
# Output: "Hi vishant-raz! You've successfully authenticated..."
```

### Created a test file:

```text
test-ssh.txt
-------------
SSH Push Test

This file is used to verify that my Git remote is using the SSH alias
(github-accountB) and key for Account B.
```

### Pushed to GitHub:

```bash
git add test-ssh.txt
git commit -m "test: verify SSH alias push"
git push
```

✅ Verified via GitHub web UI that the file was uploaded to the correct repo under Account B.

---

## 🛠️ Tools Used

- **VS Code** – primary IDE for Python, data analysis, and ML workflows.
- **Git CLI** – for version control and remote management.
- **GitKraken** – for visual Git operations and branch history.
- **macOS Terminal** – for system-level configuration.

---

## 💼 Relevance to My Career

As a data science professional, this setup reflects my:

- **Attention to reproducibility and secure coding workflows**.
- Ability to manage **complex version control environments** (multiple projects/accounts).
- Use of industry‑standard tools like Git, SSH, and GitHub in a real-world development pipeline.
- Demonstrated capability to organize public and private work under different accounts for **job applications, freelance clients, and collaboration.**

---

_This configuration is a key part of how I maintain and showcase my technical work while keeping my portfolio structured, professional, and recruiter-friendly._
