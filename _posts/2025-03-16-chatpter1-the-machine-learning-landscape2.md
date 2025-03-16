---
layout: post
title: "Chapter 1. The Machine Learning Landscape"
subtitle: "Traning Supervision"
author: Insung
excerpt_image: assets/images/Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.jpg
categories: [Machine Learning]
tags: [Machine Learning]
top:
---
## Chapter 1. The Machine Learning Landscape
---

### Traning Supervision
ML systems can be classified according to the amount and type of supervision they get suring training. There are many categories, but we'll discuss the main ones: supervised learning, unsupervised learning, self-supervised learning, semi-supervised learning, and reinforcement learning.

### Supervised learning
In supervised learning, the training set you feed to the algorithm includes the desired sloutions, called **labels** ([Figure 1-5]()).

A typical supervised learning taks is *classification*. The spam filter is a good example of this: it is trained with many example emails along with their class(spam or ham), and it must learn how to classify new emails.

Another typical task is to predict a *target* numeric value, such as the price of a car, given a set of *features* (mileage, age, barnd, etc.). This sort of task is called regression ([Figure 1-6]()). To train the system, you need to give it many examples of cars, including both their features and their targets(i.e., their prices).

Note that some regression models can be used for classification as well, and vice versa. For example, *logistic regression* is commonly used for classification, as it can output a value that corresponds to the probability of belonging to a given calss(e.g., 20% chance of being spam).

> ### Note
> The words *target* and *label* are generally treated as sysnonyms in supervised learning, but *target* is more common in regression tasks and *label* is more common in classification tasks. Moreover, *features* are sometimes called *predictors* or *attributes*. These terms may refer to indicidual samples (e.g., "this car's mileage feature is equal to 15,000") or to all samples (e.g., "the mileage feature is strongly correlated with price").

### Unsupervised learning
In unsupervised learning, as you might guess, the training data is unlabeled([Figure 1-7]()). The system tries to learn without a teacher. For example, say you have a lot of data about your blog's visitors. You may want to run a clustering algorithm to try to detect groups of similar visitors([Figure 1-8]()). At no point do you tell the algorithm which group a visitor belongs to: it finds those connections without your hlep. For example, it might notice that 40% of your visitors are teenagers who love comic books and generally read your blog after school, while 20% are adults who enjoy sci-fi and who visit during the weekends. If you use a *hierarchical clustering* algorithm, it may also subdivide each group into smaller groups. This may help you target your posts for each group.


*Visualisation* algorithms are also good examples of unsupervised learning: you feed them a lot of complex and unlabeled data, and they ouput a 2D or 3D representation of your data that can easily be plotted ([Figure 1-9]()). These algorithms try to preserve as much structure as they can (e.g., trying to keep separate clusters in the input space from overlapping in the visualisation) so that you can understand how the data is organised and perhaps identify unsuspected patterns.

A related task is **dimentionality reduction**, in which the goal is to simplify the data without losing too much information. One wa to do this is to merge several correlated features into one. For example. a car's mileage may be strongly correlated with its age, so the dimensionality reduction algorithm will merge them into one feature that represents the car's wear and tear. This is called **feature extraction**.