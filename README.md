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

### [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements)

#### Pseudocode

- Create a dictionary to store the frequency of each number
- Create a list of lists to store the numbers with the same frequency
- Iterate through the dictionary and append the numbers to the list of lists
- Iterate through the list of lists in reverse order and append the numbers to the result
- If the length of the result is equal to k, return the result

#### Code

```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        freq = [[] for i in range(len(nums) + 1)]

        for n in nums:
            count[n] = 1 + count.get(n, 0)
        for n, c in count.items():
            freq[c].append(n)

        result = []
        for i in range(len(freq)-1, 0, -1):
            for n in freq[i]:
                result.append(n)
                if len(result) == k:
                    return result
```

#### Big O Analysis

- **Time Complexity:** O(n), where n is the length of the list of numbers
- **Space Complexity:** O(n), as additional space is used to store the dictionary and the list of lists

❌ Need to come back to this one

---

### [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self)

#### Pseudocode

- Initialize a Solution Array of same size as input array with value.
- Store Prefix and Postfix Product so far in variables.
- Traverse the input array.
- Before updating the values for each i, multiply current solution array value at i with the value of prefix i.e. multiply with prefix product of the previous i-1 elements.
- Similarly, calculate the postfix product value for n-i-1 where n is length of input array at each iteration.
- As in Step 4, before calculating the postfix for i'th value , multiply the solution_array[n-i-1] with the postfix product value i.e. products of input[i+1] to input[n-1].

#### Code

```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        result = [1] * len(nums)
        prefix = 1
        postfix = 1

        for i in range(len(nums)):
            result[i] *= prefix
            prefix = prefix * nums[i]
            result[len(nums)-i-1] *= postfix
            postfix = postfix * nums[len(nums)-i-1]

        return result
```

#### Big O Analysis

- **Time Complexity:** O(n), single pass
- **Space Complexity:** O(1), as we are not supposed to count the output array.

❌ Need to come back to this one

---

### [Valid Sudoku](https://leetcode.com/problems/valid-sudoku)

#### Pseudocode

- We need to check for duplicate numbers 1-9 in each row, column, and 3x3 square
- We can use a set to store the numbers in each row, column, and 3x3 square
- Iterate through each element in the board
- If the element is a ".", skip it
- If the element is already in the set, return false
- Otherwise, add the element to the set
- If the loop completes without finding duplicates, return true

#### Code

```
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = defaultdict(set)
        cols = defaultdict(set)
        squares = defaultdict(set)

        for r in range(9):
            for c in range(9):
                if board[r][c] == ".":
                    continue
                if (board[r][c] in rows[r]) or (board[r][c] in cols[c]) or (board[r][c] in squares[(r//3,c//3)]):
                    return False
                rows[r].add(board[r][c])
                cols[c].add(board[r][c])
                squares[(r//3, c//3)].add(board[r][c])

        return True

```

#### Big O Analysis

- **Time Complexity:** O(9^2), as we are iterating through each element in the board
- **Space Complexity:** O(9^2), as we are storing each element in the board

❌ Need to come back to this one

---

### [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

#### Pseudocode

- Convert list to set using inbuilt set function.
- Create low and high integer to store low and high values in ongoing sequence and assign low and high value to current value.
- Run a while loop that continues till high + 1 or low - 1 is present in uniques set.
  - If low - 1 is present in uniques, decrease value of low by 1, and remove low - 1 element from uniques.
  - If high + 1 is present in uniques, increase value of high by 1. and remove high + 1 element from uniques.
- As we keep on iterating, we will be left with empty set, thus stopping our while loop.

#### Code

```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        nums_set = set(nums)
        res = 0
        while nums_set:
            curr = nums_set.pop()
            up, down = curr+1, curr-1
            sequence_len = 1

            while up in nums_set:
                nums_set.remove(up)
                up += 1
            sequence_len += (up-curr-1)

            while down in nums_set:
                nums_set.remove(down)
                down -= 1
            sequence_len += (curr-down-1)

            res = max(res, sequence_len)
        return res

```

#### Big O Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

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
