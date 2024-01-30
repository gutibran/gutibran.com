---
date: '2024-01-30T03:19:26-06:00'
title: 'Leetcode 9 Palindrome Numbers'
draft: true
tags: []
---

Gonna analyze these solutions later

```c
#include <stdio.h>
#include <stdlib.h>

bool isPalindrome(int x) {
    // handle the edge case of the x being negative
    if (x < 0) {
        return false; // x is not a palindrome because of the negative sign
    }

    int x_copy = x; // create a copy of x to work with
    int x_digit_length = 0; // store the number of digits that x contains

    // determine the number of digits in x
    while (x_copy != 0) {
        x_copy /= 10; // truncate the least significant digit
        x_digit_length++; // incrment the digit count by one
    }

    // declare an array to store the digits of x
    int* x_digits = (int *)malloc(x_digit_length * sizeof(int)); // allocate memory at runtime in the heap to store digits of x into an array

    int j = x_digit_length - 1; // set a loop variable to start at the end of the array

    // add digits of to the array
    for (int i = 0; i < x_digit_length; i++) {
        x_digits[j] = x % 10; // add the least significant digit to the array
        x /= 10; // truncate the least significant digit
        j--; // decrement j by one
    }

    j = x_digit_length - 1; // set a loop variable to start at the end of the array

    // determine if x is a palindrome
    for (int i = 0; i < x_digit_length / 2; i++) {
        // check if the ith and jth digit are not equal to each other rendering x to not be a palindrome
        if (x_digits[i] != x_digits[j]) {
            return false; // x is not a palindrome
        }
        j--; // decrement j by one
    }
	free(x_digits); // deallocate memory for the array in the heap
    return true; // x is a palindrome
}
```