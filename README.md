# 📊 Retail Demand Forecasting & Inventory Optimization (M5 Walmart Dataset)

An end-to-end retail analytics project that forecasts item-level weekly demand, translates those forecasts into optimal inventory decisions using Economic Order Quantity (EOQ), and surfaces everything through an interactive Power BI dashboard.

---

## 🧭 Overview

Retailers lose money two ways: **stockouts** (lost sales, unhappy customers) and **overstock** (wasted holding cost, markdowns). This project builds a pipeline that helps avoid both — using Walmart's M5 sales data to forecast short-term demand per item, then using those forecasts to calculate how much and how often each item should be reordered.



## 🔁 Pipeline


Daily M5 sales data
       │
       ▼
Weekly aggregation (per item, per store)
       │
       ▼
4-week ahead demand forecasting (per item)      
       │
       ▼
EOQ / inventory calculation
       │
       ▼
Power BI dashboard 
       │
       ▼
 Visualization        


## 🎯 Objectives

- Aggregate noisy daily sales into stable weekly demand signals
- Forecast demand for every item, 4 weeks ahead
- Feed forecasts into an EOQ model to recommend order quantities
- Classify items by sales contribution and demand pattern 
- Turn all of the above into business-usable insights, not just model metrics

---

## 🗂️ Dataset

Built on the **M5 Forecasting (Walmart)** dataset — daily unit sales for thousands of items across multiple stores and categories (FOODS, HOUSEHOLD, HOBBIES), including calendar effects like holidays and SNAP (food assistance) days, plus historical pricing.

---

## 🔬 Methodology

### 1. Preprocessing
- Aggregated daily sales to **weekly** granularity per item/store — reduces noise and aligns with realistic replenishment cycles
- Engineered features: lag values (`lag_1`, `lag_2`, `lag_4`), rolling means (`rolling_mean_4`, `rolling_mean_12`), holiday and SNAP flags, weekend sales share, and price

### 2. Forecasting
- Forecasted **4 weeks ahead** per item
- Evaluated against actuals using error metrics robust to intermittent/zero-sales weeks (WMAPE preferred over plain MAPE)

### 3. Inventory Optimization (EOQ)
- Computed **Economic Order Quantity** per item using annual demand (derived from forecasts), ordering cost, and holding cost
- Translated EOQ into estimated orders/year per item

### 4. Segmentation
- **ABC / Pareto analysis**: ranked items by sales contribution to identify the small % of SKUs driving most revenue
- **Intermittency classification**: flagged items by % of zero-sales weeks (Regular / Moderately Intermittent / Highly Intermittent) — these need buffer stock rather than tighter forecasts

---


---



---

## 🛠️ Tech Stack

| Layer | Tools |
|---|---|
| Data processing | Python, Pandas, NumPy ,Scikit-Learn|
| Forecasting | XGBoost |
| Inventory logic|EOQ=√(2DS / H)|
| Dashboard | Power BI |

---

## 📁 Project Structure

├── data/
├── visuals/
├── notebooks/                  # EDA, forecasting, EOQ calculation
├── dashboard/                  # Power BI 
└── README.md





## ⚠️ Limitations & Future Work

- EOQ inputs (holding/ordering cost) are estimated, not sourced from real Walmart cost data — results are directional, not exact dollar figure.
- Forecasts currently don't incorporate promotions/markdown events beyond what's in the base M5 calendar
- Next steps: incorporate real/estimated cost data for $-value savings estimates, extend forecast horizon, add streamlit interface.

---

## 👤 Author

Shruti Tanwar
