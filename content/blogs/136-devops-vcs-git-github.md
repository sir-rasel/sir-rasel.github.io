---
title: "DevOps - Step By Step Learning : Part 13 (Version Controlling Using Git and GitHub in a DevOps Perspectives)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-25T00:00:00Z"
tags: ["devops" , "vcs", "git", "github"]
draft: false
showtoc: false
tocOpen: false
hidemeta: false
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
cover:
    image: "img/blogs/136-devops-git.jfif"
    caption: "DevOps Version Control"
    alt: "DevOps Version Control"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 12:** [DevOps - Step By Step Learning : Part 12 (Dissection Important Part of Vagrantfile)]({{< ref "blogs/135-devops-vagrant.md" >}})
- **Part 21:** [DevOps - Step By Step Learning : Part 21 (Shell Scripting - Tool For Automation Repetitive Task)]({{< ref "blogs/137-devops-shell-scripting.md" >}})
---

{{< figure
    src="/img/blogs/136-devops-git.jfif"
    caption="DevOps Version Control (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel already learned coding in Golang, some basic scripting using Linux commands, and VM automation using Vagrant. All of them need to be stored with better change control and version control. Though Rasel is a software engineer and used to working with version control tools like Git and GitHub, he wanted to explore Git and GitHub in a DevOps perspectives. So he did so.

* * *

## Understanding Git and GitHub

**Git** – A distributed version control system

*   Tracks changes to files.
*   Allows branching and merging.
*   Helps collaborate with others.

**GitHub** – A cloud service for Git repositories

*   Hosts your Git repositories.
*   Adds collaboration features: issues, pull requests, CI/CD (GitHub Actions), etc.

## Real-Life DevOps Scenario

**Scenario**: Deploying a Web Application Automatically

Let’s say you're working on a Node.js API for your team. The goal is:

*   Track code changes.
*   Collaborate using branches.
*   Automatically test and deploy to a staging server using GitHub Actions.

In this scenario Git and GitHub helps you to achieve this.

* * *

## Know About Git as a DevOps Engineer

### 1. Git Basics – Foundation

As a DevOps engineer, Git is your primary tool for tracking and managing changes in code, configuration files, and infrastructure scripts. You'll often version-control things like Docker files, Kubernetes YAMLs, and Terraform files. You should be very comfortable with commands like:

*   **git init**: to start a repository,
*   **git add**: to stage changes,
*   **git commit**: to save snapshots of your work,
*   **git status**: to check what’s changed.

```bash
git init
echo "node_modules/" > .gitignore
git add .
git commit -m "Initial project setup"
git status        
```

### 2. Branching – Isolating Features and Fixes

In DevOps, you often work on features, fixes, or infrastructure updates without disrupting the main codebase. This is where branching comes in. You work on separate branch, test it and when feel confident merge it. You should be very comfortable with commands like:

*   **git checkout -b <branch-name> or git switch -c <branch-name>**: to create a new branch using name,
*   **git merge**: to merge back the changes,
*   **git rebase**: to rebase the changes. It is also merge but without creating a new commit,

```bash
git checkout -b feature/add-database
# work and commit
git checkout main
git merge feature/add-database        
```

### 3. Remote Repositories – Collaborating with Teams and Pipelines

Git really shines when combined with GitHub, GitLab, or Bitbucket, which are remote repositories. Remote repository is essential for team work and collaboration. As a DevOps engineer, you’ll often:

*   **git remote add origin <url>**: to add a remote,
*   **git clone**: to clone repositories from GitHub,
*   **git push**: to push your changes,
*   **git pull**: to pull updates,
*   **git fetch**: to fetch down all the branches from that Git remote,

```bash
git remote add origin https://github.com/user/repo.git
git push -u origin main
git fetch
git pull        
```

### 4. Inspect and Compare – Show Changes and History

Always we need to examining commit logs, diffs and object information. In git it is easy to do with the following commands:

*   **git log**: show the commit history for the currently active branch,
*   **git log branchB...branchA**: show the commits on branchA that are not on branchB,
*   **git log --follow [file]**: show the commits that changed file, even across renames,
*   **git diff branchB...branchA**: show the diff of what is in branchA that is not in branchB,
*   **git show [SHA]**: show any object in Git in human-readable format,

```bash
git log
git diff
git show        
```

### 5. Undoing Changes – Safety and Recovery

Mistakes happen—wrong configuration committed, bugs deployed, or bad merges. Git has powerful recovery tools like followings and is very helpful when a wrong push could break an automated deployment pipeline or when you need to quickly recover a deleted file.

*   **git restore**: which lets you undo changes that not committed,
*   **git reset**: which lets you undo commits locally,
*   **git revert**: which undoes a commit by creating a new one (great for undoing in production). If you’re ever unsure,
*   **git reflog**: If you’re ever unsure, it shows a log of everything you’ve done,

```bash
git reset --soft HEAD~1  # undo last commit but keep changes
git revert <commit>     # create a new commit that undoes changes        
```

### 6. Tags – Marking Releases and Versions

Tags are used to label specific points in history—especially useful for marking production releases. Many CI/CD systems are configured to deploy only when a specific tag is pushed. For example, you might tag the commit that contains a stable Docker image or infrastructure setup before deploying it to production. You can:

*   **git tag <tag name>**: to create a tag with name,
*   **git push origin <tag name>**: to push the tag into remote,

```bash
git tag v1.0.0
git push origin v1.0.0        
```

### 7. Stage – Temporarily Save and Get Changes Without Commit

Sometimes you need to temporarily store modified, tracked files in order to change branches. And need to restore the changes again to work on. You can do this in git using:

*   **git stash**: to save modified and staged changes,
*   **git stash list**: to list stack-order of stashed file changes,
*   **git stash apply**: to apply working from top of stash stack,
*   **git stash pop**: to write working from top of stash stack,
*   **git stash drop**: to discard the changes from top of stash stack,

```bash
git stash
git stash list
git stash apply
git stash drop        
```

### 8. Git Hooks – Automating Local Checks

Git hooks are scripts that run automatically when certain Git events occur, like before a commit or before pushing code. You can use them to run linters, unit tests, or secret scanners. For example, you might set up a pre-commit hook to make sure your YAML files are formatted correctly.

```bash
# .git/hooks/pre-commit
#!/bin/sh
npm run lint && npm test        
```

* * *

## Know About GitHub as a DevOps Engineer

### 1. Repositories – The Foundation of Everything

A GitHub repository (or repo) is where you store your project’s files and track changes using Git. As a DevOps engineer, you’ll use separate repos for:

*   Application code
*   Infrastructure (e.g. Terraform, Helm charts)
*   CI/CD configs (like .github/workflows/)

You can:

*   Clone a repo: git clone https://github.com/org/project.git
*   Push code to it using Git
*   Use the GitHub website to explore history, branches, and commits

### 2. Branches – Safely Test and Review Changes

DevOps work often requires testing infrastructure or CI pipeline changes in isolation. You create a branch like this:

```bash
git checkout -b update-database-config 
git push origin update-database-config        
```

On GitHub, this branch becomes a working area. From here, you can open a Pull Request (PR) for your team to review.

### 3. Pull Requests (PRs) – Safe, Auditable Collaboration

PRs are central to GitHub workflows. They:

*   Let you propose changes
*   Trigger CI/CD pipelines to test your changes
*   Let teammates review and comment
*   Enable approvals before merging to main or prod

In GitOps, PRs are how infrastructure changes are made — no one manually edits live servers.

### 4. Actions – GitHub’s Built-In CI/CD System

GitHub Actions let you automate workflows in response to Git events. Examples:

*   Every time you push code or open a PR, GitHub runs your test suite automatically.

You create workflows in YAML files under .github/workflows/test.yml. Example workflow:

```yml
name: Run Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: 18
    - run: npm install
    - run: npm test        
```

### 5. Secrets – Store Tokens Securely

When your workflow needs credentials (e.g., AWS keys, Docker Hub tokens), store them in GitHub Secrets (Settings → Secrets → Actions).

You can access them in workflows using:

```bash
env: AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}        
```

Secrets are encrypted and never visible in logs.

### 6. Environments – Control Deployment Stages

You can define environments like staging, production, and set rules:

*   Require approval before deploying
*   Use different secrets per environment
*   Limit who can deploy to each one

This adds safety and control to your deployment pipelines.

### 7. Releases – Publishing Stable Versions

You can publish a release directly from a tag. This is common for:

*   App versioning (v2.0.1)
*   Infrastructure module releases
*   Publicly shared tools

A GitHub Release includes changelogs, release notes, and downloadable assets (e.g., .zip, .tar.gz).

### 8. Webhooks – Trigger External Tools

GitHub can send events (e.g., push, PR, tag) to other systems like Jenkins, ArgoCD, Slack, etc. You configure webhooks to integrate GitHub with:

*   Jenkins build triggers
*   Kubernetes sync tools
*   Slack notifications

### 9. GitHub Projects & Issues – Track Work

Although not strictly Git-related, GitHub provides lightweight issue tracking and Kanban boards. You can:

*   Create issues for tasks or bugs
*   Automate them based on PR status
*   Organize features in boards using GitHub Projects

This helps align your code and DevOps workflows with project management.

* * *

## Summary:

Git is a tool that helps you track changes in code and configuration files over time. It works like a time machine, allowing you to save your work in small steps (called commits), go back to previous versions, or undo mistakes if something breaks. You can create branches to safely work on updates or new features without affecting the main project. Once the changes are tested and ready, you merge them back into the main version.

GitHub is an online platform where you store and manage your Git projects. It makes collaboration easy by letting team members review and discuss changes through pull requests before merging them. GitHub also provides powerful automation tools called GitHub Actions, which let you automatically test, build, or deploy your code every time someone makes a change. It also helps you store sensitive information securely using Secrets, and manage different deployment environments like staging or production.