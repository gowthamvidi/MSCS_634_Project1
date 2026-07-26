# Online Shoppers Purchasing Intention Data Mining Project

### Student Information
- **Name:** Shiva Gowtham Kumar Vidiyala, Raghav Gurram, Vikram Reddy Tekula
- **Course:** MSCS 634 –  Advanced Big Data and Data Mining
- **Deliverable:** Deliverable 4: Final Insights, Recommendations, and Presentation
- **Programming Language:** Python
- **Environment:** Jupyter Notebook

## Project Overview
This project analyzes the **Online Shoppers Purchasing Intention Dataset** using a complete data mining workflow: preprocessing, exploratory data analysis, feature engineering, regression, classification, clustering, and association rule mining. The business goal is to understand browsing behavior and identify practical ways an e-commerce company can improve conversion and customer experience.

## Dataset
- Source: UCI Machine Learning Repository, Online Shoppers Purchasing Intention Dataset.
- Original size: **12,330 sessions** and **18 columns**.
- Cleaned size: **12,205 sessions** after removing **125 exact duplicate rows**.
- Missing values: **0**.
- Purchase rate after cleaning: **15.6%**.

The dataset was chosen because it supports multiple data mining tasks in one coherent e-commerce problem. The `Revenue` field enables classification, `ProductRelated_Duration` enables regression, browsing variables support customer clustering, and derived behavior flags support session-level association rule mining.

## Project Steps
1. Loaded and inspected the dataset.
2. Removed exact duplicate rows and verified missing values.
3. Conducted EDA on purchase outcome, visitor type, month, page value, bounce rate, exit rate, and correlations.
4. Engineered behavioral features including total page count, total duration, average product time, engagement score, exit-bounce gap, product page share, month number, quarter, and log-transformed skewed variables.
5. Built regression models to estimate product-page duration.
6. Built classification models to predict purchase outcome.
7. Used K-Means clustering to segment sessions.
8. Applied association rule mining to session-level behavioral labels.
9. Converted findings into recommendations and ethical considerations.

## Major Results
### Regression
Best holdout regression model: **Multiple Linear Regression** with RMSE **1050.82**.

### Classification
- Highest accuracy: **Random Forest**.
- Highest F1 score: **Decision Tree** with F1 **0.621**.
- Highest ROC-AUC: **Tuned Decision Tree** with ROC-AUC **0.927**.

### Clustering
K-Means performed best at **3 clusters**, with silhouette score **0.363**. The clusters were interpreted as highly engaged researchers, typical product browsers, and brief high-bounce sessions.

### Association Rules
The strongest purchase-related rule was **Bounce_Low AND PageValue_High -> Purchase**, with confidence **87.7%** and lift **5.61**.

## Practical Recommendations
- Use purchase-probability scores to trigger assistance, reminders, or relevant offers, but tune thresholds based on business costs.
- Provide comparison tools, detailed product content, and saved-cart support for highly engaged researchers.
- Improve landing page relevance, speed, and mobile usability for brief high-bounce sessions.
- Prioritize high page-value and low-bounce sessions for retargeting and checkout assistance.
- Monitor model performance by visitor type, month, traffic source, device/browser category, and region to reduce bias and performance drift.

## Files Included
```text
Online_Shoppers_Data_Mining_Final.ipynb
README.md
Online_Shoppers_Comprehensive_Report.pdf
Online_Shoppers_Project_Presentation.pptx
```

## Video presentation
1. Please login into Cumberlands Account
2. Click the below link 
https://cumber-my.sharepoint.com/:f:/g/personal/svidiyala40297_ucumberlands_edu/IgD9X_FSQcTmR6WrKioCuSUiAfMZ6m4iqcn4mEFTUrPz9zA?e=HWSKsW

## How to Run the Notebook
1. Open `Online_Shoppers_Data_Mining_Final.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab.
2. Make sure the `data/online_shoppers_intention.csv` file remains in the `data` folder.
3. Install dependencies if needed:

```bash
pip install pandas numpy matplotlib scikit-learn jupyter nbformat nbclient
```

4. Run all cells from top to bottom. The notebook regenerates figures and output CSV files.

## References
Sakar, C., & Kastro, Y. (2018). *Online Shoppers Purchasing Intention Dataset* [Data set]. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q

Sakar, C. O., Polat, S. O., Katircioglu, M., & Kastro, Y. (2019). Real-time prediction of online shoppers’ purchasing intention using multilayer perceptron and LSTM recurrent neural networks. *Neural Computing and Applications, 31*(10), 6893-6908. https://doi.org/10.1007/s00521-018-3523-0

Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Thirion, B., Grisel, O., Blondel, M., Prettenhofer, P., Weiss, R., Dubourg, V., Vanderplas, J., Passos, A., Cournapeau, D., Brucher, M., Perrot, M., & Duchesnay, E. (2011). Scikit-learn: Machine learning in Python. *Journal of Machine Learning Research, 12*, 2825-2830.