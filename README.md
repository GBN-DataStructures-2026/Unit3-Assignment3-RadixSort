# Unit 3 - Assignment 3: Radix Sort using Queue ADT

## Overview

In this assignment, you and your partner will implement **Radix Sort** (specifically Least Significant Digit / LSD Radix Sort), a non-comparative integer sorting algorithm that uses an array of **Queues** as bucket storage.

Unlike comparison-based algorithms such as QuickSort or MergeSort (which run in $O(n \log n)$ time), Radix Sort organizes numbers by examining their individual digits from right to left (1s place, 10s place, 100s place, and so on). Because elements are enqueued and dequeued in First-In, First-Out (FIFO) order, Radix Sort maintains **stability**—preserving the relative order of elements with duplicate keys.

---

## Core Algorithmic Concept & Math

For each pass (digit position $p = 0, 1, 2, \dots$ representing $10^0, 10^1, 10^2, \dots$), you will:
1. **Distribute** each number in the array into one of 10 bucket queues ($0$ through $9$) based on its digit at position $p$.
2. **Collect** all numbers back into the original array by dequeuing from bucket $0$ completely, then bucket $1$, up through bucket $9$.
3. **Print** the array state after each complete pass.

### Arithmetic Digit Extraction

You **may not** convert numbers to `String` objects or use character parsing to extract digits. You must use integer arithmetic (division and modulo):

$$
\text{digit} = \left\lfloor \frac{\text{number}}{10^p} \right\rfloor \pmod{10}
$$

*Example for number 749 at pass p = 1 (10s digit):*

$$
\left\lfloor \frac{749}{10^1} \right\rfloor = 74 \implies 74 \pmod{10} = 4
$$

---

## Required Intermediate Output Specification

To verify that your algorithm processes digit passes correctly, your code must print the array state immediately after every pass (after collecting all elements back from the queues).

**Sample Output Format:**
```text
Pass 1 (1s digit):   [170, 90, 802, 2, 24, 45, 75, 66]
Pass 2 (10s digit):  [802, 2, 24, 45, 66, 170, 75, 90]
Pass 3 (100s digit): [2, 24, 45, 66, 75, 90, 170, 802]
```

---

## Technical Tasks & Guidelines

### Task 1: Dynamic Pass Determination
Your code must automatically determine how many passes are needed based on the largest integer present in the array. **Do not hardcode the number of passes.**

### Task 2: Queue Array Instantiation
You must construct an array of 10 `Queue<Integer>` references. 

> ⚠️ **Java Warning:** In Java, creating an array of generics (e.g., `new Queue<Integer>[10]`) requires a type cast or raw array declaration. Remember that instantiating an array of objects creates an array of `null` references—you must initialize each index with an actual Queue instance (such as `LinkedList` or `ArrayDeque`) before using it!

### Task 3: Intermediate Sorting Loop
Implement the distribution and collection loops cleanly inside `RadixSort.java`.

---

## Conceptual Thinking & Reflection Questions

Discuss these questions with your partner and include your answers in your submission:

1. **Queue (FIFO) vs. Stack (LIFO):**
   * What would happen to the sorting order if you replaced your 10 `Queue` buckets with 10 `Stack` buckets? 
   * Trace what happens to numbers `42` and `82` during Pass 2 (10s digit) if a Stack is used instead of a Queue.

2. **Time Complexity Analysis:**
   * If $n$ is the number of elements in the array and $d$ is the maximum number of digits, what is the Big-$O$ time complexity of Radix Sort?
   * Under what conditions would Radix Sort be faster than QuickSort ($O(n \log n)$)? Under what conditions would it be slower?

3. **Negative Numbers:**
   * Our current implementation assumes non-negative integers. How could you modify your bucket system to support negative numbers without converting them to strings?

---

## GitHub Repository Setup Instructions

1. **Owner / Host:** Create a new repository under your class GitHub Organization (e.g., `GBN-DataStructures-2026/Lab3-RadixSort-TeamName`).
2. **Template Import:** Push `RadixSort.java`, `RadixSortTester.java`, and `README.md` to the main branch.
3. **Branching Strategy:** 
   * Both partners must clone the repository locally.
   * Work on a feature branch (e.g., `feature/radix-implementation`).
   * Submit code via Pull Request (PR) with at least one code review approval from your partner before merging into `main`.
