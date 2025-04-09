---
layout: post
title: "Reference guide: Functions"
subtitle: Functions
author: Insung
categories: [Google Advanced Data Analytics]
tags: [Data Science, Coursera, Get Started with Python]
top:
---

As you’ve been learning, functions are bodies of reusable code for performing specific processes or tasks. They help you do more work with less code. Function examples include: 

- A specific calculation or measurement, such as converting Fahrenheit to Celsius

- An inventory utility to iterate quantities and calculate the total cost of goods in stock

- Building a DataFrame from a series or dictionary data

- An application utility such as a spell checker

In this reading, you will learn how to define, build, and call functions. 

#### Save this course item

You may want to save a copy of this guide for future reference. You can use it as a resource for additional practice or in your future professional projects. To access a downloadable version of this course item, click the following link and select “Use Template.” 

[Reference guide: Functions](https://docs.google.com/document/d/1Kxm7hv3w6ddQ6C2-m1ZNWD-EWte5QDlF6it0unmLjaw/template/preview?resourcekey=0-BeaGUzArCDKD0NLcRvzSGw)

#### Functions syntax

define functions using the following syntax and format:

**Note:** The following code block is not interactive.

```Python
def my_functions(parameters):
    '''
    Docstring.
    Summarise the function's behaviour and explain its arguments and return values.
    '''
    cide block

    return value
```

1. Begin with the def keyword followed by the function’s name, then put its parameters/arguments in parentheses, ending with a colon.

    - Python convention is to use snake_case (lowercase words separated by underscores) for function names.

2. For important functions or functions whose purposes or operations are not very obvious, include a docstring. Write the docstring between three opening and closing quotation marks. 

    - The docstring should be in the form of a command (e.g., “Add two numbers” as opposed to “Adds two numbers”).

    - The docstring should summarize the function’s behavior and explain its arguments and return values.

    - The docstring should be indented four spaces from the definition statement.

3. Write the body of the function. 

    - All code should be indented at least four spaces from the definition statement, but there can be many levels of indentation depending on the complexity of the code. 

4. Finally, use a return statement to return a value or a print statement to print something to the console and complete the function. This line should also be indented four spaces.


### return vs. print

Sometimes the difference bewteen return statements and print statements isn't clear to new learners of Python. It's important to understand what each action is and when to use it. Return statements give you a result that you can use for something else. It doesn't have to be something that prints when the function is run. Print statements print something to the console and nothing more. Think of it like this: a return statement is like your brother going to the market and bringing you back a bag of potatos. A print statement is like your brother going to the market, coming home, and telling you what kind of potatoes were for sale. With the retun statement, you have some potatoes to cook. With the print statement, you just know what potatoes are available, but you don't have any potateos.

### Functions vs. methods

Functions and methods are very similar, but there are a few key differences. Methods are a specific type of function. They are functions that belong to a class. This means that you can use them—or “call” them—by using dot notation. 

**Method example:**
```Python
my_string = 'The eagles filled the sky.'
my_string.split()
```
    ['The', 'eagles', 'filled', 'the', 'sky.']

The split method is a function that belongs to the string calss. It splits strings on their whitespaces. Standalone functions do not belong to a particular class and can often be used on multiple classes.

**Note:** The following code block is not interactive.

**Functions example:**
```Python
sum([6,3])
```
    9

You can review [Python’s list of built-in functions](https://docs.python.org/3/library/functions.html) and research how other people use them in the [Jupyter forum](https://discourse.jupyter.org/), [StackOverflow](https://stackoverflow.com/questions), and other online communities. 


### Resources for more information 
For more information on functions, consider the Python [Reference Library](https://docs.python.org/3/library/), [Data types](https://docs.python.org/3/library/stdtypes.html), [Functions](https://docs.python.org/3/library/functions.html#built-in-functions), [Symbols](https://wiki.python.org/moin/PythonGlossary?action=AttachFile&do=view&target=PySymbols.html)

- [Built-in functions](https://docs.python.org/3/library/functions.html#built-in-functions)
    - [enumerate](https://docs.python.org/3/library/functions.html#enumerate)
    - [isinstance](https://docs.python.org/3/library/functions.html#isinstance)
    - [dict](https://docs.python.org/3/library/functions.html#func-dict)
    - [type](https://docs.python.org/3/library/functions.html#type)
    - [len](https://docs.python.org/3/library/functions.html#len)
    - [set](https://docs.python.org/3/library/functions.html#func-set)
    - [zip](https://docs.python.org/3/library/functions.html#zip)

- [Docstring conventions](https://peps.python.org/pep-0257/): PEP 257 guide to writing docstings 