# Predict Future Sales (Kaggle Competition)

## Overview
This project is based on the [Predict Future Sales competition](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales) on Kaggle.  
The goal is to **forecast the total number of items sold in every shop for the next month**.  

Specifically, we predict `item_cnt_month` for each `(shop_id, item_id)` pair in the test set (month 34).  
Unlike a typical time series forecasting problem, this task involves **thousands of parallel time series** (one per shop–item pair).  
The challenge is to capture both **individual patterns** (e.g., certain products sell better in specific shops) and **global trends** (e.g., seasonality, pricing, category shifts).  

### Business Relevance
From a business perspective, accurate demand forecasting is crucial in retail and e-commerce:
- **Inventory management** – reduce overstock and stockouts.  
- **Supply-chain planning** – better demand visibility for replenishment.  
- **Sales & marketing** – understand dynamics for promotions, pricing, and assortment.  

---

## Dataset
We use the official dataset from Kaggle:  
[Predict Future Sales Competition Dataset](https://www.kaggle.com/competitions/competitive-data-science-predict-future-sales)

---

## Workflow
1. **Data Cleaning & Preprocessing** – prepare raw daily sales.  
2. **Aggregation** – convert to monthly sales at the shop–item level (the prediction target).  
3. **Feature Engineering** – build predictive signals:  
   - lag features  
   - rolling means  
   - price dynamics  
   - calendar features  
4. **Model Training** – train LightGBM on months 0–32, validate on month 33.  
5. **Prediction & Submission** – forecast month 34 and export a Kaggle-ready submission.  

---

## Model & Evaluation
We train a **LightGBM Regressor**, which is well-suited for tabular data with categorical + numerical features.  

- **Metric:** RMSE (Root Mean Squared Error)  
- **Overfitting control:** early stopping on validation error  
- **Validation Result:**  RMSE = 1.567824166482012
