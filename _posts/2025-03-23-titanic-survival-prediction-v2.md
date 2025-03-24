---
layout: post
title: Titanic Survival Prediction V2
subtitle: Competitions
author: Insung
categories: [Data Science, Competitions, Kaggle]
tags: [Data Science, Competitions, Kaggle]
top:
---

# 🛳 Titanic Survival Prediction V2 | Kaggle Challenge

## 📌 Project Overview
- Objective: Predict survival of passengers aboard Titanic based on demographic & socio-economic data.
- Dataset: Provided by [Kaggle Titanic Competition](https://www.kaggle.com/competitions/titanic)


```python
# ============================
# 📦 Library Imports
# ============================

import pandas as pd
import numpy as np
import os
import matplotlib.pyplot as plt
import seaborn as sns
import sklearn
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import GridSearchCV, StratifiedKFold, train_test_split
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report
from sklearn.base import BaseEstimator, TransformerMixin
import warnings

# ============================
# ⚙️ Configurations
# ============================

# Version Check (optional, can be removed later)
print(f"pandas: {pd.__version__}, numpy: {np.__version__}, sklearn: {sklearn.__version__}, seaborn: {sns.__version__}")

# Disable unnecessary warnings
pd.options.mode.chained_assignment = None
warnings.simplefilter(action='ignore', category=FutureWarning)

# ============================
# 📂 Data Loading
# ============================

# Auto-load paths
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        file_path = os.path.join(dirname, filename)
        if 'train.csv' in filename:
            train_path = file_path
        elif 'test.csv' in filename:
            test_path = file_path

# Load datasets
train = pd.read_csv(train_path)
test = pd.read_csv(test_path)

print(f"Train shape: {train.shape}")
print(f"Test shape: {test.shape}")
```

## 📊 Data Description

| Column | Description |
|-------|------------|
| PassengerId | Unique ID |
| Survived | Survival (0 = No, 1 = Yes) |
| Pclass | Ticket class (1st, 2nd, 3rd) |
| Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked | Passenger info |

---


```python
# Quick data overview
print("\nTrain Data Info:")
train.info()

print("\nTrain Data Summary:")
print(train.describe().T)  # Transpose for better readability

print("\nFirst 5 rows:")
print(train.head())
```

##  🕵️‍♂️ Exploratory Data Analysis (EDA)
### Missing Values Check
- Identified missing data in:
    - Age: Significant number of missing values.
    - Cabin: High percentage of missing values.
    - Embarked: Few missing values.

### Survival Distribution by Features
- Gender (Sex)
- Passenger Class (Pclass)
- Age

*(Include charts: barplots, countplots, heatmap)*

---


```python
# Check missing values
train.isnull().sum()
```


```python
# Visualise the distribution of the target variable (Survived)
sns.countplot(x='Survived', data=train)
plt.title('Survival Distritbution')
plt.show()
```


```python
# Visualise survival rate by Sex
sns.countplot(x='Sex', hue='Survived', data=train)
plt.title('Survival by Gender')
plt.show()
```


```python
# Visualise survival rate by Pclass
sns.countplot(x='Pclass', hue='Survived', data=train)
plt.title('Survival by Passenger Class')
plt.show()
```


```python
# Age distribution by survival
plt.figure(figsize=(10, 6))
sns.histplot(data=train, x='Age', hue='Survived', bins=30, kde=True)
plt.title('Age Distribution by Survival')
plt.show()
```


```python
# Select only numeric columns
numeric_features = train.select_dtypes(include=['int64', 'float64'])

# Correlation matrix
corr_matrix = numeric_features.corr()

# Plot
plt.figure(figsize=(8, 6))
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm')
plt.title('Feature Correlation Matrix')
plt.show()
```

## 🔧 Feature Engineering

Implemented a custom transformer `TitanicFeatureEngineer` to automate and integrate feature engineering directly into the Scikit-learn pipeline. This approach ensures consistency and reproducibility during both training and inference.

### Key Features Created:

| Feature        | Description |
|---------------|------------|
| **Title**     | Extracted passenger's title from `Name` column (e.g., Mr, Miss, Mrs). Mapped common titles to numeric values, grouped rare titles into a single category. |
| **FamilySize**| Calculated as `SibSp + Parch + 1`, representing the total family members including the passenger. Captures social group size which may impact survival chances. |
| **HasCabin**  | Simplified the `Cabin` feature to a binary flag: `1` if Cabin information is available, else `0`. This retains useful information while handling missing values efficiently. |

### Dropped Columns:
After extracting necessary information, dropped non-essential columns to reduce noise and dimensionality:
- `Name`
- `Cabin`
- `Ticket`
- `PassengerId`

### Benefits:
- **Modular & Scalable:** Easily integrable within the Scikit-learn pipeline framework.
- **Reusable:** Applied consistently to both training and test datasets.
- **Clean & Maintainable:** Centralised feature logic improves maintainability and reproducibility.


```python
class TitanicFeatureEngineer(BaseEstimator, TransformerMixin):
    def fit(self, X, y=None):
        return self
    def transform(self, X):
        X = X.copy()
        
        # Title Extraction
        X['Title'] = X['Name'].str.extract(r' ([A-Za-z]+)\.', expand=False)
        title_map = {'Mr':0, 'Miss':1, 'Mrs':2, 'Master':3}
        X['Title'] = X['Title'].map(lambda x: title_map.get(x, 4))  # Rare titles as 4
        
        # FamilySize
        X['FamilySize'] = X['SibSp'] + X['Parch'] + 1
        
        # HasCabin
        X['HasCabin'] = X['Cabin'].apply(lambda x: 0 if pd.isnull(x) else 1)
        
        # Drop unused columns after feature extraction
        X.drop(['Name', 'Cabin', 'Ticket', 'PassengerId'], axis=1, inplace=True)
        
        return X
```

## Data Preprocessing Pipeline (Numeric & Categorical)

Implemented a structured preprocessing pipeline using Scikit-learn's `ColumnTransformer` to ensure consistent and maintainable data preparation.

- **Numeric Features (`Age`, `Fare`, `FamilySize`, `HasCabin`):** Applied median imputation to handle missing values robustly against outliers.

- **Categorical Features (`Sex`, `Embarked`):** Applied most frequent imputation for missing values, followed by one-hot encoding (`handle_unknown='ignore'`) to convert categorical data into numeric format.

Combined both transformations using `ColumnTransformer`, allowing separate pipelines for numeric and categorical columns while keeping the process modular and reproducible.


```python
# Preprocessing Pipeline

# Numeric Features
numeric_features = ['Age', 'Fare', 'FamilySize', 'HasCabin']
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median'))
])

# Categorical Features
categorical_features = ['Sex', 'Embarked']
categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])

# Combine into ColumnTransformer
preprocessor = ColumnTransformer(transformers=[
    ('num', numeric_transformer, numeric_features),
    ('cat', categorical_transformer, categorical_features)
])
```

## Train/Validation Split

To evaluate model performance effectively and avoid overfitting, we split the dataset into training and validation sets.

**Feature & Target Separation:**
   - `X`: Contains all features (input variables), dropping the target column `Survived`.
   - `y`: Contains the target variable `Survived` (0 = Did not survive, 1 = Survived).


```python
X = train.drop('Survived', axis=1)
y = train['Survived']

# Train/Validation Split
X_train, X_valid, y_train, y_valid = train_test_split(X, y, test_size=0.2, random_state=27, stratify=y)
```

## Model Training: Random Forest with Hyperparameter Tuning

Constructed a complete Scikit-learn pipeline integrating feature engineering, preprocessing, and model training. 

- **Model:** Random Forest Classifier (`RandomForestClassifier`)
- **Hyperparameter Tuning:** Applied `GridSearchCV` with 5-fold `StratifiedKFold` cross-validation.
  - Tuned parameters: 
    - `n_estimators`: [100, 200]
    - `max_depth`: [4, 6, None]
    - `min_samples_split`: [2, 5]

This setup ensures optimised model performance with robust evaluation through cross-validation.


```python
# Full Pipeline
pipeline = Pipeline(steps=[
    ('feature_engineering', TitanicFeatureEngineer()),
    ('preprocessing', preprocessor),
    ('model', RandomForestClassifier(random_state=27))
])

# Hyperparameter Grid
param_grid = {
    'model__n_estimators': [100, 200],
    'model__max_depth': [4, 6, None],
    'model__min_samples_split': [2, 5],
}

# Cross-validation
cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=27)

# GridSearchCV
grid = GridSearchCV(pipeline, param_grid, cv=cv, scoring='accuracy', n_jobs=-1, verbose=1)
grid.fit(X_train, y_train)

# Best Hyperparameters
print("Best Parameters:", grid.best_params_)
print("Best CV Score:", grid.best_score_)
```


```python
best_pipeline = grid.best_estimator_

# Extract preprocessor from pipeline
preprocessor = best_pipeline.named_steps['preprocessing']

# Apply feature engineering first
engineered_valid = best_pipeline.named_steps['feature_engineering'].transform(X_train)

# Now extract OneHotEncoder feature names
ohe_features = preprocessor.named_transformers_['cat'].named_steps['onehot'].get_feature_names_out(['Sex', 'Embarked'])

# Combine feature names
numeric_features = ['Age', 'Fare', 'FamilySize', 'HasCabin']
all_feature_names = numeric_features + list(ohe_features)

# Apply transformation
transformed_valid = preprocessor.transform(engineered_valid)
pd.DataFrame(transformed_valid, columns=all_feature_names).head()
```

## Model Evaluation

Evaluated the optimised Random Forest model on the validation set:

- **Validation Accuracy:** Computed overall accuracy to measure model performance.
- **Confusion Matrix:** Visualised prediction results to analyse true positives, false positives, true negatives, and false negatives.
- **Classification Report:** Provided precision, recall, F1-score, and support for each class.
- **Cross-validation Score:** Reported the best cross-validation accuracy obtained during hyperparameter tuning.

This evaluation ensures both overall model effectiveness and detailed class-wise performance understanding.


```python
# Evaluate on Validation Set
y_pred = grid.predict(X_valid)
print("Validation Accuracy:", accuracy_score(y_valid, y_pred))
print(classification_report(y_valid, y_pred))


# Confusion Matrix
cm = confusion_matrix(y_valid, y_pred)
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.title('Confusion Matrix')
plt.show()
```

## 🚀 Final Model & Submission

Trained the final Random Forest model using the entire training dataset and the best hyperparameters obtained via GridSearchCV:

- `n_estimators`: 100
- `max_depth`: 6
- `min_samples_split`: 2

Generated predictions on the test set and created the submission file:

`submission.csv`


```python
# Predict directly using best pipeline
X_test = pd.read_csv(test_path)

# Submission
test_preds = grid.predict(X_test)

submission = pd.DataFrame({
    'PassengerId': X_test['PassengerId'],
    'Survived': test_preds
})
submission.to_csv('submission.csv', index=False)

print("✅ Submission file 'submission.csv' created.")
```

## 📈 8. Key Insights

- **Sex:** Females had significantly higher survival rates.
- **Pclass:** 1st class passengers survived more frequently.
- **FamilySize:** Smaller families had higher survival chances.
- **Title:** Extracted titles (Mr, Mrs, Miss, etc.) were strong predictors.
- **Fare & Age:** Moderate influence, with higher fares linked to better survival.
- **Embarked:** Minimal effect on survival prediction.

---

## 📊 Public Score: **0.76076**

While this score is slightly lower than the simple Decision Tree baseline, it highlighted key lessons:

- **Complex preprocessing and advanced models do not always guarantee better performance, especially on structured datasets like Titanic.**
- **Raw categorical features sometimes carry strong predictive power when used with Tree-based models.**
- The project reinforced the importance of **testing assumptions through experimentation**, not intuition.

Moving forward, I plan to experiment further with:

- Simplifying preprocessing.
- Combining models using ensemble techniques.
- Hyperparameter tuning to optimise performance.

---
