# Advanced Data Mining for Data-Driven Insights and Predictive Modeling

## Deliverable 1: Data Collection, Cleaning, and Exploration

### Student Information
- **Name:** Shiva Gowtham Kumar Vidiyala, Raghav Gurram, Vikram Reddy Tekula
- **Course:** MSCS 634 – Advanced Data Mining
- **Deliverable:** Deliverable 1: Data Collection, Cleaning, and Exploration
- **Programming Language:** Python
- **Environment:** Jupyter Notebook

---

# Project Overview

This project focuses on the first stage of the data mining process: data collection, preprocessing, cleaning, and exploratory data analysis (EDA). The objective is to prepare a real-world dataset for future predictive modeling by ensuring high data quality and understanding the relationships among features.

The chosen dataset is the **Online Shoppers Purchasing Intention Dataset**, which contains browsing behavior of online visitors and whether each session resulted in a purchase.

---

# Dataset Source

The dataset used in this project was obtained from the **UCI Machine Learning Repository**.

**Dataset Name:** Online Shoppers Purchasing Intention Dataset

**Dataset Source:** : https://archive.ics.uci.edu/dataset/468/online%2Bshoppers%2Bpurchasing%2B


---

# Dataset Summary

- Total Records: **12,330**
- Total Features: **18**
- Target Variable: **Revenue**
- Dataset Type: Multivariate
- Domain: E-Commerce / Customer Behavior

The dataset contains both numerical and categorical attributes describing user behavior during an online shopping session.


# Project Objectives

The objectives of this deliverable are to:

- Load and inspect the dataset.
- Examine data quality.
- Detect missing values and duplicates.
- Handle outliers.
- Reduce skewness in numerical features.
- Perform exploratory data analysis (EDA).
- Generate insights that support future predictive modeling.

---

# Data Preprocessing

The following preprocessing tasks were completed:

- Loaded the dataset using Pandas.
- Inspected data types and summary statistics.
- Checked for missing values.
- Identified and removed duplicate records.
- Detected outliers using the IQR method.
- Applied outlier capping to reduce the impact of extreme values.
- Performed logarithmic transformation on skewed numerical features.

---

# Exploratory Data Analysis (EDA)

EDA was conducted using Matplotlib and Seaborn to better understand the data.

Visualizations include:

- Histograms
- Boxplots
- Correlation Heatmap
- Distribution Plots
- Feature Relationship Analysis

These analyses helped identify feature distributions, outliers, correlations, and customer purchasing patterns.

---

# Key Findings

- The dataset contains both numerical and categorical features.
- Duplicate records were successfully removed.
- Outliers were handled using the IQR capping technique.
- Log transformation reduced skewness in numerical variables.
- Several browsing-related features showed meaningful relationships with customer purchase behavior.
- The cleaned dataset is suitable for predictive modeling in future project deliverables.

---

# Repository Contents

```
├── online_shoppers_execution.ipynb
├── online_shoppers_cleaned.csv
├── online_shoppers_intention.csv
└── README.md
```

---

# Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn

---

# Challenges Encountered

- Detecting duplicate observations.
- Handling skewed numerical distributions.
- Managing extreme outliers without losing valuable information.
- Selecting appropriate preprocessing techniques while maintaining data integrity.

---

# Future Work

The cleaned dataset will be used for the remaining project deliverables involving:

- Feature Engineering
- Classification Models
- Clustering
- Association Rule Mining
- Model Evaluation
- Predictive Analytics

---

# Conclusion

This deliverable successfully completed the data collection, cleaning, and exploratory analysis phase of the project. The preprocessing techniques improved the quality of the dataset, while EDA provided valuable insights into customer browsing behavior. The resulting dataset is well-prepared for developing predictive machine learning models in future deliverables.
