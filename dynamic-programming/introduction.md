---
description: Those who cannot remember the past are condemned to repeat it
---

# Introduction

Dynamic Programming is Enhanced Recursion. During Recursion a function calls itself using smaller input. Sometimes these calls are repetitive. In order to improve time complexity, we store the result of these recussive calls (called memoization).

`Always write recurssive solution -> memoize it -> write top-down (if necessary)`

`DP = Recursion + Storage`

### Identification :&#x20;

* There will be some sort of _**choice**_ given. For exp : In knapsack problem, we have a choice for including or excluding every element.
* The question asks for optimal result : miniumu, maximum, largest, smallest

### Parent Problems :&#x20;

* 0/1 Knapsack
  * Equal Sum Partition
  * Subset Sum
  * Count of Subset Sum
  * Minimum Subset Sum difference
  * Target Sum
  * Number of Subset with given difference
* Unbounded Knapsack
* Fibonacci
* Longest Common Subsequence (LCS)
* Longest Increasing Subsequence (LIS)
* Kadane's Algorithm
* Matrix Chain Multiplication (MCM)
* DP on Trees
* DP on Grid
* Others
