# Part 1: E-Commerce Customer Segmentation using RFM and Clustering

## 1. Project Title
**E-Commerce Customer Segmentation using RFM Analysis and K-Means Clustering**

---

## 2. Business Problem
An e-commerce company wants to better understand its customers in order to:
- Design targeted marketing campaigns
- Improve customer retention
- Identify high-value customer groups
- Reduce churn among at-risk customers

Using transaction-level purchase data, we segment customers into distinct groups based on their buying behaviour using RFM (Recency, Frequency, Monetary) analysis and K-Means clustering.

---

## 3. Dataset Source
- Source: Provided dataset for Part 1 of the Business Analysis Project
- File: `part_1_ecommerce_customer_segmentation.csv`
- See `dataset_source.md` for full details

---

## 4. Dataset Description
| Column | Description |
|---|---|
| InvoiceNo | Unique transaction/invoice identifier |
| StockCode | Unique product code |
| Description | Product name/description |
| Category | Product category (e.g. Electronics, Grocery, Apparel) |
| Quantity | Units purchased per line item |
| InvoiceDate | Date and time of transaction |
| UnitPrice | Price per unit (£) |
| CustomerID | Unique customer identifier |
| Country | Customer's country |

- **Raw rows:** 4,395
- **Unique customers (raw):** 692
- **Countries:** 11
- **Product Categories:** 11
- **Date range:** January 2025 – November 2025

---

## 5. Tools and Libraries Used
| Tool | Purpose |
|---|---|
| Python 3 | Programming language |
| Pandas | Data loading, cleaning, feature engineering |
| NumPy | Numerical operations |
| Matplotlib | Data visualizations |
| Seaborn | Statistical charts |
| Scikit-learn | StandardScaler, KMeans, silhouette_score |
| Jupyter Notebook | Interactive development environment |

---

## 6. Steps Performed
1. Imported libraries and loaded raw dataset
2. Performed data understanding — explored columns, types, missing values
3. Cleaned data — removed nulls, bad quantities/prices, cancellations, duplicates
4. Engineered customer-level RFM features
5. Conducted Exploratory Data Analysis with 7 charts
6. Applied StandardScaler to normalize RFM features
7. Used Elbow Method + Silhouette Score to select K=4
8. Trained K-Means model and assigned cluster labels
9. Profiled each cluster and interpreted customer segments
10. Delivered actionable business recommendations per segment

---

## 7. Data Cleaning Summary
| Step | Action | Rows Removed |
|---|---|---|
| Missing CustomerID | Dropped rows — cannot attribute to a customer | 208 |
| Missing Description | Dropped rows — incomplete product data | 64 |
| Non-positive Quantity | Removed zero/negative quantity (returns) | ~250 |
| Non-positive UnitPrice | Removed zero/negative prices (errors) | ~3 |
| Cancelled Invoices | Removed invoices starting with 'C' | 0 found |
| Duplicate Records | Removed fully duplicate rows | 31 |
| **Final clean dataset** | | **3,848 rows, 681 customers** |

---

## 8. Key EDA Insights
- Revenue is highly concentrated in a few top countries
- Most customers purchase infrequently (right-skewed frequency distribution)
- A small number of products drive the majority of revenue
- Significant outliers exist in quantity and revenue — likely bulk/wholesale orders
- Spend is right-skewed: a small customer group generates most revenue

---

## 9. Clustering Approach
- **Features used:** Recency, Frequency, Monetary (RFM)
- **Normalization:** StandardScaler (zero mean, unit variance)
- **Algorithm:** K-Means
- **K selection:** Elbow method + Silhouette Score → **K = 4**
- **Random state:** 42 (reproducible)

---

## 10. Cluster Interpretation

| Cluster | Avg Recency | Avg Frequency | Avg Monetary | Customer Type | Size |
|---|---|---|---|---|---|
| 0 | 74 days | 1.5 orders | £8,192 | Occasional Buyers | 257 |
| 1 | 71 days | 3.2 orders | £19,588 | Regular Customers | 163 |
| 2 | 233 days | 1.4 orders | £8,242 | Inactive / At-Risk | 217 |
| 3 | 77 days | 3.9 orders | £46,557 | High-Value Loyals | 44 |

---

## 11. Final Business Recommendations

### Cluster 3 — High-Value Loyal Customers
- Launch a **VIP loyalty programme** with exclusive perks: early product access, free express shipping, dedicated support
- Send personalised product bundles based on their top categories
- Trigger a **proactive retention alert** if no purchase in 30+ days

### Cluster 1 — Regular Customers
- Run a **"spend and earn" upgrade scheme** to move them toward Cluster 3
- Use cross-sell recommendations based on purchase history
- Offer time-limited double-points events to increase order frequency

### Cluster 0 — Occasional Buyers
- Run **seasonal and event-based promotions** to re-engage them
- Send a "We miss you" email after 45 days of inactivity with a discount voucher
- Highlight bestsellers in their preferred product category

### Cluster 2 — Inactive / At-Risk Customers
- Launch an immediate **win-back campaign** with a 15–20% discount code valid for 2 weeks
- After 2 failed re-engagement attempts, move to a low-frequency newsletter
- Investigate whether churn is concentrated in specific countries or categories

---

## 12. How to Run the Project

### Prerequisites
```bash
pip install -r requirements.txt
```

### Steps
```bash
# Clone the repository
git clone <your-repo-url>
cd part1-customer-segmentation

# Place the dataset in the project root
# File: part_1_ecommerce_customer_segmentation.csv

# Launch the notebook
jupyter notebook notebook.ipynb
```

Run all cells from top to bottom. Charts will be saved automatically to the `/images` folder.
