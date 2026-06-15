# AAI-510-IN1-ML-Fundamentals-Applications

# Supply Chain Late Delivery Risk Prediction

This project is part of the **Applied Artificial Intelligence (AAI) M.S. Program** at the **University of San Diego (USD)**. It demonstrates the application of machine learning techniques to predict shipment delays in supply chain operations using the DataCo Smart Supply Chain dataset.

**Course:** AAI-510 – Machine Learning Fundamentals & Applications
**Group:** 4
**Project Status:** Completed

---

# 📌 Project Overview

Late deliveries significantly impact supply chain performance by increasing operational costs, reducing customer satisfaction, and disrupting downstream logistics activities.

This project develops a machine learning-based decision support system capable of predicting whether an order is likely to be delivered late before shipment completion. By identifying high-risk shipments in advance, logistics teams can take proactive actions to mitigate delays and improve service levels.

The project includes:

* Exploratory Data Analysis (EDA)
* Feature Engineering
* Data Leakage Detection
* Machine Learning Model Development
* Model Evaluation & Comparison
* Feature Importance Analysis
* Deployment Architecture Design
* Business Recommendations

---

# 🎯 Project Objectives

### 1. Predict Late Delivery Risk

Develop a binary classification model capable of predicting:

* 0 = On-Time Delivery
* 1 = Late Delivery

before shipment completion.

### 2. Identify Key Business Drivers

Determine which operational factors contribute most to shipment delays, including:

* Shipping Mode
* Scheduled Shipment Days
* Order Type
* Customer Segment
* Geographic Region

### 3. Support Operational Decision-Making

Provide logistics teams with actionable risk scores to:

* Prioritize high-risk shipments
* Reduce delay-related costs
* Improve customer experience

### 4. Compare Multiple Machine Learning Models

Evaluate multiple classification approaches and identify the most effective model for deployment.

---

# 👥 Contributors

### Group 4

* Dhrub Satyam
* George David Asirvatharaj

---

# 🎓 Faculty Advisor

**Prof. Dr. Ankur Bist**
University of San Diego
Applied Artificial Intelligence Program

---

# 🧠 Methods Used

* Exploratory Data Analysis (EDA)
* Feature Engineering
* Feature Selection
* Target Leakage Detection
* One-Hot Encoding
* Classification Modeling
* Hyperparameter Optimization
* Cross Validation
* Model Explainability
* Business Analytics

---

# 🛠️ Technologies

* Python
* Pandas
* NumPy
* Scikit-Learn
* Matplotlib
* Seaborn
* Jupyter Notebook
* Git & GitHub

---

# 📊 Dataset Description

### Dataset

**DataCo Smart Supply Chain Dataset**

Source:
Kaggle DataCo Supply Chain Dataset

### Dataset Characteristics

* 180,519 records
* 53 original features
* Multi-region supply chain operations
* Order, customer, shipment, and financial information
* Real-world logistics and fulfillment data

### Selected Features

#### Numerical Features

* Days for Shipment (Scheduled)
* Product Price
* Order Item Quantity
* Sales
* Order Profit Per Order
* Order Item Discount
* Order Item Discount Rate
* Order Item Total
* Benefit per Order

#### Categorical Features

* Shipping Mode
* Market
* Customer Segment
* Order Region
* Category Name
* Department Name
* Order Country
* Customer Country
* Type

---

# ⚠️ Data Leakage Analysis

A critical part of the project involved identifying features that reveal the target outcome.

### Leakage Identified

**Delivery Status**

Examples:

* Late Delivery
* Shipping On Time
* Advance Shipping
* Shipping Canceled

This feature directly reveals shipment outcome and would artificially inflate model performance.

### Resolution

* Delivery Status removed entirely from modeling.
* Only information available before shipment completion was retained.

---

# 🤖 Machine Learning Task

## Binary Classification

### Target Variable

**Late_delivery_risk**

| Value | Meaning          |
| ----- | ---------------- |
| 0     | On-Time Delivery |
| 1     | Late Delivery    |

### Class Distribution

| Class   | Count  |
| ------- | ------ |
| Late    | 98,977 |
| On-Time | 81,542 |

The dataset is reasonably balanced, allowing effective classification without extensive resampling.

---

# 🔍 Exploratory Data Analysis

### Key Findings

#### Shipping Mode

Late delivery rates by shipping method:

| Shipping Mode  | Late Rate |
| -------------- | --------- |
| Second Class   | 95.3%     |
| Standard Class | 61.9%     |
| First Class    | 45.7%     |
| Same Day       | 38.1%     |

#### Numerical Correlations

Strongest predictor:

* Days for Shipment (Scheduled): -0.37 correlation

This indicates shipment scheduling has a substantial relationship with delivery risk.

---

# ⚙️ Data Preparation Pipeline

### 1. Leakage Removal

Removed:

* Delivery Status

### 2. Feature Selection

Selected:

* 9 Numerical Features
* 9 Categorical Features

### 3. One-Hot Encoding

Categorical variables encoded using:

```python
pd.get_dummies(drop_first=True)
```

### 4. Train-Test Split

* Training Set: 126,363 samples
* Test Set: 54,156 samples
* Split Ratio: 70/30
* Stratified Sampling Applied

### Final Dataset

* 266 encoded features

---

# 🤖 Models Evaluated

## Logistic Regression

A strong linear baseline model providing excellent interpretability.

## Random Forest

Ensemble tree-based classifier capable of capturing nonlinear relationships.

## Extra Trees Classifier

Highly randomized ensemble approach designed to improve generalization.

---

# 📈 Model Performance

| Model               | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
| ------------------- | -------- | --------- | ------ | -------- | ------- |
| Logistic Regression | 69.6%    | 83.6%     | 55.4%  | 66.7%    | 74.2%   |
| Random Forest       | 69.2%    | 79.7%     | 58.8%  | 67.7%    | 73.2%   |
| Extra Trees         | 69.2%    | 79.7%     | 58.8%  | 67.7%    | 73.9%   |

---

# 🏆 Best Model

### Tuned Random Forest

Best Hyperparameters:

```python
{
    "n_estimators": 100,
    "max_depth": 10,
    "min_samples_split": 10,
    "min_samples_leaf": 4
}
```

Performance:

* Accuracy: 69.2%
* Precision: 79.8%
* Recall: 58.8%
* F1 Score: 67.7%
* ROC-AUC: 72.6%

---

# 🔥 Feature Importance

Top predictors identified by Random Forest:

1. Shipping Mode – Standard Class
2. Days for Shipment (Scheduled)
3. Shipping Mode – Second Class
4. Transfer Payment Type
5. Shipping Mode – Same Day

### Key Insight

Shipping mode and shipment scheduling account for approximately 85% of predictive power.

---

# 💡 Business Insights

### 🚚 Shipping Mode is the Primary Risk Driver

Second Class shipments exhibit a 95% late delivery rate.

### 📅 Scheduling Matters

Shipment scheduling strongly influences delivery outcomes.

### 💳 Payment Type Influences Risk

Transfer transactions show elevated delay rates.

### 🌍 Geography Plays a Smaller Role

Markets and regions exhibit relatively similar delay patterns.

---

# 🏗️ Proposed Deployment Architecture

```text
ERP / WMS Systems
        │
        ▼
Feature Engineering Layer
        │
        ▼
Machine Learning API
(Random Forest Model)
        │
        ▼
Risk Probability Scoring
        │
        ▼
Operations Dashboard
        │
        ▼
Shipment Intervention Actions
```

Deployment Recommendations:

* Monthly model retraining
* Data drift monitoring
* Model version control
* Real-time API scoring

---

# 📌 Business Impact

### Operational Benefits

✅ Early identification of high-risk shipments

✅ Reduced logistics penalties and costs

✅ Improved customer satisfaction

✅ Better shipment prioritization

✅ Enhanced supply chain visibility

---

# 🚀 Future Enhancements

### Short-Term

* XGBoost
* LightGBM
* Threshold Optimization
* Additional Logistics Features

### Long-Term

* Real-Time Tracking Integration
* IoT-Based Shipment Monitoring
* Explainable AI using SHAP
* Automated Retraining Pipeline

---

# 📚 Key Takeaways

1. Machine learning can proactively predict shipment delays before dispatch.

2. Shipping Mode is the most influential predictor of delivery risk.

3. Logistic Regression, Random Forest, and Extra Trees deliver comparable performance.

4. Data leakage detection was critical to obtaining realistic results.

5. The solution is deployment-ready as a logistics risk scoring system.

---

## University of San Diego

### AAI-510 | Machine Learning Fundamentals & Applications

### Group 4

### Dhrub Satyam & George David Asirvatharaj
