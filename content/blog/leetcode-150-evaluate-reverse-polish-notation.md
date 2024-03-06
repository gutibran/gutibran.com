---
date: '2024-03-05T23:03:26-06:00'
title: 'Leetcode 150: Evaluate Reverse Polish Notation'
draft: false
tags: [computer science, data structures, algorithms]
description: "My solution to LeetCode problem 150 Evaluate Reverse Polish Notation."
toc: true
---

# Problem statement, constraints, and test cases

## Problem statement
You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

The valid operators are $+$, $-$, $*$, and $/$.
Each operand may be an integer or another expression.
The division between two integers always truncates toward zero.
There will not be any division by zero.
The input represents a valid arithmetic expression in a reverse polish notation.
The answer and all the intermediate calculations can be represented in a 32-bit integer.

## Problem Constraints
- The number of tokens given in the input list is in the range of $1 \leq \text{tokens} \leq 10^{4}$.
- Each element in the input list is either an arithmetic operator: $+$, $-$, $*$, $/$ or an integer in the range $-200$ to $200$.

## Problem Test Cases
The input is a list of strings representing the operands and operators in Reverse Polish Notation.

The expected output is an integer.

# Solution

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        operators = ["+", "-", "*", "/"]
        stack = []
        result = 0
        for token in tokens:
            if token in operators:
                operator = token
                operand_b = stack.pop()
                operand_a = stack.pop()
                expression = f"{operand_a} {operator} {operand_b}"
                result = int(eval(expression))
                stack.append(result)
            else:
                stack.append(token)
        if len(stack) > 0:
            return int(stack[-1])
        return result
```

## Code

## Explanation

### What is Reverse Polish Notation (RPN)
Reverse Polish Notation (RPN) is a mathematical notation that has every operator followed by all of its operands. RPN eliminates the need for parentheses or any other grouping symbol to indicate The Order of Operations which is required for infix notations. RPN is also known as Polish postfix notation, Łukasiewicz notation, and simply postfix notation. It was created by Polish logician and philosopher Jan Łukasiewicz.

For example the expression $2 \text{ } 1 + 3 \text{ } \times$ is read as $2 + 1 \times 3$ in infix notation.

{{< image src="/images/Jan-Łukasiewicz.jpg" alt="Jan Łukasiewicz" >}}

### Algorithm
First I declared and initialized a list named $operators$ containing strings representing valid arithmetic operators as defined in the problem statement. Declared another list named $stack$ which is used as a stack data structure. Lastly I declared a variable to keep track of our operations.
```python
operators = ["+", "-", "*", "/"]
stack = []
result = 0
```

Next I iterate through the input list of tokens. On each iteration I check to see if the current token is stored in the list of operators declared previously, if so then we want to pop the last two elements from the stack. I assigned three variables for clarity. $\text{operator}$ to store the arithmetic operator to be used in the expression to be evaluated. $\text{operand_b}$ for the first element popped from the stack and $\text{operand_a}$ for the second element popped from the stack. $expression$ is a Python formatted string that will represent the current expression to be evaluated. $result$ to store the result of the integer expression evaluation with the help of Python's built-in methods $eval()$ and $int()$. Then push the resulting expression evaluation back onto the stack. If the current token is not an operator then we push the current token to the top of the stack. This process will continue until we have reached the end of the stack.
```python
for token in tokens:
    if token in operators:
        operator = token
        operand_b = stack.pop()
        operand_a = stack.pop()
        expression = f"{operand_a} {operator} {operand_b}"
        result = int(eval(expression))
        stack.append(result)
    else:
        stack.append(token)
```

Before returning $result$ I handled an edge case for when the input token list only contains one integer and no operator(s). This is done by checking the length of the stack. If the length of the stack is greater than zero then return a casted integer of the top element. Other wise return the $result$.
```python
if len(stack) > 0:
    return int(stack[-1])
return result
```


# Resources
- [Wikipedia article on Reverse Polish Notation](https://en.wikipedia.org/wiki/Reverse_Polish_notation)
- [Computerphile's "Reverse Polish Notation and The Stack" video](https://www.youtube.com/watch?v=7ha78yWRDlE)
- [Wikipedia article on Jan Łukasiewicz](https://en.wikipedia.org/wiki/Jan_%C5%81ukasiewicz)