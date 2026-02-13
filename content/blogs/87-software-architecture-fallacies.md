---
title: "Tale of Software Architect(ure): Part 5 (Wrong Assumptions in Software Architecture and Fallacies of Distributed Computing)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-05T00:00:00Z"
tags: ["software-architect", "software-architecture", "software-design", "fallacies-of-distributed-system"]
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
    image: "img/blogs/87-software-architect-fallacies.png"
    caption: "Software Architecture Fallacies"
    alt: "Software Architecture Fallacies"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 4:** [Tale of Software Architect(ure): Part 4 (Things Should Consider When Design/Architect a Software System)]({{< ref "blogs/86-software-architecture-considerations.md" >}})
- **Part 6:** [Tale of Software Architect(ure): Part 6 (Framework for System Design Interview)]({{< ref "blogs/88-software-architecture-interview-framework.md" >}})
---

{{< figure
    src="/img/blogs/87-software-architect-fallacies.png"
    caption="Software Architecture Wrong Assumptions and Fallacies (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the wrong assumptions and fallacies of distributed systems everyone makes.

So let's get started...

---

## Story
In the company called **SobaiVala** (all are good), a development team, led by **ValaManush** (good man), makes several wrong assumptions while building a distributed application. They assume users will have fast internet, the network will always be reliable, and their system architecture will remain static. These fallacies lead to performance issues, crashes, and user complaints as the app struggles with slow connections, network failures, and scalability problems. Eventually, the team learns to expect failure and redesigns the system with error handling, retry mechanisms, and more flexible architecture, turning their flawed project into a resilient and successful platform.

---

## Wrong Assumption in Software Design/Architecture:
Wrong assumptions stem from incorrect or incomplete understanding of the environment, users, or system requirements. These assumptions can be implicit or explicit, and they typically lead to software that does not perform as expected. Here are some examples:
- **Assuming the users will behave in a specific way**: Designers often make assumptions about how users will interact with the software. If these assumptions are wrong (e.g., assuming all users are tech-savvy), the user experience can be poor.
- **Assuming perfect network conditions**: Architects may assume that network connectivity will always be stable and reliable. In reality, users may experience slow or intermittent connections, leading to performance issues if the system isn’t designed to handle such cases.
- **Assuming unlimited system resources**: Another common assumption is that the system will have abundant memory, CPU, or storage. This can lead to inefficient designs that consume more resources than necessary, causing performance degradation under heavy load.
- **Assuming that a component will always behave correctly**: When designing software, developers may assume that a third-party library, API, or external service will always function as expected. However, services can fail or return unexpected responses, leading to system crashes if not properly handled.
- **Assuming static or unchanging requirements**: This is a frequent assumption that results in systems that are difficult to modify or scale. Designers may fail to account for future changes in business needs, user growth, or technological advancements.
- **The product only needs to work on modern devices**: Assuming users won’t access the software on outdated hardware or browsers, potentially leading to compatibility issues.
- **Security isn’t a major concern yet**: Thinking security measures can be postponed for later development phases can lead to vulnerabilities being introduced early and exploited.
- **Scaling won’t be needed until much later**: Assuming the system can handle future growth without planning for scalability from the start may cause performance issues when the user base increases.
- **Data is always consistent**: Assuming that databases or distributed data sources are always up-to-date and in sync, which can lead to errors in data retrieval and integrity.
- **Upgrades will go smoothly**: Assuming that updating systems, libraries, or dependencies will be straightforward, ignoring potential integration issues or conflicts with legacy code.
- **Dependencies will always work as expected**: Assuming third-party libraries, APIs, or services won’t change or have outages can cause system failures when external components don’t behave as expected.
- **Bug fixes won’t introduce new bugs**: Assuming that fixing a bug won’t introduce regressions or new issues elsewhere in the system.
- **The team’s knowledge is enough**: Assuming that the team has all the expertise needed for a project without consulting domain experts, leading to potential blind spots in the design.

---

## Fallacies of Distributed Computing:
The fallacies of distributed computing are a well-known set of incorrect assumptions that architect's and engineers often make when dealing with distributed systems. These fallacies were first identified by *Peter Deutsch* and later expanded. They highlight the complexity of distributed systems and how assumptions about network behavior can lead to flawed software. The fallacies include:
- **The network is reliable**: This assumes that the network will always deliver messages as expected. In reality, networks can drop packets, connections can fail, and data may not arrive as expected. Systems must be designed to handle network failures.
- **Latency is zero**: This fallacy assumes that communication over the network is instantaneous. In distributed systems, latency is inevitable and can vary widely based on network conditions. Ignoring latency can lead to performance bottlenecks.
- **Bandwidth is infinite**: Designers may assume that the network can handle unlimited data, but in reality, bandwidth is limited and often shared with other services. This can result in slow data transfers and degraded system performance.
- **The network is secure**: Assuming that data transmitted over the network is safe can lead to security vulnerabilities. Distributed systems must account for the possibility of interception, tampering, and unauthorized access.
- **Topology doesn’t change**: This fallacy assumes that the network's structure will remain static. In practice, networks change frequently due to hardware failures, scaling, and load balancing, requiring dynamic adaptation in the system design.
- **There is only one administrator**: It’s easy to assume that a single entity manages all parts of the distributed system, but in reality, there may be multiple administrators with varying priorities and levels of access.
- **Transport cost is zero**: This fallacy assumes that transferring data over the network is free in terms of both performance and monetary cost. Network communication incurs costs in terms of bandwidth, power, and often, financial expenses.
- **The network is homogeneous**: Designers might assume that all network components behave similarly. However, different network segments can have varying speeds, security measures, and behaviors, which need to be considered.

## Other Common Design Fallacies:
Beyond distributed computing, there are other common fallacies in software design and architecture:
- **More code means better design**: Some developers believe that writing more code or adding more features leads to better software. In reality, simplicity often leads to better maintainability, readability, and performance.
- **All code can be reused**: While code reuse is often encouraged, assuming that all code can be reused without modification is unrealistic. Reuse often requires refactoring and adaptation to fit into new contexts.
- **Testing can catch all bugs**: While thorough testing is crucial, it’s a fallacy to assume that testing can uncover all bugs. Some issues, especially those related to performance, concurrency, or rare edge cases, may only surface in production environments.
- **Premature optimization improves efficiency**: Optimizing too early in the design process can lead to unnecessary complexity. It’s often better to first focus on clarity and correctness, optimizing only when performance becomes a measurable issue.
- **Monolithic architecture is more maintainable**: While simpler at the outset, monolithic architectures can become highly complex as they grow. Microservices or modular approaches can offer greater flexibility and scalability in large systems.
- **State is always synchronized**: In distributed systems, assuming that all nodes or components have the same data or state at the same time can lead to inconsistencies and errors.
- **Service calls are always successful**: Assuming that service-to-service calls (like microservices or APIs) always succeed without accounting for timeouts or partial failures.
- **The system can handle infinite traffic**: Assuming the system will scale horizontally without any architectural bottlenecks, which can lead to unanticipated capacity limits.
- **Time is consistent across systems**: Assuming that all parts of a distributed system share the same time (clock synchronization) can lead to issues in time-sensitive operations like event ordering or logging.
- **Caching is a universal performance booster**: Assuming that caching will always improve performance, without accounting for cache invalidation or the complexity of keeping cached data accurate.
- **Hardware is infallible**: Assuming the underlying hardware (servers, disks, etc.) will never fail can lead to catastrophic data loss or downtime without redundancy and failover mechanisms.
- **Load balancing is perfect**: Assuming that load balancers will distribute traffic evenly across servers without considering hot spots, misconfigurations, or performance variations.
- **The database is always available**: Assuming that databases will be online and responsive at all times without accounting for potential downtime or network partitions.
- **Testing environments match production**: Assuming that a test environment perfectly replicates production conditions, which can lead to undetected issues that only surface after deployment.
- **Encryption makes everything secure**: Assuming that encrypting data guarantees security without considering potential attack vectors such as data leaks, misconfigured encryption, or attacks on data in use.

---

## How to Avoid Wrong Assumptions and Fallacies:
Test under real-world conditions: Ensure that the software is tested under the conditions it will experience in production. This includes testing for network failures, performance under load, and user behavior.
- **Anticipate failure**: Design systems with failure in mind. This means using techniques like retries, circuit breakers, and redundancy to handle failures gracefully.
- **Use monitoring and logging**: Actively monitor system behavior to detect issues early. Logging can help track down the root cause of failures, enabling faster resolution.
- **Understand the environment**: Developers need a deep understanding of the operating environment, including network conditions, hardware constraints, and user needs. This helps in making informed design decisions.
- **Embrace flexibility and change**: Design software with the expectation that requirements and environments will change. This involves modular architectures, loose coupling, and clear documentation.
- **Design for scalability and change**: Start with scalability and flexible requirements in mind, anticipating future growth or changes in technology and usage patterns.
- **Automate testing and monitoring**: Constantly test and monitor systems to detect failures early, especially in distributed systems.

---

## Summary:
In software design and architecture, wrong assumptions and fallacies often lead to failures. Wrong assumptions include believing that users will always behave a certain way, that network conditions will be perfect, or that system resources are unlimited. These can cause software to underperform or fail under real-world conditions.

The fallacies of distributed computing highlight common misconceptions, such as assuming the network is reliable, latency is zero, bandwidth is infinite, and the network is secure. Ignoring these realities can lead to performance bottlenecks, crashes, and security vulnerabilities.

To avoid these pitfalls, software should be designed with flexibility, real-world testing, and failure handling in mind. By anticipating change and preparing for unexpected conditions, developers can build more resilient and adaptable systems.