# CloudFlow – SaaS Business Performance & Customer Intelligence Dashboard

An interactive **Power BI analytics project** designed to analyze SaaS business performance across subscription revenue, billing, customer acquisition, product usage, customer churn, retention, and cohort behavior.

CloudFlow transforms six Parquet datasets into a structured analytical model and a seven-page Power BI report, helping stakeholders explore business performance through interactive dashboards and data-driven metrics.

---

## Dashboard Preview



## Project Overview

CloudFlow represents a fictional subscription-based Software-as-a-Service (SaaS) business. The project focuses on understanding how the business acquires customers, generates recurring revenue, manages invoices, collects payments, and retains paying organizations.

The dashboard provides different analytical perspectives for business stakeholders, including executives, finance teams, revenue operations, product teams, and customer success teams.

**Key areas of analysis:**

- Customer acquisition and organizational growth
- Invoice generation and payment collection
- Subscription performance and product usage
- Monthly and annual recurring revenue
- Customer churn and retention
- Customer lifetime and paid cohort analysis

## Business Objectives

- Monitor overall SaaS business performance.
- Understand revenue generation and payment collection patterns.
- Track active subscriptions and paying organizations.
- Analyze recurring revenue movements over time.
- Identify customer churn patterns across plans and industries.
- Measure customer retention and subscription tenure.
- Understand long-term customer behavior through cohort analysis.

## Data Sources

The project uses six Parquet datasets:

| Dataset       | Description                                                  | Records |
| ------------- | ------------------------------------------------------------ | ------: |
| Plans         | Product plans, pricing, billing intervals and tiers          |       8 |
| Organizations | Customer organizations and business attributes               |   3,000 |
| Users         | Users associated with organizations                          |  26,000 |
| Subscriptions | Subscription lifecycle, plan, seats and cancellation details |   4,200 |
| Invoices      | Invoice amounts, statuses, issue dates and payment dates     |  46,000 |
| Usage Events  | Product activity and usage event records                     | 180,000 |

**Total:** 259,208 records across six source datasets.

The data was imported into Power BI from Parquet files and prepared using Power Query.

## Tools & Technologies

- **Power BI Desktop** – Dashboard development and data visualization
- **Power Query (M)** – Data preparation and transformation
- **DAX** – Measures, calculated columns and analytical calculations
- **Parquet** – Source data format
- **Power BI Data Modeling** – Relationships, dimensions, fact tables and helper tables

## Data Model

The project uses a star-like analytical model with separate fact and dimension tables.

**Dimension tables**

- `Dim_plans`
- `Dim_organizations`
- `Dim_users`
- `Dim_Date_table`

**Fact tables**

- `Fact_subscriptions`
- `Fact_invoices`
- `Fact_usage_events`

**Supporting objects**

- `_Measures (2)` – Central measure table containing 62 DAX measures
- `Waterfall Category` – Disconnected table supporting MRR movement analysis
- `Cohort Month Offset` – Disconnected table supporting cohort retention analysis

The model uses many-to-one, single-direction relationships, multiple date roles, and inactive relationships where different business dates need separate analytical treatment.

## Dashboard Pages

The report contains seven pages, each designed to answer a different business question.

### 1. Executive Overview

Provides a high-level view of the business, focusing on customer growth, active organizations, invoiced revenue, and payment collection.

**Key metrics and visuals:**

- New Organizations
- Active Organizations
- Net Invoiced Revenue
- Payment Collection Rate
- Billing versus cash collection trends
- New organizations by acquisition channel
- Revenue by plan



### 2. Revenue & Billing

Analyzes invoice performance, outstanding balances, and payment collection.

**Key metrics and visuals:**

- Net Invoiced Revenue
- Cash Collected by Payment Date
- Unpaid Amount
- Total Invoices
- Monthly billing trends
- Invoice volume by status
- Invoice summary by plan and status



### 3. Customers & Growth

Focuses on customer acquisition, organizational growth, user registrations, and customer distribution.

**Key metrics and visuals:**

- New Organizations
- Active Organizations
- New User Registrations
- Cancelled Subscriptions
- Organization sign-up trends
- Acquisition channel analysis
- Active organizations by industry
- Organization details table



### 4. Product & Plans

Provides insights into subscription distribution, seat allocation, and product activity.

**Key metrics and visuals:**

- Total Subscriptions
- Total Seats
- Active Subscriptions
- Active Users
- Subscriptions by plan
- Seats by plan
- Product usage event trends



### 5. Revenue & Churn

Analyzes recurring revenue performance and the movement of subscription revenue over time.

**Key metrics:**

- Monthly Recurring Revenue (MRR)
- Annual Recurring Revenue (ARR)
- Active Paying Organizations
- Average Revenue per Account (ARPA)
- MRR Growth %
- Net New MRR

**Key visuals:**

- Monthly closing MRR trend
- MRR movement waterfall
- Monthly New MRR, Reactivation MRR and Churned MRR
- MRR contribution by plan



### 6. Customer Churn

Provides a deeper understanding of paid customer losses, retention, customer tenure, and cohort behavior.

**Key metrics:**

- Churned Organizations
- Customer Churn Rate
- Customer Retention Rate
- Opening Paying Organizations

**Key visuals:**

- Monthly customer churn trend
- Churn by opening plan
- Customer cohort retention heatmap
- Customer tenure analysis

The page includes date and industry slicers for interactive analysis.



### 7. Organization Detail

A drill-through page that provides a more detailed view of an individual organization.

**Analysis includes:**

- Organization attributes
- Seats and active users
- Product usage activity
- Net invoiced revenue
- Monthly usage trends
- Monthly invoice revenue
- Invoice-level details
- Subscription-level details

This page allows users to navigate from organization-level analysis into an individual customer's performance.



---

## Key Business Metrics & DAX Analysis

A total of **62 DAX measures** were implemented and organized into analytical categories.

### 1. Revenue Metrics

| Metric           | Definition                                                                                   |
| ---------------- | -------------------------------------------------------------------------------------------- |
| MRR              | Monthly-equivalent recurring value of subscriptions active at a selected snapshot date       |
| ARR              | MRR multiplied by 12; represents an annualized run-rate                                      |
| ARPA             | MRR divided by active paying organizations                                                   |
| New MRR          | Recurring revenue from an organization's first observed valid paid subscription              |
| Reactivation MRR | Recurring revenue from a paid subscription that starts after previous paid service has ended |
| Churned MRR      | Recurring revenue lost when an organization has no other active paid subscription            |
| Net New MRR      | New MRR + Reactivation MRR − Churned MRR                                                     |
| MRR Growth %     | Percentage change between opening and closing MRR snapshots                                  |
| MRR Share %      | Contribution of a plan or organization segment to selected MRR                               |

### 2. Customer Metrics

| Metric                       | Definition                                                          |
| ---------------------------- | ------------------------------------------------------------------- |
| Active Organizations         | Organizations with at least one active subscription, including Free |
| Active Paying Organizations  | Organizations with at least one active paid subscription            |
| Opening Paying Organizations | Paying organizations active immediately before the selected period  |
| Closing Paying Organizations | Paying organizations active at the selected period-end snapshot     |
| Churned Organizations        | Opening-base organizations that experience a valid paid churn event |
| Customer Churn Rate          | Churned organizations divided by opening paying organizations       |
| Customer Retention Rate      | Opening organizations still paying at the closing snapshot          |

### 3. Billing & Usage Metrics

- Total Invoiced Revenue
- Net Invoiced Revenue
- Cash Collected by Payment Date
- Unpaid Amount
- Open Invoice Amount
- Failed Invoice Amount
- Refunded Invoice Amount
- Payment Collection Rate
- Average Invoice Value
- Average Invoice Value (Paid Plans)
- Total Usage Events
- Active Users
- Engaged Organizations
- Average Events per Active User

### 4. Customer Lifetime & Cohort Metrics

- Average Completed Tenure
- Average Ongoing Tenure
- First Observed Paid Cohort Month
- Cohort Customer Count
- Monthly Retained Customers
- Cohort Retention %

Cohort retention measures whether organizations maintain an active paid subscription at monthly snapshots. It does not represent product usage or login activity.

## Key Business Insights & Validation

The following are verified results from the model's validation queries, rather than assumptions about business performance.

### FY2025 Recurring Revenue

| Metric                    |    Value |
| ------------------------- | -------: |
| Opening MRR               | $422,342 |
| New MRR                   | $604,629 |
| Reactivation MRR          | $375,871 |
| Churned MRR               | $905,281 |
| Closing MRR               | $791,079 |
| Reconciliation Difference |       $0 |

The recurring revenue movement reconciles as:

`Opening MRR + New MRR + Reactivation MRR − Churned MRR = Closing MRR`

Expansion and contraction MRR are not included because historical plan and seat-change snapshots are unavailable.

### FY2025 Customer Analysis

| Metric                       |  Value |
| ---------------------------- | -----: |
| Opening Paying Organizations |    875 |
| Closing Paying Organizations |  1,621 |
| Churned Organizations        |    333 |
| Customer Churn Rate          | 38.06% |
| Customer Retention Rate      | 68.80% |

The churn rate measures losses from the opening customer base, while retention measures how much of that opening base remains active at the closing snapshot. Customers who leave and reactivate before the closing snapshot can count as retained.

## Data Quality, Assumptions & Limitations

The project includes explicit checks for subscription lifecycle consistency and reporting-period boundaries.

- **Reporting horizon:** 31 December 2025, based on the latest recorded operational activity.
- **Future subscription records:** 181 subscription starts after the reporting horizon are excluded from horizon-based reporting.
- **Invalid lifecycle records:** 23 subscriptions with end dates earlier than their start dates are excluded from valid lifecycle and churn calculations.
- **Suspicious December dates:** 33 lifecycle-valid subscriptions end on 30 December 2025. These are retained in observed churn but trigger a low-confidence warning. Of these, 28 are paid subscriptions contributing $12,947 in MRR.
- **Reactivation:** No arbitrary grace-period threshold is applied.
- **Customer cohorts:** Cohorts represent the first observed valid paid subscription month within the available data, not necessarily the customer's lifetime-first paid month.
- **Customer tenure:** Measures elapsed calendar time and includes reactivation gaps.
- **Revenue movements:** Expansion and contraction are not measured due to the absence of historical plan and seat-change snapshots.

These limitations are documented so that dashboard results can be interpreted responsibly.

## Project Structure

```text
CloudFlow-SaaS-Business-Analytics/
│
├── README.md
│
├── CloudFlow.pbix
│
│
└── Screenshots/
    ├── 01-Executive-Overview.png
    ├── 02-Revenue-and-Billing.png
    ├── 03-Customers-and-Growth.png
    ├── 04-Product-and-Plans.png
    ├── 05-Revenue-and-Churn.png
    ├── 06-Customer-Churn.png
```

The source Parquet datasets are not included in this repository.

## How to Explore the Project

1. Clone or download this repository.
2. Open `CloudFlow.pbix` using Power BI Desktop.
3. Explore the report pages using the navigation panel.
4. Use available date, plan, and industry slicers to filter the analysis.
5. Explore the Organization Detail page through drill-through from an organization.

**Note:** The original Power Query source paths point to a local dataset folder. To refresh the report on another machine, update the source paths to the corresponding Parquet files and configure the required data sources.

## Future Enhancements

Potential improvements include:

- Adding historical plan and seat snapshots to analyze expansion and contraction MRR.
- Investigating suspicious subscription lifecycle dates at source.
- Extending the available historical data for more complete cohort analysis.
- Documenting and validating the refresh process on another machine.
- Performing broader user acceptance and interaction testing.

## Project Information

**Project:** CloudFlow – SaaS Business Performance & Customer Intelligence Dashboard
**Category:** Business Intelligence | Data Analytics | SaaS Analytics
**Platform:** Microsoft Power BI
**Data Format:** Parquet
**Report Pages:** 6
**DAX Measures:** 62

---

*This project was developed as a portfolio project to demonstrate practical skills in data modeling, Power Query, DAX, business intelligence, and analytical storytelling using Power BI.*
