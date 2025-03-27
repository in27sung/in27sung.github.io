---
layout: post
title: World Happiness & Economic and Social Indicators Correlations
subtitle: Overview
author: Insung
categories: Project
tags: [Project, Artificial Intelligence, Machine Learning, Data Science]
top:
---

# World Happiness & Economic and Social Indicators Correlations

#### Video Demo:  <URL HERE>

#### Description: 
This project is submitted as the [**CS50 2025 Final Project**](https://cs50.harvard.edu/x/2025/project/).

## Overview

This project investigates the relationship between countries' happiness scores and key economic and social indicators. It specifically addresses data preprocessing challenges, including missing value treatment and data quality issues, to build reliable insights. The final output includes exploratory data analysis, data cleaning, modeling, and a summary of findings.


## Objectives

- Analyze how economic and social factors (GDP per capita, Life Expectancy, Education, Unemployment, etc.) influence the World Happiness Index.
- Handle real-world data issues, such as missing values and inconsistent data, through advanced preprocessing techniques.
- Apply different missing value treatment methods and compare their impact.
- Visualize correlations and trends.
- Build a basic regression model to predict happiness scores.

## Features

- Real-world datasets from trusted sources (World Happiness Report, World Bank, OECD).
- Detailed exploratory data analysis (EDA) and data profiling.
- Multiple missing value imputation techniques: Mean, Median, KNN, Indicator Variable, Deletion.
- Evaluation of preprocessing choices on analysis outcomes.
- Simple regression modeling.
- Clean, reproducible code and visualizations.

## Dataset Sources

1. **World Happiness Report (Official)**  
   URL: https://worldhappiness.report  
   Data: World Happiness Scores (2015–2024), downloaded from the official site.

2. **World Bank – GDP per capita (current US$)**  
   URL: https://data.worldbank.org/indicator/NY.GDP.PCAP.CD

3. **World Bank, OECD – Life Expectancy at Birth**  
   - World Bank: https://data.worldbank.org/indicator/SP.DYN.LE00.IN  
   - OECD: https://data-explorer.oecd.org

4. **World Bank – Unemployment Rate**  
   URL: https://data.worldbank.org/indicator/SL.UEM.TOTL.ZS

5. **World Bank – Educational attainment, at least Bachelor's or equivalent, population 25+, total (%)**  
   URL: https://data.worldbank.org/indicator/SE.TER.CUAT.BA.ZS

## Folder Structure

```
project/
├── data/
│   ├── raw/                               
│   │   ├── Education_Attainment_Bachelor_2015_2023.csv
│   │   ├── GDP_per_capita_2015_2023.csv
│   │   ├── OECD_Life_Expectancy_2015_2023.csv
│   │   ├── Unemployment_Rate_2015_2023.csv
│   │   ├── World_Happiness_Index_2015_2024.csv
│   │   └── WorldBank_Life_Expectancy_2015_2023.csv
│   └── processed/
│       ├── gpt_train_dataset.csv
│       ├── gpt_test_dataset(2023).csv
│       ├── train_dataset.csv
│       ├── test_dataset(2023).csv
│       └── merged_interpolated.csv
├── notebooks/
│   ├── 1_data_cleaning.ipynb
│   ├── 2_eda_analysis.ipynb   
│   └── 3_model_baseline_randomforest_2023eval.ipynb          
├── images/
│   ├── ChatGPT_RF.png
│   ├── Feature_Importance_RF.png  
│   └── Interpolated_RF.png  
├── README.md
└── requirements.txt
```

## Tools & Technologies

- **Python**: Pandas, Scikit-learn, Matplotlib, Seaborn
- **Jupyter Notebook**

## Milestones

1. Data Collection & Environment Setup
2. Data Cleaning, Missing Value Treatment, and Dataset Merging
3. Exploratory Data Analysis (EDA) & Data Profiling
4. Correlation & Trend Analysis with Visualizations
5. Simple Regression Model Development
6. 2023 Happiness Score Prediction
7. Results Interpretation & Summary


## Citations

- [World Happiness Report Data (2015-2024)](https://worldhappiness.report)
- [World Bank Data](https://data.worldbank.org)
- [OECD Data](https://data-explorer.oecd.org)


## License & Attribution

This project is for educational purposes and submitted as part of **CS50’s Introduction to Computer Science 2025 Final Project**.

**Note:** AI-based tools (ChatGPT) were used to assist with structuring the project design but all data handling, analysis, and coding are the author’s original work. AI assistance is acknowledged as required by CS50 guidelines.
