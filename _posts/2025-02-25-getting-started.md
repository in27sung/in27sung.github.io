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
### Exercises 
**2.1-1**
Using Figure 2.2 as a model, illustrate the operation of INSERTION-SORT on an array initially containing the sequence `[31, 41, 59, 26, 41, 58]`

**Step-by-step Execution**

| Step | Key  | Array State                |
|------|------|----------------------------|
| 1    | 41   | **[31, 41,** 59, 26, 41, 58] |
| 2    | 59   | **[31, 41, 59,** 26, 41, 58] |
| 3    | 26   | **[26, 31, 41, 59,** 41, 58] |
| 4    | 41   | **[26, 31, 41, 41,** 59, 58] |
| 5    | 58   | **[26, 31, 41, 41, 58,** 59] |

**Final Sorted Array**
`[26, 31, 41, 41, 58, 59]`

**2.1-2**
Consider the procedure SUM-ARRAY on the facing page. It computes the sum of the $n$ numbers in array $A[1:n]$. State a loop invariant for this procedure, and use its initialisation, maintenance, and termination properties to show that the SUM-ARRAY procedure returns the sum of the numbers in $A[1:n]$.

---

## 2.2 Analysing algorithms

<span style="color:blue">*Analysing*</span> an algorithm has come to mean predicting the resources that the algorithm requries. Most often, you will want to measure computational time. If you analyse several candidate algorithms for a problem, you can identify the most efficient one. Most of this book assumes a generic one-processor, <span style="color:blue">*random-access machine(RAM)*</span> model of computation as the implementation technology, with the understanding that algorithms are implemented as computer programs. 


### Analysis of insertion sort
How long does the INSERTION-SORT procedure take? One way to tell would be for you to run it on your computer and time how long it takes to run. Of course, you'd first have to implement it in a real programming language, since you cannot run our pseudocode directly. What would such a timing test tell you? If you run insertion osrt again on your computer with the same input, you might even get a different timing result. 
**How do we analyse insertion sort?** First, let's acknowledge that the runnig time depends on the input. To do so, we nned to define the erms "runnning time" and "input size" more carefully. We also need to be clear about whether we are discussing the running time for an input that elicits the worst-case behaviour, the best-case behaviour, or some other case. The bse notion for <span style="color:blue">*input size*</span> depends on the problem being studided. The <span style="color:blue">*running time*</span> of an algorithm on a particular input is the number of instructions and data accesses executed. 

### Worst-case and Average-case Analysis

In the analysis of **insertion sort**, we considered both the **best case** (when the array is already sorted) and the **worst case** (when the array is sorted in reverse order). However, for most algorithms in this book, we focus on the <span style="color:blue">*worst-case running time*</span>, which is the longest running time for any input of size $n$. Here are three reasons why:

1. **Guarantee of Upper Bound**:
   - The worst-case running time provides an upper bound for the algorithm's running time on any input. Knowing this guarantees that the algorithm will not take longer than this time. This is especially important in **real-time computing**, where operations must meet strict deadlines.

2. **Frequent Occurrence of Worst Case**:
   - For some algorithms, the worst-case scenario happens frequently. For example, in searching a database, the worst-case often occurs when the sought information is not present. In such cases, the worst-case analysis helps to predict performance even when no specific data is available.

3. **Average-case Analysis**:
   - The **average-case** running time for some algorithms, like insertion sort, is often as bad as the worst-case. For insertion sort, when running on an array of \(n\) randomly chosen numbers, each element is compared with half of the elements in the subarray. Therefore, the average comparison time for each insertion is about \(i/2\), leading to an average-case time complexity that is quadratic (\(O(n^2)\)), similar to the worst-case.

**Average-case Analysis and Randomized Algorithms**
- While the worst-case analysis is often more practical, we also sometimes need to consider the <span style="color:blue">*average-case*</span> running time, especially for probabilistic analysis.
- <span style="color:blue">*Probabilistic analysis*</span> can be applied to various algorithms, where inputs are assumed to be random or equally likely. This can yield an **expected running time**.
- In cases where it is unclear what constitutes an "average" input, <span style="color:blue">*randomized algorithms*</span> can be used to generate random inputs and facilitate probabilistic analysis. This approach will be explored in more detail in Chapter 5 and other chapters.

### Order of growth 

In the analysis of the **INSERTION-SORT** procedure, we used simplifying abstractions to focus on the **order of growth** of the running time rather than the actual statement costs. Here are the key points:

1. **Simplifying Assumptions**:
   - We ignored the actual cost of each statement and represented these costs using constants, like $c_k$.
   - The best-case and worst-case running times were expressed in terms of constants (e.g., $an + b$ for best case and $an^2 + bn + c$ for worst case).
   
2. **Focus on the Rate of Growth**:
   - The primary focus is on the **rate of growth** (order of growth) of the running time.
   - For large $n$, the **leading term** in the running time formula is the most important. The lower-order terms are insignificant for large inputs.
   - We ignore constants and lower-order terms to simplify analysis.

3. **Example of Dominant Term**:
   - Consider an algorithm with a running time formula like $\frac{n^2}{100} + 100n + 17$. As $n$ becomes large (e.g., $n > 10,000$), the $\frac{n^2}{100}$ term dominates over the $100n$ term, even though its coefficient is much smaller.

4. **Big Theta ($\Theta$) Notation**:
   - The **order of growth** is represented by **Big Theta ($\Theta$)** notation, which ignores constants and lower-order terms.
   - **Worst-case** running time of **insertion sort** is $\Theta(n^2)$, and the **best-case** is $\Theta(n)$.
   - $\Theta(n^2)$ means the running time is **roughly proportional** to $n^2$ for large $n$, and $\Theta(n)$ means the running time is **roughly proportional** to $n$ for large $n$.

5. **Efficiency and Order of Growth**:
   - An algorithm with a **lower order of growth** in its worst-case running time is generally more efficient.
   - Even though constant factors and lower-order terms can affect small input sizes, the algorithm with a smaller order of growth (e.g., $\Theta(n^2)$ vs $\Theta(n^3)$) will eventually outperform the other for large inputs.
   - There exists a threshold $n_0$, such that for all $n \geq n_0$, the algorithm with $\Theta(n^2)$ will be faster than the one with $\Theta(n^3)$, regardless of constant factors.

**INSERTION-SORT time complexity**
1. **Worst Case ($\Theta(n^2)$)**:
   - Occurs when the array is sorted in reverse order, meaning every element has to be compared with all previous elements.
   - In each insertion, all previous elements are compared.
   - The runing time is thus a <span style="color:blue">*quadratic function*</span> of $n$
   - Time complexity: $T(n) = 1 + 2 + 3 + \dots + (n - 1) = \frac{n(n - 1)}{2} = \Theta(n^2)$

2. **Best Case ($\Theta(n)$)**:
   - Occurs when the array is already sorted in ascending order. In this case, each element is compared only once and no shifting is necessary.
   - The runing time is thus a <span style="color:blue">*linear function*</span> of $n$
   - Time complexity: $T(n) = n - 1 = \Theta(n)$

3. **Average Case ($\Theta(n^2)$)**:
   - In the average case, the array is randomly shuffled, and each insertion will, on average, require half the comparisons.
   - Time complexity: $T(n) = \Theta(n^2)$





