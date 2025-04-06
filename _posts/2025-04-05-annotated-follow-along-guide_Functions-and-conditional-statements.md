---
layout: post
title: "Annotated follow-along guide: Functions and conditional statements"
subtitle: Functions and conditional statements
author: Insung
categories: [Google Advanced Data Analytics]
tags: [Data Science, Coursera, Get Started with Python]
top:
---

## Annotated follow-along guide: Functions and conditional statements

This notebook contains the code used in the instructional videos from [Module 2: Functions and conditional statements](https://www.coursera.org/learn/get-started-with-python/home/module/2).

### Introduction

This follow-along guide is an annotated Jupyter Notebook organized to match the content from each module. It contains the same code shown in the videos for the module. In addition to content that is identical to what is covered in the videos, you’ll find additional information throughout the guide to explain the purpose of each concept covered, why the code is written in a certain way, and tips for running the code.

As you watch each of the following videos, an in-video message will appear to advise you that the video you are viewing contains coding instruction and examples. The in-video message will direct you to the relevant section in the notebook for the specific video you are viewing. Follow along in the notebook as the instructor discusses the code.

To skip directly to the code for a particular video, use the following links:

1.   **[Define functions and returning values](#1)**
2.   **[Write clean code](#2)**
3.   **[Use comments to scaffold your code](#3)**
4.   **[Make comparisons using operators](#4)**
5.   **[Use if/elif/else statements to make decisions](#5)**


<a name="1"></a>
## 1. [Define functions and returning values](https://www.coursera.org/learn/get-started-with-python/lecture/RA9w4/define-functions-and-returning-values)

<video controls width="100%" style="max-width: 720px;">
  <source src="https://d3c33hcgiwev3.cloudfront.net/XZE-R_q4R7-V1302gW3eEw.processed/full/720p/index.mp4?Expires=1743984000&Signature=j8~iA8K-V3ZnQLINqXmmuEBl1Oj0j3k7IlznLUIcRckfBd3NwSJNkBAmD6D66ZhHFs5f9lBZLOX8EwxzwTqpPeua2ETZ0Jznmn9zo-~-W9L1FK5XJFFtlrZKsp09NFe-zwZmeabStpxvgwO35ECeP0E8Qdpp0fVSlx6cAuMwgHQ_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" type="video/mp4">
  Your browser does not support the video tag.
</video>

```python
# The print() function can print text to the screen.
print('Black dove, where will you go?')
```

    Black dove, where will you go?



```python
# The type() function returns an object's data type.
number = 15

type(number)
```




    int




```python
# The str() function converts an object into a string.
number = str(number)

type(number)
```




    str




```python
# Define a function.
def greeting(name):

    print('Welcome, ' + name + '!')
    print('You are part of the team!')

greeting('Rebecca')
```

    Welcome, Rebecca!
    You are part of the team!



```python
# Define a function to calculate the area of a triangle.
def area_triangle(base, height):
    return base * height / 2
```


```python
# Use the function to assign new variables and perform calculations.
area_a = area_triangle(5, 4)
area_b = area_triangle(7, 3)
total_area = area_a + area_b
total_area
```




    20.5




```python
# Define a function that converts hours, minutes, and seconds to total seconds.
def get_seconds(hours, minutes, seconds):
    total_seconds = 3600*hours + 60*minutes + seconds
    return total_seconds
```


```python
# Use the function to return a result.
get_seconds(16, 45, 20)
```




    60320



<a name="2"></a>
## 2. [Write clean code](https://www.coursera.org/learn/get-started-with-python/lecture/KKTTl/write-clean-code) 

<video controls width="100%" style="max-width: 720px;">
  <source src="https://d3c33hcgiwev3.cloudfront.net/Qi2G-KzwTMyCJCXHGuE5pA.processed/full/720p/index.mp4?Expires=1743984000&Signature=lY5itOfGflbM5Gl8Kdxa~QZmt8WLfep763KH95OCHoaowi2laGELJbfDn7q~naRI8D0ihZFcdsDc0pYyrUjmisedYHJe86qwMWNkaXiMeTYOvbSxM~rt-izHsLv49lDmUyipaJ3ViqmDRCPzdex-Qs4u1~XHXSaTM1tuybpIgl0_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" type="video/mp4">
  Your browser does not support the video tag.
</video>


```python
# This code does the same thing for two different people.
name = "Marisol"
number = len(name)*9
print("Hello " + name + ". Your lucky number is " + str(number))

name = "Ardashir"
number = len(name)*9
print("Hello " + name + ". Your lucky number is " + str(number))
```

    Hello Marisol. Your lucky number is 63
    Hello Ardashir. Your lucky number is 72



```python
# Define a function that simplifies the above code and makes it reusable.
def lucky_number(name):
    number = len(name)*9
    print("Hello " + name + ". Your lucky number is " + str(number))

lucky_number("Marisol")
lucky_number("Ardashir")
```

    Hello Marisol. Your lucky number is 63
    Hello Ardashir. Your lucky number is 72



```python
# This code requests a number from the user and returns its factorial,
# printing each iteration of the multiplication.
a = input(); y = 1

for i in range(int(a)):
    y = y*(i+1)
    print(y)
```


```python
# This function takes an integer as an input and returns its factorial.
def factorial(n):
    # Exclude 0 as product, start with 1
    y = 1
    for i in range(int(n)):
        y = y*(i+1)
    return y

# Enter a numerical value between 1-9 in the command line that appears.
input_num = input()
# Apply factorial function to an integer input
print(factorial(input_num))
```

<a name="3"></a>
## 3. [Use comments to scaffold your code](https://www.coursera.org/learn/get-started-with-python/lecture/EKWJa/use-comments-to-scaffold-your-code)


```python
def seed_calculator(fountain_side, grass_width):
    """
    Calculate number of kilograms of grass seed needed for
    a border around a square fountain.

        Parameters:
            fountain_side (num): length of 1 side of fountain in meters
            grass_width (num): width of grass border in meters

        Returns:
            seed (float): amount of seed (kg) needed for grass border
    """
    # Area of fountain
    fountain_area = fountain_side**2
    # Total area
    total_area = (fountain_side + 2 * grass_width)**2
    # Area of grass border
    grass_area = total_area - fountain_area
    # Amount of seed needed (35 g/sq.m)
    seed = grass_area * 35
    # Convert to kg
    seed = seed / 1000

    return seed
```


```python
seed_calculator(12, 2)
```

<a name="4"></a>
## 4. [Make comparisons using operators](https://www.coursera.org/learn/get-started-with-python/lecture/JvbMh/make-comparisons-using-operators) 


```python
# > checks for greater than
print(10>1)
```


```python
# == checks for equality
print("cat" == "dog")
```


```python
# != checks for inequality
print(1 != 2)
```


```python
# Some operators cannot be used between different data types.
print(1 < "1")
```


```python
# Letters that occur earlier in the alphabet evaluate to less than letters from later in the alphabet.
# BOTH sides of an `and` statement must be true to return True.
print("Yellow" > "Cyan" and "Brown" > "Magenta")
```


```python
# An `or` statement will return True if EITHER side evaluates to True.
print(25 > 50 or 1 != 2)
```


```python
# `not` reverses Boolean evaluation of what follows it.
print(not 42 == "Answer")
```

<a name="5"></a>
## 5. [Use if/elif/else statements to make decisions](https://www.coursera.org/learn/get-started-with-python/lecture/6JsS8/use-if-elif-else-statements-to-make-decisions)


```python
# Define a function that checks validity of username based on length.
def hint_username(username):
    if len(username) < 8:
        print("Invalid username. Must be at least 8 characters long.")
    else:
        print("Valid username.")
```


```python
# Define a function that uses modulo to check if a number is even.
def is_even(number):
    if number % 2 == 0:
        return True
    return False
```


```python
is_even(19)
```


```python
# Define a function that checks validity of username based on length.
def hint_username(username):
    if len(username) < 8:
        print("Invalid username. Must be at least 8 characters long.")
    elif len(username) > 15:
        print("Invalid username. Cannot exceed 15 characters.")
    else:
        print("Valid username.")
```


```python
hint_username("ljñkljfñklasdjflkñadjglk{a")
```

**Congratulations!** You've completed this lab. However, you may not notice a green check mark next to this item on Coursera's platform. Please continue your progress regardless of the check mark. Just click on the "save" icon at the top of this notebook to ensure your work has been logged.
