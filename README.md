# Fraud-Detection-in-Bank-Transactions

# Bank Transaction Anomaly Detection and Fraud Analysis

## Project Overview

This project focuses on **detecting anomalous and potentially fraudulent bank transactions** using a combination of:

* Exploratory Data Analysis (EDA)
* Feature engineering
* Dimensionality reduction
* Multiple unsupervised anomaly detection models
* Ensemble anomaly detection
* Model interpretability using feature importance

The goal is to simulate a **real-world fraud detection pipeline** where labeled fraud data is unavailable and anomalies must be detected using unsupervised techniques.

---

## Dataset Description

**Source:** `bank_transactions_data_2.csv`
**Records:** 2,512 transactions
**Features:** 16 original columns + engineered features

### Key Attributes

* Transaction details: Amount, Type, Duration, Channel
* Customer information: Age, Occupation
* Behavioral signals: Login attempts, Account balance
* Temporal data: Transaction date, Previous transaction date
* Device & location information

### Data Quality

* No missing values
* No duplicate records
* Dates converted to datetime format
* Numeric and categorical features handled separately

---

## Exploratory Data Analysis (EDA)

The EDA phase focused on understanding transaction behavior and identifying suspicious patterns.

### Analyses Performed

* Distribution and boxplot analysis for numeric features
* Z-score based outlier detection
* Skewness and kurtosis analysis
* Hourly, daily, and weekly transaction trends
* Category-wise comparisons:

  * Transaction amount by channel
  * Transaction amount by transaction type
  * Account balance by occupation
* Correlation analysis using heatmaps

### Key Observations

* Transaction amounts are right-skewed with extreme outliers
* Login attempts show heavy skewness, indicating abnormal access behavior
* High-value transactions are more frequent at specific hours

---

## Feature Engineering

To improve anomaly detection, several behavioral and temporal features were created:

* Hour of transaction
* Day of week
* Weekend flag
* Month
* Time since last transaction (in hours)
* Transaction amount to average-by-type ratio
* Device-level transaction frequency
* Z-score of transaction amount

Categorical variables were encoded using Label Encoding, and numerical features were standardized.

---

## Dimensionality Reduction & Visualization

To handle high-dimensional data and enable visualization:

### PCA (Principal Component Analysis)

* Reduced numerical features to 10 components
* Captured ~68.6% of total variance

### t-SNE

* Used for 2D visualization of transaction clusters
* Helped visually separate anomalous transaction behavior

---

## Anomaly Detection Models

Multiple unsupervised models were applied to detect anomalies:

### Models Used

* Isolation Forest (with GridSearchCV tuning)
* DBSCAN
* One-Class SVM
* HBOS (Histogram-Based Outlier Score)

Each model captures anomalies from a different perspective, reducing dependency on a single technique.

---

## Ensemble Anomaly Detection

A **majority-vote ensemble** was implemented using:

* Isolation Forest
* One-Class SVM
* HBOS

A transaction is flagged as anomalous if at least **two models agree**.

### Final Results

* **High-confidence anomalies detected:** ~1.27% of transactions
* Anomalous transactions show:

  * Significantly higher transaction amounts
  * Abnormal timing patterns
  * Deviations in behavioral features

This approach reduces false positives compared to standalone models.

---

## Model Interpretation

To understand which features contribute most to anomaly detection:

* A **Random Forest classifier** was trained using ensemble anomaly labels
* Feature importance was extracted

### Top Influential Features

* Transaction amount
* Amount-to-average ratio
* Account balance
* Time since last transaction
* Transaction duration
* Device transaction frequency

This improves explainability for stakeholders and fraud analysts.

---

## Visual Outputs

The project includes:

* Distribution and boxplots
* Correlation heatmaps
* PCA explained variance plots
* t-SNE anomaly visualization
* KDE plots comparing normal vs anomalous transactions
* Feature importance plots

---

## Tech Stack

* Python
* Pandas, NumPy
* Matplotlib, Seaborn
* Scikit-learn
* PyOD
* SciPy

---

## Project Structure

```
bank-transaction-anomaly-detection/
│
├── data/
│   └── bank_transactions_data_2.csv
│
├── notebooks/
│   └── anomaly_detection.ipynb
│
├── outputs/
│   └── anomaly_analysis_results.csv
│
├── requirements.txt
└── README.md
```

---

## Key Takeaways

* Unsupervised learning is effective for fraud detection when labels are unavailable
* Ensemble anomaly detection significantly improves reliability
* Feature engineering and explainability are critical for real-world adoption
* The pipeline closely mirrors industry-level fraud analytics workflows

---

## Future Improvements

* Introduce semi-supervised learning if partial labels become available
* Add SHAP for deeper feature explainability
* Deploy as a real-time fraud scoring API
* Incorporate graph-based fraud detection

---

## Author

**Jai Kishan Kokkiligadda**
Data Analyst | Data Science Practitioner


* Clean and modularize the notebook for production
* Help you explain this project confidently in interviews
