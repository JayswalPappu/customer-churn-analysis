# Customer Churn Analysis & Customer Intelligence

An end-to-end **Data Analytics project** focused on understanding customer churn, retention, revenue risk, customer tenure, and support-related factors.

The project combines **Python, Pandas, NumPy, SQLite, Matplotlib, and Seaborn** to extract, clean, transform, analyze, and visualize customer subscription data.

## 📌 Project Overview

Customer churn is a major business problem for subscription-based businesses. The objective of this project is to identify:

- How many customers are churning
- Which subscription plans have higher churn
- Which customer segments/states show higher churn
- How much revenue is at risk because of churn
- How customer tenure and age relate to churn
- Whether support escalations and complaints are associated with churn
- Which customers fall into low, medium, and high churn-risk categories

## 🛠️ Tech Stack

- **Python**
- **Pandas** – data manipulation and analysis
- **NumPy** – numerical operations and feature engineering
- **SQLite** – relational data storage and extraction
- **Matplotlib** – data visualization
- **Seaborn** – correlation and statistical visualization
- **Jupyter Notebook** – analysis environment

## 📂 Project Structure

```text
Customer-Churn-Analysis/
│
├── Churn_analysis.ipynb
├── customer_churn.db
├── test_database.sqlite
├── Exported_churn_data.csv
├── Churn_Analysis_Report.pdf
└── README.md
```

## 🗄️ Data Source & Database

The project uses a SQLite database named `customer_churn.db`.

The database contains three main relational tables:

### `db_customer`

Customer demographic information:

- `customerid`
- `name`
- `country`
- `state`
- `gender`
- `dob`
- `interests`
- `pincode`

### `db_subscription`

Subscription and churn information:

- `customerid`
- `subscription_start_date`
- `subscription_type`
- `renewal_date`
- `plan_type`
- `contract_type`
- `cancellation_date`
- `cancellation_reason`
- `monthly_charges`
- `cltv`
- `churn_score`

### `db_support`

Customer support information:

- `customerid`
- `complaint_date`
- `escalations`
- `csat_score`
- `comment`

The three tables are joined using `customerid` to create the final analytical dataset.

## 🔄 Analysis Workflow

```text
SQLite Database
      ↓
Data Extraction
      ↓
Data Cleaning
      ↓
Data Standardization
      ↓
Feature Engineering
      ↓
Table Merging
      ↓
Exploratory Data Analysis
      ↓
KPI Calculation
      ↓
Data Visualization
      ↓
Business Insights
```

## 🧹 Data Cleaning

The notebook performs several cleaning operations:

- Renames `name` to `customer_name`
- Removes unnecessary columns
- Converts date columns to datetime format
- Standardizes gender values such as `Men` → `Male` and `Women` → `Female`
- Handles missing country values using state-country mapping
- Removes unnecessary support columns
- Handles duplicate support records by keeping the latest complaint record per customer

## ⚙️ Feature Engineering

The following analytical features are created:

### Churn Flag

A customer is considered churned when a `cancellation_date` exists.

```python
df_db_subscription['churn_flag'] = np.where(
    df_db_subscription['cancellation_date'].notna(), 1, 0
)
```

### Customer Age

Customer age is calculated from the date of birth.

### Customer Tenure

Tenure is calculated using:

- Cancellation date for churned customers
- Current date for active customers

### Churn Risk

Customers are segmented using their churn score:

| Churn Score | Risk |
|---|---|
| `< 50` | Low |
| `50–69` | Medium |
| `>= 70` | High |

## 📊 Key KPIs

The analysis calculates:

- Churn Rate
- Retention Rate
- Churn by Plan Type
- Churn by State
- Churn by Subscription Type
- ARPU (Average Revenue Per User)
- Average Customer Tenure
- Revenue at Risk
- Escalation Rate
- Average Complaints per Customer
- Correlation between Escalations and Churn
- Customer Churn Risk

## 📈 Visualizations

The project includes visual analysis for:

- Monthly churn trend
- Churn by plan type
- Churn by state
- Correlation heatmap

These visualizations help identify patterns and customer segments that require attention.

## 📌 Current Notebook Results

The current version of the notebook produces the following example KPIs:

| KPI | Result |
|---|---:|
| Churn Rate | 28.57% |
| Retention Rate | 71.43% |
| Basic Plan Churn | 60.00% |
| Premium Plan Churn | 14.29% |
| Standard Plan Churn | 22.22% |
| ARPU | 18.85 |
| Average Tenure | 1,544 days |
| Revenue at Risk | 73.94 |
| Escalation Rate | 19.05% |
| Average Complaints per User | 0.43 |

> **Note:** These values are generated from the current dataset included with the project. If the dataset is expanded or replaced, rerun the notebook to generate updated KPIs.

## 💡 Business Insights

The analysis can help a business:

- Identify high-churn subscription plans
- Prioritize high-risk customers for retention campaigns
- Investigate regions with unusually high churn
- Monitor customers with repeated complaints or escalations
- Estimate potential revenue loss caused by churn
- Develop targeted retention strategies
- Encourage customers toward more stable subscription contracts

## 📄 Project Report

`Churn_Analysis_Report.pdf` contains the project documentation, churn-analysis roadmap, calculated metrics, and portfolio-oriented project summary.

## 🎯 Future Improvements

Potential next steps for this project:

- Expand the dataset for more robust analysis
- Build a machine-learning churn prediction model
- Compare Logistic Regression, Random Forest, XGBoost/LightGBM, etc.
- Perform feature importance analysis
- Build an interactive Power BI/Tableau dashboard
- Add customer-level retention recommendations
- Automate periodic churn reporting

## 👨‍💻 Author

**Pappu Kumar Jayswal**

B.Tech – Computer Science & Engineering

---

⭐ If you find this project useful, feel free to star the repository.
