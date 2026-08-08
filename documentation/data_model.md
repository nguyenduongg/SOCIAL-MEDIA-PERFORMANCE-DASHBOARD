# Data Model

## Overview

The Power BI report uses a dimensional data model to separate
post-performance data from descriptive dimensions such as date,
platform, region, content, and hashtag.

The model contains the following tables:

- `Fact_PostPerformance`
- `Dim_Date`
- `Dim_Platform`
- `Dim_Region`
- `Dim_Content`
- `Dim_Hashtag`
- `Measures_Table`
- `MissingDateTable`

---

## Model Structure

![Data Model](../dashboard/screenshots/data_model.png)

The model is centered around the `Fact_PostPerformance` table,
with dimension tables providing descriptive attributes used for
filtering and analysis.

### Fact Table

#### `Fact_PostPerformance`

This is the main performance table in the model.

It contains the post-level performance data used to calculate
the dashboard's KPIs and analytical measures.

The table is used by measures such as:

- `Total Views`
- `Total Engagement`
- `Total Posts`
- `CTR`
- `Engagement Rate`
- `Average Views per Post`
- `Average Engagement per Post`

---

## Dimension Tables

### `Dim_Date`

The date dimension provides the time-related fields used for
time-series analysis and period filtering.

It is used by the dashboard for:

- Year filtering
- Month-level analysis
- Monthly performance trends
- Month-over-month growth

Key field used in the report:

```text
Dim_Date[Month Year]
