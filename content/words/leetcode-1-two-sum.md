---
date: '2024-01-29T15:52:31-06:00'
title: 'Leetcode 1: Two Sum'
draft: true
---

```c
#include <stdio.h>

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    int* solution = (int *)malloc(2 * sizeof(int));
    *returnSize = 2;
    for (int i = 0; i < numsSize; i++) {
        int addend = target - nums[i];
        for (int j = 0; j < numsSize; j++) {
            if (nums[j] == addend && j != i) {
                solution[0] = i;
                solution[1] = j;
            }
        }
    }
    return solution;
} 
```