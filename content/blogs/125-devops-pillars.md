---
title: "DevOps - Step By Step Learning : Part 2 (12 Factor Apps, DevOps 3 P's, 6 Pillars, 8 Phases)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-14T00:00:00Z"
tags: ["devops" , "devops-pillars", "devops-3p", "12-factor-apps"]
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
    image: "img/blogs/125-devops-pillars.jfif"
    caption: "DevOps Pillars"
    alt: "DevOps Pillars"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [DevOps - Step By Step Learning: Part 1 (What it is, History, Philosophy, Practice)]({{< ref "blogs/124-devops-philosophy.md" >}})
---

{{< figure
    src="/img/blogs/125-devops-pillars.jfif"
    caption="DevOps Pillars (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

You should already know about the situation and struggle that Rasel faced in the beginning of his job from the previous part. After basic exploration about DevOps, Rasel started digging deep into how the people involved, processes, and tools can change the game. He studied the famous 12-factor app best practices that received worldwide attention.

So first of all, he decided to convince the management about the primary concern of tasks/bugs and their solution, which is codebase management. And study the 12-factor app best practices and some DevOps fundamental terms so that this knowledge can be used as a reference point. So Rasel was going to solve or raise the concern about the following 2 things first:

1.  A tool/software that can be used for reported task and bug management without manual interactions and communication. (Found JIRA and Confluence)
2.  A tool and process to centralize the codebase and its version control. (Found Git and GitHub)

* * *

## 12 Factor Apps:

*   **Codebase** – One codebase per app, deployed in multiple environments.
*   **Dependencies** – Declare all dependencies explicitly; don’t rely on system libraries.
*   **Config** – Store configurations (e.g., API keys, DB URLs) in environment variables.
*   **Backing Services** – Treat databases, caches, and third-party services as replaceable resources.
*   **Build, Release, Run** – Keep build, release, and runtime stages separate for stability.
*   **Processes** – Run the app as stateless processes; store data externally.
*   **Port Binding** – The app should run standalone, listening on a specific port.
*   **Concurrency** – Scale by running multiple instances (web, worker, etc.).
*   **Disposability** – Start fast, shut down gracefully to handle crashes smoothly.
*   **Dev/Prod Parity** – Keep development, testing, and production as identical as possible.
*   **Logs** – Treat logs as event streams; store and analyze them externally.
*   **Admin Processes** – Run admin tasks (e.g., migrations) as one-time processes.

For more details please go through in this official [link](https://12factor.net).

## DevOps 3 P's:

The 3 P’s stand for the core elements of DevOps:

1. ***People***

*   DevOps is not just about tools, people and collaboration are the most important part.
*   Teams work together (Developers, Operations, Security, QA).
*   Example: Developers, QA and Operations engineers work together to deploy a new feature.

2. ***Process***

*   Defines how work gets done efficiently.
*   Includes CI/CD, automated testing, security integration, and infrastructure automation.
*   Example: Using a CI/CD pipeline to automate software deployment.

3. ***Products (Tools)***

*   Dev and Ops uses various tools to automate and improve development & deployment.
*   Like Jira for project management, Github for codebase management etc.
*   Example: GitHub, Jenkins, Docker, Kubernetes, Terraform, Prometheus are popular tools.

✅ In short: *DevOps = People + Process + Products (Tools)*

## DevOps 6 Pillars:

These six pillars support DevOps implementation:

1. ***Culture & Collaboration***

*   Encouraging communication between teams (Developers, Ops, QA, Security).
*   Example: Daily stand-up meetings to discuss progress and blockers.

2. ***Automation***

*   Automating tasks like code testing, deployment, and infrastructure setup.
*   Example: Using Jenkins to automatically test and deploy code.

3. ***Lean & Agile***

*   Delivering small, frequent updates instead of large, risky releases.
*   Example: Releasing features weekly instead of every 6 months.

4. ***Measurement & Monitoring***

*   Tracking system performance, logs, and errors in real-time.
*   Example: Grafana/New-relic dashboards showing server health.

5. ***Security (DevSecOps)***

*   Integrating security early in the development lifecycle.
*   Example: SonarQube scanning code for vulnerabilities before deployment.

6. ***Continuous Improvement***

*   Learning from failures and always improving.
*   Example: If an update breaks production, teams analyze why and fix the process. This often known as RCA (Root Cause Analysis).

✅ In short: *DevOps is built on Culture, Automation, Agile, Monitoring, Security, and Continuous Improvement.*

## DevOps 8 Phases:

The DevOps lifecycle consists of 8 phases, forming a loop of continuous improvement:

1. ***Plan***

*   Define project goals, features, and requirements.
*   Example: The product team decides to build a "Dark Mode" feature.

2. ***Develop***

*   Developers write code and use Git for version control.
*   Example: Code for "Dark Mode" is written and pushed to GitHub.

3. ***Build***

*   The code is compiled, dependencies are installed, and a testable version is created.
*   Example: Maven, Gradle, or Docker builds the application.

4. ***Test***

*   Automated testing ensures the new code doesn’t break anything.
*   Example: Selenium or JUnit runs automated tests.

5. ***Release***

*   Approved changes are packaged and prepared for deployment.
*   Example: A CI/CD pipeline bundles the app and stores it in a repository.

6. ***Deploy***

*   The application is deployed to a server, cloud, or containerized environment.
*   Example: Using Kubernetes to deploy the app to production.

7. ***Operate***

*   The app is monitored to ensure smooth performance.
*   Example: Prometheus & Grafana track errors and system performance.

8. ***Monitor***

*   Logs and analytics provide insights for improvements.
*   Example: ELK Stack (Elasticsearch, Logstash, Kibana) collects logs.

✅ In short: *DevOps follows a continuous loop: Plan -> Develop -> Build -> Test -> Release -> Deploy -> Operate -> Monitor.*

* * *

## Summary:

After all, with the reference, Rasel was able to convince the management and they were start using the Jira for project management and Git + Github for codebase and version control. All the team along with Rasel's tried to understand and followed the best practices for development and project management. They got visible improvement and outcome but not fully as the other part means deployment hassle was still exist there.