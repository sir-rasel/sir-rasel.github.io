---
title: "Sliding Window and Two Pointer Technique"
description: "Let's learn how sliding window and two pointer technique works"
date: 2025-09-01
tags: ["programming", "algorithm", "sliding-window", "two-pointer", "problem-solving"]
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
    image: "img/blogs/24-sliding-window-1.jpeg"
    caption: "Sliding Window and Two Pointer Technique"
    alt: "Sliding Window and Two Pointer Technique"
    relative: true
    hidden: true
---

{{< figure
    src="/img/blogs/24-sliding-window-1.jpeg"
    caption="Sliding Window and Two Pointer Technique (Photo Credit: Google Image)"
    align=center
>}}

## Story
There is a school called ABC School, which frequently arranges extracurricular activities like games, dancing competitions, art competitions, etc. for their students. Today it arranged 2 interesting games called sliding window and rope pulling.

The rules for the sliding window game are: first, make 2 teams; second, each team takes their position, and then, based on some condition, they slide their window 1 or more units until the window reaches the end position.

The rules for the rope-pulling game are almost similar to those for the sliding window, and that is: first, make 2 teams; second, each team takes their position, and then they start pulling the rope. As a result, the team that has more strength than the other pulls the other team to their area, and the team with less strength comes to the other team's area. The game finishes when one team enters the other team's area.

## Sliding Window Technique
{{< figure
    src="/img/blogs/24-sliding-window-2.jpeg"
    caption="Sliding Window Technique (Photo Credit: Towards Dev)"
    align=center
>}}

The **Window Sliding** technique is a computational technique that aims to reduce the use of nested loops and replace them with a single loop, thereby reducing the time complexity. In this technique, we reuse the result of the previous step to compute the result of the next step. It is a problem-solving technique of data structure and algorithm for problems that apply arrays or lists. These problems are painless to solve using a brute force approach in **O(n²)** or **O(n³)**. However, the sliding window technique can reduce the time complexity to **O(n)**. So the main idea behind the sliding window technique is to convert two nested loops into a single loop.

In the above story, the sliding window game works like our sliding window algorithm. There window has two points and a fixed size, and it slides until the end point arrives.

### Basic Steps to Solve Sliding Window Problems:
- Find the size of the window on which the algorithm has to be performed.
- Calculate the result of the first window, as we calculate in the naive approach.
- Maintain a pointer on the start position.
- Then run a loop and keep sliding the window by one step at a time and also sliding that pointer one at a time, and keep track of the results of every window.

### Typical use cases:
>Used when you want to examine a contiguous block (window) of elements in an array/string.
* Longest substring without repeating characters
* Maximum sum of a subarray of size `k`
* Minimum size subarray sum ≥ `target`

### Pseudocode (Fixed Size Window)

```pseudo
function sliding_window_fixed_size(arr, k):
    window_sum = 0
    max_sum = -∞

    for i from 0 to length(arr) - 1:
        window_sum += arr[i]         // add current element

        if i >= k - 1:               // when window size is 'k'
            max_sum = max(max_sum, window_sum)
            window_sum -= arr[i - k + 1]  // remove the element leaving the window

    return max_sum
```

### Pseudocode (Variable Size Window)

```pseudo
function sliding_window_variable_size(arr, target):
    start = 0
    current_sum = 0
    min_length = ∞

    for end from 0 to length(arr) - 1:
        current_sum += arr[end]

        while current_sum >= target:
            min_length = min(min_length, end - start + 1)
            current_sum -= arr[start]
            start += 1

    if min_length == ∞:
        return 0
    else:
        return min_length
```

---

## Two Pointer Technique
{{< figure
    src="/img/blogs/24-two-pointer.JPG"
    caption="Two Pointer Technique (Photo Credit: Vector Stock)"
    align=center
>}}

Like the name suggests, two pointers work using 2 pointers, or positions of data structures, ideally lists/arrays. It is an excellent technique for working with pairs, separating data, finding ranges (or subsequences) in sequences, or even finding a cycle in a linked list. It compares the values of 2 positions or pointers. It is a pattern in which two pointers iterate across the data structure until one or both of them satisfy the necessary condition.

In the above story, the rope-pulling game works kind of similarly to our two-pointer technique. Where two teams act like two pointers, and they start moving their position based on force (which can be considered a condition of the 2-pointer technique), and this works until 1 team crosses their area.

### Basic Steps to Solve Two-Pointer Problems:
- Pointer initialization: First initialize the pointer positions based on the problem criteria.
- Pointer movement: Move the pointers based on the condition check of either the 1st pointer or the second pointer or both.
- Stop condition: Identify and apply the stop condition based on the problem expectation.


### Typical use cases:
> Used for non-contiguous elements or sorted arrays, often to find pairs or perform merging.
* Two sum in sorted array
* Remove duplicates
* Merging sorted arrays
* Trapping rainwater

### Pseudocode

```pseudo
function two_pointer(arr, target):
    left = 0
    right = length(arr) - 1

    while left < right:
        current_sum = arr[left] + arr[right]

        if current_sum == target:
            return [left, right]
        else if current_sum < target:
            left += 1
        else:
            right -= 1

    return []   // no pair found
```

---

## Difference Between Sliding window and Two Pointer Technique:
- Sliding window algorithms can be implemented with a single pointer and a variable for window size. Typically we use all of the elements within the window for the problem (for example, the sum of all elements in the window).
- The two-pointer technique is quite similar, but we usually compare the value at the two pointers instead of all the elements between the pointers.

| Feature           | Sliding Window                | Two Pointer                          |
| ----------------- | ----------------------------- | ------------------------------------ |
| Works on          | Contiguous subarrays/strings  | Sorted arrays / general arrays       |
| Pointer direction | Usually one moves (start/end) | Both pointers move toward each other |
| Window size       | Fixed or dynamic              | No "window", but two indices         |

---

## Problems Can Be Solved
**Using sliding window:**
- [Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)
- [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)
- [Permutation in String](https://leetcode.com/problems/permutation-in-string/)
- [Maximum Average Subarray](https://leetcode.com/problems/maximum-average-subarray-i/)I
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- [Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)
- [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

**Using two pointer technique:**
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- [Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- [Reverse Words in a String II](https://leetcode.com/problems/reverse-words-in-a-string-ii/)
- [Rotate Array](https://leetcode.com/problems/rotate-array/)
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)