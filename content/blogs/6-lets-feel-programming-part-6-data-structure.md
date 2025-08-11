---
title: "Let's Feel Programming Fundamentals - Part 6 (Data Structure)"
description: "You will be a superstar once you begin to feel programming"
date: 2025-08-12
tags: ["programming", "programming-basic", "programming-fundamentals", "data-structure"]
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
    image: "img/blogs/6-data-structure.webp"
    caption: "programming"
    alt: "programming"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 5:** [Let's Feel Programming Fundamentals - Part 5 (Procedural, Functional, OOP Style)]({{< ref "blogs/5-lets-feel-programming-part-5-programming-style.md" >}})
---

{{< figure
    src="/img/blogs/6-data-structure.webp"
    caption="Data Structure (Photo Credit: Olibr)"
    align=center
>}}

In this part, we will try to understand what a data structure is. Also see some of the well known data structure that use frequently in our day to day life with short description. Please note: ***we will not dive deep for the sake of simplicity.*** If you feel really interested, you can explore each of them in details. And may be I will write each of the topic in details in future insha Allah.

## Story
There is a village named "Opposite Town." Two types of people live there are known as "organized" and "unorganized," respectively. They are exactly the opposite of each other based on their behavior. Their behavior is as follows:

- Point 1: People who belong to "organized" groups always keep their necessary things in an organized way. So they can find or use them easily and efficiently when needed. Also, people of this group first planned and defined the steps in the simplest, smallest way. After that, they followed those steps to perform a task. That's why they are called organized people.
- Point 2: The people of an "unorganized" group are opposite to an organized group of people. They are unorganized; they don't keep their things organized, and they don't plan and define necessary steps efficiently before performing any task. That's why they are called unorganized, and their life is harder than the organized people.

## Data Structure
In simple words, data structure is a way of storing, organizing, and arranging the data. The primary motivation of a data structure is to make operations on that data smooth, efficient, and performant. Operations that should be kept in mind when choosing a data structure are:

1. Read: Access some point/index of the data,
2. Write: Add new data at any point.
3. Update: Update the current value of a data point.
4. Search: Search for data from the collection of the data.
5. Delete: Remove data or a record from the collection.

In the above story at point 1, the organized group of people use data structure to organize their things so that their life becomes easy and efficient. But point 2: Unorganized people don't know data structure, so their life is so hard.

Some most used and common data structure based on complexity are as follows:

### Basic
1. **Array**: Sequential collection of the same (or different as per some language support) type of data. Data is stored in memory sequentially. Can be multidimensional like 2D array (Matrix), 3D array etc.
2. **String**: It is also like an array but an array can store any type of data but need to be the same type. Otherwise string is a sequential collection of character type data only.
3. **Stack**: It is a LIFO (last in first out) style data structure. That is the last in data be out first.
4. **Queue**: It is the opposite of stack. Means it is a FIFO (first in first out) style data structure. Here first in data be out first.
5. **Dequeue**: It is a combination of stack and queue. That is data can be in and out in any order.

### Intermediate
6. **Linked list / Singly linked list**: It is also a sequential collection structure but data is not stored in the memory sequentially like an array. Every data point is called a node where a node holds data and references (address) to the next node. It creates a chain relationship in one direction. Means once we go to the next we can not revert back to the previous one.
7. **Doubly linked list**: It is also a link list but 2 ways. Means we can go both forward and backward.
8. **Priority queue**: It is like a queue but a priority tag is also added with data. And data will be auto sorted based on their priority and high priority data are out first not the data that was in first in like queue.
9. **Tree**: A tree is non-linear and a hierarchical data structure consisting of a collection of nodes (it is also like a linked list node) such that each node of the tree stores a value and a list of references to other nodes (the “children”).
10. **Binary Search Tree**: It is a special kind of tree where each node can stores at most 2 reference of other nodes called left node and right node. That's why it called binary tree. And in binary search trees, the left node value always becomes smaller or equal to the current (parent) node and the right node value is bigger than the current (parent) node value.
11. **Graph**: Graph is almost similar to the tree data structure, it also holds the node called vertices and different nodes/vertices are connected by edges. The only difference is that, graph can be in a circular relationship and need not maintain the hierarchical structure. So a tree is also a graph but a graph can not always be a tree.

### Advanced
12. **Trie**: Trie data structure is defined as a Tree based data structure that is used for storing some collection of strings and performing efficient search operations on them. The word Trie is derived from reTRIEval, which means finding something or obtaining it. 
13. **Heap**: A Heap is a special Tree-based data structure in which the tree is a complete binary tree that satisfies the heap property. Heap property means each node in a tree has a key which is more extreme (greater or less) than or equal to the key of its parent that is max or min.
14. **Set**: A set is a data structure that stores unique elements of the same type in a sorted order. Each value is a key, which means that we access each value using the value itself.
15. **Hash table/ hash map/ map/ dictionary**: Hash/Map is a data structure that uses a hash function to map identifying values, known as keys, to their associated values. It contains “key-value” pairs and allows retrieving value by its key.
16. **Binary indexed tree/ Fenwick tree**: A Fenwick tree or binary indexed tree is a data structure that can efficiently update elements and calculate prefix sums in a table of numbers. Its index is calculated in a binary incrementing way that's why it is called Binary Index tree.
17. **Segment tree**: A segment tree, also known as a statistic tree, is a tree data structure used for storing information about intervals, or segments. It allows querying which of the stored segments contain a given point.
18. **Disjoint set**: A disjoint-set data structure, also called a union–find data structure or merge–find set, is a data structure that stores a collection of disjoint (non-overlapping) sets. Equivalently, it stores a partition of a set into disjoint subsets.

---

*Insha Allah, in the upcoming blogs we will deep dive each fundamental concepts. Till than, may Allah keep you healthy and happy.*