---
title: "All About Software Engineering: Part 3 (Involved Parties at Different Stages of SDLC)"
description: "Let's learn the software engnieering differently!"
date: "2025-12-01T00:00:00Z"
tags: ["software-engineering"]
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
    image: "img/blogs/65-sdlc-parties.jpeg"
    caption: "Involved Parties at SDLC"
    alt: "Involved Parties at SDLC"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [All About Software Engineering: Part 2 (Software Development Life Cycle (SDLC) and Process Models)]({{< ref "blogs/64-software-engineering-sdlc.md" >}})
- **Part 4:** [All About Software Engineering: Part 4 (Challenges in Modern Software Engineering)]({{< ref "blogs/66-software-engineering-challenges.md" >}})
---

{{< figure
    src="/img/blogs/65-sdlc-parties.jpeg"
    caption="Involved Parties at SDLC (Photo Credit: Google)"
    align=center
>}}

In this series, we try to explore software engineering in a modern way. We will try to learn the different software engineering aspects one by one. In this part, we try to explore the different parties involved at software develpment life cycle (SDLC).

So let's get started...

---

## Story
Up until now, Shuvo and Tapu have studied the engineering and scientific aspects of software engineering. In addition, they established the necessity in their early attitude. They also go over several process models, the software process, and the SDLC again.

They now want to know who is participating and in what position at each step of the software development life cycle. They would need a brief explanation of their role in the SDLC and its relevance.

---

## Involved Parties at Different Phases of SDLC:

***Stage 1: Brainstorming & setting goals***

Business objectives and goals determination stage.
- **Stockholders/clients**: Sometimes stockholders or clients directly define the goals or wants they need. Basically a freelance or outsource-type company gets goals from its clients.
- **Business Analyst**: In a product-based company, business analysts set goals by analyzing the market and interviewing their customers. Basically they stay under the commercial department of an organized company.

***Stage 2: Requirement analysis & planning***

Stage of defining the functionality, features, and constraints of the software system to be developed based on stage 1 results.
- **Product manager**: PMs are responsible for the overall success of the product, from conception to launch and beyond. They focus on defining the product vision, strategy, and roadmap, as well as overseeing its execution. They are working closely with cross-functional teams, including design, engineering, and marketing, to execute the product roadmap.
- **Architecture & Engineering**: When PMs design the features and requirements, then software architects and engineers validate the requirements. Are the requirements technically feasible or not, etc.? They help PMs for planning.

***Stage 3: Design & Architecture***

Stage of selecting appropriate technologies and defining the system's structure, interfaces, modules, and data architecture.
- **Software architect**: Design and architect the individual software component from high level to low level. Address the business requirements and cost when designing.
- **Lead/Staff Engineer**: Analyzes the feasibility and helps the architect if fine-tuning is needed in the design in terms of coding/implementation.
- **DevOps/SRE**: Analyze the feasibility and help the architect if fine-tuning is needed in the design in terms of infra/deployment pipeline.

***Stage 4: Coding & Implementation***

Writing code, testing code, and integrating code are the parts of this phase.
- **Software engineer/developer/programmer**: Simply, they convert the requirements into code so that the machine can understand. So software engineers/developers/programmers write code in this phase based on the requirements and system architecture design.

***Stage 5: Testing & QA***

The testing phase verifies that the software meets its requirements and functions correctly by designing, executing, and evaluating test cases and ensuring quality.
- **SQA**: They perform manual testing and automated testing to ensure the functional requirements.
- **Security Tester**: They perform the security-related testing rather than the functional testing of the system.
- **Performance Tester**: They are also known as load testers or stress testers. They test the performance of the implemented software system and benchmark the system based on load.

***Stage 6: Deployment***

Deployment involves installing, configuring, and distributing the software to production.
- **DevOps/SRE**: They are responsible for provisioning different environment servers and configuring the pipeline for CI/CD and deployment of the software.

***Stage 7: Maintenance & feedback***

The maintenance phase involves ongoing support, monitoring, and maintenance of the software after deployment.
- **Service Operation**: Monitor the system, report unusual incidents to the responsible party, analyze the log for any complaints or bugs, etc.
- **Support Engineer**: Gives on-call support to the customer, fixes bugs, identifies and improves performance, etc.

Outside of all of the above-mentioned parties, 2 other parties are involved in software engineering indirectly in some big organizations. They are the **network engineer** and **system engineer**.

A network engineer is responsible for smooth and secure internet connection. This connection can be server machines or other devices related to the software development.

On the other hand, the system engineer is responsible for managing the data centers and their related staff.

---

## Summary:

The majority of individuals mistakenly believe that software engineering is limited to writing code. Even while coding plays a big role, every other component is as crucial. Effective, user-focused, and high-quality software that exclusively addresses problems in real life may be created by a well-coordinated team from every department.

All the above roles or parties' segregation can vary based on the company size and structure. But the idea should remain something of a similar type.