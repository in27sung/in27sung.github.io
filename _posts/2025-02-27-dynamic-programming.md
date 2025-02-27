---
layout: post
title: Chapter14 Dynamic Programming
subtitle: Introduction to algorithm
excerpt_image: https://github.com/user-attachments/assets/34172b0d-4abd-4f10-80f1-758d9cd140df
categories: markdown
tags: [algorithm]
top: 
---
## Dynamic Programming

- like the divide-and-conquer method, solves problems by combining the solutions to subproblems.
- typically apllies to **optimization problems**.
- To develop a dynamic-programming algorithm, follow a sequence of four steps:
  1. Characterise the structure of an optimal solution.
  2. Recursively define the value of an optimal solution. 
  3. Compute the value of an optimal solution, typically in a bottom-up fashion.
  4. Construct an optimal solutino from computed information.

> Step 1-3 form the basis of a dynamic-programming solutin to a problem. If you need only the value of an optimal solution, and not the solution itself, then you can omit step 4. When you do perform step 4, it often pays to maintain additional information  during step 3 so that you can easily construct an optimal solution.

---
## 14.1 Rod cutting 

