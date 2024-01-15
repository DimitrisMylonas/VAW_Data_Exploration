# Analysis of VAW Dataset and Machine Learning Approach

## Overview
This project focuses on analyzing and predicting the `OUTCOME` variable from the `VAW.csv` dataset, which contains information related to violence against women. Various preprocessing steps, data cleaning techniques, feature engineering, and machine learning models were applied in an attempt to achieve meaningful predictions.

## Dataset Description
The dataset contains multiple categorical and numerical features, with significant amounts of missing data and class imbalance issues. Below is a brief overview of the dataset:

- **Original Number of Features:** 23
- **Features Dropped Due to High Missing Rate or Zero Entropy:** 12
- **Final Features Used:** 11
- **Total Rows:** 2016
  - **Training Set:** 544 rows (where `OUTCOME` is known)
  - **Test Set:** 1472 rows (where `OUTCOME` is missing)

## Preprocessing Steps
### 1. Data Cleaning
- Column names were standardized by removing redundant text.
- The `_T: Any` category in `OUTCOME` was replaced with `NaN` to indicate missing values.
- Features with **zero entropy** (constant values) or **more than 60% missing data** were removed.

### 2. Handling Missing Values
- **Numerical Features:** Imputed using an `IterativeImputer` with `ExtraTreesRegressor`.
- **Categorical Features:** Imputed using the most frequent value via `SimpleImputer`.

### 3. Feature Encoding & Scaling
- Categorical variables were **ordinally encoded**.
- Numerical variables were **standardized** using `StandardScaler`.

## Exploratory Data Analysis (EDA)
1. **Feature Importance:** 
   - Using a `RandomForestClassifier`, the most significant features identified were:
     - `OBS_VALUE`
     - `TOPIC`
     - `CONDITION`
   - Least significant features were removed.

2. **Class Imbalance:**
   - The dataset exhibited severe class imbalance, with a few dominant classes (e.g., `INJ`, `LOSCONS`), while many other categories had significantly fewer instances.

## Model Selection & Training
### Models Tested:
1. **K-Nearest Neighbors (KNN)**
2. **Random Forest**
3. **XGBoost**
4. **Multi-Layer Perceptron (MLP)**

### Addressing Class Imbalance:
- **SMOTE + Tomek Links** was applied to the training set to generate synthetic data and remove noise.

### Hyperparameter Tuning:
- **GridSearchCV** was used for each model to optimize hyperparameters.

## Model Performance
- **Best Performing Model:** `Random Forest`
- **Balanced Accuracy Scores:**
  - **KNN:** 0.7167
  - **Random Forest:** 0.7278
  - **XGBoost:** 0.7141
  - **MLP:** 0.6465

- **Issue Identified:**
  - The model struggles due to the **small dataset size** and **high class imbalance**.
  - Even with oversampling, the **test predictions were highly skewed**, mostly predicting only two classes.

## Conclusion
- Due to the limited number of labeled samples and the extreme imbalance in `OUTCOME`, the models were unable to generalize well.
- Future improvements could include:
  - Collecting more data.
  - Exploring alternative feature engineering techniques.
  - Trying different strategies to handle class imbalance.

## Files in Repository
- `VAW.csv` – Original dataset.
- `preprocessing.py` – Preprocessing pipeline.
- `model_training.py` – Model training and evaluation.
- `data_test_predicted.csv` – Predictions for the test set.
- `README.md` – This document.
