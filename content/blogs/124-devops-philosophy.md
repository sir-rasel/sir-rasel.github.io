---
title: "DevOps - Step By Step Learning: Part 1 (What it is, History, Philosophy, Practice)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-13T00:00:00Z"
tags: ["devops" , "devops-philosophy"]
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
    image: "img/blogs/124-devops-philosophy.jfif"
    caption: "DevOps Philosophy"
    alt: "DevOps Philosophy"
    relative: true
    hidden: true
---

{{< figure
    src="/img/blogs/124-devops-philosophy.jfif"
    caption="DevOps Philosophy (Photo Credit: LinkedIn Image)"
    align=center
>}}

## Story:

In 2021, Rasel just finished his university and marked himself as a fresher :). But fortunately he managed to get a job and joined as a “junior engineer” in a software firm. On his first day in the office, he spent most of his time fulfilling office formality and saying hi-hello with colleagues.

Within a few days, he started working and contributing to the project actively. But the organization's working patterns were something like the following:

1. Project managers, QA, or business people create/report tasks/bugs in an Excel sheet, and there is a column for status.
2. Then the engineer works on a task/bug from this Excel sheet and updates the status of the status column.
3. After development, the engineer notifies QA via message about the change.
4. QA test and update the status column in the Excel sheet.
5. The latest code needs to compile locally and create executables/build files and then share these with operation people.
6. After that, operation people SSH/log in to the server, back up the current state by copying the current files, and replace the current files with the shared latest build files.
7. Then, after successfully pasting, a manual command is run to restart the server.
8. Also, no standard shared/central version control is used efficiently.

So due to manual interaction, operations always tried to delay and sum up more work before deployment, but developers always wanted to deploy the fixes or changes as soon as possible due to customer/client satisfaction.

In this type of situation, after some months, he felt tired and upset. He thought, are these the actual patterns of working, or is there anything that has an efficient way that makes developers', QAs', operations', or other stakeholders' lives easy? So he started exploring for a better approach to save lives and found a term called "DevOps."

* * *

## What is DevOps?

DevOps is a set of practices and tools that combine software development (Dev) and IT operations (Ops) to deliver software faster and more reliably. It's based on the idea that better communication and collaboration between teams can lead to better software. 

📌 So in short DevOps is:

1.  Set of **practices**.
2.  Use of set of **tools** (primarily for automations).
3.  **Communication** and **Collaboration** between developers and operations for win win handshaking.

## History of DevOps

DevOps emerged in the late 2000s as a response to problems caused by the separation of development and operation teams.

📌 Key Events in DevOps History:

*   2007-2008: Software engineers noticed issues with slow software delivery and lack of collaboration between Dev and Ops.
*   2009: The first "**DevOps Days**" conference was held in Belgium. Belgian IT professional Patrick Debois coined the term "**DevOps**" in 2009.
*   2010s: The rise of cloud computing (AWS, Azure, GCP) made DevOps more necessary.
*   Today: DevOps is widely used, with tools like Docker, Kubernetes, Jenkins, and Terraform improving automation.

## Philosophy of DevOps

DevOps is not just about tools - it’s a culture that focuses on collaboration, automation, and continuous improvement.

📌 Key Principles of DevOps Philosophy:

1.  **Collaboration & Communication** - Dev and Ops work together as a single team.
2.  **Automation** - Everything from testing to deployment is automated.
3.  **Continuous Integration & Continuous Deployment (CI/CD)** - Software is built, tested, and deployed automatically.
4.  **Monitoring & Feedback** - Teams continuously track performance and improve. Focus on user needs and gather feedback to quickly address issues. 
5.  **Security (DevSecOps)** - Security is integrated from the beginning, not as an afterthought.

## DevOps Practices

DevOps is not a role, its all about mindset, collaboration, cultural shift and of-course follow standard working practices.

📌 Key Practices of DevOps:

1.  Use of centralized Version Control System (**VCS**) like GIT.
2.  **Automation** of every possible repetitive task.
3.  Follow proper planning and execution means be **Agile**.
4.  Manage servers and cloud infrastructure using code (**IaC**).
5.  Package applications so they run the same way everywhere (**Containerization**).
6.  Track system health and performance in real time (**Monitoring**).
7.  Automate **security** testing in the development pipeline.

* * *

## Summary:

So after a basic exploration about DevOps, Rasel could understand that it is not a role. It is all about collaboration, communication, culture and practices, achieve via set of tools and techniques. Then he pushed his organization and let them know about DevOps.