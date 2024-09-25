# Bank Customer Churn Analysis

This project analyzes bank customer churn, identifying key factors influencing customer retention. The dataset includes customer demographic data, financial metrics, and customer engagement features. The goal is to build a model that can accurately predict customer churn and offer insights for improving retention strategies.

## Table of Contents
- [Introduction](#introduction)
- [Dataset Overview](#dataset-overview)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Observations Summary from EDA](#observations-summary-from-eda)
- [Data Cleaning](#data-cleaning)
- [Feature Engineering](#feature-engineering)
- [Data Preprocessing](#data-preprocessing)
- [Classification Modelling](#classification-modelling)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

## Introduction
Customer churn is a critical issue for banks, impacting profitability and growth. This project uses a bank customer churn dataset to understand the factors driving customer exits and build predictive models to prevent churn. The dataset includes demographic details like age and gender, financial metrics like credit score and account balance, and engagement features like tenure and product usage. By analyzing this data, we aim to improve customer retention strategies.

## Dataset Overview
The dataset consists of 10,002 entries and 14 columns:

| Column          | Description                          | Data Type |
|-----------------|--------------------------------------|-----------|
| RowNumber       | Index                                | int64     |
| CustomerId      | Unique customer identifier           | int64     |
| Surname         | Customer surname                     | object    |
| CreditScore     | Credit score                         | int64     |
| Geography       | Country of residence (e.g., France)  | object    |
| Gender          | Male or Female                       | object    |
| Age             | Age of the customer                  | float64   |
| Tenure          | Years of customer relationship       | int64     |
| Balance         | Account balance                      | float64   |
| NumOfProducts   | Number of products held by customer  | int64     |
| HasCrCard       | Whether the customer has a credit card | float64   |
| IsActiveMember  | Whether the customer is an active member | float64  |
| EstimatedSalary | Customer's estimated salary          | float64   |
| Exited          | Whether the customer has exited the bank (1 = Yes, 0 = No) | int64     |

## Exploratory Data Analysis (EDA)
This section performs a thorough exploration of the data to uncover patterns and trends. We aim to understand the relationships between various features like age, geography, balance, credit score, and tenure, and how they correlate with customer churn.

### Key Insights:
- **Geography**: There are regional differences in churn rates. Customers from France and Spain exhibit different exit behaviors.
- **Gender**: No significant difference is observed in churn rates between genders.
- **Age**: Customers between the ages of 40 and 70 have higher churn rates.
- **Balance**: A high number of customers have zero balance, which requires further analysis.
- **CreditScore vs EstimatedSalary**: No clear correlation observed.
- **Products**: Customers with 4 products all exited the bank, highlighting a need for special attention to high-class customers.

## Observations Summary from EDA:
- **RowNumber and CustomerId**: These are unique identifiers with no predictive power, so they will be removed.
- **Surname**: Has no significant impact on churn and will also be removed.
- **Exited**: There is a class imbalance, with around 80% of customers staying and 20% exiting.
- **Balance**: High frequency of zero values, needing investigation.
- **Geography**: Regional imbalances observed, especially in France and Spain.
- **Age**: Customers aged 40-70 are more likely to exit.

## Data Cleaning
In this section, we clean the data by:
- Removing irrelevant columns (`RowNumber`, `CustomerId`, `Surname`).
- Dropping rows with null values in `Geography`, `Age`, `HasCrCard`, and `IsActiveMember`.
- Investigating zero balance values for further analysis.

## Feature Engineering
We create additional features to enhance the model’s performance:
- **Grouping Zero Balance Customers**: Customers with zero balance are grouped based on 'IsActiveMember' and 'Exited'.
- **Feature Creation**:
    - `total_active`: Sum of `IsActiveMember`, `NumOfProducts`, and `HasCrCard`.
    - `Balance_to_Salary`: Ratio of `Balance` to `EstimatedSalary`.
    - `Tenure_to_Age`: Ratio of `Tenure` to `Age`.
    - Interaction terms like `Balance_Age_Interaction`, `Products_Age_Interaction`, `Balance_to_Age`, and `Balance_to_Products`.

## Data Preprocessing
Steps in data preprocessing:
1. **Encoding categorical features**: Encoding `Geography` and `Gender` using Label Encoding or One-Hot Encoding.
2. **Splitting the data**: Dividing the data into training and test sets.
3. **Feature scaling**: Normalizing features like `CreditScore`, `Balance`, `EstimatedSalary`, and `Age` using StandardScaler.

## Classification Modelling
We evaluated various machine learning models to predict customer churn:
- **Logistic Regression**
- **K-Nearest Neighbors (KNN)**
- **Decision Tree**
- **Support Vector Machine (SVM)**
- **Random Forest**
- **XGBoost**

### Evaluation:
Using **5-fold cross-validation** and focusing on the **F1 score** due to the class imbalance. The best-performing model was tuned using **GridSearchCV** to optimize hyperparameters. We used metrics like **accuracy**, **precision**, **recall**, **F1 score**, and **ROC AUC** to evaluate model performance.

## Technologies Used
- **Python**: Programming language used for analysis and modeling.
- **Pandas**: For data manipulation and analysis.
- **NumPy**: For numerical operations.
- **Matplotlib & Seaborn**: For data visualization.
- **Plotly**: For interactive visualizations.
- **Scikit-learn**: For machine learning algorithms and model evaluation.
- **XGBoost**: For gradient boosting models.

