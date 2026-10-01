Bank Marketing Data Analysis

Exploratory data analysis (EDA) of a bank telemarketing dataset, done in Python with pandas. The goal is to understand who the bank's customers are and which of them subscribe to a term deposit.

Files


File Description
bank.csv, Raw dataset: 11,162 rows, 17 columns
Bank.py, Python script that loads the data: checks for missing values and produces summary tables
Analyzed_bank_document.docx, Output tables: numeric summary and frequency tables for the categorical columns

Dataset overview

- Rows: 11,162 (one row per customer contact)
- Columns: 17 (7 numeric, 10 categorical)
- Missing values: none recorded as blank, but several columns use `"unknown"` as a category 
- Target variable: `deposit` (did the customer subscribe to a term deposit? `yes` / `no`)

Data dictionary

| Column | Type | Description |

| age | numeric | Customer age in years (18 to 95) |
| job | categorical | Type of job (12 categories, e.g. management, blue-collar, student, retired) |
| marital | categorical | Marital status: married, single, divorced |
| education | categorical | Education level: primary, secondary, tertiary, unknown |
| default | categorical | Has credit in default? yes / no |
| balance | numeric | Average yearly account balance |
| housing | categorical | Has a housing loan? yes / no |
| loan | categorical | Has a personal loan? yes / no |
| contact | categorical | Contact channel: cellular, telephone, unknown |
| day | numeric | Day of the month of the last contact |
| month | categorical | Month of the last contact |
| duration | numeric | Length of the last call in seconds |
| campaign | numeric | Number of contacts made to this customer during this campaign |
| pdays | numeric | Days since the customer was last contacted in a previous campaign (`-1` = never contacted before) |
| previous | numeric | Number of contacts before this campaign |
| poutcome | categorical | Outcome of the previous campaign: success, failure, other, unknown |
| deposit | categorical | **Target.** Subscribed to a term deposit? yes / no |

Key findings so far

Numeric summary
- Average customer is about 41 years old (median 39).
- Balance is heavily right-skewed: mean 1,528 vs median 550, ranging from -6,847 to 81,204.
- Median call lasts about 255 seconds (mean 372); the longest is 3,881 seconds.
- Most customers (about 75%) had no previous campaign contact (`pdays = -1`).

Customer profile
- Top jobs: management (23.0%), blue-collar (17.4%), technician (16.3%), admin. (12.0%).
- 56.9% married, 31.5% single, 11.6% divorced.
- Education: 49.1% secondary, 33.1% tertiary, 13.4% primary.
- Credit default is rare (1.5%); 47.3% have a housing loan; 13.1% have a personal loan.
- 72.0% were contacted by cellular.

Target balance
- 47.4% subscribed (5,289) and 52.6% did not (5,873), so the classes are fairly balanced.

How to run

```bash
pip install pandas numpy matplotlib seaborn
python Bank.py
```

When prompted for a file name, type `bank.csv` or press Enter to use the default.

Most `print`, `to_csv` and plotting lines in `Bank.py` are commented out. Uncomment the ones you need to see charts or export the tables.

Data quality notes

- `unknown` appears in `job` (0.6%), `education` (4.5%), `contact` (21.0%) and `poutcome` (74.6%). These are not true blanks, so `isnull()` does not catch them.
- `balance` includes 688 negative values (overdrafts) and extreme positive outliers.
- `pdays = -1` is a code for "not previously contacted", not a real number of days. Treat it separately when calculating averages.
- `duration` is only known after a call ends, so it should not be used to predict the outcome before a call is made.


Source and tools

- Dataset: Public Bank Marketing dataset (telemarketing campaigns of a Portuguese bank).
- Tools: Python, pandas, NumPy, Matplotlib, Seaborn.
