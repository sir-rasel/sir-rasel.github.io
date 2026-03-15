---
title: "DevOps - Step By Step Learning : Part 3 (A Simplified Roadmap to Start)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-15T00:00:00Z"
tags: ["devops" , "devops-roadmap"]
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
    image: "img/blogs/126-devops-roadmap.jfif"
    caption: "DevOps Roadmap"
    alt: "DevOps Roadmap"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [DevOps - Step By Step Learning : Part 2 (12 Factor Apps, DevOps 3 P's, 6 Pillars, 8 Phases)]({{< ref "blogs/125-devops-pillars.md" >}})
---

{{< figure
    src="/img/blogs/126-devops-roadmap.jfif"
    caption="DevOps Roadmap (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel was able to convince the management and finally his team, and other teams started using **Jira** for project management, **Confluence** for documentation management, **Git** for version control, and **GitHub** for hosting the codebase rather than manual management via an **Excel** sheet.

But this was solved in the first part of the overall problems. Though they got better control and flow for managing projects and tasks/bugs, the deployment and operation parts were still manual, thus problematic.

So Rasel was inspired and confident from the overall result so far and decided to take the initiative to solve the other parts too. But like before, to convince the management, he needs the data and knowledge. As a result, he decided to gather a **simplified roadmap** so that everyone who was willing to learn the DevOps practice and tools hands-on could easily follow that.

* * *

## A Simplified Roadmap:

***Step 1 (Learn a Programming Language)***

Why?

*   Programming fundamentals help you to understand and build software stuffs.
*   DevOps requires scripting for automation, infrastructure management, and CI/CD.
*   Python is widely used for automation, while Go is common in cloud-native tools.

How to Learn?

*   Learn variables, loops, functions, error handling and basic language constructs.
*   Write scripts to automate tasks (e.g., rename multiple files).
*   Practice: Write REST API services.

***Step 2 (Learn Computer Networking)***

Why?

*   DevOps engineers manage servers and cloud networks.
*   Helps in troubleshooting deployments, DNS issues, and firewall rules.

How to Learn?

*   Understand TCP/IP, DNS, HTTP, HTTPS, and firewalls.
*   Learn cloud networking (VPCs, security groups).
*   Practice: Set up a local server and access it via IP.

***Step 3 (Learn Linux)***

Why?

*   Most servers run on Linux, and DevOps heavily depends on it.
*   Essential for managing cloud infrastructure and deployments.

How to Learn?

*   Master basic commands (ls, cd, chmod, rm, ps, top).
*   Understand user permissions and system monitoring.
*   Practice: Use a Linux VM or WSL and execute system tasks.

***Step 4 (Be Fluent in Terminal or CLI Use)***

Why?

*   CLI is more efficient for automation and remote server management.
*   Many DevOps tools (Docker, Kubernetes, Terraform) rely on CLI.

How to Learn?

*   Learn advanced commands (grep, awk, sed, find, curl).
*   Practice piping (|) and redirection (>, <, >>).
*   Practice: Write a command to find and replace text in multiple files.

***Step 5 (Learn Scripting with Bash)***

Why?

*   Automates repetitive system tasks (e.g., log rotation, backups).
*   Essential for running DevOps pipelines and cloud automation.

How to Learn?

*   Write scripts with variables, loops, and conditionals.
*   Automate system tasks like user creation and log management.
*   Practice: Write a script to monitor disk usage and send alerts.

**Step 6 (Learn Source Control Like GIT)**

Why?

*   Git is the backbone of collaboration and CI/CD workflows.
*   Required for managing infrastructure as code (Terraform, Kubernetes).

How to Learn?

*   Learn git init, clone, commit, push, pull, branch, merge, hooks.
*   Work with GitHub/GitLab for version control.
*   Practice: Create a GitHub repo and push a simple project.

***Step 7 (Learn Automation With Github Action)***

Why?

*   Automates testing, deployments, and CI/CD pipelines.
*   Reduces human errors and speeds up software delivery.

How to Learn?

*   Understand YAML-based workflows.
*   Automate testing and deployments with GitHub Actions.
*   Practice: Set up an action that runs on every git push.

***Step 8 (Learn About Web Server Like Nginx)***

Why?

*   Web servers host applications and manage traffic.
*   Used in reverse proxies, load balancing, and API gateways.

How to Learn?

*   Install and configure Nginx.
*   Learn reverse proxy, load balancing, and SSL setup.
*   Practice: Deploy a simple static website with Nginx.

***Step 9 (Learn Containerization Using Docker)***

Why?

*   Containers make applications portable and scalable.
*   Essential for modern cloud deployments and CI/CD.

How to Learn?

*   Understand Docker images, containers, volumes, networking.
*   Build, run, and manage Docker containers.
*   Practice: Containerize a simple Go or Python app.

***Step 10 (Learn Cloud Provider Like AWS)***

Why?

*   DevOps is heavily cloud-based, and AWS/Azure/GCP are industry standards.
*   Needed for infrastructure provisioning, scaling, and automation.

How to Learn?

*   Learn AWS basics (EC2, S3, IAM, VPC, Lambda).
*   Deploy a small application on the cloud.
*   Practice: Launch an EC2 instance and configure a web server.

***Step 11 (Learn Infrastructure Provisioning by Code - IaC Using Terraform)***

Why?

*   Automates infrastructure provisioning and management.
*   Used to define cloud resources in a consistent, reusable way.

How to Learn?

*   Learn how Terraform manages cloud infrastructure.
*   Write Terraform configurations for AWS/GCP.
*   Practice: Deploy an EC2 instance with Terraform.

***Step 12 (Learn Container Orchestration Using Kubernetes)***

Why?

*   Kubernetes manages multiple containers efficiently.
*   Enables high availability, auto-scaling, and self-healing applications.

How to Learn?

*   Learn about Pods, Deployments, Services, and Ingress.
*   Understand Kubernetes networking and scaling.
*   Practice: Deploy a web app in a Kubernetes cluster.

***Step 13 (Learn Logging and Infrastructure Monitoring)***

Why?

*   Monitoring is essential for identifying issues and optimizing performance.
*   Helps track server health, logs, and alerts.

How to Learn?

*   Learn Prometheus for metrics collection and Grafana for visualization.
*   Set up logging with ELK Stack (Elasticsearch, Logstash, Kibana).
*   Practice: Monitor a running Docker container with Prometheus.

* * *

## Summary:

DevOps is all about automating software development, deployment, and infrastructure management. To get started, begin by learning a programming language like Golang, as scripting is essential for automation. Understanding computer networking concepts such as IP addressing, DNS, and firewalls is crucial since DevOps involves managing servers and cloud environments. Since most DevOps tools and cloud servers run on Linux, mastering Linux commands and becoming comfortable with the terminal (CLI) will help you navigate and control systems efficiently. Bash scripting is another key skill that allows you to automate repetitive tasks like backups and log management.

Version control using Git is essential for tracking code changes and collaborating with teams, while learning GitHub Actions will help you automate testing and deployments through CI/CD pipelines. Since applications need to be hosted, understanding web servers like Nginx will allow you to manage traffic and serve applications efficiently. To make applications portable and scalable, Docker is used for containerization, allowing apps to run seamlessly across different environments.

Cloud platforms like AWS, Azure, or Google Cloud are widely used in DevOps, so learning how to deploy and manage cloud infrastructure is a must. Infrastructure as Code (IaC) with Terraform enables automated provisioning of cloud resources, making deployments more efficient. For managing multiple containers, Kubernetes is essential, as it helps with scaling and orchestrating workloads. Finally, monitoring tools like Prometheus and Grafana are used to track application and server performance, ensuring reliability and quick issue resolution.