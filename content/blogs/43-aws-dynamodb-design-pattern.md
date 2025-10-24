---
title: "AWS DynamoDB, A Key Value Pair Database - Part 2 (Design Patterns and Best Practices)"
description: "Let's learn the AWS dynamoDb"
date: 2025-10-25
tags: ["aws", "dynamoDb", "database", "key-value-pair-database"]
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
    image: "img/blogs/42-aws-dynamo-db.png"
    caption: "AWS DynamoDB"
    alt: "AWS DynamoDB"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [AWS DynamoDB, A Key Value Pair Database - Part 1 (Introduction)]({{< ref "blogs/42-aws-dynamodb-intro.md" >}})
---

{{< figure
    src="/img/blogs/42-aws-dynamo-db.png"
    caption="AWS DynamoDB (Photo Credit: AWS)"
    align=center
>}}

In this series, we try to explore AWS DynamoDB, a key-value pair database developed by AWS. In the previous part we were trying to explore the answers to some basic questions about AWS DynamoDB and introduce ourselves to DynamoDB. In this part we are trying to explore AWS DynamoDB design patterns and table design best practices so that we can utilize the power of it with minimum cost.

So let's get started...

---

## Data Modeling / Table Design
If you are from relational/SQL databases, then you are already familiar with database normalization. This means in a relational database we are trying to model our data into multiple smaller data with relationship references. But in a NoSQL database like Dynamo, unlike a relational database, we are trying to keep our data closer and in a single place. So it is clear that we need a different mindset than SQL databases when working with NoSQL databases.

## Data/Table Design Best Practices
General design principles in Amazon DynamoDB recommend that you keep the number of tables you use to a minimum. In the majority of cases, AWS recommends that you consider using a single table. When needed, you can design multi-tables also.

1. ***Single table design:***
DynamoDB stores items with the same partition key (known as an item collection) on the same partition(s) as each other. In this design, different types of data are stored as items in the same table, and each item is identified by a unique sort key. So single table design helps you to store multiple types (entities) of data in a single DynamoDB table. It aims to optimize data access patterns, improve performance, and reduce costs by eliminating the need for maintaining multiple tables and complex relationships between them.

**Advantages:**
- Data locality to support queries for multiple entity types in a single database call
- Reduces overall financial and latency costs of reads and multi-table management headaches
- Smooth traffic and fast query

**Disadvantages:**
- The learning curve can be steep due to the paradoxical design compared to relational databases.
- When using GraphQL, single table design will be more difficult to implement.
- All changed data will be propagated to DynamoDB Streams even if only a subset of entities needs to be processed.

2. ***Multiple table design:***
Multiple table design is a pattern that is more like a traditional database design where you store a single type (entity) of data in each DynamoDB table. Data within each table will still be organized by partition key, so performance within a single entity type will be optimized for scalability and performance, but queries across multiple tables must be done independently.

**Advantages:**
- Simpler to design for those who aren't used to working with single-table design
- Easier implementation of GraphQL resolvers due to each resolver mapping to a single entity (table)

**Disadvantages:**
- Multiple tables need to be queried individually, and it can cause performance issues.
- Multi-table management headache

## Best Practices For Key Component Design
- Keep the number of tables to a minimum (possibly a single table).
- Explore your data shape, data size, and data velocity, and keep related data together.
- For related data, use sort order by using a composite key, meaning a partition key and sort key.
- Use a secondary index, which can be a local or global secondary index based on the use case for performing the query.
- Design and choose the right partition key to distribute workloads.
- Use random suffixes with the partition key for balance and distribute workloads and better sharding.
- Choose the right sort key, which is easily comprisable, and add random similar prefixes. Use a sort key for versioning also.
- Choose and balance secondary indexes and use them for sharding, overloading, and aggregation.

## When To Use and When Not To Use DynamoDB
**When to use**:
- Key-value or simple queries
- Very high read/write rate
- Need auto-sharding
- Need on-line scaling across multiple nodes
- Consistently low latency
- No size or throughput limits
- No tuning
- High durability

**When not to use**:
- Need multi-item/row or cross table transactions
- Need complex queries or joins
- Need real time analytics on historic data

## DynamoDB Pricing
DynamoDB pricing depends on the following things:

- Read/write request
- Backup
- Tables
- Streams
- DAX
- Export

For better understanding please read the documentation on this [link](https://aws.amazon.com/dynamodb/pricing/on-demand/).

For cost optimization of DynamoDB, please read this [link](https://repost.aws/knowledge-center/dynamodb-optimize-costs).


---

### References / Sources:
- [Data modeling / Table design](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/data-modeling.html)
- [Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)
- [Pricing](https://aws.amazon.com/dynamodb/pricing/on-demand/)
- [Cost optimization](https://repost.aws/knowledge-center/dynamodb-optimize-costs)
- [**Sample Practice Project**](https://github.com/sir-rasel/rest-service-using-spring-boot-and-DynamoDB)