---
layout: post
title: "Testing and Validating"
subtitle: "Chapter 1. The Machine Learning Landscape 3"
author: Insung
excerpt_image: assets/images/Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.jpg
categories: [Machine Learning]
tags: [Machine Learning]
top:
---

---

## <span style="color:#800000">Testing and Validating</span>

The only way to know how well a model will generalise to new cases is to actually try it out on new cases. One way to do that is to put your model in production and monitor how well it performs. This works well, but if your model is horribly bad, your users will complain--not the best idea.

A better option is to split your data into two sets: the *training set* and the *test set*. As these names imply, you train your model using the training set, and you test it using the test set. The error rate on new cases is called the *generalisation error* (or out-of-sample error), and by evaluating your model on the test set, you get an estimate of this error. This value tells you how well your model will perform on instances it has never seen before.

If the training error is low (i.e., your model makes few mistakses on the training set) but the generalisation error is high, it means that your model is overfitting the training data.

> ### Tip 
> It is common to use 80% of the data for training and hold out 20% for testing. However, this depends on the size of the dataset: if it contains 10 million instances, then holding out 1% means your test est will contain 100,000 instances, probably more than enoufh to get a good estimate of the generalisation error.

### Hyperparameter Tuning and Model Selection 
Evaluating a model is simple enough: just use a test set. But suppose you are hesitating bewteen two types of models (say, a linear model and a polynomial model): how can you decide between them? One option is to train both and compare how well they generalise using the test set.