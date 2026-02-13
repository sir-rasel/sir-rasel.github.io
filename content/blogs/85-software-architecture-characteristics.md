---
title: "Tale of Software Architect(ure): Part 3 (Characteristics of Software Architecture)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-03T00:00:00Z"
tags: ["software-architect", "software-architecture", "software-design", "architecture-characteristics"]
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
    image: "img/blogs/85-software-architect-characteristics.png"
    caption: "Software Architecture Characteristics"
    alt: "Software Architecture Characteristics"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [Tale of Software Architect(ure): Part 2 (Role of Software Architect and Knowledge To Have)]({{< ref "blogs/84-software-architecture-architect.md" >}})
- **Part 4:** [Tale of Software Architect(ure): Part 4 (Things Should Consider When Design/Architect a Software System)]({{< ref "blogs/86-software-architecture-considerations.md" >}})
---

{{< figure
    src="/img/blogs/85-software-architect-characteristics.png"
    caption="Software Architecture Characteristics (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the characteristics of software architecture.

So let's get started...

---

## Story
A well-known company named **UraDhura** is growing rapidly day by day, and thus their current software system was struggling to keep up with the increasing number of shipments, customers, and new services. So the CEO decided it was time to revamp their architecture. She gathered her team of software architects, including **Pagla**, the lead architect, to design a new system.

At the first meeting, the CEO laid out the business goals like "We need to handle ten times the current load in the next two years," "Our customers expect real-time tracking of their shipments," and "Data breaches are a no-go." The team also knew that as a well-known company, the system needed to be reliable to ensure 24/7 **availability**.

After that, Pagla, the lead architect, talks with other stakeholders of the system, like software engineers, DevOps, IT support, the legal team, etc., for understanding their needs and pain points. Finally, he designs an architecture and makes some **tradeoff** decisions, and after developing, he reevaluates and measures the architecture.

---

## 4 Dimensions of Software Architecture an Architect Needs to Tackle:
1. **Structure**:
Structure refers to how the software system is organized and decomposed into various components, layers, modules, or services.

2. **Architecture Characteristics**:
Architecture characteristics are often referred to as non-functional requirements (NFRs). These are the qualities or attributes that the architecture should exhibit.

3. **Architecture Decisions**:
Architecture decisions refer to the choices made in designing the system's architecture. These include the selection of technology stacks, patterns, deployment models, and integration strategies.

4. **Design Principles**:
Design principles are the guidelines that steer the development of the architecture to ensure it adheres to certain qualities.

---

## Characteristics of Software Architecture:
Architecture characteristics, also known as non-functional requirements (NFRs) or quality attributes, define the system’s operational qualities beyond its basic functional requirements. These characteristics directly impact the system’s performance, scalability, security, and maintainability.

There are different categories of architecture characteristics based on the concerns they address. Typically, these characteristics are grouped into **Operational**, **Structural**, and **Cross-Cutting** architecture characteristics. Let’s explore each category in detail:

1. **Operational Architecture Characteristics**
Operational characteristics deal with the runtime behavior of the system. They define how the system should behave when deployed and in operation. These qualities impact the end-user experience, system performance, and overall efficiency.
- **Performance**: Defines how fast a system performs under a specific load. This includes response times, latency, and throughput. Performance is often influenced by the system’s ability to process data efficiently and handle concurrent users or requests.
- **Scalability**: The system’s ability to handle growth, either vertically (by upgrading hardware) or horizontally (by adding more machines). Scalability is essential when anticipating future growth in user traffic or data.
- **Availability**: Refers to the system's ability to be operational and accessible. Measured in terms of uptime, availability is often expressed as a percentage (e.g., 99.99% availability). This characteristic impacts Service Level Agreements (SLAs).
- **Reliability**: The system’s capability to perform consistently over time without failure. It includes features like error detection, fault tolerance, and redundancy to ensure that the system remains stable.
- **Security**: Ensures the protection of the system’s data and resources from unauthorized access and cyber-attacks. It includes encryption, authentication, authorization, and regular audits to maintain integrity and confidentiality.
- **Recoverability**: How quickly and efficiently the system can recover from failures. This includes data backup and restoration processes, disaster recovery strategies, and failure handling mechanisms.
- **Elasticity**: The ability of the system to dynamically scale resources up or down in response to changing demands without affecting service availability.

2. **Structural Architecture Characteristics**
Structural characteristics focus on the internal design of the system. They define how the system is organized and how its various components interact with each other.
- **Modularity**: The degree to which the system is composed of discrete components or modules, each with a specific responsibility. A modular architecture facilitates independent development, maintenance, and scaling.
- **Cohesion**: Refers to how closely related and focused the responsibilities of a module or component are. High cohesion within a module leads to more maintainable and understandable code.
- **Coupling**: Refers to the degree of dependency between modules. Loose coupling means that modules are less dependent on each other, making the system more flexible and easier to change.
- **Extensibility**: The ability of the system to be extended with new features or components without affecting existing functionality. This is often achieved through well-defined interfaces and modular design.
- **Flexibility**: The ease with which the architecture can adapt to changing requirements, such as adding new features, modifying existing components, or integrating with external systems.
- **Portability**: The ability of the system to run in different environments, such as different operating systems or hardware platforms, without requiring major changes. Portability is essential when considering cloud deployment or multi-platform support.
- **Maintainability**: The ease with which the system can be updated, fixed, and improved over time. High maintainability allows the system to evolve with minimal technical debt.
- **Configurability**: Ability for end users to easily change aspects of the software's configurations.
- **Upgradeability**: Ability to easily/quickly upgrade and support change.

3. **Cross-Cutting Architecture Characteristics**
Cross-cutting characteristics are those that affect multiple parts of the system. These attributes often do not belong to one specific module but influence the entire system or several subsystems. They require careful architectural planning because they impact the system globally.
- **Accessibility**: Access all your users, including those with disabilities. 
- **Privacy**: Ability to hide transactions from internal company employees (encryption, decryption). Proper authentication and authorization are in place.
- **Security**: Although also an operational characteristic, security spans across the entire system architecture. This includes not only runtime concerns like authentication and encryption but also secure coding practices, secure deployment, and access control at multiple layers of the architecture.
- **Usability**: This deals with how easy it is for end-users to interact with the system. It impacts the design of the user interface (UI), user experience (UX), and system feedback mechanisms. Usability is often overlooked in architecture but can impact the system's success or failure.
- **Interoperability**: The ability of the system to work with other systems or components, especially external systems. Interoperability involves designing APIs, data formats, and protocols to ensure seamless interaction with third-party systems.
- **Testability**: The extent to which the system can be tested efficiently. Testability is related to the system's modularity and loose coupling. High testability ensures that components can be independently tested, and comprehensive testing strategies can be employed (e.g., unit tests, integration tests).
- **Auditability**: The ability of the system to provide a record of its operations and changes. This characteristic is crucial in regulated industries where audits are required to ensure compliance with standards (e.g., financial, healthcare).
- **Observability**: Observability is the ability to understand the internal state of a system by examining its outputs, typically through logs, metrics, and traces. This helps in monitoring, debugging, and optimizing the system in real time.
- **Compliance/Legal**: Systems in industries such as healthcare, finance, and government must comply with regulations and standards (e.g., GDPR, HIPAA). Compliance ensures that the system operates within legal and industry requirements.
- **Globalization and Localization**: The ability of the system to support multiple languages, regions, and cultural conventions (e.g., different date formats and currencies). This is important for systems intended for global audiences.

---

## Identifying Architecture Characteristics:
Identifying architecture characteristics involves understanding the system’s key requirements and the quality attributes that will shape its architecture. This can be broken down into the following steps:

### Steps to Identify Architecture Characteristics
1. **Understand Business Goals**:
- Talk to stakeholders to understand the business needs and goals for the system. Ask questions like: What level of performance is expected? How important is security for the system? Will the system need to scale significantly in the future?
- Business goals often directly translate into architecture characteristics. For example, a business need for 24/7 service availability will translate into characteristics like high availability and reliability.

2. **Analyze Functional Requirements**:
- Look at the system’s functional requirements to infer the non-functional ones. For example, a requirement to process financial transactions implies security and performance are important.

3. **Consider Stakeholder Priorities**:
- Different stakeholders (e.g. users, developers, IT staff) may have different priorities. For instance: End-users might prioritize usability. Developers may care about maintainability. IT staff may focus on scalability and deployability.

4. **Review Compliance and Regulatory Needs**:
- Some architecture characteristics are driven by industry standards, legal regulations, or compliance. For example: Security characteristics are mandatory in finance and healthcare systems. Auditability may be essential for regulatory compliance.

5. **Look at the System Context**:
- Consider external systems the architecture will interact with (e.g. third-party APIs, legacy systems). This can help identify characteristics like interoperability and portability.

6. **Use Architectural Frameworks**:
- Utilize well-known frameworks like ISO/IEC 25010 (for software quality models) or the Quality Attribute Workshop (QAW), which helps prioritize and document important architecture characteristics.

---

## Measuring Architecture Characteristics
Once identified, it’s essential to measure these characteristics to validate the architecture. Some characteristics can be measured quantitatively, while others are more qualitative.

### Steps to Measure Architecture Characteristics
1. **Define Measurable Metrics**:
- For each characteristic, define specific metrics or Key Performance Indicators (KPIs) that will help measure success. These should be: Quantitative where possible (e.g. response time, CPU utilization). Qualitative for characteristics like usability or maintainability, which may rely on expert reviews or user feedback.

2. **Establish Baseline and Target Values**:
- Determine the current performance (baseline) for each characteristic and set target values based on business goals and stakeholder expectations. For example, availability might be set at 99.95%, or performance might target a response time of <200ms for 90% of requests.

3. **Use Benchmarks and Simulations**:

For characteristics like performance, scalability, and availability, use benchmarking tools or simulations:
- **Performance Testing**: Tools like JMeter or LoadRunner can simulate load and measure response times.
- **Scalability Testing**: Use cloud-based scaling simulations to test how well the system handles additional users or requests.
- **Availability Monitoring**: Tools like Nagios or New Relic can monitor uptime and fault-tolerance mechanisms.

4. **Monitor in Real-time**:

Use monitoring tools and APMs (Application Performance Management) to continuously track system behavior in production.
- **Performance**: Monitoring CPU, memory usage, or response times using tools like Prometheus, Grafana, or Datadog.
- **Security**: Security audits, vulnerability scanners, and penetration testing can help measure security over time.

5. **Collect User and Developer Feedback**:

For more qualitative characteristics like usability or maintainability, feedback from end-users and developers is crucial.
- **Usability**: Measure using tools like Google Analytics (time on page, bounce rates) or user surveys.
- **Maintainability**: Measure using metrics like code churn (how often code is modified), defect rates, and time to resolve issues.

6. **Measure Technical Debt**:
- Tools like SonarQube can assess code quality and detect issues that affect maintainability, extensibility, or testability. Metrics like code complexity, duplication, and code smells indicate architecture health.

7. **Risk Analysis**:
- For characteristics like security and reliability, perform risk analysis using tools like Failure Mode and Effects Analysis (FMEA) or threat modeling to anticipate issues and track how well mitigations are working.

## Common Metrics for Architecture Characteristics: (Characteristic vs Possible Metrics)
- **Performance**: Response time, latency, throughput, resource utilization.
- **Scalability**: Number of concurrent users supported, resource consumption under load.
- **Availability**: Uptime percentage, Mean Time Between Failures (MTBF), Mean Time to Repair (MTTR).
- **Security**: Number of vulnerabilities, time to patch, unauthorized access incidents.
- **Maintainability**: Defect density, time to resolve defects, code complexity (Cyclometric complexity).
- **Extensibility**: Time to add a new feature, number of code changes for new functionality.
- **Usability**: User satisfaction scores, task completion time, error rates.
- **Reliability**: Failure rates, system downtime, successful transactions.
- **Portability**: Number of environments supported, number of issues when migrating.
- **Interoperability**: Number of integrations, success rate of interactions with external systems.

### Example: Measuring Performance
If you need to measure performance, you can define specific metrics like:
- **Response time**: The time taken for the system to respond to a user request. Target: <200ms for 90% of requests.
- **Throughput**: The number of requests the system can handle per second. Target: 1,000 requests/second under peak load.
- **Resource Utilization**: CPU and memory usage under load. Target: CPU utilization should not exceed 80% during peak periods.

### Example: Measuring Security
For security, measurement might involve:
- **Number of vulnerabilities**: Track how many security vulnerabilities are detected and patched.
- **Time to patch**: The time it takes from detecting a vulnerability to deploying a fix. Target: <24 hours for critical vulnerabilities.
- **Penetration Test Results**: The number of successful/unsuccessful attempts to breach the system during a penetration test.

---

## Managing Trade-offs Between Architecture Characteristics
An architect often faces trade-offs between various architecture characteristics. For example:
- **Performance vs. Security**: Implementing security features like encryption can reduce system performance.
- **Scalability vs. Consistency**: In distributed systems, achieving high scalability may come at the cost of strong consistency (as in the CAP theorem).
- **Flexibility vs. Performance**: A highly flexible system that allows easy configuration and extension might have slower performance due to the additional abstractions.

The key to effective architecture design is balancing these trade-offs to meet the system's most critical business and technical needs.

---

## Summary:
In software architecture, focusing on characteristics such as operational performance, structural modularity, and cross-cutting concerns like security and usability ensures a system that not only works but is maintainable, scalable, and adaptable over time. An architect must carefully consider how these characteristics interact and balance them according to the system's goals and context.