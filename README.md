# Data Cleaning & Preparation – Online Retail II

## SWYNEX Technologies – Data Analytics Internship

This project was completed as **Task 1 of my Data Analytics Internship at SWYNEX Technologies**.

The objective of this task was to select a real-world dataset, identify data quality issues, clean and transform the data using Python, and prepare an analysis-ready dataset for further exploratory data analysis.

---

## Project Overview

Real-world datasets often contain missing values, duplicate records, incorrect data types, inconsistent values, and unusual business transactions.

For this project, I worked with the **Online Retail II dataset** from the UCI Machine Learning Repository.

The original dataset contained:

- **1,067,371 transaction records**
- **8 original features**
- Transactions covering two years of online retail activity

The cleaning process focused on preserving meaningful business information while removing or correcting genuine data quality problems.

---

## Dataset Features

The original dataset contains the following columns:

| Column | Description |
|---|---|
| Invoice | Unique invoice/transaction identifier |
| StockCode | Product identifier |
| Description | Product description |
| Quantity | Number of products purchased or returned |
| InvoiceDate | Date and time of transaction |
| Price | Unit price of the product |
| Customer ID | Unique customer identifier |
| Country | Customer/transaction country |

---

## Technologies Used

- Python
- Pandas
- NumPy
- Jupyter Notebook
- Matplotlib
- Seaborn
- OpenPyXL

---

## Data Quality Assessment

Initial analysis identified several data quality issues.

| Issue | Initial Count |
|---|---:|
| Missing Customer IDs | 243,007 |
| Missing Descriptions | 4,382 |
| Exact Duplicate Records | 34,335 |
| Negative Quantity Records | 22,950 |
| Zero Price Records | 6,202 |
| Negative Price Records | 5 |

Rather than automatically deleting unusual records, each issue was investigated to determine its business meaning.

---

## Data Cleaning Process

### 1. Duplicate Records

The dataset contained **34,335 exact duplicate records**.

These records were removed to prevent duplicate transactions from affecting subsequent analysis.

### 2. Missing Customer IDs

The raw dataset contained **243,007 missing Customer IDs**.

These transactions were not automatically removed because they still contained useful information such as product, quantity, price, transaction date, and country.

After duplicate removal and other cleaning operations, **235,146 records** still contained missing Customer IDs.

### 3. Missing Product Descriptions

There were initially **4,382 missing product descriptions**.

StockCode-based mapping was used to recover descriptions from other records containing the same product identifier.

- **4,019 descriptions recovered**
- **363 descriptions remained missing**

Descriptions that could not be reliably determined were left missing rather than artificially assigning values.

### 4. Negative Quantities

The raw dataset contained **22,950 negative-quantity records**.

Investigation showed that many represented cancellations, returns, damaged products, missing stock, and inventory adjustments.

Therefore, these records were retained instead of being treated as invalid data.

After duplicate removal, **22,496 negative-quantity records** remained.

### 5. Transaction Classification

Transactions were classified into three categories:

| Transaction Type | Records |
|---|---:|
| Sale | 1,010,534 |
| Cancellation/Return | 19,104 |
| Adjustment | 3,393 |

This preserves useful business events for future analysis.

### 6. Zero-Price Transactions

The raw dataset contained **6,202 zero-price records**.

Investigation showed descriptions including adjustments, damaged products, missing inventory, checks, and other non-standard transactions.

Instead of automatically deleting these records, they were retained and identified using an `IsZeroPrice` flag.

After duplicate removal, **6,014 zero-price records** remained.

### 7. Negative Prices

Five records contained negative prices.

All five were associated with **"Adjust bad debt"** entries and represented accounting adjustments rather than normal retail sales.

These five records were removed from the final analysis-ready dataset.

### 8. Data Type Correction

`Customer ID` was originally represented as a floating-point value because the column contained missing values.

It was converted to Pandas' nullable integer (`Int64`) data type, allowing customer identifiers to be represented correctly while preserving missing values.

`InvoiceDate` was retained as a datetime data type.

---

## Feature Engineering

Additional features were created to support future analysis:

| Feature | Purpose |
|---|---|
| IsCancellation | Identifies cancellation/return invoices |
| IsZeroPrice | Identifies zero-price transactions |
| TransactionType | Classifies Sale, Cancellation/Return, and Adjustment transactions |
| Revenue | Quantity × Price |
| Year | Transaction year |
| Month | Transaction month |
| MonthName | Name of transaction month |
| YearMonth | Year-month period for time-series analysis |

---

## Cleaning Results

| Metric | Result |
|---|---:|
| Original Records | 1,067,371 |
| Final Records | 1,033,031 |
| Records Removed | 34,340 |
| Exact Duplicates Removed | 34,335 |
| Negative Price Records Removed | 5 |
| Descriptions Recovered | 4,019 |
| Remaining Missing Descriptions | 363 |
| Remaining Missing Customer IDs | 235,146 |
| Data Retention Rate | 96.78% |

The final dataset contains **1,033,031 records and 16 features**.

---

## Final Validation

After cleaning:

- Exact duplicate records: **0**
- Negative-price records: **0**
- Missing transaction dates: **0**
- Missing revenue values: **0**
- Remaining missing values are documented rather than artificially replaced
- Returns, cancellations, and inventory adjustments are preserved for future analysis

---

## Project Structure

```text
SWYNEX-Data-Cleaning-Preparation/
│
├── data/
│   ├── raw/
│   │   └── online_retail_II.xlsx
│   └── cleaned/
│       └── online_retail_II_cleaned.csv
│
├── notebooks/
│   └── 01_Data_Cleaning_Preparation.ipynb
│
├── output/
│   └── cleaning_summary.csv
│
├── .gitignore
├── README.md
└── requirements.txt
```

The original Excel dataset is excluded from version control and can be obtained from the UCI Machine Learning Repository.

---

## How to Run

Clone the repository:

```bash
git clone <repository-url>
```

Move into the project:

```bash
cd SWYNEX-Data-Cleaning-Preparation
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Place the original Online Retail II Excel dataset inside:

```text
data/raw/
```

Then open:

```text
notebooks/01_Data_Cleaning_Preparation.ipynb
```

and execute the notebook cells sequentially.

---

## Key Learning Outcomes

Through this task, I practiced:

- Data quality assessment
- Missing-value analysis
- Duplicate detection and removal
- Data-type correction
- Handling unusual and inconsistent transaction records
- Business-aware data-cleaning decisions
- Feature engineering
- Dataset validation
- Preparing reproducible analysis-ready data

---

## Dataset Source

**Online Retail II**  
UCI Machine Learning Repository

The dataset is used for educational and analytical purposes.

---

## Internship

**Organization:** SWYNEX Technologies  
**Domain:** Data Analytics  
**Task:** Task 1 – Data Cleaning & Preparation