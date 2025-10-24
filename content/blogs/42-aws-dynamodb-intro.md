---
title: "AWS DynamoDB, A Key Value Pair Database - Part 1 (Introduction)"
description: "Let's learn the AWS dynamoDb"
date: 2025-10-24
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
- **Part 2:** [AWS DynamoDB, A Key Value Pair Database - Part 2 (Design Patterns and Best Practices)]({{< ref "blogs/43-aws-dynamodb-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/42-aws-dynamo-db.png"
    caption="AWS DynamoDB (Photo Credit: AWS)"
    align=center
>}}

In this series, we try to explore AWS DynamoDB, a key-value pair database developed by AWS. In this article we will try to find the answer to the following questions:
- What is DynamoDB?
- Is it relational or non-relational?
- What are the building blocks or core components of DynamoDB?
- How it stores and retrieves data efficiently, meaning the data structure used by DynamoDB?
- Practical example of DynamoDB by AWS CLI.

So let's get started...

---

## What Is DynamoDB?
According to the official [docs](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html), "Amazon DynamoDB is a fully **managed NoSQL database** service that provides fast and predictable performance with seamless scalability. DynamoDB lets you offload the administrative burdens of operating and **scaling** a **distributed** database so that you don't have to worry about **hardware provisioning**, **setup and configuration**, **replication**, **software patching**, or **cluster scaling**. DynamoDB also offers **encryption** at rest, which eliminates the operational burden and complexity involved in protecting sensitive data."

Pretty confusing and hard, right? Don't worry; let's try to understand the above bold word to understand the AWS DynamoDB.

1) ***Managed database, hardware provisioning, setup, configuration, replication, software patching, or versioning:***

In a word, a database is something that stores data or information. And here, managed database means we don't need to maintain the hardware, database setup, its configuration, and its patch or version by ourselves. Instead of this, AWS manages all these hassles itself, and that's why it's called managed.

2) ***Scaling, distributed, cluster, encryption:***
- Database scalability is the ability of a database to improve its availability and behavior when the business demands more resources.
- A distributed database is a database that consists of two or more files located in different sites, either on the same network or on entirely different networks.
- A database cluster is a collection of databases that is managed by a single instance of a running database server.
- Database encryption refers to the use of encryption techniques to transform a plain text database into a (partially) encrypted database, thus making it unreadable to anyone except those who possess the knowledge of the encryption key(s). Hence, data keeps secure and sound.

## Is It Relational or Non-relational?
Databases can be divided into 2 types from a high level. One is relational, meaning different tables of the database can maintain some sort of relation between them. And relational databases support SQL (Structured Query Language) for querying data.

Another type of database is non-relational, also called a NoSQL database. As the name refers to, it doesn't support SQL for querying data. And DynamoDB is a NoSQL (Key-Value pair), or non-relational, database.

## Building Blocks or Core Components of DynamoDB
We can consider the following things as the basic building blocks of DynamoDB:
1. **Tables:** 
Similar to other database systems, DynamoDB stores data in tables. A table is a collection of data. For example, a Cars table to store information about vehicles that people drive.

2. ***Items:***
Each table contains zero or more items. An item is a group of attributes that is uniquely identifiable among all of the other items. For a Cars table, each item represents one vehicle. Items in DynamoDB are similar in many ways to rows, records, or tuples in other database systems. In DynamoDB, there is no limit to the number of items you can store in a table.

3. ***Attributes:*** 
Each item is composed of one or more attributes. An attribute is a fundamental data element, something that does not need to be broken down any further. For example, an item in a Cars table contains attributes called BrandName, EngineNumber, and so on. Attributes in DynamoDB are similar in many ways to fields or columns in other database systems.

4. ***Key:***
A key in a database is something that is being used for individual identification of a row/item. DynamoDB supports 2 types of key. First is the **partition key**, and second is the **sort key**. DynamoDB uses the partition key's value as input to an internal hash function. The output from the hash function determines the partition (physical storage internal to DynamoDB) in which the item will be stored. In a table that has only a partition key, no two items can have the same partition key value. The partition key and sort key together are referred to as a **composite primary key**; this type of key is composed of two attributes. The first attribute is the partition key, and the second attribute is the sort key. DynamoDB uses the partition key value as input to an internal hash function. The output from the hash function determines the partition (physical storage internal to DynamoDB) in which the item will be stored. All items with the same partition key value are stored together, in sorted order by sort key value. In a table that has a partition key and a sort key, it's possible for multiple items to have the same partition key value. However, those items must have different sort key values.

5. ***Index:***
An index lets you query the data in the table using an alternate key, in addition to queries against the primary key. DynamoDB supports two kinds of indexes: **Global secondary index** — An index with a partition key and sort key that can be different from those on the table. **Local secondary index** — An index that has the same partition key as the table but a different sort key.

## How It Stores and Retrieves Data Efficiently Means The Data Structure Used By DynamoDB?
According to [Wikipedia](https://en.wikipedia.org/wiki/Amazon_DynamoDB#:~:text=table%20in%20DynamoDB-,Data%20structures,read%20capacity%20units%20(RCU).) and [Scylla](https://www.scylladb.com/learn/dynamodb/introduction-to-dynamodb/#:~:text=As%20mentioned%20before%2C%20DynamoDB%20is,be%20very%20different%20from%20others.), DynamoDB uses [hashing](https://en.wikipedia.org/wiki/Hash_function) and [B-trees](https://en.wikipedia.org/wiki/B-tree) to manage data. Upon entry, data is first distributed into different partitions by hashing on the partition key. Each partition can store up to 10 GB of data and handle by default 1,000 write capacity units (WCU) and 3,000 read capacity units (RCU). DynamoDB is a **key-value** store database that uses a document-oriented JSON data model. Data is indexed using a primary key composed of a partition key and a sort key. There is no set schema to data in the same table; each partition can be very different from others. So when anyone tries to retrieve a value by a partition key, then DynamoDB hashes it and detects the correct partition and then chooses data from the tree.

---

## Practical Example of DynamoDB Using AWS CLI:
AWS CLI for ad hoc operations, such as creating a table. You can also use it to embed Amazon DynamoDB operations within utility scripts. Before you can use the AWS CLI with DynamoDB, you must get an access key ID and secret access key. Please follow the [link](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Tools.CLI.html#Tools.CLI.DownloadingAndRunning) to do so.

- Create table:
```bash
aws dynamodb create-table 
    --table-name Music \
    --attribute-definitions \
        AttributeName=Artist,AttributeType=S \
        AttributeName=SongTitle,AttributeType=S \
    --key-schema AttributeName=Artist,KeyType=HASH AttributeName=SongTitle,KeyType=RANGE \
    --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1 \
    --table-class STANDARD\
```

- Save or update item:
```bash
aws dynamodb put-item 
    --table-name Music \
    --item \
        '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Call Me Today"}, "AlbumTitle": {"S": "Somewhat Famous"}}' \
    --return-consumed-capacity TOTAL  


aws dynamodb put-item \
    --table-name Music \
    --item '{
        "Artist": {"S": "Acme Band"},
        "SongTitle": {"S": "Happy Day"},
        "AlbumTitle": {"S": "Songs About Life"} }' \
    --return-consumed-capacity TOTAL\
```

- Query
```bash
aws dynamodb query --table-name Music --key-conditions file://key-conditions.json
```

---

### References / Sources:
- [AWS DynamoDB docs](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [Wikipedia](https://en.wikipedia.org/wiki/Amazon_DynamoDB#:~:text=table%20in%20DynamoDB-,Data%20structures,read%20capacity%20units%20(RCU).)