# Bank Marketing Campaign Optimization

Predictive model to optimize bank term deposit campaign targeting using the [UCI Bank Marketing dataset](https://archive.ics.uci.edu/ml/datasets/bank+marketing).

---

## Problem Overview

**Business Challenge**: Bank direct marketing campaigns have **11.7% average response rate**. How can we use machine learning to identify **best prospects** and achieve **2-4x higher response rates**?

**Dataset**: 45,211 customer records with demographics, account info, and campaign contact details
- **Target**: `y` (did customer subscribe to term deposit? yes/no)
- **Features**: age, job, marital status, education, balance, housing/loan status, contact details, campaign timing

---

## 🛠️ Modeling Approach

### Models Tested (5-fold Cross-Validation, ROC-AUC)
| Model | CV ROC-AUC | Test ROC-AUC |
|-------|------------|--------------|
| **Random Forest** | **0.778** | **0.793** |
| XGBoost | 0.782 | 0.793 |
| Logistic Regression | 0.738 | 0.746 |
| Decision Tree | 0.728 | 0.727 |
| KNN | 0.720 | 0.716 |

### Hyperparameter Tuning
**GridSearchCV** with 5-fold stratified cross-validation for all models:
Random Forest (Best):
```r
├── n_estimators: 100
├── max_depth: 20
├── min_samples_leaf: 5
└── max_features: sqrt
```
XGBoost (Best):
```r
├── learning_rate: 0.05
├── max_depth: 6
└── n_estimators: 200
```
### Primary Metric
**ROC-AUC**: Handles class imabalnce

---

## **Best Model: Random Forest**
**Why Random Forest?**
- Tied for highest test ROC-AUC (0.793)
- Excellent business lift (4.0x in top 10%)
- Tree-based → Natural feature importance
- Robust to outliers & missing values
- No scaling needed (unlike KNN/LogReg)

---

## Key Results

### **Business Lift Table** (Test Set)
| Top % | Response Rate | Lift |
|-------|---------------|------|
| **10%** | **46.8%** | **4.0x** |
| **20%** | **34.6%** | **3.0x** |
| **30%** | **27.1%** | **2.3x** |
| **40%** | **22.6%** | **1.9x** |


### **Campaign Strategy**
- PRIORITY 1: Target top 20% by model score
→ 34.6% response vs 11.7% random (3x lift)

- PRIORITY 2: Focus on "retired" job segment
→ Highest natural subscription rate

- PRIORITY 3: May campaigns get 2x response
→ Time campaigns optimally

- ROI: 5x cost reduction per subscriber

---

## Notebook Structure
- Data Loading + EDA
- Preprocessing (One-hot + Scaling)
- Model Training + GridSearchCV
- Model Evaluation + Confusion Matrix
- Feature Importance Analysis
- Business Lift + Post-hoc Insights

