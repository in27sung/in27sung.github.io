---
layout: post
title: World Happiness & Economic and Social Indicators Correlations
subtitle: Repost
author: Insung
categories: Project
tags: [Project, Artificial Intelligence, Machine Learning, Data Science]
top:
---

## Project Report: Predicting Country-Level Happiness Scores

### Project Overview
This project investigates the relationship between countries' happiness scores and key economic and social indicators. It aims to build a robust predictive model while addressing data quality challenges such as missing values and inconsistent formatting. The output includes complete data cleaning, exploratory data analysis (EDA), model development, evaluation, and interpretation.

---

### Dataset Description
The dataset combines multiple global indicators for 131 countries, including:
- **Year:** The year for which the data is recorded(e.g., 2015, 2020, 2024)
- **Country:** The name of the country.
- **GDP_per_capita:** Gross Domestic Product per capita, which is a measure of a country's economic outout per person.
- **Education_Attainment:** The level of education achieved by the population.
- **Life_Expectancy:** The average number of years a person is expected to live.
- **Unemployment_Rate:** The percentage of the labour force that is unemployed.
- **Happiness Score(target):** A metric measuring the self-reported happiness of individuals in a country.

---

### Data Preprocessing

#### Initial Cleaning Steps(Chat GPT)
- **Country Name Standardisation**: Converted to title case.
- **Education_Attainment**:
  - Missing values filled using **country-wise median**.
  - Remaining nulls filled with **overall median**.

- **Life_Expectancy**:
  - Applied **country-wise linear interpolation**.
  - Remaining missing values filled with **overall mean**.
- Final dataset contains **no missing values**.

- Outputs:
  - `gpt_merged_dataset.csv`

---

### Exploratory Data Analysis (EDA)
![2023 Life Expactancy Missingness](/assets/images/jupyter/2023_life_expactancy_missingness.png)

- **GDP per capita** shows a **strong positive correlation** with **Happiness Score** (linear trend observed).
- **Impact of Life Expectancy Missingness on Happiness Score**
  - Countries **missing Life Expectancy data** in 2023 showed **significantly lower average Happiness Scores** (mean ≈ 5.24) compared to those with available data (mean ≈ 6.66).
  - Countries with available 2023 life expectancy data tend to report higher minimum happiness scores and tighter variance, implying they may be technologically advanced or more transparent.
  - Although the mean happiness score is clearly lower for countries with missing life expectancy data, the imbalance in group size (103 vs 28) suggests caution in interpreting statistical differences.
  - The absence of data in other countries might not directly reflect poor life expectancy, but could stem from limited data infrastructure, delayed reporting cycles, or geopolitical factors.
- Identified a few **outlier countries** with **low GDP per capita but high Happiness Score** — flagged for further qualitative analysis.
- Visualised trends using **scatter plots**, **pairplots**, and **correlation heatmaps** for cross-feature relationship assessment.

---

#### Post Cleaning Steps

- **Lebanon (2023) GDP per capita** manually set to **3350** (source: [TradingEconomics](https://tradingeconomics.com/lebanon/gdp-per-capita-us-dollar-wb-data.html)).
- Applied **country-wise linear interpolation** for:
  - `Education_Attainment`
  - `Life_Expectancy`
- No global imputation needed after interpolation.
- Final dataset contains **no missing values**.
- Outputs:
  - `merged_dataset_v1.1.csv` (manual fix)
  - `merged_interpolated.csv` (interpolated version)

---

### Modelling
#### 📌 Model: RandomForestRegressor
- Trained on cleaned dataset, using features from 2023 for final test.
- Feature Importance: GDP > Life Expectancy > Unemployment > Education

#### Performance Comparison
1. **Model A**: Trained on the dataset with missing values filled with ChatGPT
![test 2023 gpt](/assets/images/jupyter/test_2023_gpt.png)

**Post EDA version:**
![test 2023 interpolation](/assets/images/jupyter/test_2023_interpolation.png)

- **No overfitting observed**: Validation and Test performance are consistent.
- R² ~0.8 indicates **strong predictive power**.

---

### Conclusion & Insights

- The model successfully predicts national happiness based on quantifiable indicators.
- Cleaned data greatly improved predictive performance (compared to R² ~0.6 on unoptimised data).
- Results suggest that **economic strength, education, and health indicators** are key drivers of national happiness.
- However, the model shows a tendency to **underestimate happiness scores for low-GDP countries**, indicating **an over-reliance on GDP-related features**.
- This highlights the need for **further feature engineering** to incorporate non-economic factors—such as cultural, social, or environmental elements—especially for economically weaker nations, to better capture the multifaceted nature of happiness.

---

### Model Misestimation & Root Cause Hypothesis
![Feature Importance](/assets/images/jupyter/Feature_Importance_interpolation.png)
- Preliminary analysis suggested a tendency to underestimate happiness in low-GDP countries.
- However, further validation is required to confirm if **low GDP consistently aligns with low happiness**, or if other socio-political factors are contributing.
- Potential causes of underestimation include:
  - **Feature bias** toward GDP in the training data
  - **Incomplete or imputed data** for low-income nations
  - **Underrepresentation** of low-GDP countries in training samples
  - **Uncaptured factors** like trust, safety, and cultural context

---

### Next Step

- Enhance model robustness by incorporating **non-economic features**, particularly for low-GDP countries (e.g., social trust, freedom, mental well-being).
- Integrate **qualitative or geopolitical indicators** such as governance quality, safety perception, and civil liberties.
- Conduct **targeted feature engineering** to reduce bias toward GDP and better capture drivers of happiness across varying economic contexts.
- Analyse **outlier countries** (high happiness, low GDP) to uncover latent factors through domain research or case studies.
- Apply **clustering and temporal analysis** to identify evolving happiness patterns and region-specific trends over time.
- Evaluate model generalisation using **cross-year validation** to ensure robustness beyond the 2023 dataset.

---

### Artifacts
- ✅ Cleaned Dataset: `merged_interpolated.csv`
- ✅ Cleaning Summary: `1_data_cleaning.ipynb`
- ✅ Visualisation: Actual vs Predicted Plot (2023)
- ✅ Model: Trained `RandomForestRegressor`

---

### Citations

- [World Happiness Report Data (2015-2024)](https://worldhappiness.report)
- [World Bank Data](https://data.worldbank.org)
- [OECD Data](https://data-explorer.oecd.org)

---

### License & Attribution

This project is for educational purposes and submitted as part of **[CS50’s Introduction to Computer Science 2025 Final Project](https://cs50.harvard.edu/x/2025/project/)**.

**Note:** AI-based tools (ChatGPT) were used to assist with structuring the README and project design but all data handling, analysis, and coding are the author’s original work. AI assistance is acknowledged as required by CS50 guidelines.

---