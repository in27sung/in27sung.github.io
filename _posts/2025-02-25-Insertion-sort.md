---
layout: post
title: Insertion sort
subtitle: This is a quick markdown example
excerpt_image: https://github.com/user-attachments/assets/34172b0d-4abd-4f10-80f1-758d9cd140df
categories: markdown
tags: [algorithm]
top: 
---

## 2.1 Insertion sort

### Sorting problem 
**Input**: A sequence of $n$ numbers $<a_1, a_2, \dots, a_n>$.

**Output**: A permutation (reordering) $<a_1^\{'}, a_2^{'}, \dots, a_n^{'}>$. of the input sequence such that $a_1^\{'} \leq a_2^{'} \leq \dots \leq a_n^{'}$.

**keys**: The number to be storted
**satellite data**: The input comes in the form of an array with $n$ elements. When we want to srot numbers, it's often beacuse they are the keys accociated with other data.
**recode**: A key and satellite data form

<img width="540" alt="image" src="https://github.com/user-attachments/assets/34172b0d-4abd-4f10-80f1-758d9cd140df" />

```pseudocode
INSERTION-SORT(A, n)
for i = 2 to n
  key = A[i]
  // Insert A[i] into the sorted subarray A[1:i - 1]
  j = i - 1
  whiel j > 0 and A[j] > key
    A[j + 1] = A[j]
    j = j - 1
  A[j + 1] = key
```

### Loop invariants and the correctness of insertion sort

Figure 2.2 shows how this algorithm works for an array A that starts out with the sequence <5, 2, 4, 6, 1, 3>. The index $i$ indicates the "current card" being inserted into the hand. At the beginning of each iteration of the **for** loop, which is indexed by $i$, the <span style="color:blue">*subarray* </span> (a contiguous portion of the array) consisting of elements `A[1: i - 1]` (that is, `A[1]` through `A[i - 1]`)constitutes the currently sored hand, and the remaining subarray `A[i + 1:n]` (elements `A[i + 1]` through `A[n]`) corresponds to the pile of card still on the table. In face, elements `A[1: i - 1]` are the elements originally in positions 1 through $$i - 1$$, but now in sorted order. We state these properties of `A[1: i - 1]` formally as a <span style="color:blue">*loop invariant* </span>:

![image](https://github.com/user-attachments/assets/c3f3cc8b-26d0-4c53-9ef2-a6f0f4f95991)
