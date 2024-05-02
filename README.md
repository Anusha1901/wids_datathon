# WiDS Datathon 2024: Predicting Metastatic Cancer Diagnosis

## Overview

The WiDS Datathon 2024 focuses on a prediction task using a dataset of approximately 18,000 records representing patients and their characteristics (age, race, BMI, zip code), their diagnosis and treatment information (breast cancer diagnosis code, metastatic cancer diagnosis code, metastatic cancer treatments, etc.), their geo (zip-code level) demographic data (income, education, rent, race, poverty, etc.), and toxic air quality data (Ozone, PM25, and NO2) that tie health outcomes to environmental conditions. The task is to assess whether the likelihood of a patient's Diagnosis Period being less than 90 days is predictable using these features.

## Data

The dataset is provided in two files:

1. `train.csv`: The training dataset, where the observed values of the target variable `DiagPeriodL90D` (Diagnosis Period being Less Than 90 Days) are provided.
2. `test.csv`: The test dataset, where the observed values of the target variable are withheld.

An example solution file is also provided for submission.

## Task

The goal is to submit a solution file containing the probabilities (e.g., 0.5) of `DiagPeriodL90D` being True for each row in the test dataset. The submitted probabilities will be compared against the observed outcomes for the test dataset to determine the participant's standing on the leaderboard during the competition and their final standing when the competition closes.

## External Data Usage

While the task can be tackled successfully without using external data, participants are allowed to use additional external data for building predictive models.

## Data Dictionary

### Covariates

The dataset is derived from a real-world evidence dataset from Health Verity (HV), one of the largest healthcare data ecosystems in the US. It contains health-related information of patients diagnosed with metastatic triple-negative breast cancers in the US. The dataset has been enriched with socioeconomic information from the US Zip Codes Database and toxicology data from NASA/Columbia University to explore the relationships between health outcomes and toxic air conditions.

### Target

- `DiagPeriodL90D`: Diagnosis Period Less Than 90 Days. This is an indication of whether the cancer was diagnosed within 90 days.

## Approach

### Data Preprocessing
- Handled missing values by imputing with appropriate strategies (mean/median imputation for numerical features, mode imputation for categorical features).
- Performed one-hot encoding for categorical features to make them suitable for machine learning algorithms.
- Standardized numerical features to ensure they're on the same scale.

### Feature Engineering
- Derived new features from existing ones, such as calculating the body mass index (BMI) from height and weight.
- Encoded ordinal features (e.g., education level) using ordinal encoding.
- Performed feature selection using variance inflation factor (VIF) to remove highly correlated features and mitigate multicollinearity.

### Model Selection and Hyperparameter Tuning
- Evaluated several machine learning algorithms, including logistic regression, random forest, XGBoost, and CatBoost.
- Performed hyperparameter tuning using randomized search cross-validation to find the best combination of hyperparameters for each model.
- Chose the CatBoostClassifier as the final model due to its superior performance.

### Model Evaluation
- Evaluated the model's performance on the test set using metrics such as area under the receiver operating characteristic curve (AUC-ROC), Gini coefficient, precision, recall, and F1-score.
- The CatBoostClassifier model achieved an AUC-ROC of 0.86 and a Gini coefficient of 0.72, indicating excellent predictive performance.

### Model Interpretation
- Analyzed feature importances to identify the most influential predictors of metastatic cancer diagnosis within 90 days.
- Performed partial dependence plots and SHAP (SHapley Additive exPlanations) analysis to understand the model's behavior and the relationships between features and the target variable.



