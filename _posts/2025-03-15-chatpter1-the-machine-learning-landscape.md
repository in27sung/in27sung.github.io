---
layout: post
title: "Chapter 1. The Machine Learning Landscape"
subtitle: "Part I The Fundamentals of Machine Learning"
author: Insung
excerpt_image: https://github.com/user-attachments/assets/8db81747-2d78-436d-8342-72db5423e4ff
categories: [Machine Learning]
tags: [Machine Learning]
top:
---
# Part I The Fundamentals of Machine Learning
## Chapter 1. The Machine Learning Landscape
---

In this chapter I will start by clarifying what machine learning is and why you may want to use it.
Then, befroe we set out to explore the machine learning continent, we will take a look at the map and elarn about the main regions and the most notable landmarks: supervised versus unsupervised learning and thier varinats, online versus batch learning, instance-based versus model-based learning. Then we will look at the workflow of a typical ML project, dicuss the main challenges you may face, and cover how to evaluate and fine-tune a machine learning system.

### What Is Machine Learning?

Machine learning is the science (and art) of programming computers so they can learn from data.

Here is a slightly more general definition:

> "Machine learning is the field of study that gives computers the ability to learn without being explicitly programmed." – Arther Samuel, 1959

And a more engineering-oriented one:

> "A computer program is said to learn from expereince E with respect to some task T and some performance measure P, if its performance on T, as measured by Pm improves with expereience E. - Tom Mitchell, 1997

Your spam filter is a machine learning program that, given examples of spam emails (flagged by users) and examples of regular emails (nonspam, also called "ham"), can learn to flag spam. The examples that the system uses to learn are called the **training set**. Each training example is called a **training instance** (or sample). The part of a machine learning system that learns and makes predictions is called a **model**. Neural networks and random forests are examples of modles. the task T is to flag spam for new emails, the expereience E is thr training data, and the performance measure P needs to be defined; for example, you can use the ratio of correctly classified emails. This particular performance measure is called **accuracy**, and it is often used in classification tasks.

### Why Use Machine Learning?

Consider how you would write a spam filter using traditional programming techniques ([Figure 1-1](https://github.com/user-attachments/assets/8db81747-2d78-436d-8342-72db5423e4ff)):

1. First you would examine what spam typically looks like. You might notice that some words or phrases (such as "4U", "credit card", "free", and "amazing") tend to come up a lot in the subject line. Perhaps you would also notice a few other patterns in the sender's name, the email's body, and other parts of the eamil.

2. You would write a detection algorithm for each of the patterns that you noticed, and your program would flag emails as spam if a number of these patterns were detected.

3. You would test your program and repeat steps 1 and 2 until it was good enough to launch.

![Figure 1-1. The traditional approach](https://github.com/user-attachments/assets/8db81747-2d78-436d-8342-72db5423e4ff)

A rule-based spam filter becomes complex and hard to maintain due to numerous rules. In contrast, a machine learning-based filter automatically detects frequent spam patterns, making it shorter, easier to maintain, and more accurate.([Figure 1-2](https://github.com/user-attachments/assets/9b846ffc-d0a7-4a29-bf3c-41bafd5dec4f)).

![Figure 1-2. The machine learning approach](https://github.com/user-attachments/assets/9b846ffc-d0a7-4a29-bf3c-41bafd5dec4f)

Spammers can bypass traditional rule-based spam filters by altering keywords (e.g., changing “4U” to “For U”), requiring constant manual updates. In contrast, a machine learning-based spam filter automatically detects new spam patterns based on user feedback and adapts without manual intervention.([Figure 1-3](https://github.com/user-attachments/assets/b62c2d06-77ff-458b-9ace-b102c8abeabd))

![Figure 1-3. Automatically adapting to change](https://github.com/user-attachments/assets/b62c2d06-77ff-458b-9ace-b102c8abeabd)

Machine learning is particularly useful for solving problems that are too complex for traditional rule-based approaches or lack a known algorithm. Speech recognition is a prime example—while a simple program might distinguish “one” and “two” using high-pitch detection, this method does not scale to thousands of words spoken by diverse individuals in various environments and languages. Instead, the most effective approach today is to develop a machine learning model that learns from large datasets of recorded speech, enabling it to generalise across different speakers and conditions.

Machine learning enables humans to gain insights by analysing what models have learned([figure 1-4](https://github.com/user-attachments/assets/7ff93963-9256-4482-acab-42f8d26f9440)), though this can be challenging for some models. For example, a trained spam filter can reveal key words or word combinations that strongly indicate spam, sometimes uncovering unexpected correlations or emerging trends. This process, known as **data mining**, is where machine learning excels, helping to identify hidden patterns in large datasets and leading to a deeper understanding of complex problems.

![Figure 1-4. Machine learning can help humans learn](https://github.com/user-attachments/assets/7ff93963-9256-4482-acab-42f8d26f9440)

To summarise, machine learning is great for:
- Problems for which existing colutions require a lot of fine-tuning or long lists for rules(a machine learning model can often simplofy code and perform better than the traditional approach)

- Complex problems for which using a traditional approach yields no good solution (the best machine learning techniques can perhaps find a solution)

- Fluctuating environments (a machine learning system can easily be retrained on new data, always keeping it up to date)

- Getting insights about complex problems and large amounts of data

### Examples of Applications

Let's look at some concrete examples of machine learning tasks, along with the techniques that can tackle them:

*Analyzing images of products on a production line to automatically classify them*
- This is image classification, typically performed using **convolutional neural networks(CNNs)**.

*Detecting tumors in brain scans*
- This is semantic image segmentation, where each pixel in the image is classified (as we want to determine the exact location and shape of tumors), typically using CNNs or transformers.

*Automatically classifying news articles*
- This is **natural language processing(NLP)**, and more specifically text classification, which can be tackled using **recurrent neural networks(RNNs)** and CNNs, but transformers work even better.

*Creating a chatbot or a personal assistant*
- This involves many NLP components, including **natural language understanding(NLU)** and question-answering modules.

*Forecasting your company's revenue next year, based on many performance metrics*
- This is a regression task(i.e.,predicting values) that may be tackled using any regression model, such as a linear regression or polynomial regression model, a regression support vector machine, a regression random forest, or an artificial neural network. If you want to take into account sequences of past performance metrics, you may want to RNNs, CNNs, or transformers

*Segmenting vlients based on their purchases so that you can design a different marketing strategy for each segment*
- This is clustering, which can be achieved using k-means, DBSCAN, and more.

### Type of Machine Learning Systems
There are so many different types of machine learning systems that it is useful to classify them in broad categories, based on the following criteria:

- How they are supervised during training (supervised, unsupervised, semi-supervised, self-supervised, and others)
- Whether or not they can learn incrementally on the fly(online versus batch learning)
- Whether they work by simply comparing new data points to known data points, or instead by detecting patterns in the training data and building a predictive model, much like scientist do(instance-based versus model-based learning)

These criteria are not exclusive; you can combine them in any way you like. For example, a state-of-the-art spam filter may learn on the fly using a deep neural network model trained using human-provided examples of spam and ham; this makes it an online, model-based, supervised learning system.