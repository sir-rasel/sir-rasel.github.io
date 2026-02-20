---
title: "Journey To Database World: Part 7 (Document Database - MongoDB As Example)"
description: "Let's learn the fundamental database concepts!"
date: "2026-02-02T00:00:00Z"
tags: ["database", "nosql", "document-database", "mongoDb"]
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
    image: "img/blogs/114-database-mongoDB.png"
    caption: "MongoDB"
    alt: "MongoDB"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 6:** [Journey To Database World: Part 6 (Key-Value Pair Database - Redis As Example)]({{< ref "blogs/113-database-key-value-redis.md" >}})
---

{{< figure
    src="/img/blogs/114-database-mongoDB.png"
    caption="Document Database - MongoDB (Photo Credit: LinkedIn Image)"
    align=center
>}}

## Story:

Once upon a time, there was a toy store owner named Toma. Toma had a lot of different toys to manage like action figures, dolls, board games, and puzzles. Each toy was unique and had its own special features.

Tim initially tried to use a traditional table to keep track of his toys. But soon, Toma faced problems: Not all toys had the same fields (like "Number of Players" didn’t apply to the Teddy Bear or Robot), Every time Toma added a new type of toy (like a puzzle), he had to change the entire table to add new columns for special features like "number of pieces", It was too rigid and hard to manage as new toy categories arrived.

One day, Toma's friend, Milon the Coder, told him about Document. "With a document database," Milon explained, "you can store each toy's information in a flexible, **self-contained document**. Each toy can have its own structure, and you don't have to worry about changing the entire system to add new toy categories." Tim loved the idea! Instead of rigid rows and columns, each toy was stored as a **document**.

* * *

## What is a Document Database?

A **document database** is a type of **NoSQL** database that stores data in a semi-structured, document-oriented format, typically using **JSON**, **BSON**, or **XML** documents. Each document contains key-value pairs, arrays, and nested structures, similar to objects in programming languages like JavaScript or Python. Example: **MongoDB**.

Unlike relational databases (SQL) that store data in tables with rows and columns, document databases treat each record (document) as a self-contained unit. This makes document databases more flexible and capable of handling dynamic, hierarchical, or complex data structures.

Key Features of Document Databases:

*   **Document Format**: JSON, BSON (binary JSON), or XML.
*   **Self-Contained Documents**: Each document can have its own structure, unlike relational databases that require a fixed schema.
*   **Hierarchical Data**: Supports nested objects and arrays (like hierarchical or tree structures).
*   **Rich Queries**: Supports queries using operators like $gt, $lt, $in, and full-text search.
*   **Schema Flexibility**: No need to predefine a schema, making it easy to add, remove, or modify fields.
*   **Horizontal Scalability**: Supports data distribution across multiple servers (sharding).

## Use Cases of Document Databases

1.  **Content Management Systems (CMS)**: Store and retrieve dynamic and diverse content like blog posts, product descriptions, and user profiles.
2.  **E-commerce Platforms**: Store catalog data where each product may have different attributes (size, color, brand, etc.).
3.  **Real-Time Analytics**: Store clickstream or event logs as documents for real-time data analysis.
4.  **IoT Data**: Store sensor data where each device might have different formats or specifications.
5.  **Social Media Apps**: Store user profiles, comments, and likes.

## Benefits of Document Databases

*   **Flexibility**: No fixed schema, easy to evolve.
*   **Efficiency**: Documents are self-contained, reducing joins.
*   **Scalability**: Horizontally scalable with sharding.
*   **Developer Friendly**: JSON-like syntax, easy to use.
*   **Faster Reads**: Queries are faster due to indexing and self-contained docs.

## Drawbacks of Document Databases

*   **Data Duplication**: Embedding can lead to redundant data.
*   **Complex Queries**: Lacks SQL-style joins, requiring manual lookups.
*   **Memory Overhead**: Documents can consume more space than relational rows.

## When to Use a Document Database

*   **Dynamic Schema**: When schema changes frequently (like product catalogs or IoT sensor data).
*   **Hierarchical Data**: When data is naturally hierarchical (like JSON or nested objects).
*   **High Write/Read Performance**: When high write throughput and fast reads are required.
*   **Horizontal Scalability**: When you need to scale the database across multiple servers.

## When Not to Use a Document Database

*   **Complex Joins**: If your queries require multiple joins, a relational database may be a better choice.
*   **Strict ACID Transactions**: Relational databases offer stronger guarantees for transactional integrity.

* * *

## MongoDB as a Document Database

**MongoDB** is one of the most popular NoSQL, document-oriented databases. It stores data in a JSON-like format (**BSON**) where each document is a self-contained unit of data. Unlike relational databases, MongoDB does not require a fixed schema, making it highly flexible for applications with evolving data needs. It is known for its scalability, flexibility, and performance.

Each "**row**" (records) in a traditional RDBMS is equivalent to a **document** in MongoDB, and each "**table**" (combine of records) is known as a **collection**.

## Getting Started with MongoDB

**mongosh** (MongoDB Shell) is a command-line interface used to interact with MongoDB databases. It allows you to run queries, execute commands, and manage databases. To install MongoDB and and getting started with mongosh please follow the below instructions:

1.  Install MongoDB Community Server ([https://www.mongodb.com/try/download/community](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fwww%2Emongodb%2Ecom%2Ftry%2Fdownload%2Fcommunity&urlhash=00UN&trk=article-ssr-frontend-pulse_little-text-block))
2.  Create account and setup cluster.
3.  Install mongosh ([https://www.mongodb.com/docs/mongodb-shell/install/](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fwww%2Emongodb%2Ecom%2Fdocs%2Fmongodb-shell%2Finstall%2F&urlhash=mAzn&trk=article-ssr-frontend-pulse_little-text-block))
4.  Connect to the database with connection string.

```zsh
mongosh "mongodb+srv://cluster0.ex4ht.mongodb.net/myFirstDatabase" --apiVersion 1 --username YOUR_USER_NAME        
```

Now you are ready to play with MongoDB queries.

### Data Model in MongoDB

Here’s an example of a MongoDB document representing a user profile:

```js
{
  "_id": ObjectId("64893f..."),
  "name": "John Doe",
  "age": 29,
  "email": "john.doe@example.com",
  "address": {
    "street": "123 Elm St",
    "city": "New York",
    "zip": "10001"
  },
  "hobbies": ["Cycling", "Gaming", "Traveling"],
  "created_at": ISODate("2024-12-15T10:00:00Z")
}        
```

**Explanation**:

*   _id: The unique identifier for the document (automatically generated if not provided).
*   name, age, email: Simple key-value fields.
*   address: A nested document containing street, city, and zip.
*   hobbies: An array of multiple values.
*   created_at: Stores the timestamp of when the document was created.

* * *

## MongoDB Operations

### 1. Insert Operations

To insert a document, use insertOne or insertMany.

Example 1: Insert a Single Document

```js
db.users.insertOne({
  "name": "A",
  "age": 25,
  "email": "a@example.com",
  "hobbies": ["Reading", "Traveling"]
});        
```

This creates a new document in the users collection.

Example 2: Insert Multiple Documents

```js
db.users.insertMany([
  { "name": "B", "age": 30, "hobbies": ["Football", "Cooking"] },
  { "name": "C", "age": 35, "hobbies": ["Gaming", "Coding"] }
]);        
```

This inserts two new users into the users collection.

### 2. Query Operations (Read)

You can query documents using find, findOne, and projection to control which fields are returned.

Example 1: Find All Users

```js
db.users.find();
```

Returns all documents in the users collection.

Example 2: Find Users with Age Greater than 25

```js
db.users.find({ "age": { $gt: 25 } });        
```

This returns users whose age is greater than 25.

Example 3: Find a User by Name

```js
db.users.findOne({ "name": "A" });        
```

Finds a document where name = "A".

Example 4: Projection (Return Only Name and Age)

```js
db.users.find({}, { name: 1, age: 1, _id: 0 });        
```

This returns only the name and age fields for all users, excluding the \_id field.

### 3. Update Operations

You can update a document using updateOne, updateMany, and $set.

Example 1: Update One Document

```js
db.users.updateOne(
  { "name": "A" },
  { $set: { "age": 26 } }
);        
```

Updates A's age to 26.

Example 2: Update Multiple Documents

```js
db.users.updateMany(
  { "age": { $lt: 30 } },
  { $set: { "status": "young" } }
);        
```

Adds a status field with a value of young to users where age < 30.

### 4. Delete Operations

To delete documents, you use deleteOne or deleteMany.

Example 1: Delete One Document

```js
db.users.deleteOne({ "name": "B" });        
```

Deletes a single user where name = "B".

Example 2: Delete Multiple Documents

```js
db.users.deleteMany({ "age": { $lt: 25 } });        
```

Deletes all users whose age is less than 25.

### 5. Aggregation Pipeline

Aggregation pipelines allow for more complex transformations like grouping, filtering, sorting, and projecting.

Example: Find the Average Age of Users

```js
db.users.aggregate([
  { $group: { _id: null, averageAge: { $avg: "$age" } } }
]);        
```

This calculates the average age of all users.

Example: Count Users by Age

```js
db.users.aggregate([
  { $group: { _id: "$age", count: { $sum: 1 } } },
  { $sort: { count: -1 } }
]);        
```

This groups users by age and counts how many users have each age.

### 6. Indexing

Indexes speed up queries on large collections.

Example: Create an Index on the 'name' Field

```js
db.users.createIndex({ "name": 1 });        
```

This creates an ascending index on the name field, making queries like db.users.find({ "name": "A" }) faster.

### 7. Transactions

You can group multiple operations into a transaction to ensure atomicity.

Example: Transaction with Multiple Updates

```js
const session = db.getMongo().startSession();
session.startTransaction();
try {
  db.users.updateOne({ "name": "Alice" }, { $set: { "age": 30 } });
  db.orders.updateOne({ "order_id": 12345 }, { $set: { "status": "Shipped" } });
  session.commitTransaction();
} catch (error) {
  session.abortTransaction();
}        
```

If either update fails, both changes are rolled back.

### 8. Schema Validation

MongoDB supports [JSON Schema](https://www.linkedin.com/redir/redirect?url=http%3A%2F%2Fjson-schema%2Eorg%2F&urlhash=7AKK&trk=article-ssr-frontend-pulse_little-text-block) validation. The **$jsonSchema** operator allows us to define our document structure.

```js
db.createCollection("posts", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: [ "title", "body" ],
      properties: {
        title: {
          bsonType: "string",
          description: "Title of post - Required."
        },
        body: {
          bsonType: "string",
          description: "Body of post - Required."
        },
        category: {
          bsonType: "string",
          description: "Category of post - Optional."
        },
        likes: {
          bsonType: "int",
          description: "Post like count. Must be an integer - Optional."
        },
        tags: {
          bsonType: ["string"],
          description: "Must be an array of strings - Optional."
        },
        date: {
          bsonType: "date",
          description: "Must be a date - Optional."
        }
      }
    }
  }
})        
```

This will create the posts collection in the current database and specify the JSON Schema validation requirements for the collection.

* * *

## Summary

A document database like MongoDB provides a flexible, schema-less, and horizontally scalable approach to storing and managing data. By representing data as self-contained documents, MongoDB can handle complex, hierarchical, and evolving data with ease. It’s ideal for dynamic applications, real-time analytics, and e-commerce platforms.