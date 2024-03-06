---
date: '2024-03-06T06:44:08-06:00'
title: 'LeetCode 739: Daily Temperatures'
draft: false
tags: [computer science, data structures, algorithms]
description: "My solution to LeetCode problem 739 Daily Temperatures."
toc: true
---

# Solution
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