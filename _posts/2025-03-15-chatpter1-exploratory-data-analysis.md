---
layout: post
title: "Practical Statistics for Data Scientists, 2nd Edition"
subtitle: "50+ Essential Concepts Using R and Python"
author: Insung
excerpt_image: assets/images/Practical_Statistics_for_Data_Scientists_-_Peter_Gedeck.jpg
categories: [Data Science, Statistics]
tags: [Data Science, Statistics]
top:
---
## Chapter 1. Exploratory Data Analysis
---


### Elements of Structured Data
Data comes from many sources: sensor measurements, events, text, images, and videos. The *Internet of Things*(IoT) is spewing out streams of information. Much of this data is unstructured: images are a collection of pixels with each pixel containing RGB(red, green, blue) colour information. Texts are sequences of words and nonword characters, often organised by sections, subsections, and so on. Clickstreams are sequences of actions by a user interacting with an app or web page. In fact, a major challenge of data sceince is to harness this torrent of raw data into actionable information. To apply the statistical concepts covered in this book, unstructured raw data must be processed and manipulated into a sturucted form as it might emerge from a relational database or be collected for a study.

# **📌 Key Terms for Data Types**

| Data Type | Description | Examples | Synonyms |
|-----------|------------|----------|----------|
| **Continuous** | Data that can take any real value within an interval. | Height (cm), Weight (kg), Temperature (°C), Salary (USD) | interval, float, numeric |
| **Discrete** | Data that can take only integer values, typically representing counts. | Number of students, Number of cars, Coin tosses | integer, count |
| **Categorical** | Data that belongs to a specific set of possible categories. | Blood type (A, B, O, AB), Country (Korea, USA) | enums, enumerated, factors, nominal, polychotomous |
| **Binary** | A special case of categorical data with only two possible values. | Gender (Male/Female), Approval (Yes/No), 0 and 1 | dichotomous, logical, indicator, boolean |
| **Ordinal** | Categorical data with an explicit order or ranking. | Grade (A > B > C), Satisfaction (Low < Medium < High) | ordered factor |

Why do we bother with a taxonomy of data types? It turns out that for the purposes of data analysis and predictive modeling, the data type is important to help determine the type of visual display, data analysis, or statistical model. In fact, data science software, such as R and Python, uses these data types to improve computational performace. More important, the data type for a variable determines how software will handle computations for that variable.

Software enginners and database programmmers may wonder why we even need the notion of *categorical* and *ordinal* data for analytics. After all, categories are merely a collection of text(or numeric) values, and the underlyting database automatically handles the internal representation. However, explicit identification of data as categorical, as distinct from text, does offer some advantages:

- Knowing that data is categorical can act as a signal telling software how statistical procedures, such as producting a chart or fitting a model, should behave. In particular, ordinal data can be represented as an `ordered.factor` in R, preserving a user-specified ordering in charts, tables, and models. In Python, scikit-learn supports ordinal data with the `sklearn.preprocessing.OrdinalEncoder`
- Storage and indexing can be optimised(as in a relational database).
- The possilbe values a given ategorical variable can take are enforced in the software(like an enum).