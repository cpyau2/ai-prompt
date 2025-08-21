---
description: GitHub MCP Rules
alwaysApply: true
---

# GitHub MCP Rules

## Private Repository Setup

**WHEN** the user instructs to create a private repo, **SHALL** respond with only the git commands in this exact order:

```bash
git init --initial-branch=main
git clone https://github.com/kennethmokapp/<repo name>
git remote add origin git@github.com:kennethmokapp/<repo name>.git
git branch -m main
git push -u origin main
```

**Replace `<repo name>` with the actual repository name provided by the user.**

## Repository Naming

**Use the provided repository name** in place of `<repo name>` in all commands.

**Example for repository "my-project":**

```bash
git clone https://github.com/kennethmokapp/my-project
git remote add origin git@github.com:kennethmokapp/my-project.git
```
