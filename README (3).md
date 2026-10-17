# 💳 Credit Card Revenue & Customer Analytics Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-Data%20Prep-336791?logo=postgresql&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Measures-0078D4)
![Power Query](https://img.shields.io/badge/Power%20Query-ETL-217346)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

> An end-to-end business intelligence project that turns raw credit card and customer data into an interactive Power BI dashboard, so a business team can see **where revenue comes from, who drives it, and where risk is building up**.

<!-- Add your dashboard screenshot here -->
<!-- ![Dashboard Preview](screenshots/dashboard_preview.png) -->

---

## 📑 Table of Contents

1. [Why This Project](#-why-this-project)
2. [Business Questions](#-business-questions)
3. [Tech Stack](#-tech-stack)
4. [Data](#-data)
5. [Approach](#-approach)
6. [KPIs and DAX](#-kpis-and-dax)
7. [Dashboard Walkthrough](#-dashboard-walkthrough)
8. [Key Insights](#-key-insights)
9. [Recommendations](#-recommendations)
10. [Run It Yourself](#-run-it-yourself)
11. [Repository Structure](#-repository-structure)
12. [Skills Demonstrated](#-skills-demonstrated)
13. [About Me](#-about-me)

---

## 🎯 Why This Project

A credit card business generates thousands of transactions and customer records every week. On their own, those rows say very little. Leadership needs quick answers:

- Is revenue growing or slipping, and how fast?
- Which card types and customer groups bring in the most money?
- How many customers are actually using their cards?
- Where is delinquency showing up?

I built this dashboard to answer those questions in one place, with filters that let anyone slice the numbers by week, quarter, card category, age group, income group, and more, without writing a single query.

---

## ❓ Business Questions

| # | Question |
|---|----------|
| 1 | How does revenue move week over week and quarter over quarter? |
| 2 | Which card categories (Blue, Silver, Gold, Platinum) contribute the most? |
| 3 | How do transaction amount and volume differ across periods? |
| 4 | Which age groups and income groups spend and earn the most for the business? |
| 5 | Does revenue differ by gender, occupation, education, or marital status? |
| 6 | Which states and customer segments are the top performers? |
| 7 | What share of customers are activated? |
| 8 | What is the delinquency rate, and which segments carry it? |

---

## 🛠 Tech Stack

| Tool | How I used it |
|------|---------------|
| **SQL** | Loaded the CSVs, joined tables, and checked data quality before modelling |
| **Power Query** | Cleaned data, fixed data types, and shaped tables for reporting |
| **DAX** | Built calculated columns and measures for KPIs, segmentation, and week-over-week logic |
| **Power BI Desktop** | Data model, visuals, slicers, and dashboard layout |
| **GitHub** | Version control and documentation |

---

## 📂 Data

Four CSV files make up the model:

| File | Contents |
|------|----------|
| `credit_card.csv` | Card-level financial data: card category, annual fees, transaction amount and count, interest earned, credit limit, utilisation |
| `cc_add.csv` | Additional card records for the later reporting weeks |
| `customer.csv` | Customer demographics: age, gender, education, marital status, income, occupation, state |
| `cust_add.csv` | Additional customer records for the later reporting weeks |

The additional files are appended to their base tables so the dashboard covers the full reporting period.

### Data quality checks
- Column names and data types verified
- Missing values and duplicates identified
- Date fields validated and converted to a weekly reporting calendar
- Customer and card identifiers checked for clean one-to-many joins
- Metric definitions agreed before any KPI was calculated

---

## 🔧 Approach

**1. Integrate**: Combined base and additional files, then joined card data to customer data on the client identifier.

**2. Clean and transform**: Standardised types and dates in Power Query, and added week and quarter fields for time analysis.

**3. Model**: Built a relationship between the customer and card tables so every slicer filters the whole report consistently.

**4. Segment**: Created age bands, income bands, and a combined revenue measure using DAX.

**5. Measure**: Wrote reusable DAX measures for revenue, interest, income, activation, delinquency, and week-over-week growth.

**6. Visualise**: Designed two report pages: a customer view and a financial performance view, with consistent filters.

---

## 📊 KPIs and DAX

| KPI | Definition |
|-----|------------|
| **Total Revenue** | Annual fees + transaction amount + interest earned |
| **Total Interest** | Sum of interest earned |
| **Total Income** | Sum of customer income across the filtered population |
| **Transaction Count / Amount** | Volume and value of card activity |
| **Avg. Transaction Value** | Transaction amount ÷ transaction count |
| **Activation Rate** | Activated customers ÷ total customers |
| **Delinquency Rate** | Delinquent customers ÷ total customers |
| **Week-over-Week Revenue Growth** | Change in revenue vs. the previous reporting week |

### Sample measures

```DAX
Revenue =
    credit_card[Annual_Fees]
    + credit_card[Total_Trans_Amt]
    + credit_card[Interest_Earned]
```

```DAX
Age Group =
SWITCH (
    TRUE (),
    customer[Customer_Age] < 30, "20-30",
    customer[Customer_Age] < 40, "30-40",
    customer[Customer_Age] < 50, "40-50",
    customer[Customer_Age] < 60, "50-60",
    "60+"
)
```

```DAX
Current Week Revenue =
CALCULATE (
    SUM ( credit_card[Revenue] ),
    FILTER (
        ALL ( credit_card ),
        credit_card[Week_Num] = MAX ( credit_card[Week_Num] )
    )
)

Previous Week Revenue =
CALCULATE (
    SUM ( credit_card[Revenue] ),
    FILTER (
        ALL ( credit_card ),
        credit_card[Week_Num] = MAX ( credit_card[Week_Num] ) - 1
    )
)

WoW Revenue Growth % =
DIVIDE ( [Current Week Revenue] - [Previous Week Revenue], [Previous Week Revenue] )
```

> Column names above should match your final model. Adjust if yours differ.

---

## 🖥 Dashboard Walkthrough

### Page 1: Customer Report
- KPI cards: Total Revenue, Total Interest, Total Income, Customer Satisfaction Score
- Weekly revenue trend split by gender
- Revenue by age group
- Revenue by occupation, with total transaction amount and income
- Slicers: quarter, income group, card category, week start date

### Page 2: Financial Performance
- Weekly revenue and week-over-week growth
- Card category comparison
- Top states, salary group, dependent count, marital status, and education level breakdowns
- Activation and delinquency monitoring

---

## 💡 Key Insights

> Replace the bracketed values with the numbers from your final, verified dashboard. Keep each insight to the format below.

1. **[Top segment]** drives the largest share of revenue at **[X%]**, so retention efforts there protect the most income.
2. **[Card category]** leads on transaction volume, but **[Card category]** generates more revenue per customer.
3. **[Age group]** is the highest-spending group, while **[Age group]** is under-penetrated.
4. Revenue **[rose / fell] [X%]** between **[Week A]** and **[Week B]**, driven mainly by **[driver]**.
5. The delinquency rate is **[X%]**, concentrated in **[segment]**.
6. **[X%]** of customers are activated, leaving **[Y]** inactive accounts as an engagement opportunity.

---

## 🚀 Recommendations

| Finding | Suggested action |
|---------|------------------|
| High-value segment identified | Build loyalty and cashback offers aimed at that segment |
| Low activation in some groups | Run onboarding nudges and first-spend incentives |
| Delinquency concentrated in a segment | Tighten credit-limit review and send early payment reminders |
| Weak-performing card category | Review fees and benefits, or target upgrades from a lower tier |
| Weekly revenue swings | Track week-over-week growth on a regular review cadence |

---

## ▶️ Run It Yourself

1. Clone the repository
   ```bash
   git clone https://github.com/ANUSHKA13102003/credit-card-revenue-customer-analytics.git
   ```
2. Install **Power BI Desktop** (free, Windows).
3. Open `dashboard/credit_card_dashboard.pbix`.
4. If prompted, point the data source to the `data/` folder and click **Refresh**.
5. Use the slicers to explore the report.

SQL queries used for data preparation are in `sql/analysis_queries.sql`.

---

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
├── dashboard/
│   └── credit_card_dashboard.pbix
├── screenshots/
│   └── dashboard_preview.png
└── docs/
    └── business_case_study.pdf
```

---

## 🧰 Skills Demonstrated

- Data cleaning and validation (SQL, Power Query)
- Data modelling and table relationships
- DAX: calculated columns, measures, time-based comparisons
- KPI definition and business metric design
- Dashboard design and interactive storytelling
- Turning findings into business recommendations

---

## 👩‍💻 About Me

**Anushka**
Final-year B.Tech CSE (Data Science & AI), IILM University, Greater Noida
Aspiring Data Analyst, passionate about SQL, Power BI, and turning data into decisions.

📫 [GitHub](https://github.com/ANUSHKA13102003) · [LinkedIn](#) · [Email](#)

⭐ If you found this project useful, consider giving it a star.
