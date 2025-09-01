---
title: "Searching Algorithm (Linear Search and Binary Search)"
description: "Let's learn how can we search effectively from a list of items"
date: 2025-08-31
tags: ["programming", "algorithm", "linear-search", "binary-search"]
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
    image: "img/blogs/23-linear-binary-search.png"
    caption: "Searching Algorithm"
    alt: "Searching Algorithm"
    relative: true
    hidden: true
---

{{< figure
    src="/img/blogs/23-linear-binary-search.png"
    caption="Linear and Binary Search (Photo Credit: Crio.Do)"
    align=center
>}}

## Story
Let's say students of the CSE department of University XYZ are going on a study tour in a tourist place. They are staying in a hotel, and surprisingly, they booked rooms on different floors, not the same, with one student per floor. And students get their room according to their rank/roll. This means students with the highest rank are staying on the topmost floor, and those with the lowest are staying on the lower floor. So the 1st rank lives at the top, and the last rank lives in the low, let's say the 1st floor.

Now the hotel authority booked 2 hotel boys for their service. So when any service is needed by the students, they call these hotel boys and ask for service by only mentioning their rank or roll number. So hotel boys need to figure out the room number or floor number by the student rank. Now the approach of finding the room/floor number using the student rank by the hotel boys is as follows:

- Hotel Boy 1: He looks at the students' records and their room information one by one and looks for it until he finds it. So every time he needs to find a student's room information, he goes through the whole list of the students.

- Hotel Boy 2: He is smart, and as he knows, students get their room according to their rank, so it stays in a sorted manner. So when he needs to find student information, he searches it in a middle-point-looking manner. This means he looks in the middle of the student list and matches it to the student information he is looking for. If not, he goes to one of the left or right sides of the list according to the student's rank he is looking for. And by using this technique, he saves his time and effort compared to hotel boy 1.

## What Does Searching Mean?
Searching means to look into or over carefully or thoroughly in an effort to find or discover something. So searching in programming can be defined as looking for something from a collection or list or group.

It can be many ways, and different ways have different pros and cons. We are talking here about 2 types named:
1) linear search
2) binary search

---

## Linear Search
As its name refers, linear search is a type of search algorithm that is performed linearly, meaning one by one from one side to another. So implementation-wise it is easy, but time complexity-wise it is not good enough for frequent operation like the above scenario by the hotel boy 1. But it can perform its operation on any type or formation of data, unlike binary search. Data does not necessarily need to be sorted beforehand in this case.

### Pseudo code of linear search:
```bash
procedure LinearSearch(array, value) 
  
   foreach item in array  
      if item == value    
         return the item's index    
      end if    
   end foreach      
   return -1  
  
end procedure 
```

- Time complexity : O(N)
- Space complexity: O(1)

## Binary Search
Unlike the linear search, the binary search is not searching the whole list. It searches the midpoint of the list and then cuts the list in half. Based on the target and current midpoint value, it cut either the left half or the right half of the list that time. As it cut down the half of its search space, that is why it is called a binary search. But to perform the binary search algorithm on a collection, there needs to be fulfillment of some condition. 

Like:

### Prerequisite for the binary search algorithm:
- A collection or list must need to be accessible by index.
- The collection or list must need to be sorted.

### Binary search algorithm:
- Begin with the middle element of the whole array as a search key.
- If the value of the search key is equal to the item, then return an index of the search key.
- Or if the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half.
- Otherwise, narrow it to the upper half.
- Repeatedly check from the second point until the value is found or the interval is empty.

### Pseudo code of binary search:
```bash
Procedure BinarySearch(array,value) 
  
   Set lowerBound = 1  
   Set upperBound = size of array   
  
   while (lowerBound <= upperBound)      
      set midPoint = (lowerBound + upperBound ) / 2        
       if array[midPoint] > value  
         set upperBound = midPoint - 1             
       else if array[midPoint] < value  
         set lowerBound = midPoint + 1           
       else return midPoint  
   end while  
     
   return -1;     
     
end procedure
```
- Time complexity : O(Log(N))
- Space Complexity : O(1)

---

## Problems Can Be Solved Using Binary Search
- [Search Insert Position](https://leetcode.com/problems/search-insert-position)
- [Sqrt(x)](https://leetcode.com/problems/sqrtx)
- [Search In Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array)
- [Pin Peak Element](https://leetcode.com/problems/find-peak-element)
- [Find K-th Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance)