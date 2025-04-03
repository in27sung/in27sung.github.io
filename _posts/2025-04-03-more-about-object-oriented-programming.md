---
layout: post
title: More about object-oriented programming
subtitle: The power of Python
author: Insung
categories: [Google Advanced Data Analytics]
tags: [Data Science, Google, Get Started with Python]
top:
---

This reading contains only a brief introduction to object-oriented programming. A more detailed discussion about the nuances of object oriented programming is beyond the scope of this course.

Previously, we identified object-oriented programming as a programming paradigm that is based around objects, which can contain both data and code that manipulates that data. You may recall that a class is an object’s data type that bundles data and functionality together, and you’ve encountered some examples of this class-specific functionality in the form of methods and attributes. In this reading, you’re going to learn more about object-oriented programming and how it works. Although this certificate program will not require you to define your own classes, having a basic understanding of how this process works will be very helpful when you encounter these concepts along your learning journey.

#### Review:Attributes and methods

Python classes are powerful and convenient because they come with build-in features that simplify common data analysis tasks. These features are known as attributes and methods.

- **Attribute:** A value associated with an object or class which is referenced by name using dot notation.

- **Method:** A function that belongs to a class and typically performs an action or operation. 

A simpler way of thinking about the distinction between attributes and methods is to remember that attributes are characteristics of the object, while methods are actions or operations.

For example, if the class were Spaceship, then attributes might be:

`name`

`kind`

`speed`

`tractore_beam`

These attritbues could be accessed by typing:

`Spaceship.name`

`Spaceship.kind`

`Spaceship.speed`

`Spaceship.tractor_beam`

Notice that these characteristics are accessed using only a dot.

On the other hand, methods of the Spaceship class might be:

`warp()`

`tractor()`

These methods could be used by typing:

`Spaceship.warp()`

`Spaceship.tractor()`

Notice that methods are followed by parentheses, and it's possible for them to take arguments. For example, `Spaceship.warp(7)` could change the speed of the ship to warp seven.

#### Defining classes with unique attributes and methods

Python lets you define your own classes, each with their own special attributes and methods. This helps all different kinds of programmers to build reusable code that makes their work more efficient. You can even build the Spaceship class mentioned previously. The example, here, demonstrates how to do this. 

**Note:** The following code block is not interactive.

```Python
class Spaceship:
   # Class attribute
   tractor_beam = 'off'

   # Instance attributes
   def __init__(self, name, kind):
       self.name = name
       self.kind = kind
       self.speed = None

  # Instance methods
   def warp(self, warp):
       self.speed = warp
       print(f'Warp {warp}, engage!')

   def tractor(self):
       if self.tractor_beam == 'off':
           self.tractor_beam = 'on'
           print('Tractor beam on.')
       else:
           self.tractor_beam = 'off'
           print('Tractor beam off')
```
