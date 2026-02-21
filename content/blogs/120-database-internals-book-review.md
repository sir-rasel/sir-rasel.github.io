---
title: "Book Review and Takeaways: (Database Internals: A Deep Dive into How Distributed Data Systems Work)"
description: "Let's learn the fundamental database concepts!"
date: "2026-02-08T00:00:00Z"
tags: ["database-internals-book" , "book-review"]
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
    image: "img/blogs/120-database-internals-book.png"
    caption: "Database Internals Book"
    alt: "Database Internals Book"
    relative: true
    hidden: true
---

---
### Detailed Database Series:
- **Part 1:** [Journey To Database World: Part 1 (Data, Record, Information, Historic Evaluation of Data Store, Database)]({{< ref "blogs/108-database-intro.md" >}})
---

{{< figure
    src="/img/blogs/120-database-internals-book.png"
    caption="Database Internals Book (Photo Credit: Google)"
    align=center
>}}

## Book Introduction

"**Database Internals: A Deep Dive into How Distributed Data Systems Work**" by Alex Petrov is a technical book that explores how modern databases work under the hood. It covers key concepts like storage engines, indexing, concurrency control, transaction management, and distributed systems. The book explains both traditional and distributed databases, helping readers understand the design trade-offs behind different architectures. It’s great for software engineers, database enthusiasts, and anyone curious about the inner workings of data systems.

## About Author(s)

According to the book, **Alex Petrov** is a data infrastructure engineer, database and storage systems enthusiast, Apache Cassandra committer and PMC member, interested in storage, distributed systems and algorithms.

## High Level Overview

The book is divided into two main parts:

1.  **Storage Engines & Single-Node Databases** – This section explains the core components of database storage, including different data structures like B-Trees and LSM-Trees, indexing mechanisms, write-ahead logging, and concurrency control. It dives into how databases manage durability, consistency, and transactions at a single-node level.
2.  **Distributed Systems & Databases** – The second part focuses on distributed database architectures, covering concepts like replication, sharding, consensus algorithms (e.g., Raft, Paxos), and distributed transactions. It explores the trade-offs between consistency, availability, and partition tolerance (CAP theorem) in distributed systems.

* * *

## Key Takeaways

**Storage Engine Fundamentals:**

*   Databases rely on two main storage engine types: B-Tree-based (used in relational databases) and LSM-Tree-based (common in NoSQL systems like Cassandra and RocksDB).
*   Write-ahead logging (WAL) ensures durability by persisting changes before applying them to data structures.
*   Concurrency control (e.g., locks, MVCC) prevents conflicts when multiple users access the database simultaneously.

**Transactions and Consistency:**

*   ACID (Atomicity, Consistency, Isolation, Durability) properties define transactional integrity.
*   Isolation levels (e.g., Read Committed, Repeatable Read, Serializable) balance consistency and performance.
*   Optimistic and pessimistic concurrency control help manage concurrent access.

**Distributed Database Architecture:**

*   Sharding divides data across multiple nodes for scalability.
*   Replication (leader-follower, multi-leader) improves availability and fault tolerance.
*   Distributed transactions are complex due to network failures and require protocols like Two-Phase Commit (2PC) or more resilient alternatives.

**Consensus and Coordination:**

*   Consensus algorithms like Paxos and Raft help distributed databases agree on a single truth despite failures.
*   Leader election ensures one node coordinates writes, reducing conflicts.
*   CAP theorem forces trade-offs between Consistency, Availability, and Partition tolerance - you can't have all three simultaneously.

**Trade-offs in Database Design:**

*   Choosing between consistency and availability depends on use cases (e.g., banking vs. social media).
*   LSM-Trees optimize write-heavy workloads, while B-Trees work better for read-heavy operations.
*   Distributed databases must balance latency, fault tolerance, and scalability.

* * *

## Conclusion

This book provides a deep yet practical understanding of how modern databases function, from storage engines to distributed systems. It highlights key trade-offs in database design, including consistency, availability, and performance. By exploring fundamental data structures, transaction management, and distributed architectures, the book empower engineers with the knowledge to build and optimize scalable data systems.