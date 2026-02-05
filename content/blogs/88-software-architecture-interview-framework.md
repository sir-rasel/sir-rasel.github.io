---
title: "Tale of Software Architect(ure): Part 6 (Framework for System Design Interview)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-06T00:00:00Z"
tags: ["software-architect", "software-architecture", "software-design"]
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
    image: "img/blogs/88-software-architect-interview.png"
    caption: "Software Architecture Interview Framework"
    alt: "Software Architecture Interview Framework"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 5:** [Tale of Software Architect(ure): Part 5 (Wrong Assumptions in Software Architecture and Fallacies of Distributed Computing)]({{< ref "blogs/87-software-architecture-fallacies.md" >}})
---

{{< figure
    src="/img/blogs/88-software-architect-interview.png"
    caption="Software Architecture Interview Framework (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the general framework of a system design interview.

So let's get started...

---

## Story
Jahanara, preparing for a system design interview, was tasked with designing a URL shortener. She began by clarifying the requirements, focusing on scalability, speed, and availability. After estimating the system's scale, she proposed a high-level design involving load balancers, app servers, NoSQL databases, and caching layers. She defined APIs and dove into low-level details like using Base62 for generating short URLs and sharding databases for scalability. Addressing bottlenecks, she suggested caching and database optimizations. In the end, Jahanara summarized her design, emphasizing key trade-offs, leaving the interviewer impressed with her structured approach.

---

## Framework for System Design Interview:
***1. Understand the Problem***
- **Goal**: Grasp the core problem you're solving. Before diving into the design, make sure you fully understand what the system needs to accomplish. Ask questions to clarify the high-level goals and constraints. This ensures that the solution aligns with the intended objectives.
- **Example**: If asked to design a URL shortening service (like bit.ly), understand the primary objective: mapping long URLs to short, easily shareable links.
- **What to do**: Restate the problem in your own words and confirm the high-level goal with the interviewer.

***2. Clarification of the Requirements***
- **Goal**: Get specific about what’s required to build the system. Break down the requirements, distinguishing between must-have features and nice-to-haves. Clarify ambiguities such as scalability, security, performance, or user expectations. This also includes understanding the non-functional requirements like latency, availability, and fault tolerance.

**Example**: For the URL shortener:
- *Functional requirements*: Create short URLs, redirect to long URLs when short links are accessed, and expiration of URLs.
- *Non-functional requirements*: Handle millions of users, low latency for redirects, high availability.

**What to do**: Ask questions like: 
- How many users?
- What level of consistency and availability is expected?
- Are there privacy or security concerns (e.g. access control)?
- What’s the expected response time or latency?

***3. Establish a Design Scope***
- **Goal**: Define the scope and avoid designing an overly complex system. Based on the requirements, define the boundaries of the system you're designing. This scope focuses on the essential components or features you need to implement in the interview timeframe, avoiding excessive complexity or off-track discussions.

**Example**: If designing a messaging service like WhatsApp:
- Focus on text messaging for now, leaving out features like file sharing or voice calls.
- Only consider basic encryption, deferring advanced privacy features.

**What to do**: Discuss with the interviewer what can be achieved in the given time. Choose the essential components to design while setting aside optional or advanced features.

***4. Back-of-the-Envelope Estimation***
- **Goal**: Estimate the scale to understand infrastructure needs. Estimate the scale and resources required for the system. For example, estimate the number of active users, requests per second, data storage, or bandwidth requirements. This gives you a sense of the infrastructure needs and challenges related to performance and scaling.

**Example**: For a URL shortening service:
- How many URLs will be shortened per day? Let’s assume 10 million requests/day.
- Estimation of storage: Assume each shortened URL takes 500 bytes; then for 10 million URLs per day, you’ll need approximately 5 GB/day.

**What to do**: Perform simple calculations for:
- Request rates (e.g. active users per second),
- Storage requirements,
- Bandwidth,
- Compute capacity (e.g. how many servers).

***5. Define Data Model***
- **Goal**: Design how data will be structured and stored. Outline how data will be structured and stored. This includes deciding between relational (SQL) or non-relational (NoSQL) databases and defining key entities, relationships, and their attributes. Consider the consistency, availability, and partition tolerance of the data.

**Example**: For a URL shortener:
- Store a mapping between a short URL (key) and a long URL (value).
- Use a NoSQL database like DynamoDB for speed, as you don’t need complex joins.
- Schema: { short_url: string, long_url: string, created_at: timestamp, expiration: timestamp }

**What to do**: Decide whether a relational database (e.g. MySQL, PostgreSQL, etc.) or NoSQL (e.g. MongoDB, Cassandra, etc.) is appropriate based on access patterns and scalability needs.

***6. Propose High-Level Design***
- **Goal**: Outline the architecture with major components and interactions. Draw a high-level architecture diagram that includes major components, their responsibilities, and how they interact. This could involve layers like load balancers, application servers, databases, and caching layers. Explain your decisions about how data and control flow through the system.

**Example**: For a URL shortener, a simple high-level design could include:
- Load balancer to handle incoming requests.
- Application servers to generate and store short URLs.
- NoSQL database to store URL mappings.
- Cache (e.g. Redis) to store frequently accessed URLs.

**What to do**: Draw or describe an architecture diagram:
- Components like databases, servers, caching layers, load balancers, etc. 
- Show how a request flows from the user to the backend and back.
- Identify where you need replication, failover, or redundancy.

***7. System Interfaces and APIs Definition***
- **Goal**: Define how clients interact with the system. Define how different parts of the system will communicate through interfaces or APIs. Clearly define what operations the system will support and how external entities will interact with it. Focus on RESTful APIs, RPCs, or WebSockets depending on the use case.

**Example**: For a URL shortener, API definitions might include:
- POST /shorten – Accepts a long URL and returns a short one.
- GET /{short_url} – Redirects to the corresponding long URL.
- DELETE /{short_url} – Deletes a short URL mapping if it has expired.

**What to do**: Clearly define the input and output of each endpoint, the protocol used (e.g. REST or gRPC), and the status codes or errors that might be returned.

***8. Design Deep Dive (Low-Level Design)***
- **Goal**: Go deeper into specific components, algorithms, or trade-offs. Zoom into one or two core components of your system to provide a more detailed design. This could include database schemas, internal logic of key components, algorithms, caching strategies, or how you handle concurrency and distributed systems issues.

**Example**: For a URL shortener:
- How to generate unique short URLs: Use hash functions or a Base62 encoding scheme to create short links.
- Caching strategy: Cache frequently accessed short URLs in Redis to reduce load on the database.
- Consistency trade-offs: Decide between eventual consistency (using distributed systems like Cassandra) vs. strong consistency (using traditional databases).

**What to do**: Focus on a critical piece of the system, like database partitioning, load balancing algorithms, or API rate limiting.

***9. Identifying and Resolving Bottlenecks***
- **Goal**: Analyze performance and scaling issues, then propose optimizations. Analyze potential bottlenecks such as network latency, database load, or computational limits. Propose solutions to address these, such as introducing sharding, load balancing, caching, or data replication strategies to improve performance and fault tolerance.

**Example**: For a URL shortener:
- Bottleneck: Database write contention when millions of URLs are being generated per second.
- Solution: Implement database sharding based on the first letter of the short URL to distribute load.
- Bottleneck: Slow lookup times for popular URLs.
- Solution: Add a caching layer (e.g., Redis) for hot URLs to reduce database lookups.

**What to do**: Highlight potential performance issues and propose solutions like horizontal scaling, replication, caching, load balancing, or queuing.

***10. Wrap Up (Finishing Touch)***
- **Goal**: Summarize the design and highlight key trade-offs or decisions. Summarize your design, highlighting key decisions and trade-offs. Reflect on any additional considerations, such as scaling for future growth, monitoring and logging, or security concerns. Ensure you’ve covered the key parts and are ready to take questions or discuss alternatives.

**Example**: For a URL shortener:
- Trade-off: Chose eventual consistency for better performance and scalability.
- Highlighted: Using a cache to reduce latency, database sharding for better distribution, and fault tolerance measures like backup and replication.

**What to do**: Restate the key components and decisions:
- Mention scalability and fault tolerance considerations.
- Note any open questions or future improvements (e.g. more robust security, better analytics).
- Be ready to discuss why you chose certain trade-offs or how the system will evolve.

---

## Summary:
In this system design interview, we can follow an essential framework for system design interviews. Like: understand the problem, clarify the requirements, establish a design scope, back-of-the-envelope estimation, define the data model, propose high-level design, define system interfaces and APIs, conduct a deep dive (low-level design), identify and resolve bottlenecks, and finally wrap up (finishing touch). By following this well-established framework, we can impress in the interview, hopefully.