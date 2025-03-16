---
layout: post
title: "Chapter 1. Exploratory Data Analysis"
subtitle: "50+ Essential Concepts Using R and Python"
author: Insung
excerpt_image: assets/images/Practical_Statistics_for_Data_Scientists_-_Peter_Gedeck.jpg
categories: [Data Science, Statistics]
tags: [Data Science, Statistics]
top:
---
## Chapter 1. Exploratory Data Analysis
---
This chapter focuses on the first step in any data science project: exploring the data. *Exploratory data analysis*, or EDA, is a comparatively new area of statistics. Classical statistics focused almost exclusively on *inference*, a sometimes complex set of procedures for drawing conclusinons about large populations based on small samples. In 1962, John W. Tukey called for a reformation of statistics in hisseminal paper "The Future of Data Analysis"[Tukey-1962]. He proposed a new scientific discipline called *data analysis* that included statistical inference as just one component. Tukey forged links to the engineering and computer science communities(he coined the terms *bit*, short for binary digit, and *software*), and his original tenets are surprisingly durable and form part of the foundation for data science. Key drivers of this discipline have been the rapid development of new technology, access tomore and bigger data, and the greater use of quantitative analysis in a variety of disciplines.

### Elements of Structured Data
Data comes from many sources: sensor measurements, events, text, images, and videos. The *Internet of Things*(IoT) is spewing out streams of information. Much of this data is unstructured: images are a collection of pixels with each pixel containing RGB(red, green, blue) colour information. Texts are sequences of words and nonword characters, often organised by sections, subsections, and so on. Clickstreams are sequences of actions by a user interacting with an app or web page. In fact, a major challenge of data sceince is to harness this torrent of raw data into actionable information. To apply the statistical concepts covered in this book, unstructured raw data must be processed and manipulated into a sturucted form as it might emerge from a relational database or be collected for a study.

### 📌 Key Terms for Data Types

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
- The possible values a given ategorical variable can take are enforced in the software(like an enum).

The third "benefit" can lead to unintended or unexpected behaviour: the default behaviour of dta import functions in R(e.g., `read.csv`) is to automatically convert a text column into a `factor`. Subsequent operations on that column will assume that the only allowable values for that column are the ones originally imported, and assigning a new text value will introduce a warning and produce and `NA`(missing value). The pandas package in Python will not make such a conversion automatically. You can however specify a column as categorical explicitly in the `read_csv` function.

> ### Key Ideas
> - Data is typically classified in software by type.
> - Data types include continuos, discrete, categorical (which includes binary), and ordinal.
> - Data typing in software acts as a signal to the software on how to process the data.


#### Further Reading
- [Pandas Documentation](https://pandas.pydata.org/docs/user_guide/basics.html#basics-dtypes)

### Rectangular Data 
The typical frame of reference for an analysis in data science is a rectangular data object, like a spreadsheet or database table.

### 📌 Key Terms for Rectangular Data

| **Key Term** | **Description** | **Synonyms** |
|-------------|-----------------|-------------|
| **Data Frame** | A rectangular data structure composed of rows and columns, commonly used in statistics and machine learning. Similar to a spreadsheet or SQL table. | Table, Spreadsheet, Matrix |
| **Feature** | A column in the data frame, representing a specific attribute or variable. Features serve as inputs to machine learning models. | Attribute, Input, Predictor, Variable |
| **Outcome** | The target variable to be predicted, often binary (e.g., Yes/No) or continuous. Features are used to predict the outcome in models or experiments. | Dependent Variable, Response, Target, Output |
| **Record** | A row in the data frame, representing one instance, case, or observation of data. Each record contains values for all features and the outcome (if available). | Case, Example, Instance, Observation, Pattern, Sample |

### 🔑 Additional Notes:
- **Data Frame**: In Python, implemented as `pandas.DataFrame`. Fundamental for data manipulation and modelling.
- **Feature**: Also called **independent variable**. In supervised learning, used to predict outcomes.
- **Outcome**: Also called **dependent variable**, **label**, or **target**. The value models attempt to predict.
- **Record**: Each observation (row) in the dataset. Often referred to as a **sample** in machine learning contexts.

---

*Rectangular data* is essentially a two-dimentional matrix with rows indicating records(cases) and columns indicating features(variables). The data dosen't always start in this form: unstructured data(e.g., text) must be processed and manipulated so that it can be represented as a set of features in the rectangular data(see [Elements of Structured Data](/data%20science/statistics/2025/03/15/chatpter1-exploratory-data-analysis.html#h-elements-of-structured-data)). Data in relational databases must be extracted and put into a single table for most data analaysis and modeling tasks.
