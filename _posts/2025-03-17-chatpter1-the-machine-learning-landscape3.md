---
layout: post
title: "Main Challenges of Machine Learning"
subtitle: "Chapter 1. The Machine Learning Landscape 3"
author: Insung
excerpt_image: assets/images/Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.jpg
categories: [Machine Learning]
tags: [Machine Learning]
top:
---

---

## <span style="color:#800000">Main Challenges of Machine Learning</span>

In short, since your main task is to select a model and train it on some data, the two things that can go wrong are "bad model" and "bad data". Let's start with examples of bad data.

### Insufficient Quantity of Training Data
For a toddler to learn what an apple is, all it takes is for you to point to an apple and say "apple" (possibly repeating this procedure a few times). Now the child is able to recognise apples in all sorts of colours and shapes.

Machine learning is not quite there yet; it takes a lot of data for most machine learning algorithms to work properly. Even for very simple problems you typically nned thousands of examples, and for complex problems such as image or speech recognistion you may need millions of examples (unless you can reuse parts of an existing model).


> ## The Unreasonable Effectiveness of Data
> In a [famous paper](https://dl.acm.org/doi/10.3115/1073012.1073017) published in 2001, Microsoft researchers Muchele Banko and Eric Brill showed that very different machine learning algorithms, including fairly simple ones, performed almost identically well on a complex problem of natural language disambiguation once they were given enough data (as you can see in [Figure 1-21]()).
>
> As the authors put it, "these results suggest taht we may want to reconsider the trade-off bewteen spending time and money on algorithm development versus spending it on corpus developement"
> 
> The idea that data matters more than algorithms for xomplex problems was further popularised by Peter Borvig et al. in a paper titled ["The Unreasonable Effectiveness of Data"](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/35179.pdf), published in 2009. It should be noted, however, that small and medium-sized datasets are still very common, and it is not always easy or cheap to get extra training data.

### Nonrepresentative Training Data
In order to generalise well, it is crucial that your training data be representative of the new cases you want to generalise to. This is true whether you use instance-based learning or model-based learning.

For example, the set of countries you used ealer for training the linear model was not perfectly representative; it did not contain any country with a GDP per capita lower than $23,500 or higher than $62,500. [Figure 1-22]() shows what the data looks like when you add such countries.
![Figure 1-22](https://github.com/user-attachments/assets/c3cfa7d1-2591-4a5b-bdaa-46fd95e4ea53)

### Poor-Quality Data
Obviously, if your training data is full of errors, outliers, and noise(e.g., due to poor-quality measurements), it will make it harder for the system to detect underlying patterns, so your system is less liekly to perform well. It is often well worth the effort to spend time clearning up your training data. The truth is, most data scientists spend a significant part of their time doing just that. The following are a couple examples of when you'd want to clean up training data:
- If some instances are clearly outliers, it may help to somply discard them or try to fix the errors manually.
- If some instances are missing a few features (e.g., 5% of your customers did not specify their age), you must decide whether you want to ignore this attribute altogether, ignore these instances, fill in the missing values (e.g., with the median age), or train one model with the feature and one model without it.
- Creating new features by gathering new dadta

Now that we have looked at many examples of bad data, let's look at a couple examples of bad algorithms. 

### Overfitting the Training Data 
Say you are visiting a foreign country and the taxi driver rips you off. You might be tempted to say that all taxi drivers in that country are thieves. Overgeneralising is something that we humans do all too often, and unfortunately machines can fall into the same trap if we are not careful. In machine learning this is called overfitting: it means that the model performs well on the training data, but it does not generalise well.

[Figure 1-23]() shows an example of a high-degree polynomial life satisfaction model that strongly overfits the training data. Even though it performs much better on the training data than the simple linear model, would you really trust its predictions?

![Figure 1-23](https://github.com/user-attachments/assets/d976b1ae-8b70-4565-8c66-e2cbf9770f34)

Complex models such as deep neural networks can detect subtle patterns in the data, but if the training set is noisy, or if it is too small, which introduces sampling noise, then the model is likely to detect patterns in the noise itself (as in the taxi driver example). Obviously these partterns will not generalise to new instances. For example, say you feed your life satisfaction model many more attributes, including uniinformative ones such as the country's name. In that case, a complex model may detect patterns like the fact that all countires in the training data with a $w$ in their name have a life satisfaction greater than 7: New Zealand (7.3), Norway (7.6), Sweden (7.3), and Switzerland (7.5). How confident are you that the w-satisfaction rule generalises to Rwanda or Zimbabwe? Obviously this pattern occurred in the training data by pure chance, but the model has no way to tell whether a pattern is real or simply the result of noise in the data.

> <span style="color:#884848">Warning</span>
>
> Overfitting happens when the model is too complex relative to the amount and noisiness of the training data. Here are possible solutions:
> - Simplify the model by selecting one with fewer parameters (e.g., a linear model rather than a high-degree polynomial model), by reducing the number of attributes in the training data, or by constraining the model.
> - Gather more trainig data
> - Reduce the noise in the training data (e.g., fix data errors and remove outliers).


