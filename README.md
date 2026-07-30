# Collection Performance Arabic Dashboard — Power BI

An end-to-end Arabic business intelligence solution for monitoring electricity collection performance, receipt issuance, remaining balances, collection ratios, daily targets, operational trends, and performance rankings across company, sector, and administration levels.

This project was developed in response to a real operational need encountered in my current professional role. The objective was to replace fragmented manual and paper-based reporting with a centralized analytical experience that presents the same information in a clearer, faster, and more decision-oriented format.

The public portfolio version uses anonymized terminology and fully synthetic data. No production data, internal server details, credentials, customer information, or proprietary implementation code are included.

---

## Project Overview

The solution brings together data from multiple operational sources, transforms it through a SQL Server data warehouse, and presents it in Power BI through an Arabic right-to-left interface.

It supports:

- company-level performance monitoring
- sector-level comparison and ranking
- administration-level drill-down
- daily, monthly, and financial-year trend analysis
- daily target monitoring
- identification of highest and lowest performers
- current-period, previous-period, and year-over-year comparisons
- contextual Arabic narrative analysis for non-technical users

---

## Business Problem

The original process depended on manual follow-up, paper-based reporting, and repeated preparation of operational summaries. This created several challenges:

- delayed visibility into collection performance
- repeated manual calculations
- difficulty comparing sectors and administrations consistently
- limited access to daily trends and financial-year analysis
- dependence on specialist users to interpret tables and charts
- fragmented reporting across multiple organizational levels

The dashboard addresses these challenges by centralizing the data, standardizing the calculations, and presenting the results in an interactive and readable format.

---

## Solution Architecture

The project follows a layered business intelligence architecture:

1. **Source Data Collection**  
   Operational data is collected from external databases through SQL stored procedures.

2. **Staging Layer**  
   Extracted records are stored in a staging table before warehouse processing.

3. **Warehouse Processing**  
   A dedicated loading procedure calculates issuance, collection, remaining balances, collection ratios, active snapshots, latest monthly records, and collection-cycle information.

4. **Semantic Model**  
   Power BI uses a dimensional model with separate date, collection-month, sector, administration, and cycle tables.

5. **Reporting Layer**  
   DAX measures drive KPIs, comparisons, rankings, targets, trend analysis, and Arabic narrative outputs.

---

## Data Model

The model is centered around a single fact table and supporting dimensions.

### Fact table

`FactCollection`

Main analytical fields include:

- issuance
- monthly collection
- remaining amount
- collection ratio
- balance before issuance
- paid and unpaid bill values
- paid and unpaid bill counts
- latest monthly snapshot flag
- active daily snapshot flag

### Dimensions

- `DimDate`
- `DimCollectionMonth`
- `DimSector`
- `DimEngineering`
- `DimEngineeringCollectionCycle`
- `SectorEngineerHierarchy`

### Control table

- `SyncControl`

The financial year starts in July, allowing the report to analyse the periods:

- 2024/2025
- 2025/2026
- 2026/2027

---

## Core Report Experiences

The landing page provides direct access to five core areas of the solution.

### 1. Company Performance

The company view provides an executive summary of overall performance, including:

- total issuance
- monthly collection
- remaining balance
- collection ratio
- daily target
- actual daily collection
- daily surplus or deficit
- highest and lowest performing sectors
- highest and lowest performing administrations
- daily and monthly trend switching
- KPI switching between issuance, collection, remaining balance, collection ratio, and daily target
- sector contribution analysis
- in-page controls for metric, time perspective, and month-performance selection

![Company Performance](screenshots/company-overview.png)

---

### 2. Sector Performance

The sector view enables focused analysis of a selected sector and its administrations.

It includes:

- sector-level issuance, collection, remaining balance, and collection ratio
- sector ranking across the company
- highest and lowest performing administration within the sector
- daily target and daily actual collection
- administration-level target comparison
- administration ranking within the selected sector
- daily and monthly trend switching
- KPI switching between issuance, collection, remaining balance, collection ratio, and daily target
- in-page controls for sector selection, time perspective, and month-performance selection

![Sector Performance](screenshots/sector-overview.png)

---

### 3. Administration Performance

The administration view provides the most detailed operational analysis in the report.

It includes:

- administration selection
- parent-sector context
- issuance, collection, remaining balance, and collection ratio
- paid and unpaid bill counts and values
- daily target, actual collection, and daily gap
- ranking within the sector and across the company
- contribution to sector totals
- contribution to company totals
- monthly trend analysis
- best, weakest, or all-month views
- previous-month and peer-period comparison
- current-period versus prior-period values
- sector-level versus company-level positioning
- in-page controls for trend type, month-performance view, comparison reference, and organizational benchmark

![Administration Performance](screenshots/administration-overview.png)

---

### 4. Time Trend Analysis

The trend analysis area provides three distinct time perspectives:

- daily trend
- monthly trend
- financial-year trend

Users can analyse issuance and collection behaviour across the full organization or within a selected sector or administration.

The trend experience supports:

- financial-year filtering
- month filtering
- daily date analysis
- sector and administration filtering
- comparison across multiple financial years
- organizational scope selection and reset controls

![Daily Trend](screenshots/daily-trend.png)

![Monthly Trend](screenshots/monthly-trend.png)

![Financial Year Trend](screenshots/yearly-trend.png)

---

### 5. Detailed Collection Data

The detailed-data view provides a structured operational table grouped by sector and administration.

It includes:

- balance before issuance
- issuance
- total amount
- monthly collection
- collection ratio
- remaining balance

This page supports detailed review and reconciliation while remaining connected to the same organizational filters used throughout the report.

![Detailed Data](screenshots/detailed-data.png)

---

## Contextual Insight Pages

Each performance view is supported by a dedicated set of contextual insight pages. They are accessed from the related company, sector, or administration page and extend the current analysis with written interpretation, comparison, and decision support.

They are especially useful for users who prefer a guided explanation rather than interpreting charts and tables independently.

### Company insights

The company view is supported by analysis pages covering:

- operational performance comparison
- daily target achievement across sectors
- best and weakest financial-year months
- sector performance summary
- sector contribution analysis

### Sector insights

The sector view is supported by analysis pages covering:

- sector operational comparison
- administration achievement against daily targets
- best and weakest months for the selected sector
- administration performance summary
- administration contribution within the selected sector

### Administration insights

The administration view is supported by analysis pages covering:

- current performance compared with the previous month and peer period
- contribution to sector and company totals
- daily target performance
- monthly performance ranking

---

## Narrative Analysis Framework

The report includes a narrative interpretation layer that adapts to the context of the current page and selection. Rather than repeating a fixed set of measures, it converts the active analysis into a structured written explanation.

Depending on the page and selected view, the narrative may summarize current operational results, compare performance across periods, explain the distribution of results between sectors or administrations, highlight best and weakest months, describe target achievement, or evaluate contribution and ranking.

The narrative experience is organized into three complementary purposes:

- **Performance reading** — translates the currently displayed table, KPIs, or comparison into clear business language.
- **Interpretation** — explains what the observed pattern means, such as improvement, decline, consistency, concentration, imbalance, or mixed performance.
- **Priorities** — highlights the areas that require attention and provides concise recommendations derived from the active results.

This approach helps users who are less comfortable interpreting charts and tables understand the current situation without leaving the analytical context of the page.

---

## Key Analytical Capabilities

### Daily Target Analysis

The dashboard compares actual daily collection with the calculated daily target at company, sector, and administration levels.

It identifies:

- entities that achieved the target
- entities that remained below target
- daily surplus or deficit
- counts and names of successful and underperforming sectors or administrations

### Best and Weakest Months

Users can switch between:

- all available months
- strongest months
- weakest months

This helps identify seasonal patterns and recurring performance issues.

### Ranking and Contribution

The report calculates:

- sector ranking across the company
- administration ranking within the sector
- administration ranking across the company
- issuance contribution
- collection contribution
- remaining-balance contribution
- gap against the target collection ratio

### Comparative Analysis

The dashboard supports comparison with:

- previous month
- same period in the previous year
- peer month
- financial-year performance

### Interactive View Switching

The report uses in-page controls to let users change the analytical perspective without moving to another page. These controls are applied across the company, sector, administration, and trend experiences according to the purpose of each page.

Examples include:

- switching between daily and monthly views
- showing all months, best-performing months, or weakest-performing months
- comparing performance at sector or company level
- changing the reference period between previous month and peer period
- filtering by financial year, month, sector, or administration
- resetting the current selection to the full organizational scope

Metric selectors also change both the measure and the visual treatment. In the company view:

- **Issuance**, **monthly collection**, and **remaining balance** are presented as contribution shares, using a donut chart to show how each sector contributes to the company total.
- **Collection ratio** is presented as a comparative ranking across sectors, making it easier to identify the strongest and weakest performers.
- **Daily target** is presented as a column-based gap analysis, showing the difference between actual daily collection and the calculated target for each sector.

The sector page follows the same principle at administration level: the selected metric changes the visual so that users see either contribution, ranking, or target-gap performance in the form best suited to that measure.

---

## Business Impact

The solution was designed to improve operational visibility and reduce dependence on manual reporting.

Expected benefits include:

- faster access to daily performance
- consistent calculations across organizational levels
- reduced manual preparation of reports
- clearer identification of underperforming sectors and administrations
- easier comparison across months and financial years
- improved accessibility for non-technical users through Arabic narrative analysis
- better support for follow-up and management discussions

---

## Technologies Used

- Microsoft Power BI
- DAX
- Power Query
- Microsoft SQL Server
- T-SQL
- Stored procedures
- Dimensional data modeling
- ETL and warehouse loading
- GitHub for portfolio documentation

---

## Design Approach

The report was designed for Arabic right-to-left usage with a consistent visual identity.

Key design characteristics include:

- Arabic labels and narratives
- right-to-left composition
- dark teal and off-white color palette
- consistent navigation across pages
- dynamic titles
- conditional KPI indicators
- clear hierarchy between company, sector, and administration levels
- focused use of color for positive and negative performance

Primary colors:

- `#283E45`
- `#FEFBF4`

---

## Portfolio Scope and Confidentiality

This repository presents the project as a professional case study.

The following are intentionally excluded from the public repository:

- Power BI source file
- SQL scripts and stored procedures
- DAX measures
- source data
- credentials
- internal server details
- production database names
- company-identifying information

All screenshots use synthetic demonstration data created specifically for portfolio presentation.

---

## Repository Contents

```text
README.md
screenshots/
docs/Collection-Performance-Case-Study.pdf
LICENSE
```

---

## Detailed Case Study

A full project case study is available here:

[Download the detailed project case study](docs/Collection-Performance-Case-Study.pdf)

The case study covers:

- business context
- source-data collection
- warehouse design
- data model
- loading workflow
- report navigation
- page-by-page explanation
- switching options
- narrative analysis
- performance logic
- business impact

---

## Disclaimer

This repository is a portfolio representation of a professional business intelligence project. All data shown is synthetic and all organizational references have been anonymized.
