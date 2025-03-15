---
layout: post
title: "Training Supervision"
subtitle: "Part I The Fundamentals of Machine Learning"
author: Insung
excerpt_image: assets/images/Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.jpg
categories: [Machine Learning]
tags: [Machine Learning]
top:
---
## Chapter 1. The Machine Learning Landscape

### Traning Supervision
ML systems can be classified according to the amount and type of supervision they get suring training. There are many categories, but we'll discuss the main ones: supervised learning, unsupervised learning, self-supervised learning, semi-supervised learning, and reinforcement learning.

#### Supervised learning
In supervised learning, the training set you feed to the algorithm includes the desired sloutions, called **labels** ([Figure 1-5]()).

A typical supervised learning taks is *classification*. The spam filter is a good example of this: it is trained with many example emails along with their class(spam or ham), and it must learn how to classify new emails.

Another typical task is to predict a *target* numeric value, such as the price of a car, given a set of *features* (mileage, age, barnd, etc.). This sort of task is called regression ([Figure 1-6]()). To train the system, you need to give it many examples of cars, including both their features and their targets(i.e., their prices).

Note that some regression models can be used for classification as well, and vice versa. For example, *logistic regression* is commonly used for classification, as it can output a value that corresponds to the probability of belonging to a given calss(e.g., 20% chance of being spam).