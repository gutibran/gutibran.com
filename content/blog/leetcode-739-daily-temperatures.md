---
date: '2024-03-06T15:23:06-06:00'
title: 'Leetcode 739 Daily Temperatures'
draft: true
tags: [computer science, data structures, algorithms]
description: "My solution to LeetCode Problem 739: Daily Temperatures."
toc: true
---

# Problem statement, constraints, and test cases


## Problem Statement
Given an array of integers temperatures represents the daily temperatures, return an array answer such that $\text{answer[i]}$ is the number of days you have to wait after the ith day to get a warmer temperature. If there is no future day for which this is possible, keep $\text{answer[i] == 0}$ instead.

## Problem Constraints
$1 \leq \text{tempartures.length} \leq 10^{5}$ defines the range that the length of $\text{temperatures}$ will be in.

$30 \leq \text{temperatures[i]} \leq 100$ defines the range that the elements within $\text{temperatures}$ will be in.

## Problem Test Cases
The input is a list called $\text{temperatures}$ that holds numbers that represents a temperature for the $\text{ith}$ day.
```python
temperatures = [73,74,75,71,69,72,76,73]
```

The expected output is a list that holds numbers that represents the number of days from the $\text{ith}$ position for the temperature to be higher.
```python
[1,1,4,2,1,1,0,0]
```

For index position 0 the temperature is 73 the next closest spot within the array with a higher temperature is in index position 1 where the temperature is 74 so in the resulting array index position 0 will store 1 to represent one day. This is done for all the other temperatures.

# Solution

## Code
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        result = [0] * len(temperatures)
        stack = []
        for i in range(len(temperatures)):
            while len(stack) > 0 and temperatures[i] > temperatures[stack[-1]]:
                previous_index = stack.pop()
                result[previous_index] = i - previous_index
            stack.append(i)
        return result
```

## Explanation

# Resources
- [LeetCode Problem 739: Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/)
- [GeeksForGeeks Monotonic stack article](https://www.geeksforgeeks.org/introduction-to-monotonic-stack-data-structure-and-algorithm-tutorials/)
- [liuzhenglaichn's Algorithm GitBook (monotonic stack section)](https://liuzhenglaichn.gitbook.io/algorithm/monotonic-stack)