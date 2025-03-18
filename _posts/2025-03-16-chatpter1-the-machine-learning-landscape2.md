---
layout: post
title: "Type of Machine Learning System"
subtitle: "Chapter 1. The Machine Learning Landscape"
author: Insung
excerpt_image: assets/images/Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.jpg
categories: [Machine Learning]
tags: [Machine Learning]
top:
---
## Chapter 1. The Machine Learning Landscape 2
---

## <span style="color:#800000">Type of Machine Learning Systems</span>
There are so many different types of machine learning systems that it is useful to classify them in broad categories, based on the following criteria:

- How they are supervised during training (supervised, unsupervised, semi-supervised, self-supervised, and others)
- Whether or not they can learn incrementally on the fly(online versus batch learning)
- Whether they work by simply comparing new data points to known data points, or instead by detecting patterns in the training data and building a predictive model, much like scientist do(instance-based versus model-based learning)

These criteria are not exclusive; you can combine them in any way you like. For example, a state-of-the-art spam filter may learn on the fly using a deep neural network model trained using human-provided examples of spam and ham; this makes it an online, model-based, supervised learning system.

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


---

### Instance-Based Versus Model-Based Learning
One more way to categorise machine learning systems is by how they generalise. Most machine learning tasks are about making predictions. This means that given a number of training examples, the system needs to be able to make good predictions for (generalise to) examples it has never seen before. Having a good performance measure on the training data is good, but insufficient; the true goal is to perform well on new instances.

There are two main approaches to generalisation: instance-based learning and model-based learning.

### <span style="color:#666666">Instance-based learning</span>
Possibly the most trivial form of learning is simply to learn by heart.If you were to create a spam filter this way, it would just flag all emails that are identical to emials that have already been flagged by users - not the worst solution, but certainly not the best.

Instead of just flagging emails that are identical to known spam emails, your spam filter could be programmed to also flag emails that are very similar to known spam emails. This requries a measure of similarity between two emails. A (very basic) Similarity measure bewteen two emails could be to count the number of words they have in common. The system would flag an email as spam if it has many words in common with a known spam email.

This is called instance-based learning: the system learns the examples by heart, then generalises to new cases by using a similarity measure to compare them to the learned examples (or a subset of them). For example, in [Figure 1-16]() the new instance would be classified as a triangle because the majority of the most similar instances belong to that class. 

![Figure 1-16](https://github.com/user-attachments/assets/53e71d73-b5a5-48da-bbe2-ab8387f99479)

### <span style="color:#666666">Model-based learning and a typical machine learning workflow</span>
Another way to generalise from a set of examples is to build a model of these examples and then use that model to make predictions. This is called model-based learning ([Figure 1-17]()).

![Figure 1-17](https://github.com/user-attachments/assets/2e353aa4-63c0-41ce-a2cb-37afeaa3f8d9)

For example, suppose you want to know if money makes people happy, so you download the better Life Index data from the [OECD's website]() and [World Bank stats]() about gross domestic product(GDP) per capita. Then you join the tables and sort by GDP per capita. [Table 1-1]() shows an excerpt of what you get.

![Table 1-1](https://github.com/user-attachments/assets/526d5f44-56d0-4365-8139-9ff0c2cad2ff)

Let's plot the data for these countires([Figure 1-18]())

![Figure 1-18](https://github.com/user-attachments/assets/ab9eef58-87d2-40df-b613-80ee7b1a7f3c)
