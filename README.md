# M-Pesa Fraud Detection Using Machine Learning (Random Forest)

## Overview

This project builds a Machine Learning fraud detection system for M-Pesa transactions using the Random Forest algorithm. The objective is to identify fraudulent transactions based on transaction characteristics, account behavior, and user activity patterns.

The project covers the complete machine learning workflow including data exploration, data cleaning, fraud analysis, feature engineering, model building, evaluation, and fraud prediction.



## Business Problem

A mobile money company operating across East Africa has experienced an increase in suspicious transactions. The company wants to automatically detect potentially fraudulent transactions and understand the factors that contribute most to fraud.

### Key Business Questions

* Which transactions are likely fraudulent?
* Does changing devices increase fraud risk?
* Are large transactions riskier?
* Are weekend transactions riskier?
* Does account age matter?
* Does logging in from a new location increase fraud risk?



## Dataset Information

The dataset contains 5,000 M-Pesa transactions and 13 features.

### Features

| Feature                 | Description                                |
| ----------------------- | ------------------------------------------ |
| TransactionID           | Unique transaction identifier              |
| Amount                  | Transaction amount (KES)                   |
| SenderCounty            | Sender's county                            |
| ReceiverCounty          | Receiver's county                          |
| TimeOfDay               | Hour transaction occurred                  |
| TransactionType         | Transaction category                       |
| AccountAgeMonths        | Age of account in months                   |
| TransactionsLast24Hours | Number of transactions in last 24 hours    |
| DeviceChangedRecently   | Whether user recently changed device       |
| NewLocationLogin        | Whether login occurred from a new location |
| FailedPinAttempts       | Number of failed PIN attempts              |
| IsWeekend               | Whether transaction occurred on weekend    |
| Fraudulent              | Target variable (Yes/No)                   |



## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-Learn



## Project Workflow

### 1. Data Exploration

The dataset was explored to understand its structure, data types, and summary statistics.

Performed:

* First and last records inspection
* Shape analysis
* Data type identification
* Numerical and categorical variable separation
* Descriptive statistics

### Findings

* Dataset contains 5,000 records
* 5 numerical features
* 8 categorical features
* No missing values
* No duplicate records



### 2. Data Cleaning

The dataset was checked for:

* Missing values
* Duplicate records
* Outliers using IQR Method

### Findings

* No missing values
* No duplicates
* No significant outliers detected



### 3. Fraud Analysis

#### Total Transactions

total number of transactions  = 5000


#### Fraudulent Transactions

Total number of fraudulent transactions = 2754


#### Fraud Percentage


55.08%


### Interpretation

More than half of the transactions in the dataset were labeled as fraudulent.



## Exploratory Analysis

### Fraud by Transaction Type

Fraudulent transaction counts:

| Transaction Type | Fraud Count |
| ---------------- | ----------- |
| Send Money       | 708         |
| Withdraw         | 700         |
| Paybill          | 693         |
| Till             | 653         |

### Finding

Send Money transactions recorded the highest number of fraudulent cases.



### Fraud by County

Top Counties with Fraudulent Transactions:

| County      | Fraud Cases |
| ----------- | ----------- |
| Kisumu      | 310         |
| Machakos    | 305         |
| Uasin Gishu | 297         |
| Nairobi     | 275         |

### Finding

Fraud cases were distributed across all counties, with Kisumu recording the highest count.



### Failed PIN Attempts

Fraud cases increased significantly when users had multiple failed PIN attempts.

### Finding

Failed PIN attempts are a strong indicator of suspicious activity.



### Device Change Analysis

Fraudulent Transactions:

| Device Changed | Count |
| -------------- | ----- |
| Yes            | 1977  |
| No             | 777   |

### Finding

Users who recently changed devices experienced substantially higher fraud rates.



### New Location Login Analysis

Fraudulent Transactions:

| New Location Login | Count |
| ------------------ | ----- |
| Yes                | 1959  |
| No                 | 795   |

### Finding

Transactions initiated from unfamiliar locations were highly associated with fraud.



### High-Value Transaction Analysis

Fraud Rates:

| Transaction Category | Fraud Rate |
| -------------------- | ---------- |
| Above KES 100,000    | 57.67%     |
| Below KES 100,000    | 45.01%     |

### Finding

High-value transactions were more likely to be fraudulent.



## Feature Engineering

### Label Encoding

Categorical variables were transformed into numerical values using LabelEncoder.

Encoded Features:

* SenderCounty
* ReceiverCounty
* TransactionType
* DeviceChangedRecently
* NewLocationLogin
* IsWeekend
* Fraudulent



## Machine Learning Model

### Algorithm

Random Forest Classifier

### Train-Test Split


80% Training Data
20% Testing Data


### Model Training


RandomForestClassifier(
    n_estimators=100,
    random_state=42
)




## Model Evaluation

### Accuracy


99.6%


### Confusion Matrix


[[467   0]
 [  4 529]]


### Interpretation

| Metric          | Count |
| --------------- | ----- |
| True Negatives  | 467   |
| False Positives | 0     |
| False Negatives | 4     |
| True Positives  | 529   |

The confusion matrix showed that the Random Forest model performed very well in detecting fraudulent transactions.
The model correctly identified most fraud cases (529 true positives) while missing only 4 fraud cases. 
Additionally, there were no false positives, meaning no legitimate transactions were incorrectly flagged as fraud.


### Classification Report

| Class     | Precision | Recall | F1 Score |
| --------- | --------- | ------ | -------- |
| Non-Fraud | 0.99      | 1.00   | 1.00     |
| Fraud     | 1.00      | 0.99   | 1.00     |

### Interpretation

The classification report showed that the Random Forest model achieved extremely high performance in detecting fraudulent transactions. 
Both precision and recall were close to 1.00 for both classes, indicating that the model correctly identified nearly all fraudulent and non-fraudulent cases.
The overall accuracy of 100% suggested that the model was highly effective in distinguishing between fraudulent and legitimate transactions within the dataset.



## Feature Importance Analysis

### Top Fraud Indicators

| Feature                 | Importance |
| ----------------------- | ---------- |
| DeviceChangedRecently   | 0.2856     |
| FailedPinAttempts       | 0.2800     |
| NewLocationLogin        | 0.2786     |
| Amount                  | 0.0476     |
| TransactionsLast24Hours | 0.0339     |
| AccountAgeMonths        | 0.0288     |
| TimeOfDay               | 0.0148     |
| SenderCounty            | 0.0113     |
| ReceiverCounty          | 0.0106     |
| TransactionType         | 0.0057     |
| IsWeekend               | 0.0030     |

### Key Finding

The strongest indicators of fraud are:

1. DeviceChangedRecently
2. FailedPinAttempts
3. NewLocationLogin

These features contribute over 84% of the model's predictive power.

---

## Business Insights

The analysis reveals that fraud is primarily driven by suspicious account access behavior rather than geographical location or transaction type.

High-risk characteristics include:

* Recent device changes
* Multiple failed PIN attempts
* Logins from new locations
* Large transaction amounts
* High transaction frequency



## Sample Fraud Prediction

### Input Transaction

| Feature                 | Value      |
| ----------------------- | ---------- |
| Amount                  | 250,000    |
| SenderCounty            | Nairobi    |
| ReceiverCounty          | Kisumu     |
| TimeOfDay               | 23         |
| TransactionType         | Send Money |
| AccountAgeMonths        | 1          |
| TransactionsLast24Hours | 15         |
| DeviceChangedRecently   | Yes        |
| NewLocationLogin        | Yes        |
| FailedPinAttempts       | 5          |
| IsWeekend               | Yes        |

### Predicted Outcome

Fraud

### Reason

The transaction exhibits several high-risk characteristics identified by the model:

* Recent device change
* New location login
* Multiple failed PIN attempts
* High transaction amount
* New account






## Author

Caroline Nkatha

Data Scientist
