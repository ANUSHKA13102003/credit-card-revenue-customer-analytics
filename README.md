# 💳 Credit Card Revenue & Customer Analytics

**Power BI | SQL | Power Query | DAX | Business Intelligence**

An interactive Power BI analytics project focused on credit card revenue, transaction trends, and customer behaviour. The goal is to understand business performance, explore customer segments, and turn financial data into insights that support better decisions.

---

## 📑 Table of Contents

1. [Project Overview](#-project-overview)
2. [Business Objectives](#-business-objectives)
3. [Business Questions](#-business-questions)
4. [Tools & Technologies](#-tools--technologies)
5. [Dataset Overview](#-dataset-overview)
6. [Data Preparation & Modelling](#-data-preparation--modelling)
7. [Key Performance Indicators](#-key-performance-indicators)
8. [Dashboard Overview](#-dashboard-overview)
9. [Business Insights](#-business-insights)
10. [Recommendations](#-recommendations)
11. [How to Run the Project](#-how-to-run-the-project)
12. [Repository Structure](#-repository-structure)
13. [Skills Demonstrated](#-skills-demonstrated)
14. [About Me](#-about-me)

---

## 📌 Project Overview

Credit card businesses deal with large amounts of financial and customer data. While this data contains valuable information, understanding revenue trends, transaction activity, and customer behaviour can be difficult without a clear reporting system.

This project explores how Power BI can bring these different aspects together in one place. It focuses on financial performance, customer segmentation, and weekly trends, making it easier to identify patterns and investigate changes in business performance.

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

The project aims to answer the following questions:

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
|---|---|
| **Power BI Desktop** | Interactive dashboards and visual reporting |
| **SQL** | Data querying, aggregation, and analysis |
| **Power Query** | Data cleaning and transformation |
| **DAX** | KPI calculations and time-based comparisons |
| **CSV** | Source datasets |
| **GitHub** | Project documentation and version control |

## 📂 Dataset Overview

The project uses four CSV datasets containing credit card and customer information.

| Dataset | Description |
|---|---|
| `credit_card.csv` | Credit card financial and transaction information |
| `cc_add.csv` | Additional credit card records |
| `customer.csv` | Customer demographic and profile information |
| `cust_add.csv` | Additional customer records |

The datasets will be inspected to understand their structure, identify relevant columns, and establish appropriate relationships before analysis.

## 🔍 Data Preparation & Modelling

The analysis follows a structured workflow.

### 1. Data Inspection

Review the source datasets to understand column names, data types, identifiers, and reporting periods.

### 2. Data Cleaning

Use Power Query to check missing values, duplicate records, inconsistent data types, and date-related issues.

### 3. Data Integration

Combine compatible datasets and establish relationships between customer and credit card information using appropriate identifiers.

### 4. Customer Segmentation

Explore customer behaviour through age groups, income groups, and other available demographic attributes.

### 5. DAX Calculations

Create measures for revenue, transaction activity, customer activation, delinquency, and weekly performance comparisons.

### 6. Data Validation

Verify the KPI calculations and check that relationships, filters, and aggregations produce consistent results.

## 📊 Key Performance Indicators

The dashboard is designed to monitor the following metrics, subject to data availability and validation.

| KPI | Business Purpose |
|---|---|
| **Total Revenue** | Track overall financial performance using a defined revenue measure |
| **Total Interest** | Monitor interest earned |
| **Total Transaction Amount** | Measure the value of recorded transactions |
| **Transaction Count** | Track transaction activity |
| **Average Transaction Value** | Understand average transaction size |
| **Customer Activation Rate** | Measure activation among eligible customers |
| **Delinquency Rate** | Monitor the proportion of customers classified as delinquent |
| **Week-over-Week Revenue Growth** | Compare revenue across reporting weeks |

KPI definitions and calculations will be documented and validated against the underlying data. Revenue, transaction amount, interest, and fees will be interpreted according to their respective definitions.

## 📈 Dashboard Overview

The dashboard is organised around two analytical areas.

### Credit Card Financial Performance

This section focuses on:

- Revenue and transaction trends.
- Weekly financial performance.
- Revenue contributions across card categories.
- Transaction amounts and counts.
- Customer activation and delinquency indicators.

### Customer Analysis

This section focuses on:

- Revenue across customer segments.
- Age and income group comparisons.
- Occupation and demographic analysis.
- Customer transaction behaviour.
- Interactive filters for exploring different customer groups.

## 📈 Dashboard Reports

The project includes two dashboard reports covering financial performance and customer analytics.

### 1. Credit Card Transaction Analysis

Explores transaction activity, revenue trends, expenditure categories, and credit card performance.

[View Transaction Dashboard Report](./Credit%20Card%20Financial%20Dashboard-Transaction.pdf)

### 2. Credit Card Customer Analysis

Explores customer revenue, interest, income groups, demographics, and customer job categories.

[View Customer Dashboard Report](./Credit%20Card%20Financial%20Dashboard-Customer.pdf)

The reports are available as PDF documents. An interactive Power BI `.pbix` file is not currently included in this repository.

## 💡 Business Insights

The analysis focuses on understanding what the numbers reveal about credit card performance and customer behaviour.

The final findings will examine:

- Which card categories contribute the most to revenue.
- Which customer segments generate the highest revenue.
- How revenue and transaction activity change over time.
- Whether spending patterns differ across demographic groups.
- What activation and delinquency indicators reveal about customer activity.

Each finding will be supported by verified calculations and relevant dashboard visuals.

## 🚀 Recommendations

The findings will be used to develop practical recommendations in areas such as:

| Focus Area | Potential Business Action |
|---|---|
| Customer Engagement | Explore ways to improve card activation |
| Card Performance | Review revenue and transaction trends across card categories |
| Customer Segmentation | Identify customer groups that may benefit from tailored engagement |
| Financial Performance | Monitor significant changes in revenue and transaction activity |
| Delinquency | Investigate relevant customer risk indicators |

Final recommendations will be based on validated findings from the analysis.

## ▶️ How to Run the Project

Once the relevant files are available in the repository:

1. Clone or download the repository.
2. Review the source CSV datasets and SQL queries.
3. Open the Power BI `.pbix` report in Power BI Desktop.
4. Update the data-source paths and refresh the data if necessary.
5. Explore the dashboard pages, interactive filters, KPIs, and documented findings.

## 📁 Repository Structure

```text
credit-card-revenue-customer-analytics/
│
├── README.md
│
├── data/
│   ├── credit_card.csv
│   ├── cc_add.csv
│   ├── customer.csv
│   └── cust_add.csv
│
├── sql/
│   └── analysis_queries.sql
│
├── dashboard/
│   └── credit_card_dashboard.pbix
│
├── screenshots/
│   ├── financial_dashboard.png
│   └── customer_dashboard.png
│
└── docs/
    └── business_case_study.pdf
```

*The structure above shows the intended organisation of the project. Files and folders will be added as they become available.*

## 🧠 Skills Demonstrated

This project brings together several important areas of data analytics:

- Data cleaning and transformation.
- SQL querying and aggregation.
- Data modelling and table relationships.
- DAX calculations and KPI development.
- Time-based performance analysis.
- Interactive dashboard design.
- Business analysis and data storytelling.

## 👩‍💻 About Me

I'm Anushka, a B.Tech Computer Science Engineering student specialising in Data Science at IILM University, Greater Noida.

I'm interested in data analytics and business intelligence, especially using SQL and Power BI to understand business problems and communicate findings clearly.

This project is part of my effort to build practical analytical skills and present analysis in a way that connects technical work with business decisions.
