# NYC Property Sales Analysis


> Analyzed NYC property transaction records from 2016--2025 using Python and Power BI to identify changes in transaction activity and how recorded prices vary by borough, property type, and property characteristics.

---

## ⚙️ Project Type Flags


- [x] Exploratory Data Analysis (EDA)
- [ ] SQL Analysis / Querying
- [x] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [x] Data Cleaning / Wrangling
- [x] End-to-End (data profiling, cleaning, analysis, and reporting)
- [ ] Other

---

## Table of Contents


1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Data Workflow](#5-data-workflow)
6. [Data Model & Schema](#6-data-model--schema)
7. [Analysis & Metrics](#8-analysis--metrics)
8. [Key Insights](#9-key-insights)
9. [Recommendations](#10-recommendations)
10. [Assumptions & Limitations](#11-assumptions--limitations)
11. [Future Enhancements](#12-future-enhancements)
12. [Deliverables](#13-deliverables)
13. [Author](#14-author)

---

## 1. Project Overview


**Context:** NYC property transactions vary by year, borough, and
property characteristics. Looking at transaction counts alone does not
show how recorded sale prices differ across segments, while looking at
prices alone does not describe how frequently transactions occur.

**Problem Statement:** How has NYC property transaction activity changed
from 2016--2025, and what locations and property characteristics are
associated with differences in transaction activity and sale prices?

**Approach:** I profiled and cleaned the Citywide Annualized Calendar
Sales Update dataset in Python, documented data-quality decisions, and
performed exploratory analysis. I then built a Power BI report to
compare yearly activity, transaction composition, boroughs,
neighborhoods, property types, unit groups, and property age.

**Outcome:** The project includes a documented cleaning workflow, a
cleaned analysis dataset, three Jupyter notebooks, and a four-page Power
BI dashboard. The analysis highlights differences in transaction
activity and median positive sale prices across years, boroughs, and
property segments.

---

## 2. Objectives


- **Primary Objective:** Quantify how recorded NYC property
    transaction activity changed from 2016 through 2025.
- **Secondary Objective 1:** Compare median positive sale prices across boroughs and property types, and examine how property age relates to median sale price.
- **Secondary Objective 2:** Prepare a reproducible cleaning workflow
    that documents missing values, duplicate handling, zero-price
    records, and retained fields.
- **Secondary Objective 3:** Communicate the analysis through a Power
    BI dashboard and supporting exploratory visualizations.

---

## 3. Project Scope & Tools


### Scope

| Dimension | Details |
|-----------|---------|
| **In Scope** | NYC property transaction records, annual transaction trends, borough and neighborhood comparisons, property types, property age, and sale-price metrics. |
| **Out of Scope** | Predictive modeling, casual explanations for price differences, individual buyer behavior, mortgage or rental-market analysis, and estimating total market value from transaction counts and median prices. These require additional data or methods beyond this descriptive project. |
| **Time Period** | Calendar years 2016--2025. |
| **Granularity** | Transaction-record level in the source datase, with grouped summaries used for comparisons and dashboard visuals. Records represent recorded property transactions or ownership transfers, not necessarily unique buyers. |

### Tools & Technologies

| Category | Tool(s) Used |
|----------|-------------|
| Data Storage | CSV files |
| Data Processing | Python |
| Analysis | Pandas & Jupyter Notebook |
| Visualization | Matplotlib & Power BI |
| Version Control | Git & GitHub |
| Documentation | Markdown & Excel data dictionary |
| Other | Visual Studio Code |

*SQL and machine learning were not used in this project*

---

## 4. Repository Structure


```
nyc-property-sales-analysis/
├── data/
│   ├── raw/
│   │   └── README.md
│   └── processed/
│       └── README.md
├── docs/
│   └── Annualized_Calendar_Sales_Update_Data_Dictionary.xlsx
├── notebooks/
│   ├── 01_data_profiling.ipynb
│   ├── 02_data_cleaning.ipynb
│   └── 03_exploratory_analysis.ipynb
├── reports/
│   └── nyc_property_sales_dashboard.pbix
├── visuals/
│   ├── Location & Property Characteristics.png
│   ├── Market Composition & Value.png
│   ├── Market Overview.png
│   └── Market Segments & Business Findings.png
├── .gitignore
└── README.md
```

**Note:** The raw and processed CSV datasets are excluded from Git tracking to keep the repository lightweight. The `data/raw/README.md` documents the original source data, and the `data/processed/README.md` provides access to the downloadable cleaned dataset.

---

## 5. Data Workflow


```
NYC Open Data: Citywide Annualized Calendar Sales Update
                         ↓
             Load and profile source CSV
                         ↓
       Clean types, fields, duplicates, and values
                         ↓
       Validate and export cleaned transaction data
                         ↓
       Exploratory analysis in Python / pandas
                         ↓
          Build and refine Power BI report
                         ↓
      Dashboard screenshots and project documentation
```

1. **Source:** NYC Open Data's *Citywide Annualized Calendar Sales
    Update*, covering calendar years 2016--2025, supplied as a CSV with
    a related data dictionary.

2. **Ingestion:** Loaded the CSV into pandas for profiling and
    cleaning.

3. **Cleaning:** Standardized field types, reviewed missing values and
    duplicate records, and removed fields not needed for the core
    analysis. The raw dataset contained 845,607 rows and 29 columns. The
    cleaned dataset contains 842,256 rows and 20 columns.

4. **Transformation:** Prepared date and numeric fields for analysis
    and created grouped measures and categories for dashboard
    comparisons, including borough names, unit groups, and property-age
    groups.

5. **Analysis:** Used descriptive statistics, year-over-year trend
    analysis, and comparisons by borough, neighborhood, property type,
    unit group, and property age.

6. **Output:** Three Jupyter notebooks, a cleaned dataset for analysis,
    a four-page Power BI report, dashboard screenshots, and this project
    documentation.

---

## 6. Data Model & Schema


### Dataset / Table: `nyc_sales_property_cleaned`

This is a single transaction-level dataset rather than a relational
database with multiple joined tables. The cleaned version has **842,256
rows and 20 columns**.

  ----------------------------------------------------------------------------------------
 | Field | Data Type (cleaned) | Description | Example / Notes |
|-------|---------------------|-------------|-----------------|
| `BOROUGH` | Integer / code | Numeric code identifying the borough. | Codes 1–5; mapped to borough names for reporting. |
| `NEIGHBORHOOD` | Text | Neighborhood label assigned in the source data. | Some values include `*-UNKNOWN`. Their meaning is not explained in the available dictionary. |
| `BUILDING CLASS CATEGORY` | Text | Source building-class category. | Used to group property records. |
| `TAX CLASS AT PRESENT` | Text / category | Tax class recorded in the source. | May be missing for some records. |
| `BLOCK` | Integer / code | Tax block identifier. | Retained in the cleaned dataset. |
| `LOT` | Integer / code | Tax lot identifier. | Retained in the cleaned dataset. |
| `BUILDING CLASS AT PRESENT` | Text / category | Present building class. | May be missing for some records. |
| `ADDRESS` | Text | Recorded property address. | Canont by used to identify unique buyers. |
| `APARTMENT NUMBER` | Text | Apartment or unit identifier, where available. | Often missing for non-apartment records. |
| `ZIP CODE` | Numeric / code | Recorded ZIP code. | Treated as a category, not a quantity. |
| `RESIDENTIAL UNITS` | Numeric | Recorded residential unit count. | Missing values are retained unless required by a specific analysis. |
| `COMMERCIAL UNITS` | Numeric | Recorded commercial unit count. | Missing values may occur. |
| `TOTAL UNITS` | Numeric | Recorded total unit count. | Missing values may occur. |
| `LAND SQUARE FEET` | Numeric | Recorded land area in square feet. | Many records contain zero. Not used for size analysis without further validation. |
| `GROSS SQUARE FEET` | Numeric | Recorded gross building area in square feet. | Many records contain zero. Not used for size analysis without further validation. |
| `YEAR BUILT` | Numeric | Recorded year the property was built. | Used to derive property-age groups after validity checks. |
| `TAX CLASS AT TIME OF SALE` | Text / category | Tax class at sale. | Source classification. |
| `BUILDING CLASS AT TIME OF SALE` | Text / category | Building class at sale. | Source classification. |
| `SALE PRICE` | Integer / numeric | Recorded transaction sale price in dollars. | Zero-price records are retained for activity counts and excluded from positive-price metrics. |
| `SALE DATE` | Date/time | Recorded transaction date. | Used for annual trend analysis. |
  ----------------------------------------------------------------------------------------

> **Row count (approx.):** 842,256 cleaned records\
> **Date range:** 2016--2025\
> **Key join / relationship:** No ERD or table joins apply; the analysis uses one
> cleaned transaction-level dataset.

---

## 7. Analysis & Metrics


### Analytical Approach

This is a descriptive and exploratory analysis, not a causal or
predictive model. The analysis compares transaction activity and
positive sale prices across time and property segments. Median sale
price is used for group comparisons because sale prices are highly
skewed and can be affected by extreme values.

### Key Metrics Defined

| Metric | Plain-Language Definition | Why It Matters |
|--------|---------------------------|----------------|
| **Total Transactions** | Count of records in the selected date range or segment, including zero-price records. | Measures recorded transaction activity. |
| **Positive-Price Transactions** | Count of records where `SALE PRICE > 0`. | Shows how many records are eligible for positive sale-price analysis. |
| **Zero-Price Share** | Number of records with `SALE PRICE = 0` divided by all transaction records. | Shows how the share of zero-price transfers varies over time. |
| **Median Sale Price** | Median `SALE PRICE` among records where `SALE PRICE > 0`. | Provides a robust measure of typical recorded price while reducing sensitivity to extreme values. |
| **Transaction Volume by Segment** | Count of transaction records grouped by borough, neighborhood, property type, unit group, or age group. | Allows comparison of activity across market segments. |

### Methods Used

-   Data profiling: dataset shape, data types, missingness, and value
    distributions.
    
-   Data cleaning and validation: type standardization, duplicate
    review, and export/reload checks.

-   Trend analysis across calendar years 2016--2025.

-   Group comparisons by borough, neighborhood, property type, unit
    group, and property-age group.

-   Median-based sale-price analysis using positive-price records only.

-   Visual analysis using Matplotlib and Power BI.

---

## 8. Key Insights

The following findings are supported by the current analysis and should
be presented as descriptive patterns rather than causal conclusions.

**Insight 1: Transaction activity changed substantially over the study
period.**

Recorded transactions declined from 80,068 in 2016 to 51,061 in 2020,
increased to 69,256 in 2021, and then fell before recovering to 59,247
in 2025. This shows that transaction activity varied considerably across
the decade rather than following a steady trend.

**Insight 2: Zero-price records form a material share of recorded
activity.**

The zero-price share rose from about 29.2% in 2016 to about 40.2% in
2025, with particularly high shares in 2020 and from 2023--2025. These
records are retained when counting transaction activity but excluded
from median sale-price calculations.

**Insight 3: Transaction activity and median sale price differ by
borough.**

Queens and Brooklyn had the largest recorded transaction counts in the
cleaned dataset, while Manhattan had the highest borough-level median
positive sale price. Transaction volume and median price therefore
describe different aspects of the recorded market.

**Insight 4: Recorded prices vary across property segments and age
groups.**

Median positive sale prices differ across property types, unit groups,
and property-age categories. These differences are descriptive
associations. Location, property type, and other unmeasured
characteristics may also contribute to the observed variation.


---

## 10. Recommendations


These are analytical next steps for a stakeholder using the report, not
claims that the dataset establishes a cause.

  | Priority | Recommendation | Based On | Suggested Owner |
|----------|----------------|----------|-----------------|
| **High** | Review annual transaction counts alongside the zero-price share to distinguish changes in recorded activity from changes in positive-price transactions. | Insights 1 and 2 | Real estate research / analytics team |
| **Medium** | Compare borough and property-type segments using both transaction volume and median positive sale price before prioritizing a market segment for further review. | Insight 3 | Market research / strategy team |
| **Medium** | Investigate property-age patterns while controlling for borough and property type in a follow-up analysis. | Insight 4 | Data analytics team |
| **Low** | Add complementary data, such as interest rates, housing inventory, or other market indicators, before attempting to explain why activity or prices changed. | Project limitations | Research / analytics team |


---

## 11. Assumptions & Limitations


### Assumptions

-   The source's `SALE DATE` field is used to assign records to calendar
    years.

-   A `SALE PRICE` greater than zero is required for positive sale-price
    metrics.

-   Zero-price records are treated as recorded transfers without cash
    consideration according to the source documentation, not as ordinary
    market-price observations.

-   Grouped comparisons describe the records in the dataset and do not
    necessarily represent unique properties or unique buyers.

### Limitations

-   The dataset records property transactions or ownership transfers,
    not unique buyers. One person or property may appear in multiple
    records.

-   A sale price of zero does not represent a typical market sale price.
    These records are included in transaction counts and excluded from
    positive-price metrics.

-   The source contains substantial zero values in `GROSS SQUARE FEET`
    and `LAND SQUARE FEET` (approximately 89.6% and 92.6%, respectively,
    in the reviewed data). The available dictionary does not explain
    these zeros, so size-based conclusions are not emphasized.

-   Missing values occur in optional property details, including unit
    counts and year built. Analyses requiring these fields may use fewer
    records than overall transaction counts.

-   The source dictionary does not explain all `*-UNKNOWN` neighborhood
    labels. Their cause should not be inferred without further
    documentation.

-   Extreme prices can affect averages and visual scales, so medians are
    preferred for typical-price comparisons.

-   The analysis is descriptive. It does not establish that a particular
    property characteristic or location causes a price difference.

-   Findings depend on the source dataset's coverage, definitions, and
    data quality. No independent reconciliation against a complete
    external transaction registry was performed.

---

## 12. Future Enhancements

-   [ ] Validate the final cleaned schema and key totals against the
    latest source documentation.

-   [ ] Add contextual market indicators, such as interest rates or
    housing inventory, to investigate possible explanations for
    year-to-year changes.

-   [ ] Explore property age while controlling for borough and property
    type.

-   [ ] Automate repeatable data validation and reporting if the source
    data is updated in future.

-   [ ] Add a documented comparison of results before and after key
    cleaning decisions.

---

## 13. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| **Raw dataset** | Original NYC property sales CSV, preserved without edits. See the data source and access details in the folder README. | `data/raw/README.md` |
| **Profiling notebook** | Reviews dataset structure, data types, missingness, and distributions. | `notebooks/01_data_profiling.ipynb` |
| **Cleaning notebook** | Documents cleaning decisions, validation, and cleaned-data export. | `notebooks/02_data_cleaning.ipynb` |
| **EDA notebook** | Performs descriptive analysis and selected visualizations. | `notebooks/03_exploratory_analysis.ipynb` |
| **Cleaned dataset** | Processed NYC property sales data used in this analysis, available as a downloadable ZIP file. | `data/processed/README.md` |
| **Data dictionary** | Reference definitions for source fields. | `docs/` |
| **Power BI report** | Four-page dashboard covering overview, composition/value, location/characteristics, and business findings. | `reports/nyc_property_sales_dashboard.pbix` |
| **Dashboard screenshots** | Static previews of the four report pages. | `visuals/` |
| **Project documentation** | Overview, methods, findings, limitations, and deliverables. | `README.md` |

---

## 14. Author

**Isabel P Lopez Paez**

Aspiring Business Analyst

- 🔗 LinkedIn: [LinkedIn URL](https://www.linkedin.com/in/isabelplopezpaez/?isSelfProfile=true)
- 💼 Portfolio: [Github Portfolio](https://github.com/lopezpaezisabel-alt)
- 📧 Email: [Email](mailto:lopezpaezisabel@gmail.com)

---

*Last updated: October 2026*
