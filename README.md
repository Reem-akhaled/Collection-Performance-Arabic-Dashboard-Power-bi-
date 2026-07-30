# Collection Performance Arabic Dashboard - Power BI

An Arabic right-to-left business intelligence solution for monitoring electricity collection performance and receipt issuance across company, sector, and administration levels.

The project was developed in response to an operational need encountered in my current professional role. It replaces fragmented manual and paper-based reporting with a centralized analytical experience that provides faster access to performance results, consistent calculations, and clearer decision support.

> **Portfolio note:** The public version uses anonymized terminology and fully synthetic data. It does not include production data, company-identifying information, credentials, internal server details, the Power BI source file, SQL procedures, or DAX measures.

---

## Project at a Glance

The solution combines data from multiple operational databases, processes it through a SQL Server data warehouse, and presents it in Power BI through an Arabic right-to-left interface.

It supports:

- company-level performance monitoring
- sector comparison and ranking
- administration-level operational analysis
- daily, monthly, and financial-year trends
- daily target monitoring and gap analysis
- best- and weakest-month identification
- previous-period and year-over-year comparisons
- contribution and ranking analysis
- contextual Arabic analysis for users who prefer guided interpretation
- custom tooltips that provide additional detail without overcrowding the main pages

---

## Business Problem

The original reporting process relied on manual follow-up, paper-based summaries, and repeated calculations. This created several challenges:

- delayed visibility into collection performance
- repeated preparation of the same operational reports
- inconsistent comparison between sectors and administrations
- limited access to daily and financial-year trends
- dependence on specialist users to interpret charts and tables
- fragmented reporting across organizational levels

The dashboard centralizes the information, standardizes the calculations, and presents the results in an interactive format that supports operational follow-up and management discussions.

---

## Solution Architecture

The project follows a layered business intelligence architecture:

1. **Source data collection**  
   Operational records are collected from external databases through SQL stored procedures.

2. **Staging layer**  
   Extracted records are stored locally before warehouse processing.

3. **Incremental warehouse loading**  
   A control table stores process checkpoints so only new or changed records are processed.

4. **Fact and dimension processing**  
   The warehouse procedure calculates issuance, monthly collection, remaining balances, collection ratios, bill counts, latest monthly snapshots, active daily snapshots, and collection-cycle information.

5. **Power BI semantic model**  
   Separate date, collection-month, sector, administration, and cycle dimensions support daily and financial-year analysis.

6. **Reporting and analysis layer**  
   DAX measures drive KPIs, comparisons, rankings, targets, trend analysis, dynamic titles, tooltips, and Arabic analytical narratives.

---

## Data Model

![Power BI data model](screenshots/30-data-model.jpg)

The model is centered on `FactCollection` and uses supporting dimensions for dates, collection months, sectors, administrations, and administration collection cycles.

### Main fact data

`FactCollection` includes:

- balance before issuance
- issuance
- total amount
- monthly collection
- remaining balance
- collection ratio
- paid and unpaid values
- paid and unpaid bill counts
- latest monthly snapshot flag
- active daily snapshot flag

### Supporting tables

- `DimDate`
- `DimCollectionMonth`
- `DimSector`
- `DimEngineering`
- `DimEngineeringCollectionCycle`
- `SectorEngineerHierarchy`
- `SyncControl`

The financial year begins in July and supports the periods 2024/2025, 2025/2026, and 2026/2027 in the synthetic portfolio dataset.

---

## Report Navigation

![Landing page](screenshots/01-cover.jpg)

The landing page provides direct access to five connected report experiences:

1. Company Performance
2. Sector Performance
3. Administration Performance
4. Time-Trend Analysis
5. Detailed Collection Data

The company, sector, and administration experiences also provide access to contextual analysis pages that expand the selected view with comparisons, written interpretation, target analysis, contribution analysis, and performance summaries.

---

## 1. Company Performance

![Company performance](screenshots/02-company-overview.jpg)

The company page provides an executive view of the selected reporting date.

### Main information

- total issuance
- monthly collection
- remaining balance
- collection ratio
- daily target
- actual daily collection
- daily surplus or deficit
- highest and lowest sectors
- highest and lowest administrations

### Interactive controls

- daily or monthly trend
- all months, best months, or weakest months
- metric selection
- date and financial-year context
- access to company analysis pages

### Metric-driven visual behavior

The metric selector changes both the calculation and the visual form:

- **Issuance**, **monthly collection**, and **remaining balance** show each sector's share of the company total in a donut chart.
- **Collection ratio** changes the left visual to a column-based gap analysis showing the difference between the collection ratio target and the actual collection ratio for each sector.
- **Daily target** changes the left visual to a column-based gap analysis showing the difference between actual daily collection and the calculated target for each sector.

### Tooltip behavior

- The main trend chart uses the daily or monthly comparison tooltip.
- The contribution donut uses the sector relative performance tooltip.
- The month-performance area uses the month-performance tooltip.

---

## 2. Sector Performance

![Sector performance](screenshots/03-sector-overview.jpg)

The sector page evaluates one selected sector and the administrations within it.

### Main information

- sector issuance, collection, remaining balance, and collection ratio
- sector ranking across the company
- highest and lowest administration in the sector
- sector daily target and actual collection
- administration target values and daily gaps
- administration ranking within the selected sector

### Interactive controls

- sector selection
- daily or monthly trend
- all months, best months, or weakest months
- metric selection
- access to sector analysis pages

### Metric-driven visual behavior

- **Issuance**, **monthly collection**, and **remaining balance** show administration contribution within the selected sector.
- **Collection ratio** changes the left visual to a column-based gap analysis showing the difference between the collection ratio target and the actual collection ratio for each administration in the sector.
- **Daily target** compares each administration's actual daily collection with its calculated target and displays the surplus or deficit.

### Tooltip behavior

- The trend chart uses the daily or monthly comparison tooltip.
- The contribution donut uses the administration relative performance tooltip.
- The month-performance area uses the month-performance tooltip.

---

## 3. Administration Performance

![Administration performance](screenshots/04-administration-overview.jpg)

The administration page provides the most detailed operational view in the report.

### Main information

- administration and parent-sector context
- issuance, monthly collection, remaining balance, and collection ratio
- paid and unpaid bill counts and values
- daily target, actual daily collection, and daily gap
- ranking within the sector and across the company
- contribution to sector and company totals
- monthly history and period comparisons

### Interactive controls

- administration selection
- daily or monthly trend
- all months, best months, or weakest months
- sector or company benchmark
- previous month or peer-period comparison
- current and reference-period values
- access to administration analysis pages

### Tooltip behavior

- The trend chart uses daily or monthly comparison tooltips.
- The month-performance area uses the month-performance tooltip.

---

## 4. Time-Trend Analysis

### Daily trend

![Daily trend](screenshots/05-daily-trends.jpg)

### Monthly trend

![Monthly trend](screenshots/06-monthly-trends.jpg)

### Financial-year trend

![Financial-year trend](screenshots/07-yearly-trends.jpg)

The trend experience supports:

- daily, monthly, and financial-year perspectives
- financial-year and month filtering
- company, sector, or administration scope
- comparison across multiple financial years
- reset to the full organizational scope

The three trend perspectives use dedicated daily, monthly, and financial-year tooltips so the reference values and comparison logic match the active time level.

---

## 5. Detailed Collection Data

![Detailed collection data](screenshots/08-detailed-data.jpg)

The detailed-data page provides an operational table grouped by sector and administration.

It includes:

- balance before issuance
- issuance
- total amount
- monthly collection
- collection ratio
- remaining balance
- sector totals and administration-level details

The page supports detailed review and reconciliation while remaining connected to the same date and organizational filters used throughout the report.

---

## Contextual Analysis Experiences

The company, sector, and administration pages are supported by contextual analysis experiences. They preserve the selected date and organizational context while extending the main report with comparison tables, written interpretation, target results, ranking, contribution, and month-performance analysis.

These pages are particularly useful for users who prefer a guided explanation rather than interpreting charts and tables independently.

### Company analysis

- operational performance comparison
- daily target achievement across sectors
- best and weakest financial-year months
- sector performance summary
- sector contribution analysis

![Company operational comparison](screenshots/09-company-insight-overview.jpg)
![Company daily target analysis](screenshots/10-company-daily-target-insight.jpg)
![Company month performance](screenshots/11-company-month-performance-insight.jpg)
![Company sector performance](screenshots/12-company-sector-performance-insight.jpg)
![Company sector contribution](screenshots/13-company-sector-contribution-insight.jpg)

### Sector analysis

- sector operational comparison
- administration achievement against daily targets
- best and weakest months for the selected sector
- administration performance summary
- administration contribution within the selected sector

![Sector operational comparison](screenshots/14-sector-comparison-insight.jpg)
![Sector daily target analysis](screenshots/15-sector-daily-target-insight.jpg)
![Sector month performance](screenshots/16-sector-month-performance-insight.jpg)
![Sector administration performance](screenshots/17-sector-administration-performance-insight.jpg)
![Sector administration contribution](screenshots/18-sector-administration-contribution-insight.jpg)

### Administration analysis

- current performance compared with previous and peer periods
- contribution to sector and company totals
- daily target context and monthly performance

![Administration comparison](screenshots/19-administration-comparison-insight.jpg)
![Administration contribution](screenshots/20-administration-contribution-insight.jpg)
![Administration month performance](screenshots/21-administration-month-performance-insight.jpg)

---

## Narrative Analysis Framework

The report includes an Arabic interpretation layer that adapts to the current page and active selection. It does not repeat a fixed set of KPIs; the content changes according to the analytical context.

Depending on the page, it can explain:

- current operational results
- previous-period and year-over-year comparisons
- target achievement
- distribution of performance between sectors or administrations
- best and weakest months
- contribution and ranking
- concentration, balance, improvement, decline, or mixed performance

The narrative follows three complementary purposes:

- **Performance reading** - translates the displayed KPIs, table, or comparison into clear business language.
- **Interpretation** - explains the meaning of the observed pattern.
- **Priorities** - highlights areas requiring attention and provides concise recommendations based on the active results.

The supporting values remain visible beside the narrative so users can verify the written analysis against the underlying figures.

---

## Contextual Tooltips

The report uses custom report-page tooltips to provide additional analytical context without overcrowding the main layouts.

Depending on the visual, tooltips may show:

- current values
- previous-month values
- peer-period or previous-year values
- absolute and percentage changes
- sector or administration context
- ranking and contribution details
- daily, monthly, or financial-year comparison logic

![Daily comparison tooltip](screenshots/22-tooltip-daily-comparison.jpg)

![Monthly comparison tooltip](screenshots/23-tooltip-monthly-comparison.jpg)

![Sector performance tooltip](screenshots/24-tooltip-sector-performance.jpg)

![Administration performance tooltip](screenshots/25-tooltip-administration-performance.jpg)

![Ranking tooltip](screenshots/26-tooltip-ranking.jpg)

![Daily metric tooltip](screenshots/27-tooltip-daily-metric.jpg)

![Monthly metric tooltip](screenshots/28-tooltip-monthly-metric.jpg)

![Financial-year metric tooltip](screenshots/29-tooltip-yearly-metric.jpg)

---

## Key Analytical Capabilities

### Daily target analysis

The report compares actual daily collection with the calculated daily target at company, sector, and administration levels. It identifies entities that achieved the target, entities below target, and the resulting surplus or deficit.

### Best and weakest months

Users can review all months or isolate the strongest and weakest months to identify recurring patterns and seasonal performance differences.

### Ranking and contribution

The report calculates sector and administration rankings, contribution to issuance and collection, remaining-balance share, and the gap against the target collection ratio.

### Comparative analysis

Current results can be compared with the previous month, the corresponding period in the previous year, a peer month, or financial-year performance.

---

## Business Impact

The solution was designed to improve operational visibility and reduce dependence on manually prepared reports.

Expected benefits include:

- faster access to daily performance
- consistent calculations across organizational levels
- reduced manual report preparation
- clearer identification of underperforming sectors and administrations
- easier comparison across months and financial years
- improved accessibility through Arabic analysis and contextual tooltips
- better support for follow-up and management discussions

---

## Technologies and Skills

- Microsoft Power BI
- DAX
- Power Query
- Microsoft SQL Server
- T-SQL and stored procedures
- incremental warehouse loading
- dimensional data modeling
- Arabic right-to-left report design
- GitHub portfolio documentation

---

## Design Approach

The report uses a consistent Arabic right-to-left visual system with:

- Arabic labels and analytical narratives
- dark teal and off-white color palette
- consistent navigation and page hierarchy
- dynamic titles and selected-context labels
- conditional performance indicators
- focused use of color for positive and negative results

Primary colors:

- `#283E45`
- `#FEFBF4`

---

## Repository Scope and Confidentiality

This repository presents the project as a professional case study.

The following are not publicly distributed:

- Power BI source file
- SQL scripts and stored procedures
- DAX measures
- source and production data
- credentials and internal server details
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

A complete project case study is available here:

[Download the detailed project case study](docs/Collection-Performance-Case-Study.pdf)

The case study covers the business context, data acquisition, warehouse workflow, semantic model, report navigation, page-level interactions, tooltip mapping, contextual analysis, and business impact.

---

## Disclaimer

This repository is a portfolio representation of a professional business intelligence project. All data shown is synthetic and all organizational references have been anonymized.
