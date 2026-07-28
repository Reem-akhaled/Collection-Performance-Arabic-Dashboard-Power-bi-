# Collection Performance Arabic Power BI Dashboard

An end-to-end business intelligence project for monitoring issuance, collection performance, remaining balances, collection ratios, daily targets, sectors, and administrations.

The project combines:

- Microsoft Power BI
- SQL Server
- DAX
- Data modeling
- ETL and warehouse loading
- Arabic dashboard design
- Dynamic narrative reporting

> All data included in this repository is synthetic and was created for demonstration and portfolio purposes.

---

## Dashboard Preview

![Company Overview](screenshots/02-company-overview.png)

---

## Project Overview

This dashboard provides a comprehensive view of financial collection performance at three organizational levels:

1. Company
2. Sector
3. Administration

It supports daily, monthly, yearly, and financial-year analysis while allowing users to move between high-level executive KPIs and detailed administration-level records.

The financial year begins in July.

---

## Main KPIs

The dashboard tracks:

- Issuance
- Monthly collection
- Remaining balance
- Collection ratio
- Daily collection
- Daily target
- Daily target gap
- Paid bill count
- Unpaid bill count
- Sector ranking
- Administration ranking
- Contribution to company and sector totals

---

## Dashboard Pages

### 1. Landing Page

A modern Arabic landing page that provides navigation to:

- Company performance
- Sector performance
- Administration performance
- Time trends
- Detailed collection data

### 2. Company Overview

Displays company-level KPIs including:

- Total issuance
- Monthly collection
- Remaining amount
- Collection ratio
- Daily target
- Actual daily collection
- Daily surplus or deficit
- Highest and lowest performing sectors and administrations

### 3. Sector Performance

Provides sector-level analysis including:

- Sector ranking
- Monthly collection ratio
- Strongest and weakest administrations
- Administration daily targets
- Daily target gaps
- Monthly trends

### 4. Administration Performance

Displays detailed performance for a selected administration including:

- Issuance
- Collection
- Remaining balance
- Collection ratio
- Paid and unpaid bill counts
- Ranking within sector and company
- Contribution to sector and company totals
- Monthly and yearly comparisons

### 5. Time Trend Analysis

Supports three analysis modes:

- Daily trends
- Monthly trends
- Financial-year trends

The user can analyze issuance and collection performance across multiple periods.

### 6. Detailed Collection Table

Provides administration-level financial records grouped by sector, including:

- Balance before issuance
- Issuance
- Total amount
- Monthly collection
- Collection ratio
- Remaining balance

### 7. Comparison and Narrative Analysis

The dashboard includes dynamically generated Arabic narratives covering:

- Current performance
- Previous-month comparison
- Previous-year comparison
- Sector performance
- Administration performance
- Daily target achievement
- Contribution analysis
- Best and weakest months

---

## Daily Target Logic

Daily collection is calculated as the difference between the current cumulative collection and the previous calendar day's cumulative collection.

The daily target is calculated using the remaining amount and the remaining calendar days in the selected month.

```DAX
Daily Collection =
Current Month Collection - Previous Day Month Collection
