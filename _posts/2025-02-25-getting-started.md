---
layout: post
title: Chapter2 Getting Started
subtitle: Introduction to algorithm
author: Insung
excerpt_image: https://github.com/user-attachments/assets/34172b0d-4abd-4f10-80f1-758d9cd140df
categories: Algorithm
tags: [algorithm]
top: 
---

This chapter will familiarise you with the framework we'll use throughout the book to think about the design and analysis of algorithms. We'll begin by examining the insertion sort algorithm to solve the sorting problem. We'll specify algorithms using a pseudocode that should be understandable to you if you have done computer programming. We'll see why insertion sort correctly sorts and analyse its running time. The analysis introduces a notation that describes how running time increases with the number of times to be sorted. Following a discussion of insertion sort, we'll use a method called divide-and-conquer to develop a sorting algorithm called marge sort. We'll end with an analysis of merge sort's running time.

---
## 2.1 Insertion sort

### Sorting problem 
**Input**: A sequence of $n$ numbers $<a_1, a_2, \dots, a_n>$.

**Output**: A permutation (reordering) $<a_1^\{'}, a_2^{'}, \dots, a_n^{'}>$. of the input sequence such that $a_1^\{'} \leq a_2^{'} \leq \dots \leq a_n^{'}$.

**keys**: The number to be sorted

**satellite data**: The input comes in the form of an array with $n$ elements. When we want to sort numbers, it's often because they are the keys associated with other data.

**recode**: A key and satellite data form

<img width="540" alt="image" src="https://github.com/user-attachments/assets/34172b0d-4abd-4f10-80f1-758d9cd140df" />

```pseudocode
INSERTION-SORT(A, n)
for i = 2 to n
  key = A[i]
  // Insert A[i] into the sorted subarray A[1:i - 1]
  j = i - 1
  while j > 0 and A[j] > key
    A[j + 1] = A[j]
    j = j - 1
  A[j + 1] = key
```

### Loop invariants and the correctness of insertion sort

Figure 2.2 shows how this algorithm works for an array `A` that starts out with the sequence <5, 2, 4, 6, 1, 3>. The index $i$ indicates the "current card" being inserted into the hand. At the beginning of each iteration of the **for** loop, which is indexed by $i$, the <span style="color:blue">*subarray* </span> (a contiguous portion of the array) consisting of elements `A[1: i - 1]` (that is, `A[1]` through `A[i - 1]`)constitutes the currently sored hand, and the remaining subarray `A[i + 1:n]` (elements `A[i + 1]` through `A[n]`) corresponds to the pile of cards still on the table. In fact, elements `A[1: i - 1]` are the elements originally in positions 1 through $i - 1$, but now in sorted order. We state these properties of `A[1: i - 1]` formally as a <span style="color:blue">*loop invariant* </span>:

![image](https://github.com/user-attachments/assets/c3f3cc8b-26d0-4c53-9ef2-a6f0f4f95991)

**Initialisation:** It is true prior to the first iteration of the loop.

- Purpose: To set up the algorithm before it starts processing.
- Explanation:
  - The algorithm starts with the second elements of the array (i = 2), as the first element is considered "sorted" (a single element is trivially sorted).
  - For each elemnet starting from the second position, the algorithm will attempt to insert it into the sorted subarray that begin at the first element.

- Example:

  `A = [5, 2, 4, 6, 1, 3]`

**Maintenance:** If it is true before an iteration of the loop, it remains true before the next iteration.

- Purpose: This step keeps the sorting process ongoing by iterating through the array and ensuring that the array is progressively sorted.
- Explanation:
  - **In each iteration:** The current element `A[i]` is compared with elements in the sorted subarray (`A[0]` to `A[i - 1]`).
  - This comparison continues until the correct position for `A[i]` is found. The elements greater than `A[i]` are shifted one position to the right, making space for `A[i]` to be inserted at the correct location.
- Example: (continuing from above)
  - After the first comparison, `A[1]` (which is 2) is compared with `A[0]` (which is 5).
  - Since $2 /gt 5$, we shift 5 to the right and insert 2 in the first position. Now, the array looks like this: `[2, 5, 4, 6, 1, 3]`.

The maintenance step guarantees that the array is sorted from the beginning up to i.

**Termination:** The loop terminates, and when it terminates, the invariant – usually along with the reason that the loop terminated – gives us a useful property that helps show that the algorithm is correct.

- Purpose: The algorithm stops when all elements have been inserted in to the sorted portion of the array.
- Explanation:
  - The algorithm terminates when the index `i` exceeds the length of the array. At this point, all elements have been processed, and the array is fully sorted.
- Example:
  - Once the algorithm reaches the last element `A[5]`, after completing all necessary comparisons and shifts, the sorted array is: `[1, 2, 3, 4, 5, 6]`.

```python
def inssertion_sort(A, n):
	for i in range(1, n):
    key = A[i] # Start from the second element
    j = i - 1
    # Shift elements of A[0..i-1], that are greater than key, to one postion ahead 
    while j >= 0 and A[j] > key:
      A[j + 1] = A[j]
      j -= 1
    A[j + 1] = key # Insert the key at its correct position

# Example usage
A = [5, 2, 4, 6, 1, 3]
n = len(A)
insertion_sort(A, n)
print(A) # Output: [1, 2, 3, 4, 5, 6]
```

---

## 2.2 Analysing algorithms

<span style="color:blue">*Analysing* </span> an algorithm has come to mean predicting the resources that the algorithm requries. 







