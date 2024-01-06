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

## Problems

### [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

#### Pseudocode

- Create two pointers, one at the beginning of the string and one at the end
- Iterate through the string
- If the character at the left pointer is not alphanumeric, increment the left pointer
- If the character at the right pointer is not alphanumeric, decrement the right pointer
  - NOTE: if we dont want to use built in isalnum() function, we can use ord() to check if the character is alphanumeric a-z, A-Z, 0-9
- If the characters at the left and right pointers are not equal, return false
- If the loop completes without finding any non-matching characters, return true

#### Code

```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1

        while l < r:
            while l < r and not s[l].isalnum():
                l+=1
            while l < r and not s[r].isalnum():
                r-=1
            if s[l].lower() != s[r].lower():
                return False
            l,r = l+1, r-1


        return True

```

#### Big O Analysis

- **Time Complexity:** O(n), where n is the length of the string
- **Space Complexity:** O(1), as we are not using any additional space

---

### [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

#### Pseudocode

- Create two pointers, one at the beginning of the array and one at the end
- Iterate through the array
- If the sum of the elements at the left and right pointers is equal to the target, return the indices
- Since the array is sorted, we can increment and decrement the pointers based on the sum of the elements

#### Code

```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers) - 1

        while l < r:
            added = numbers[l] + numbers[r]
            if added == target:
                return [l+1, r+1]
            elif added > target:
                r -= 1
            else:
                l += 1

```

#### Big O Analysis

- **Time Complexity:** O(n), where n is the length of the array
- **Space Complexity:** O(1), as we are not using any additional space

---

### [3Sum](https://leetcode.com/problems/3sum)

#### Pseudocode

- Sort the array
- Iterate through each element in the array, use enumerate to get the index and value
- Since we want to avoid duplicates, if the current element is equal to the previous element, continue
- Create two pointers, one at the current element + 1 and one at the end of the array
- Now we can take a similar approach to the two sum problem
- If the sum of the current element, left pointer, and right pointer is equal to 0, append the elements to the result
  - increment the left pointer (could be either the right or left pointer)
  - while the left pointer is less than the right pointer and the left pointer is equal to the previous element, increment the left pointer
- If the sum is greater than 0, decrement the right pointer
- If the sum is less than 0, increment the left pointer
- Return the result

#### Code

```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()

        for i, num in enumerate(nums):
            if i > 0 and nums[i] == nums[i-1]:
                continue

            l, r = i+1, len(nums) -1
            while l < r:
                three_sum = num + nums[l] + nums[r]

                if three_sum == 0:
                    res.append([num, nums[l], nums[r]])
                    l += 1
                    while nums[l] == nums[l-1] and l < r:
                        l += 1
                elif three_sum > 0:
                    r -= 1
                else:
                    l += 1
        return res

```

#### Big O Analysis

- **Time Complexity:** O(n^2), where n is the length of the array
- **Space Complexity:** O(n), as we are using a list to store the results

---

### [Container With Most Water](https://leetcode.com/problems/container-with-most-water)

#### Pseudocode

- Create two pointers, one at the beginning of the array and one at the end
- Iterate through the array
- Calculate the area of the container using the minimum height of the two pointers and the distance between the two pointers
- since we want to maximize the area, we can move the pointer with the smaller height
- Return the maximum area

#### Code

```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_water = 0
        l,r = 0, len(height) -1

        while l < r:
            curr_area = min(height[l], height[r]) * (r - l)
            max_water = max(max_water, curr_area)

            if height[l] > height[r]:
                r -= 1
            else:
                l += 1
        return max_water
```

#### Big O Analysis

- **Time Complexity:** O(n), where n is the length of the array
- **Space Complexity:** O(1), as we are not using any additional space

---

### [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

#### Pseudocode

- Create two pointers, one at the beginning of the array and one at the end
- create two variables to store the maximum height of the left and right pointers, this will be used to calculate the amount of water that can be trapped
- while the left pointer is less than the right pointer
  - if the maximum height of the left pointer is less than the maximum height of the right pointer
    - increment the left pointer
    - update the maximum height of the left pointer
    - add the difference between the maximum height of the left pointer and the height of the left pointer to the result
  - otherwise
    - decrement the right pointer
    - update the maximum height of the right pointer
    - add the difference between the maximum height of the right pointer and the height of the right pointer to the result

#### Code

```
class Solution:
    def trap(self, height: List[int]) -> int:
        if not height: return 0
        l,r = 0, len(height)-1
        l_max,r_max = height[l],height[r]
        res = 0

        while l < r:
            if l_max < r_max:
                l += 1
                l_max = max(l_max, height[l])
                res += l_max - height[l]
            else:
                r -= 1
                r_max = max(r_max, height[r])
                res += r_max - height[r]
        return res
```

#### Big O Analysis

- **Time Complexity:** O(n), where n is the length of the array
- **Space Complexity:** O(1), as we are not using any additional space

---

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
