# Seattle Airbnb Data Cleaning & Tableau Dashboard

An end-to-end data analysis project that combines, cleans, and visualizes the Seattle Airbnb Open Dataset in Tableau to help a prospective host decide **where to buy**, **how to price**, and **when to list** a short-term rental property.

🔗 **Live Dashboard:** [View on Tableau Public](https://public.tableau.com/app/profile/hunter.woodruff/viz/AirbnbProject_17869807024900/Dashboard1?publish=yes)

![Dashboard Preview](images/dashboard_overview.png)

---

## Project Overview

Using publicly available Airbnb listing, calendar, and review data for Seattle, this project answers a set of practical questions for someone considering entering the short-term rental market:

- Which zip codes command the highest average nightly price?
- Where are those high-value zip codes located geographically?
- What time of year generates the most rental revenue?
- How does bedroom count affect average nightly price?
- How much competition (number of listings) exists at each bedroom count?

## Data Source

- **Seattle Airbnb Open Data** (Kaggle) — three raw files: `listings.csv`, `calendar.csv`, `reviews.csv`
- Note: the dataset used here reflects a 2016 snapshot. Kaggle periodically publishes updated versions of this dataset if more recent data is preferred.
- ⚠️ **Raw and cleaned data files are not included in this repository** due to their size. To reproduce this project, download the dataset directly from Kaggle and follow the join/cleaning steps below.

## Data Preparation

The three raw CSVs were combined into a single Excel workbook and joined in Tableau. Key steps:

1. **Combined** `listings`, `calendar`, and `reviews` into one workbook, one sheet per table.
2. **Joined `calendar` to `listings`** on `listing_id = id` (inner join), since every calendar row belongs to a listing.
3. **Joined `reviews` to `listings`** on `listing_id = id`. This required correcting Tableau's auto-suggested join, which defaulted to matching `id = id` — incorrectly pairing the *review's own ID* with the *listing's ID* rather than the actual foreign key. Fixing the join key changed the row count from ~2,500 rows to over 2 million, confirming the correct relationship.
4. **Filtered to a single calendar year** (2016) to bring the dataset under Tableau Public's 15-million-row limit.
5. **Removed invalid records**: excluded listings with null zip codes and listings with 0 bedrooms, since neither is usable in a location- or bedroom-based analysis.
6. **Converted `bedrooms` from a measure to a dimension** so it could be used as a categorical grouping field rather than a continuous numeric value.

## Tools Used

- **Tableau Desktop / Public** — joins, calculated fields, dashboard design
- **Microsoft Excel** — combining and staging raw CSVs prior to import

## Dashboard Components

| Visualization | Purpose |
|---|---|
| **Average Price by Zip Code** (bar chart) | Ranks zip codes by average nightly rate to surface the highest-earning areas |
| **Price by Zip Code** (map) | Shows the same pricing data geographically, color-coordinated with the bar chart |
| **Revenue by Time of Year** (line chart) | Tracks weekly revenue across the year to identify seasonal booking patterns |
| **Average Price by Bedroom Count** (bar chart) | Shows how nightly price scales with the number of bedrooms |
| **Listing Count by Bedroom Count** (bar chart) | Shows the level of competition (number of active listings) at each bedroom count |

## Key Insights

- Nightly prices vary significantly by zip code, with the top-performing area averaging roughly $206/night.
- Bookings and revenue rise in the summer and again around the holiday season (November–December), while January and February are the slowest months.
- Average price increases substantially with bedroom count, but competition (listing volume) drops off sharply above 3–4 bedrooms — suggesting an opportunity in larger properties with less saturated supply.

## Repository Structure

```
seattle-airbnb-tableau-analysis/
├── README.md
├── tableau/
│   └── seattle_airbnb_dashboard.twbx
└── images/
    └── dashboard_overview.png
```
