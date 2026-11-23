# Walmart Sales Analysis

A retail analytics practice project that cleans the supplied Walmart-labelled transaction dataset with Python and pandas, then explores branch performance, payment methods, ratings, sales timing, and revenue changes with SQL.

## Project contents

| File | Purpose |
| --- | --- |
| [Data/Walmart.csv](Data/Walmart.csv) | Supplied raw transaction data. |
| [Code/python_cleanup.ipynb](Code/python_cleanup.ipynb) | Data inspection, duplicate/missing-row removal, price conversion, and revenue calculation. |
| [Code/walmart_analysis_query.dbquery.ipynb](Code/walmart_analysis_query.dbquery.ipynb) | SQL analysis questions and working queries. |

## Business questions

- Which payment methods account for the most transactions and units?
- Which category has the highest average rating in each branch?
- Which weekdays and times of day have the most recorded activity?
- How do category ratings and calculated profit measures vary across branches and cities?
- Which branches have the largest revenue declines between 2022 and 2023?

## Run the preparation notebook

Use Python 3 and a Jupyter-capable editor.

```sh
git clone https://github.com/ebaprk/Walmart-Sales-Analysis.git
cd Walmart-Sales-Analysis
python3 -m venv .venv
source .venv/bin/activate
python -m pip install pandas ipykernel
```

Open `Code/python_cleanup.ipynb` in VS Code with the Python and Jupyter extensions and select `.venv` as the kernel. Run cells from top to bottom with `Code/` as the working directory; the input path is `../Data/Walmart.csv`.

The notebook removes duplicate rows and rows containing missing values, converts dollar-prefixed unit prices to numbers, and creates `total_revenue = unit_price * quantity`. Its final cell exports **`~/Downloads/walmart_cleaned.csv`**. Create that directory or change the output path before exporting.

## Run the SQL analysis

Import the cleaned CSV into your SQL workspace as `walmart_data`. The `.dbquery.ipynb` file holds SQL source; use a SQL editor or import workflow rather than running it as Python.

The queries were assembled for SQL exploration and contain dialect-specific syntax. Review them for the engine you use: the date/time bucketing query includes `time::time`, while other queries use Databricks-style date formatting. Confirm that dates are parsed correctly, particularly before grouping by weekday or comparing years.

## Metric and query limitations

- Revenue is calculated from recorded unit price and quantity; it is not audited accounting revenue.
- The profit query multiplies price, quantity, and the supplied `profit_margin`. Confirm that field’s units before interpreting its result as currency.
- The category-profit query groups by **branch and category**, rather than category alone.
- The payment-preference query lists all methods by branch; it does not yet filter each branch to its top-ranked method.
- Dropping every row with any missing value can change the analysis population. Record excluded counts before drawing conclusions.
- The dataset is supplied in the repository without a verified original source citation. Its Walmart label does not establish that it is official company data; confirm provenance and usage terms before redistribution.

This repository contains preparation and query work. It does not include a separate validated findings report or dashboard.

## License

Original software and documentation are licensed under the [Apache License 2.0](LICENSE). See [NOTICE](NOTICE) for copyright, attribution, and the scope of this grant. Third-party materials retain their own terms.

The supplied CSV dataset is excluded: its original source/license has not been verified, so the Apache grant does not provide dataset reuse or redistribution permission.
