---
date: '2024-01-30T01:08:19-06:00'
title: 'Hashing'
draft: true
tags: [computer science, data structures, algorithms]
---

Dictionary: Abstract Data Type (ADT)
- maintain set of items each with a key
- $\text{insert}(item)$ -> overwrites exising key in python
- $\text{delete}(item)$
- $\text{search}(key): \text{return the item with given key, exact search, there is a key and return item or there isn't a key and report it}$

BST allow for finding the successor or predecessor.
balanced binary search tree like avl trees is a solution for logn time
searching is faster in log n time -> constant time with high probability with hashing (randomized data structure)

lookup key -> search
set key to value -> insert
delete key -> delete
how are these implenented
item is key-value pair

# implementations
A an array with a hash function. Takes an input hashes the input (key) which will map to an index in the array to store the value. Hash function should ALWAYS PRODUCE THE SAME OUTPUT FOR A GIVEN INPUT. HASH FUNCTION NEEDS TO BE FAST FOR FAST LOOKUPS. OUTPUTS (INDEX) should be random enough. Distribute the placement of values within the array to maximized efficacy.

A checksum. What is this. adding the sum of chearcters assci codes. multiply the sum by current character. then use modulo by table size to get last digit

collision is when two keys map to the same location. how to deal with that. array of poniters to sthe structs null pointer is a empty location

open addressing

external chaining -> each locatoin is the head of a linked list
rehash or linear probing, start at index and check till a spot is empty, if back at orginal index then use external chaining
can resize the array by a loading factor
quadratic probing
double hashing

# resources
- [Jacob Sorber: Understanding and implementing a Hash Table (in C)](https://www.youtube.com/watch?v=2Ti5yvumFTU)
- [MIT 6.006 (OCW) Lecture 8: Hashing and Chaining](https://www.youtube.com/watch?v=0M_kIqhwbFo)