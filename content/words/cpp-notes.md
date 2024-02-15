---
date: '2024-02-15T03:31:54-06:00'
title: 'Cpp Notes'
draft: true
tags: [programming, c++]
---

Here are all my notes on C++. Re-read the book and check with chatgpt to make sure conceptual facts are correct.

# General

## What is main() 
main() is the entry point for the program. When the program is ran main() will execute.

## What are exit codes
Exit codes are integers that tell the OS how the program ran. 0 indicates success and any other non-zero integer indicates failure. This is why the return type for main is int.

## What is the compiler tool chain (pre-processor, compiler, linker)

### Pre-processor
Performs basic source-code manipulation. Produces a single translation unit which is passed to the compiler.

### Compiler
Reads in a translation unit from the pre-processor and generates an object file which contains object code. Compilers work on one object file at a time.

### Linker
Generates an executable from object files by linking them together.

## How to write hello, world!
```c++
#include <iostream>

int main() {
    std::cout << "Hello, world!" std::endl;
    return 0;
}
```

## Basic syntax

### Declaring variables

### Conditional statements

### Functions

## Basics of debugging with GDB


## Ehat is 
```c++
int main() {
    return 0
}
```

# Resources

## Official documentation

## Books

## Videos

## Podcasts

## Miscellaenous