---
date: '2024-01-30T02:43:28-06:00'
title: 'Leetcode 14 Longest Common Prefix'
draft: true
tags: [algorithms]
---

# Initial ideas
- find the length of the shortest string
- iterate till the length of the shortest string and determine what the longest prefix is
- iterate through each string at the same time m times, m being the length of the shortest string
- while iterating compare the ith string to all the other strings, if they all are the same add this character
to the result variable, do this till they all do not match
- null terminate the string and return the string

```c
#include <stdio.h>
#include <limits.h>

char* longestCommonPrefix(char** strs, int strsSize) {
    int shortest_string_length = INT_MAX;
    for (int i = 0; i < strsSize; i++) {
        int current_string_size = 0;
        for (char* character = strs[i]; *character != '\0'; character++) {
            current_string_size++;
        }
        if (current_string_size < shortest_string_length) {
            shortest_string_length = current_string_size;
        }
    }

 char* longest_common_prefix = (char*)malloc((shortest_string_length + 1) * sizeof(char));
    for (int i = 0; i < shortest_string_length; i++) {
        char current_char = strs[0][i];
        for (int j = 1; j < strsSize; j++) {
            if (strs[j][i] != current_char) {
                longest_common_prefix[i] = '\0';
                return longest_common_prefix;
            }
        }
        longest_common_prefix[i] = current_char;
    }
    longest_common_prefix[shortest_string_length] = '\0';
    return longest_common_prefix;
}
```