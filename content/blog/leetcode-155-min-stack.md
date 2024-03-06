---
date: '2024-03-05T21:56:48-06:00'
title: 'Leetcode 155: Min Stack'
draft: false
tags: [computer science, data structures, algorithms]
description: "My solution to LeetCode problem 155 Min Stack."
toc: true
---

# Problem statement, constraints, and test cases

## Problem statement
Design a stack that supports push, pop, top, and retrieving the minimum element in $\mathcal{O}(1)$ time.

Implement the MinStack class:

- $\text{MinStack()}$ initializes the stack object.
- $\text{void push(int val)}$ pushes the element val onto the stack.
- $\text{void pop()}$ removes the element on the top of the stack.
- $\text{int top()}$ gets the top element of the stack.
- $\text{int getMin()}$ retrieves the minimum element in the stack.

You must implement a solution with $\mathcal{O}(1)$ time complexity for each function.

## Problem Constraints
- The values used in the test cases will be in the range $-2^{31} \leq \text{val} \leq 2^{31} - 1$.
- $\text{pop()}$, $\text{top()}$, and $\text{getMin()}$ will be called on non-empty stacks.
- At most $3 \cdot 10^{4}$ calls will be made to $\text{pop()}$, $\text{top()}$, and $\text{getMin()}$.

## Problem test cases
This problems test case input will be in the form of two lists, one containing strings that represent the stack methods called and another list for the arguments passed to those stack methods. The output will also be a list containing the return values.

Input
```python
["MinStack","push","push","push","getMin","pop","top","getMin"]
```

Input arguments
```python
[[],[-2],[0],[-3],[],[],[],[]]
```

Output
```python
[null,null,null,null,-3,null,0,-2]
```

# Solution
The problem gives you a "skeleton" of a the $\text{MinStack}$ class definition. You just have to write the function definition to fit the requirements given in the problem statement. The list data structure in Python makes it very easy to implement and use stacks. The main idea is that one stack is the "main" stack that keeps track of all elements regardless if is considered a minimum and the other stack is "min" or "minimum" stack which keeps track elements that are considered the smallest element at a certain time.

## Code
```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        if len(self.min_stack) > 0:
            if val > self.min_stack[-1]:
                val = self.min_stack[-1]
        self.min_stack.append(val)

    def pop(self) -> None:
        self.stack.pop()
        self.min_stack.pop()

    def top(self) -> int:
        if len(self.stack) > 0:
            return self.stack[-1]

    def getMin(self) -> int:
        if len(self.min_stack) > 0:
            return self.stack[-1]
```

## Explanation

### $\text{class MinStack and}$ $\text{\_\_init\_\_(self)}$
The $\text{\_\_init\_\_(self)}$ is assigns a two variables to store two lists which can be used as stacks. $\text{stack}$ is used to keep track of elements added to the stack. $\text{min_stack}$ keeps track of all elements that were the considered the smallest element a different points in time.
```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []
```

### $\text{push(self, val)}$
```python
def push(self, val: int) -> None:
    self.stack.append(val)
    if len(self.min_stack) > 0:
        if val > self.min_stack[-1]:
            val = self.min_stack[-1]
    self.min_stack.append(val)
```
The $\text{push(self, val)}$ adds $\text{val}$ to $\text{self.stack}$. Next it will check if $\text{self.min\_stack}$ is empty. If $\text{self.min\_stack}$ is not empty, check if $\text{val}$ is greater than the current minimum value stored at top of $\text{self.min\_stack}$, if $\text{val}$ is greater then the value to be added to the top of $\text{self.min\_stack}$ will be the current minimum located at the top of $\text{self.min\_stack}$. Otherwise if $\text{val}$ is lesser than the current minimum value stored at top of $\text{self.min\_stack}$, it will be stored instead. Also if $\text{self.min\_stack}$ is empty then it will just add $\text{val}$ to $\text{self.min\_stack}$ because there is no element to compare $\text{val}$ to, to determine a minimum.


### $\text{pop(self)}$
```python
def pop(self) -> None:
    self.stack.pop()
    self.min_stack.pop()
```
The $\text{pop(self)}$ method just runs Python's built-in list method $\text{pop()}$ on both of the stacks $\text{self.stack}$ and $\text{self.min\_stack}$ which removes the top element of both stacks respectively.

### $\text{top(self)}$
```python
def top(self) -> int:
    if len(self.stack) > 0:
        return self.stack[-1]
```
$\text{top(self)}$ returns the element at the top of $\text{self.stack}$. It first checks if the stack is not empty to prevent Python index errors then returns the element at the top of $\text{self.stack}$.

### $\text{getMin(self)}$
```python
def top(self) -> int:
    if len(self.min_stack) > 0:
        return self.min_stack[-1]
```
$\text{getMin(self)}$ returns the element at the top of $\text{self.min_stack}$ which is the current minimum element. It also first checks if the stack is not empty to prevent Python index errors then returns the element at the top of $\text{self.min_stack}$ which is the current minimum element.

# Resources
- [LeetCode 155 Min Stack Problem](https://leetcode.com/problems/min-stack/description/)