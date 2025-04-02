---
layout: post
title: "Annotated follow-along guide: Hello, Python!"
subtitle: Get Started with Python - The power of Python
author: Insung
categories: [Google Advanced Data Analytics]
tags: [Data Science, Google]
top:
---
<video controls width="100%" style="max-width: 720px;">
  <source src="https://d3c33hcgiwev3.cloudfront.net/AGuVcwrcTyOsgS6eH5ZlMw.processed/full/720p/index.mp4?Expires=1743638400&Signature=ayHdSU79sj7oHfpWiIzzCvNuPvDK23pItDkVH6ITJ9I0DCURJu2XSpYqAcGqHGZrk2VJqvQY3~FE-8iv4hp79WrlfQDbWlkOGMxHofRqI1Zmx4GyCt7YzYRCAjvI0OtS6CZeUPEuqrS3p6z8gPP-IQ8VPWXHPtxn2kXZv~YCbqQ_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" type="video/mp4">
  Your browser does not support the video tag.
</video>
<p class="source-text"><em>Source: "Discover more about Python" - Google Advanced Data Analytics Professional Certificate</em></p>

## Annotated follow-along guide: Hello, Python!

This notebook contains the code used in the instructional videos from [Module 1: Hello, Python!](https://www.coursera.org/learn/get-started-with-python/home/module/1).


### Introduction

This follow-along guide is an annotated Jupyter Notebook organized to match the content from each module. It contains the same code shown in the videos for the module. In addition to content that is identical to what is covered in the videos, you’ll find additional information throughout the guide to explain the purpose of each concept covered, why the code is written in a certain way, and tips for running the code.

As you watch each of the following videos, an in-video message will appear to advise you that the video you are viewing contains coding instruction and examples. The in-video message will direct you to the relevant section in the notebook for the specific video you are viewing. Follow along in the notebook as the instructor discusses the code.

To skip directly to the code for a particular video, use the following links:

1.   **[Discover more about Python](#1)**
2.   **[Jupyter Notebook](#2)**
3.   **[Object-oriented programming](#3)**
4.   **[Variables and data types](#4)**
5.   **[Create precise variable names](#5)**
6.   **[Data types and conversions](#6)**

<a name="1"></a>
## 1. [Discover more about Python](https://www.coursera.org/learn/get-started-with-python/lecture/JC2zu/discover-more-about-python)



```python
# Print to the console.
print("Hello, world!")
```

    Hello, world!



```python
# Print to the console.
print(22)
```

    22



```python
# Simple arithmetic
(5 + 4) / 3
```




    3.0




```python
# Assign variables.
country = 'Brazil'
age = 30

print(country)
print(age)
```

    Brazil
    30



```python
# Evaluations
# Double equals signs are used to check equivalency.
10**3 == 1000
```




    True




```python
# Evaluations
# A single equals sign is reserved for assignment statements.
10 ** 3 = 1000
```


      File "<ipython-input-6-8baa8abf97f4>", line 3
        10 ** 3 = 1000
                      ^
    SyntaxError: can't assign to operator




```python
# Evaluations
# Double equals signs are used to check equivalency.
10 * 3 == 40
```




    False




```python
# Evaluations
# Double equals signs are used to check equivalency.
10 * 3 == age
```




    True




```python
# Conditional statements
if age >= 18:
    print('adult')
else:
    print('minor')
```

    adult



```python
# Loops
for number in [1, 2, 3, 4, 5]:
    print(number)
```

    1
    2
    3
    4
    5



```python
# Loops
my_list = [3, 6, 9]

for x in my_list:
    print(x / 3)
```

    1.0
    2.0
    3.0



```python
# Functions
def is_adult(age):

    if age >= 18:
        print('adult')
    else:
        print('minor')
```


```python
# Use the function that was just created.
is_adult(14)
```

    minor



```python
# Use the built-in sorted() function.
new_list = [20, 25, 10, 5]

sorted(new_list)
```




    [5, 10, 20, 25]



<a name="2"></a>
## 2. [Jupyter Notebooks](https://www.coursera.org/learn/get-started-with-python/lecture/2l42i/jupyter-notebooks)

**NOTE:** The import statements cell must be run before running some of the following cells. This setup step was not shown in the instructional video, but you will learn about import statements later in this course.


```python
# Import statements.
import warnings
warnings.filterwarnings('ignore')

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import seaborn as sns
```


```python
# Create a list.
my_list = [10, 'gold', 'dollars']
```


```python
# Use the helper function to calculate F1 score used in the following graphics.
def f1_score(precision, recall):
    score = 2*precision*recall / (precision + recall)
    score = np.nan_to_num(score)

    return score
```


```python
# Generate a graph of F1 score for different precision and recall scores.
x = np.linspace(0, 1, 101)
y = np.linspace(0, 1, 101)
X, Y = np.meshgrid(x, y)
Z = f1_score(X, Y)
fig = plt.figure()
fig.set_size_inches(10, 10)
ax = plt.axes(projection='3d')
ax.plot_surface(X, Y, Z, rstride=2, cstride=3, cmap='plasma')

ax.set_title('$F_{1}$ of precision, recall', size=18)
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('z')
ax.view_init(35, -65)
```


![png](output_22_0.png)


**NOTE:** The following cells use markdown (like this cell) to create formatted text like headers and bullets, tables, and mathematical equations. You can select any cell and enter into edit mode to view the markdown text. Then run the cell to view the rendered output.

### **Section 2**

* Part 1:
* Part 2:

|Title|Author|Date|
|:--|:--|:-:|
|The Art of War|Sun Tzu|5th cent. BCE|
|Don Quixote de la Mancha|Miguel de Cervantes Saavedra|1605|
|Pride and Prejudice|Jane Austen|1813|


$$
  \int_0^\infty \frac{x^3}{e^x-1}\,dx = \frac{\pi^4}{15}
$$

<a name="3"></a>
## 3. [Object-oriented programming](https://www.coursera.org/learn/get-started-with-python/lecture/1SJMN/object-oriented-programming) 


```python
# Assign a string to a variable and check its type.
magic = 'HOCUS POCUS'
print(type(magic))
```

    <class 'str'>



```python
# Use the swapcase() string method to convert from caps to lowercase.
magic = 'HOCUS POCUS'
magic = magic.swapcase()
magic
```




    'hocus pocus'




```python
# Use the replace() string method to replace some letters with other letters.
magic = magic.replace('cus', 'key')
magic
```




    'hokey pokey'




```python
# Use the split() string method to split the string into two strings.
magic = magic.split()
magic
```




    ['hokey', 'pokey']




```python
# Set up the cell to create the `planets` dataframe.
# (This cell was not shown in the instructional video.)
import pandas as pd
data = [['Mercury', 2440, 0], ['Venus', 6052, 0,], ['Earth', 6371, 1],
        ['Mars', 3390, 2], ['Jupiter', 69911, 80], ['Saturn', 58232, 83],
        ['Uranus', 25362, 27], ['Neptune', 24622, 14]
]

cols = ['Planet', 'radius_km', 'moons']

planets = pd.DataFrame(data, columns=cols)
```


```python
# Display the `planets` dataframe.
planets
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Planet</th>
      <th>radius_km</th>
      <th>moons</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mercury</td>
      <td>2440</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Venus</td>
      <td>6052</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Earth</td>
      <td>6371</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mars</td>
      <td>3390</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jupiter</td>
      <td>69911</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Saturn</td>
      <td>58232</td>
      <td>83</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Uranus</td>
      <td>25362</td>
      <td>27</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Neptune</td>
      <td>24622</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Use the shape dataframe attribute to check the number of rows and columns.
planets.shape
```




    (8, 3)




```python
# Use the columns dataframe attribute to check column names.
planets.columns
```




    Index(['Planet', 'radius_km', 'moons'], dtype='object')



<a name="4"></a>
## 4. [Variables and data types](https://www.coursera.org/learn/get-started-with-python/lecture/k3ex2/variables-and-data-types) 


```python
# Assign a list containing players' ages.
age_list = [34, 25, 23, 19, 29]
```


```python
# Find the maximum age and assign to `max_age` variable.
max_age = max(age_list)
max_age
```




    34




```python
# Convert `max_age` to a string.
max_age = str(max_age)
max_age
```




    '34'




```python
# Reassign the value of `max_age`.
max_age = 'ninety-nine'
max_age
```




    'ninety-nine'




```python
# FIRST, RE-RUN THE SECOND CELL IN THIS VIDEO.
# Check the value contained in `max_age` (SHOULD OUTPUT 34).
max_age
```




    'ninety-nine'




```python
# Find the minimum age and assign to `min_age` variable.
min_age = min(age_list)

# Subtract `min_age` from `max_age`
max_age - min_age
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-20-cd60915be1ae> in <module>
          3 
          4 # Subtract `min_age` from `max_age`
    ----> 5 max_age - min_age
    

    TypeError: unsupported operand type(s) for -: 'str' and 'int'


<a name="5"></a>
## 5. [Create precise variable names](https://www.coursera.org/learn/get-started-with-python/lecture/fB03O/create-precise-variable-names) 


```python
# Trying to assign a value to a reserved keyword will return a syntax error.
else = 'everyone loves some esparagus'
```


      File "<ipython-input-55-1f1f078fc2a2>", line 2
        else = 'everyone loves some esparagus'
           ^
    SyntaxError: invalid syntax




```python
# The word "asparagus" is misspelled. That's allowed.
esparagus = 'everyone loves some esparagus'
```


```python
# Order of operations
2 * (3 + 4)
```




    14




```python
# Order of operations
(2 * 3) + 4
```




    10




```python
# Order of operations
3 + 4 * 10
```




    43



<a name="6"></a>
## 6. [Data types and conversions](https://www.coursera.org/learn/get-started-with-python/lecture/z9zda/data-types-and-conversions)


```python
# Addition of 2 ints
print(7+8)
```

    15



```python
# Addition of 2 strings
print("hello " + "world")
```

    hello world



```python
# You cannot add a string to an integer.
print(7+"8")
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-62-199724c0b4c0> in <module>
          1 # You cannot add a string to an integer
    ----> 2 print(7+"8")
    

    TypeError: unsupported operand type(s) for +: 'int' and 'str'



```python
# The type() function checks the data type of an object.
type("A")
```




    str




```python
# The type() function checks the data type of an object.
type(2)
```




    int




```python
# The type() function checks the data type of an object.
type(2.5)
```




    float




```python
# Implicit conversion
print(1 + 2.5)
```

    3.5



```python
# Explicit conversion (The str() function converts a number to a string.)
print("2 + 2 = " + str(2 + 2))
```

    2 + 2 = 4


**Congratulations!** You've completed this lab. However, you may not notice a green check mark next to this item on Coursera's platform. Please continue your progress regardless of the check mark. Just click on the "save" icon at the top of this notebook to ensure your work has been logged.
