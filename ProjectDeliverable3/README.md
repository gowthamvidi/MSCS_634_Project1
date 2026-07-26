# MSCS 634 Project Deliverable 3
## Classification, Clustering, and Association Rule Mining

This repository analyzes the **Online Shoppers Purchasing Intention Dataset** from the UCI Machine Learning Repository. Each record represents an e-commerce browsing session, and the binary target `Revenue` indicates whether the session resulted in a purchase.

The project extends the earlier data-cleaning, exploratory-analysis, and regression deliverables by applying supervised classification, unsupervised clustering, and association rule mining to the same online-shopping context.

## Repository Contents

```text
MSCS_634_ProjectDeliverable_3/
├── MSCS_634_ProjectDeliverable_3.ipynb
├── README.md
├── requirements.txt
├── .gitignore
├── online_shoppers_intention.csv
├── figures/
│   ├── 01_classification_model_comparison.png
│   ├── 02_decision_tree_confusion_matrix.png
│   ├── 03_random_forest_confusion_matrix.png
│   ├── 04_tuned_decision_tree_confusion_matrix.png
│   ├── 05_classification_roc_curves.png
│   ├── 06_random_forest_feature_importance.png
│   ├── 07_kmeans_silhouette_scores.png
│   ├── 08_kmeans_pca_clusters.png
│   ├── 09_cluster_profile_heatmap.png
│   └── 10_top_purchase_association_rules.png
└── outputs/
    ├── association_rules.csv
    ├── best_hyperparameters.json
    ├── classification_metrics.csv
    ├── classification_reports.csv
    ├── cluster_profiles.csv
    ├── frequent_itemsets.csv
    ├── purchase_association_rules.csv
    ├── random_forest_feature_importance.csv
    └── silhouette_scores.csv
```

## Dataset and Preparation

The original dataset contains **12,330 sessions and 18 columns**. Cleaning identified and removed **125 exact duplicate rows**, leaving **12,205 unique sessions**. No missing values remained after cleaning.

The purchase target is imbalanced: approximately **15.6%** of cleaned sessions resulted in revenue, while approximately **84.4%** did not. The notebook therefore uses:

- a stratified 80/20 train-test split;
- class weighting in both classifiers;
- F1 score and ROC-AUC in addition to accuracy;
- confusion matrices to show false positives and false negatives; and
- cross-validated F1 score for hyperparameter selection.

Categorical identifier fields such as operating system, browser, region, and traffic type are one-hot encoded instead of being treated as continuous measurements. Five behavioural features are also engineered: `TotalPageCount`, `TotalDuration`, `AvgProductTime`, `EngagementScore`, and `ExitBounceGap`.

## Classification Models

Two model families were developed:

1. **Decision Tree Classifier** — an interpretable nonlinear baseline using balanced class weights.
2. **Random Forest Classifier** — an ensemble benchmark using 200 trees and balanced subsample weights.

A second Decision Tree was produced through hyperparameter tuning.

### Hyperparameter Tuning

`GridSearchCV` used three-fold stratified cross-validation and optimized positive-class F1 score. The search compared:

- split criteria: Gini impurity and entropy;
- maximum tree depths: 4, 6, 8, and 10;
- minimum samples per split: 2 and 20; and
- minimum samples per leaf: 10 and 30.

The selected parameters were:

```json
{
  "model__criterion": "entropy",
  "model__max_depth": 6,
  "model__min_samples_leaf": 30,
  "model__min_samples_split": 2
}
```

### Test-Set Results

| Model | Accuracy | F1 Score | ROC-AUC |
|---|---:|---:|---:|
| Decision Tree | 0.8472 | **0.6213** | 0.9072 |
| Tuned Decision Tree | 0.8275 | 0.6148 | **0.9270** |
| Random Forest | **0.8947** | 0.5965 | 0.9241 |

The untuned Decision Tree produced the highest holdout F1 score, while the tuned Decision Tree produced the highest ROC-AUC. The Random Forest achieved the highest overall accuracy but identified fewer purchase sessions at the default probability threshold. This illustrates why model selection should not rely on accuracy alone when classes are imbalanced.

For a real e-commerce implementation, the tuned Decision Tree or Random Forest probability scores could be converted into alerts using a threshold chosen from business costs. A lower threshold may capture more potential buyers but will also create more false-positive interventions.

## K-Means Clustering

K-Means was applied to ten behavioural variables after log-transforming skewed counts, durations, and page values and then standardizing all clustering inputs. `Revenue` was excluded from clustering and used only afterward to interpret business outcomes.

Silhouette scores were compared for two through six clusters. The best score occurred at **three clusters**.

### Identified Groups

| Cluster | Sessions | Purchase Rate | Average Product Pages | Average Product Duration | Average Bounce Rate |
|---|---:|---:|---:|---:|---:|
| Highly Engaged Researchers | 2,310 | **24.5%** | 66.6 | 2,632.7 | 0.007 |
| Typical Product Browsers | 9,021 | 14.8% | 26.1 | 955.2 | 0.010 |
| Brief High-Bounce Sessions | 874 | **0.5%** | 2.5 | 37.8 | 0.165 |

### Cluster Interpretation and Application

**Highly Engaged Researchers** visit many administrative, informational, and product pages and have the highest conversion rate. They are good candidates for comparison tools, detailed product information, saved carts, and personalized recommendations.

**Typical Product Browsers** form the largest segment and show moderate product engagement. Clearer calls to action, social proof, shipping information, and relevant cross-selling may help move these visitors toward purchase.

**Brief High-Bounce Sessions** view few pages, exit quickly, and almost never purchase. This group should be investigated for landing-page mismatch, slow page performance, weak mobile usability, confusing navigation, or poor traffic-source targeting.

## Association Rule Mining

The dataset contains one session per row rather than product baskets. Session-level transactions were therefore created from Boolean behavioural items such as:

- positive or high page value;
- high product-page count or duration;
- low or high bounce and exit rates;
- visitor type and weekend activity;
- November sessions;
- special-day proximity;
- discovered cluster membership; and
- purchase outcome.

A custom Apriori implementation mines frequent itemsets up to length three with minimum support of 3%. Rules require at least 55% confidence and lift greater than 1.10.

### Strong Purchase-Related Rules

| Antecedent | Support | Confidence | Lift |
|---|---:|---:|---:|
| Low bounce and high page value | 3.49% | **87.65%** | **5.61** |
| Typical browser cluster and high page value | 3.52% | 81.90% | 5.24 |
| High page value | 4.37% | 78.04% | 4.99 |
| Low bounce and positive page value | 7.14% | 73.15% | 4.68 |
| Low exit rate and positive page value | 6.04% | 67.24% | 4.30 |
| November and positive page value | 4.22% | 65.94% | 4.22 |

These rules indicate association rather than causation. They can support trigger-based personalization, campaign timing, and funnel diagnostics. For example, a session combining low bounce behaviour with high page value is much more likely than average to end in a purchase.

## Key Practical Insights

- Purchase prediction should use F1, recall, and ROC-AUC alongside accuracy because the target is imbalanced.
- Page value, engagement depth, bounce rate, and exit rate are major indicators of purchase intention.
- Highly engaged visitors deserve decision-support content rather than generic promotions.
- Brief high-bounce sessions need experience and acquisition-channel improvements.
- November sessions with positive page value show a strong purchase association and may justify additional seasonal campaign resources.
- Model probability thresholds should reflect the cost of false positives and false negatives.

## Challenges and Solutions

### Class Imbalance

Only about one in six sessions resulted in revenue. Class weighting, stratified splitting, F1-based tuning, ROC-AUC, and confusion matrices were used to prevent misleading conclusions from accuracy alone.

### Mixed Data Types

Several integer fields are category identifiers. They were converted to strings and one-hot encoded, while genuinely numerical features were retained as continuous measures.

### Skewed Behavioural Data

Page counts, durations, and page values contain long right tails. Valid high-engagement sessions were preserved. Log transformations and standardization were applied before K-Means clustering.

### Choosing the Number of Clusters

Instead of selecting `k` arbitrarily, silhouette scores were compared for two through six clusters. Three clusters produced the strongest separation and understandable business profiles.

### No Product-Level Basket Data

Traditional market-basket analysis expects products purchased together. This dataset contains session summaries, so association mining was adapted to session-level behavioural events. The notebook clearly labels this interpretation and does not claim that products were purchased together.

### Page-Value Timing and Possible Leakage

`PageValues` is highly predictive but may become available late in a browsing session. Before production use, the organization should verify when this feature is calculated and compare early-session models with and without it.

## How to Run

1. Clone or download this repository.
2. Install the required packages:

```bash
pip install -r requirements.txt
```

3. Open `MSCS_634_ProjectDeliverable_3.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab.
4. Run all cells from top to bottom.

The executed notebook already contains outputs. Running it again regenerates all figures and CSV result files.

## Reference

Sakar, C., & Kastro, Y. (2018). *Online Shoppers Purchasing Intention Dataset* [Data set]. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q
