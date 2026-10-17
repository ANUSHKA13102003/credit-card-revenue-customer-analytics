# 💳 Credit Card Revenue & Customer Analytics

**Power BI | SQL | Power Query | DAX | Business Intelligence**

An interactive Power BI analytics project focused on credit card revenue, transaction trends, and customer behaviour. The goal is to understand business performance, explore customer segments, and turn financial data into insights that support better decisions.


---

## 📑 Table of Contents

1. [Project Overview](#-project-overview)
2. [Business Objectives](#-business-objectives)
3. [Business Questions](#-business-questions)
4. [Tools & Technologies](#️-tools--technologies)
5. [Dataset Overview](#-dataset-overview)
6. [Data Preparation & Modelling](#-data-preparation--modelling)
7. [Key Performance Indicators](#-key-performance-indicators)
8. [SQL Business Analysis](#-sql-business-analysis)
9. [Dashboard Overview](#-dashboard-overview)
10. [Dashboard Reports](#-dashboard-reports)
11. [Business Insights](#-business-insights)
12. [Recommendations](#-recommendations)
13. [How to Explore the Project](#️-how-to-explore-the-project)
14. [Repository Structure](#-repository-structure)
15. [Skills Demonstrated](#-skills-demonstrated)
16. [About Me](#-about-me)

---

## 📌 Project Overview

Credit card businesses deal with large amounts of financial and customer data. While this data contains valuable information, understanding revenue trends, transaction activity, and customer behaviour can be difficult without a clear reporting system.

This project shows how Power BI and SQL can bring these different aspects together in one place. It focuses on financial performance, customer segmentation, and weekly trends, making it easier to spot patterns and investigate changes in business performance.

The analysis is organised around practical business questions, with an emphasis on clear metrics, useful visualisations, and evidence-based conclusions.

## 🎯 Business Objectives

- Analyse credit card revenue and transaction performance over time.
- Compare financial performance across different card categories.
- Understand spending patterns across customer segments.
- Examine customer activation and delinquency indicators.
- Develop meaningful KPIs using DAX.
- Create interactive reports for exploring financial and customer data.
- Identify opportunities to improve business performance based on the findings.

## ❓ Business Questions

The project answers the following questions:

1. How does credit card revenue change week over week?
2. Which card categories contribute the most to revenue?
3. How do transaction amounts and counts vary across reporting periods?
4. Which customer segments contribute the most to revenue?
5. How do spending patterns differ by age, income, occupation, and other demographic factors?
6. What percentage of eligible customers have activated their cards?
7. What is the delinquency rate among the relevant customer population?
8. Which customer segments or performance trends need further investigation?
9. What business decisions could be supported by these findings?

## 🛠️ Tools & Technologies

| Tool | Purpose |
| --- | --- |
| **Power BI Desktop** | Interactive dashboards and visual reporting |
| **SQL** | Data querying, aggregation, and analysis |
| **Power Query** | Data cleaning and transformation |
| **DAX** | KPI calculations and time-based comparisons |
| **CSV** | Source datasets |
| **GitHub** | Project documentation and version control |

## 📂 Dataset Overview

The project uses four CSV datasets containing credit card and customer information.

| Dataset | Description |
| --- | --- |
| `credit_card.csv` | Credit card financial and transaction information |
| `cc_add.csv` | Additional credit card records |
| `customer.csv` | Customer demographic and profile information |
| `cust_add.csv` | Additional customer records |

The additional files are appended to their base tables, and the card and customer tables are linked on the client number.

## 🔍 Data Preparation & Modelling

The analysis follows a structured workflow.

**1. Data Inspection:** Review column names, data types, identifiers, and reporting periods.

**2. Data Cleaning:** Check missing values, duplicate records, inconsistent data types, and date issues.

**3. Data Integration:** Combine the base and additional files, then join customer and card data on the client number.

**4. Customer Segmentation:** Group customers by age, income, and other demographic attributes.

**5. DAX Calculations:** Build measures for revenue, transaction activity, activation, delinquency, and weekly comparisons.

**6. Data Validation:** Check that relationships, filters, and aggregations return consistent results.

## 📊 Key Performance Indicators

| KPI | Definition | Business Purpose |
| --- | --- | --- |
| **Total Revenue** | Annual fees + transaction amount + interest earned | Track overall financial performance |
| **Total Interest** | Sum of interest earned | Monitor interest income |
| **Total Transaction Amount** | Sum of transaction amounts | Measure the value of card activity |
| **Transaction Count** | Number of transactions | Track transaction activity |
| **Average Transaction Value** | Transaction amount ÷ transaction count | Understand average transaction size |
| **Customer Activation Rate** | Activated customers ÷ total customers | Measure card engagement |
| **Delinquency Rate** | Delinquent customers ÷ total customers | Monitor credit risk |
| **Week-over-Week Revenue Growth** | (This week − last week) ÷ last week | Spot short-term revenue swings |

Revenue, transaction amount, interest, and fees are kept as separate measures, because they answer different business questions.

## 🧮 SQL Business Analysis

These queries answer the business questions directly from the data. Each one is also saved in `sql/analysis_queries.sql`.

**1. Which card categories earn the most revenue?**

```sql
SELECT
    Card_Category,
    ROUND(SUM(Annual_Fees + Total_Trans_Amt + Interest_Earned), 0) AS total_revenue,
    ROUND(100 * SUM(Annual_Fees + Total_Trans_Amt + Interest_Earned)
          / SUM(SUM(Annual_Fees + Total_Trans_Amt + Interest_Earned)) OVER (), 2) AS revenue_share_pct
FROM cc_detail
GROUP BY Card_Category
ORDER BY total_revenue DESC;
```

**2. How does revenue change quarter over quarter?**

```sql
WITH quarterly AS (
    SELECT current_year, Qtr,
           SUM(Annual_Fees + Total_Trans_Amt + Interest_Earned) AS revenue
    FROM cc_detail
    GROUP BY current_year, Qtr
)
SELECT current_year, Qtr, revenue,
       ROUND(100 * (revenue - LAG(revenue) OVER (ORDER BY current_year, Qtr))
             / LAG(revenue) OVER (ORDER BY current_year, Qtr), 2) AS qoq_growth_pct
FROM quarterly;
```

**3. How does revenue change week over week?**

```sql
WITH weekly AS (
    SELECT Week_Start_Date,
           SUM(Annual_Fees + Total_Trans_Amt + Interest_Earned) AS revenue
    FROM cc_detail
    GROUP BY Week_Start_Date
)
SELECT Week_Start_Date, revenue,
       ROUND(100 * (revenue - LAG(revenue) OVER (ORDER BY Week_Start_Date))
             / LAG(revenue) OVER (ORDER BY Week_Start_Date), 2) AS wow_growth_pct
FROM weekly
ORDER BY Week_Start_Date;
```

**4. Which age groups and genders drive revenue?**

```sql
SELECT
    CASE
        WHEN c.Customer_Age < 30 THEN '20-30'
        WHEN c.Customer_Age < 40 THEN '30-40'
        WHEN c.Customer_Age < 50 THEN '40-50'
        WHEN c.Customer_Age < 60 THEN '50-60'
        ELSE '60+'
    END AS age_group,
    c.Gender,
    ROUND(SUM(d.Annual_Fees + d.Total_Trans_Amt + d.Interest_Earned), 0) AS total_revenue
FROM cc_detail d
JOIN cust_detail c ON d.Client_Num = c.Client_Num
GROUP BY age_group, c.Gender
ORDER BY total_revenue DESC;
```

**5. Which occupations are the most valuable?**

```sql
SELECT
    c.Customer_Job,
    ROUND(SUM(d.Annual_Fees + d.Total_Trans_Amt + d.Interest_Earned), 0) AS total_revenue,
    ROUND(AVG(c.Income), 0) AS avg_income
FROM cc_detail d
JOIN cust_detail c ON d.Client_Num = c.Client_Num
GROUP BY c.Customer_Job
ORDER BY total_revenue DESC;
```

**6. How do activation and delinquency vary by card category?**

```sql
SELECT
    Card_Category,
    ROUND(100 * SUM(Activation_30_Days) / COUNT(*), 2) AS activation_rate_pct,
    ROUND(100 * SUM(Delinquent_Acc) / COUNT(*), 2)     AS delinquency_rate_pct
FROM cc_detail
GROUP BY Card_Category
ORDER BY delinquency_rate_pct DESC;
```

## 📈 Dashboard Overview

The dashboard is organised around two analytical areas.

**Credit Card Financial Performance**
- Revenue and transaction trends
- Weekly financial performance
- Revenue contributions across card categories
- Transaction amounts and counts
- Customer activation and delinquency indicators

**Customer Analysis**
- Revenue across customer segments
- Age and income group comparisons
- Occupation and demographic analysis
- Customer transaction behaviour
- Interactive filters for exploring different customer groups

## 📄 Dashboard Reports

| Report | What it covers | Link |
| --- | --- | --- |
| **Transaction Analysis** | Transaction activity, revenue trends, expenditure categories, card performance | [View PDF](reports/Credit%20Card%20Financial%20Dashboard-Transaction.pdf) |
| **Customer Analysis** | Customer revenue, interest, income groups, demographics, job categories | [View PDF](reports/Credit%20Card%20Financial%20Dashboard-Customer.pdf) |

## 💡 Business Insights

Each insight below comes from running the SQL queries above against the data.

| # | Question | Finding |
| --- | --- | --- |
| 1 | Top card category by revenue (Query 1) | **[Category]** earns **[X%]** of total revenue |
| 2 | Quarterly trend (Query 2) | Revenue **[rose / fell] [X%]** from **[Quarter]** to **[Quarter]** |
| 3 | Weekly trend (Query 3) | Biggest weekly swing: **[X%]** in the week of **[date]** |
| 4 | Age and gender (Query 4) | **[Age group, gender]** generates the most revenue at **[amount]** |
| 5 | Occupation (Query 5) | **[Job]** leads on revenue; **[Job]** has the highest average income |
| 6 | Activation and risk (Query 6) | **[Category]** has the highest delinquency at **[X%]** |

## 🚀 Recommendations

| Focus Area | Business Action |
| --- | --- |
| Customer Engagement | Run onboarding nudges and first-spend incentives to lift activation |
| Card Performance | Review fees and benefits for the weakest card categories |
| Customer Segmentation | Offer tailored rewards to the highest-revenue age and job segments |
| Financial Performance | Review week-over-week growth on a regular schedule to catch dips early |
| Delinquency | Review credit limits and send early payment reminders in high-risk segments |

## ▶️ How to Explore the Project

1. Clone or download the repository.
2. Look through the dashboard screenshots in `screenshots/` and the PDF reports in `reports/`.
3. Load the CSV files from `data/` into a SQL database (MySQL or similar).
4. Run the queries in `sql/analysis_queries.sql` and compare the results with the dashboard.

## 📁 Repository Structure

```text
credit-card-revenue-customer-analytics/
│
├── README.md
├── data/
│   ├── credit_card.csv
│   ├── cc_add.csv
│   ├── customer.csv
│   └── cust_add.csv
├── sql/
│   └── analysis_queries.sql
├── screenshots/
│   ├── customer_dashboard.png
│   └── transaction_dashboard.png
└── reports/
    ├── Credit Card Financial Dashboard-Customer.pdf
    └── Credit Card Financial Dashboard-Transaction.pdf
```

## 🧠 Skills Demonstrated

- Data cleaning and transformation
- SQL querying, joins, window functions, and aggregation
- Data modelling and table relationships
- DAX calculations and KPI development
- Time-based performance analysis
- Interactive dashboard design
- Business analysis and data storytelling

## 👩‍💻 About Me

I'm **Anushka**, a final-year B.Tech Computer Science Engineering student specialising in Data Science and AI at IILM University, Greater Noida.

I'm interested in data analytics and business intelligence, especially using SQL and Power BI to understand business problems and communicate findings clearly.

This project is part of my effort to build practical analytical skills and present analysis in a way that connects technical work with business decisions.

### 📫 Let's Connect

| | |
| --- | --- |
| 💼 **LinkedIn** | [linkedin.com/in/anushka-38b2b227a](https://www.linkedin.com/in/anushka-38b2b227a) |
| 📧 **Email** | [its.anushka869@gmail.com](mailto:its.anushka869@gmail.com) |
| 🐙 **GitHub** | [ANUSHKA13102003](https://github.com/ANUSHKA13102003) |
| 🧩 **LeetCode** | [optimizer86](https://leetcode.com/u/optimizer86/) |

⭐ If you found this project useful, consider giving it a star.
