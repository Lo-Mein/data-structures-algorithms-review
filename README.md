# Algorithm and Data Structures Review

Welcome to the Algorithm and Data Structures Review repository! This repository will go over all of the data structures and algorithms in [Neetcode 150](https://neetcode.io/practice). Each section will review the data structure and explain the optmized solution to each probllem.

## Table of Contents

1. [Arrays & Hashing](#arrays--hashing)
2. [Two Pointers](#two-pointers)
3. [Sliding Window](#sliding-window)
4. [Stack](#stack)
5. [Binary Search](#binary-search)
6. [Linked List](#linked-list)
7. [Trees](#trees)
8. [Tries](#tries)
9. [Heap / Priority Queue](#heap--priority-queue)
10. [Backtracking](#backtracking)
11. [Graphs](#graphs)
12. [Advanced Graphs](#advanced-graphs)
13. [1-D Dynamic Programming](#1-d-dynamic-programming)
14. [2-D Dynamic Programming](#2-d-dynamic-programming)
15. [Greedy](#greedy)
16. [Intervals](#intervals)
17. [Math & Geometry](#math--geometry)
18. [Bit Manipulation](#bit-manipulation)

---

## Arrays & Hashing

### Arrays

Array is a linear data structure that is a collection of similar data types. It is a static data structure with a fixed size. Each element is accessed using an index. Arrays provide a simple and efficient way to organize and manipulate data.

#### When to Use Arrays

- **Storing and accessing data:** Arrays are used to store and retrieve data in a specific order.
- **Sorting:** Arrays can be used to sort data in ascending or descending order. Sorting algorithms such as bubble sort, merge sort, and quicksort rely heavily on arrays.
- **Searching:** Arrays can be searched for specific elements using algorithms such as linear search and binary search.
- **Matrices:** Arrays are used to represent matrices in mathematical computations such as matrix multiplication, linear algebra, and image processing.
- **Stacks and Queues:** Arrays are used as the underlying data structure for implementing stacks and queues, which are commonly used in algorithms and data structures.
- **Graphs:** Arrays can be used to represent graphs in computer science. Each element in the array represents a node in the graph, and the relationships between the nodes are represented by the values stored in the array.

#### Advantages

1. **Constant Time Access:** Accessing elements by index is done in constant time, O(1).
2. **Memory Efficiency:** Arrays allow for fast data retrieval because the data is stored in contiguous memory locations
3. **Fast data retrieval::** The concept of arrays is straightforward and widely understood.

#### Disadvantages

1. **Fixed Size:** Arrays have a fixed size, making it challenging to dynamically resize them.
2. **Insertion and Deletion:** Inserting or deleting elements in the middle requires shifting elements, leading to a time-consuming operation.
3. **Memory allocation issues:** Allocating a large array can be problematic, particularly in systems with limited memory.
4. **Limited data type support:** Arrays have limited support for complex data types such as objects and structures, as the elements of an array must all be of the same data type.

### Hashing

Hashing is a technique that maps data to a fixed-size array, providing efficient data retrieval. It involves using a hash function to compute an index into an array where the desired data can be found.

#### When to Use Hashing

- **Fast Retrieval:** When you need fast data retrieval based on a key.
- **Avoiding Collisions:** Hashing is useful when effective collision resolution mechanisms are implemented.

#### Advantages

1. **Fast Retrieval:** Hashing provides constant-time average-case complexity for data retrieval.
2. **Dynamic Sizing:** Hash tables can dynamically resize to accommodate varying amounts of data.

#### Disadvantages

1. **Collision Handling:** Collisions may occur, and effective strategies (like chaining or open addressing) are needed to handle them.
2. **Deterministic Output:** Hash functions provide deterministic output, which can lead to clustering of keys.

---

## Problems

### [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

#### Pseudocode

- Create an empty set to store unique elements
- Iterate through each element in the array
- If the element is already in the set, it's a duplicate
- Otherwise, add the element to the set
- If the loop completes without finding duplicates, return false

#### Code

```
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        hashset = set()

        for num in nums:
            if num in hashset:
                return True
            hashset.add(num)

        return False
```

---

### [Valid Anagram](https://leetcode.com/problems/valid-anagram)

#### Pseudocode

- In order for two strings to be a valid anagram, they must have the same length and contain the same characters
- We can sort both strings and compare them to see if they are equal

#### Code

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s) == sorted(t)
```

#### Big O Analysis

- **Time Complexity:** O(nlogn), where nnn is the length of the input strings. The dominant factor is the sorting operation.
- **Space Complexity:** O(n), as additional space is used to store the character arrays.

---

### [Two Sum](https://leetcode.com/problems/two-sum/)

#### Pseudocode

- Create an empty dictionary
- Iterate through each element in the list of numbers
- If the complement of the target is already found in the dictionary then return the index of the complement and the current index
- Otherwise, add the element and its index to the dictionary

#### Code

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        required = {}
        for i in range(len(nums)):
            if target - nums[i] in required:
                return [required[target - nums[i]],i]
            else:
                required[nums[i]]=i
```

#### Big O Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

### [Group Anagrams](https://leetcode.com/problems/group-anagrams)

#### Pseudocode

- Create a dictionary to store the anagrams
- Iterate through each string in the list of strings
- Create a key for each string by counting the number of occurrences of each character
- If the key already exists in the dictionary, append the string to the list of anagrams
- Otherwise, create a new key and add the string to the list of anagrams
- Return the values of the dictionary

#### Code

```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        result = defaultdict(list)
        print(result)

        for string in strs:
            key = [0] * 26

            for char in string:
                key[ord(char) - ord("a")] += 1

            result[tuple(key)].append(string)

        return result.values()
```

#### Big O Analysis

- **Time Complexity:** O(nk), where n is the length of the list of strings and k is the length of the longest string
- **Space Complexity:** O(nk), as additional space is used to store the dictionary

❌ Need to come back to this one

---

## Two Pointers

## Sliding Window

## Stack

## Binary Search

## Linked List

## Trees

## Tries

## Heap / Priority Queue

## Backtracking

## Graphs

## Advanced Graphs

## 1-D Dynamic Programming

## 2-D Dynamic Programming

## Greedy

## Intervals

## Math & Geometry

## Bit Manipulation

---
