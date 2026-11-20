# Day 7 Mini Project: Sales KPIs & Business Review

## 📌 Business Question
The Head of E-commerce asked: *"Give me a monthly business review. How are we doing, where is the problem, and what should we do?"* 
This project transforms raw transactional data into a clean, defensible suite of Key Performance Indicators (KPIs) to answer that question and provide actionable recommendations.

## 📊 The Dataset
**Note:** This dataset is **synthetic** (fake) and was generated for educational purposes. It does not represent a real company. 
- **Source:** `ecommerce_sales_flat.csv`
- **Timeframe:** January 2024 to late 2026.
- **Size:** ~23,500 rows of transactional order lines (including order status, geography, category, revenue, and margin data).

## 🧹 Data Cleaning & Decisions
Before calculating any KPIs, a `sales_clean` table was created. The following business rules were applied:
1. **Duplicates:** Removed 30 exact duplicate rows to prevent revenue inflation. (Rows went from 23,538 to 23,508).
2. **Unmatched Categories (P999):** Kept the revenue to maintain honest reporting, but labeled the category as `"Unknown"` so it wouldn't break category-level aggregations.
3. **Payment Spelling:** Standardized casing (e.g., "upi" and "credit card" to Title Case).
4. **Date Anomalies:** Flagged rows where the delivery date occurred before the order date (`is_bad_date`) so they could be excluded from delivery-time calculations.

## 📈 KPI Definitions
- **GMV (Gross Merchandise Value):** Sum of line_amount across all statuses.
- **Net Revenue:** Sum of line_amount for `Delivered` orders only.
- **Average Order Value (AOV):** Net Revenue ÷ Distinct Order IDs.
- **Gross Margin %:** Total Margin ÷ Total Net Revenue (excluding rows with null unit costs).
- **Cancellation Rate:** Distinct Cancelled Orders ÷ Total Distinct Orders.
- **Return Rate:** Distinct Returned Orders ÷ Distinct Delivered Orders.
- **Average Discount:** Weighted discount (Total Discount Amount ÷ Total Gross Amount).

## 🔍 3 Key Findings
1. **The Electronics Trap:** Electronics drives **53%** of all net revenue, but has the lowest profit margin at **15.6%**. Conversely, Beauty drives only 3.4% of revenue but boasts a **50.7%** margin.
2. **Seasonal Hangover:** The business has a severe post-holiday drop. Revenue plummets by **-31.6%** in February compared to January.
3. **The East Region Lags:** The East region generates ₹2.27 Crore in revenue, which is nearly half of what the South (₹4.19 Crore) generates. This is largely because Eastern customers are buying lower-value items (Mixer Grinders) compared to high-end electronics bought in other regions.

## 🛠️ Tools Used
- **Databricks / Apache Spark (PySpark):** For data cleaning, aggregation, and Window Functions.
- **Markdown:** For documentation and business logic definitions within the notebook.

## 🚀 How to Run
1. Clone this repository.
2. Import the `.ipynb` notebook into Databricks (or any Jupyter environment with PySpark installed).
3. Upload the `ecommerce_sales_flat.csv` dataset to a Databricks table.
4. Run the notebook top-to-bottom. It will automatically build the `sales_clean` table, calculate the KPIs, and output the trend tables.