# 🛒 Instacart Market Basket Analysis

### A Complete Data Analytics Project using SQL, Python & Power BI

---

## 📌 Project Overview

This project analyzes **Instacart’s market basket data**, exploring customer purchase behavior, product affinities, and reorder patterns.
It demonstrates how data from a transactional database can be **cleaned, modeled, and visualized** for actionable business insights.

---

## 🧠 Key Objectives

* Understand **customer behavior** (order frequency, retention, basket size).
* Identify **top-performing departments, aisles, and products**.
* Discover **co-purchase patterns** and potential **cross-selling opportunities**.
* Build a full **end-to-end analytical workflow** — from raw SQL queries to Power BI dashboards.

---

## 🧩 Data Source

Dataset: [Instacart Market Basket Analysis (Kaggle)](https://www.kaggle.com/psparks/instacart-market-basket-analysis)
Tables used:

* `orders`
* `order_products_train`
* `products`
* `aisles`
* `departments`

---

## 🧱 Data Pipeline

### 1️⃣ **Data Extraction — MySQL**

All data exploration and transformations were done in MySQL.

📄 File: `queries.sql`
Includes:

* Order and user-level metrics
* Reorder ratios
* Department and aisle summaries
* Product co-purchase relationships
* View creation for Power BI import

Example views:

```sql
CREATE OR REPLACE VIEW v_department_summary AS
SELECT 
    d.department,
    COUNT(DISTINCT opt.order_id) AS orders_count,
    SUM(opt.reordered) / COUNT(*) AS reorder_ratio
FROM order_products_train opt
JOIN products p ON opt.product_id = p.product_id
JOIN departments d ON p.department_id = d.department_id
GROUP BY d.department;
```

---

### 2️⃣ **Data Transformation — Python (Pandas)**

📄 File: `add_data.ipynb`
Used for additional transformations:

* Chunked CSV loading (due to dataset size)
* Feature engineering for basket size, co-occurrence
* Exporting summarized tables for Power BI

---

### 3️⃣ **Data Visualization — Power BI**

Power BI dashboards were built using the SQL views and Python outputs.
Each dashboard focuses on a specific business question.

---

## 📊 Power BI Dashboards

### 🧍‍♀️ **User Behavior & Retention Dashboard**

**Goal:** Understand customer loyalty and churn trends.
**Key Metrics:**

* Total Users: `206K`
* Avg Orders per User: `16.59`
* Avg Days Between Orders: `15.45 days`
* Retention drops after the 4th order → needs re-engagement campaigns.

📈 *Insight:*

> All users complete at least 4 orders before churn; retention remains 100% until then and declines sharply afterward — suggesting fatigue or lack of novelty.

---

### ⏱️ **Orders & Time Analysis**

**Goal:** Analyze when customers buy and what their basket sizes look like.

**Insights:**

* Most orders happen **Monday–Tuesday (start of week)**.
* Peak hours: **9 AM – 4 PM**.
* 50% of baskets are **medium-sized (6–15 items)** → planned purchases.
* Weekly ordering pattern confirms **habitual shopping cycles**.

**Added Metric:**

* **Order Frequency Histogram** (based on `days_since_prior_order`)

---

### 🧺 **Basket Composition & Aisle Insights**

**Goal:** Identify which aisles dominate and how products are co-purchased.

**Highlights:**

* **Fresh Fruits & Vegetables** = 35% of total basket share.
* **Dairy products (milk, yogurt, cheese)** co-occur most often.
* **Cross-sell opportunities:**

  * 🥗 *Healthy Combo:* Fresh Produce + Yogurt
  * 🍿 *Snack Pack:* Chips + Sparkling Water

**Visuals:**

* Aisle Heatmap (co-purchase matrix)
* Basket Share Donut Chart
* Basket Volume by Aisle

---

### 🏬 **Department & Product Analysis**

**Goal:** Assess which departments drive the most sales and reorders.

**Findings:**

* **Produce, Dairy & Eggs, Beverages** = ~50% of orders, highest reorder (65–67%).
* **Household & Personal Care** show lowest reorders → opportunity for loyalty incentives.
* Dynamic slicer for viewing *Top 8 Products* per department.

---

## 🧩 Key Insights Summary

| Theme                 | Takeaway                                                                         |
| --------------------- | -------------------------------------------------------------------------------- |
| **Customer Behavior** | Average user places ~16 orders, churns after 4th order without retention effort. |
| **Timing**            | Peak activity Monday–Tuesday, 9AM–4PM.                                           |
| **Basket Dynamics**   | 48% medium baskets → planned shopping.                                           |
| **Product Mix**       | Fresh, perishable goods drive repeat orders.                                     |
| **Opportunity**       | Low-repeat departments can be targeted with promotions and cross-sells.          |

---

## ⚙️ Tools & Technologies

| Category      | Tools                                  |
| ------------- | -------------------------------------- |
| Database      | MySQL                                  |
| Data Analysis | Python (Pandas, Matplotlib)            |
| Visualization | Power BI                               |
| Other         | SQL Views, DAX, Markdown for reporting |

---

## 🧾 Folder Structure

```
📂 Instacart_Market_Basket_Analysis
 ┣ 📜 queries.sql
 ┣ 📔 add_data.ipynb
 ┣ 📁 /PowerBI Dashboard screan
 ┃ ┣ user_behavior.png
 ┃ ┣ order_and_time_analysis.png
 ┃ ┣ basket_composition.png
 ┃ ┗ department_analysis.png
 ┗ 📄 README.md
```

---

## 💡 Future Improvements

* Predict reorder probability using **XGBoost or CatBoost**.
* Implement RFM segmentation for user clustering.
* Add profitability metrics to rank products by margin, not just order count.

---

## ✍️ Author

**Maryam Mohammadtalebi**
📧 *mohammadtalebi.maryam@gmail.com*
