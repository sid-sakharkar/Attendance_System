# End-to-End Vendor Insights

![Workflow](Workflow.png)

---

## Problem Statement

This project analyzes vendor performance for a wholesale/retail business. The goal is to find which vendors and brands are profitable, where pricing or inventory issues are hurting the business, and how to fix them using data.

---

## What This Project Does

- Identifies top-performing and underperforming vendors
- Highlights slow-moving or stuck inventory
- Detects pricing inconsistencies
- Analyzes how bulk purchases affect margins
- Answers core business questions with clear data

---

## Project Highlights

- Identify top-performing and underperforming vendors
- Highlight stuck or slow-moving inventory
- Spot pricing mismatches
- Understand how bulk purchases impact margins
- Answer actual business questions through clean, structured analysis

---

## Why This Matters

Businesses constantly ask:
- Which vendors are boosting profits — and which are draining them?
- Where are we losing money — in pricing, inventory, or buying decisions?
- How can we optimize vendor relationships?

This project tackles those questions head-on using data and dashboards.

---

## How It Works

1. **Ingest Data**  
   Load CSVs into SQLite using Python. Handles large files and logs each step.
2. **Clean + Analyze**  
   Use SQL and Pandas to explore, join, and clean the data.
3. **Generate Insights**  
   Calculate KPIs like margins, sales, stuck inventory, and vendor-level performance.
4. **Visualize**  
   Build a Power BI dashboard that’s easy to read and ready for business users.

---

## What’s in the Data?

- Opening and closing inventory
- Vendor purchases and pricing
- Product-level sales data
- Vendor invoice details

All datasets are loaded into a single SQLite database.

---

## Key Files

| File                            | Purpose                                                   |
|---------------------------------|-----------------------------------------------------------|
| `Ingestion.ipynb`              | Loads CSVs into SQLite with logging and error handling    |
| `Exploratory Data Analysis.ipynb` | Cleans and explores data using Pandas and SQL            |
| `Vendor Performance.ipynb`     | Analyzes vendor/brand-level performance                   |
| `inventory.db`                 | Final database used for querying and analysis             |
| `final_table.csv`              | Merged and cleaned data used in Power BI                  |
| `Workflow.png`                 | Project flow diagram                                      |
| `Dashboard.gif`                | Preview of interactive Power BI dashboard                 |

---

## Example Code Snippets

**Data Ingestion**
```python
import pandas as pd
import sqlite3

conn = sqlite3.connect('inventory.db')
df = pd.read_csv('data/sales.csv')
df.to_sql('sales', conn, if_exists='replace', index=False)
```

**Cleaning & Merging**
```python
df_sales = pd.read_sql('SELECT * FROM sales', conn)
df_purchases = pd.read_sql('SELECT * FROM purchases', conn)
merged = pd.merge(df_sales, df_purchases, on='product_id', how='left')
merged = merged.dropna()
merged['date'] = pd.to_datetime(merged['date'])
```

**Analysis**
```python
vendor_sales = merged.groupby('vendor_name')['sales_amount'].sum().reset_index()
top_vendors = vendor_sales.sort_values(by='sales_amount', ascending=False).head(5)
```

**Export for Power BI**
```python
merged.to_csv('final_table.csv', index=False)
```

---

## Skills Demonstrated

- SQL (joins, filtering, grouping)
- Python scripting (with logging, chunking, error handling)
- Data wrangling with Pandas
- Power BI for dashboarding
- Breaking down real business problems into data workflows

---

## Dashboard Preview

![Dashboard](Dashboard.gif)

Interactive Power BI dashboard covering sales, purchases, margins, vendor health, and more.

---

## How to Run

1. Clone the repo  
   ```bash
   git clone https://github.com/eharshit/End-to-End-Vendor-Insights
   ```
2. Install dependencies  
   ```bash
   pip install pandas numpy
   ```
3. Launch Jupyter Notebook  
   ```bash
   jupyter notebook
   ```
4. Run the notebooks in this order:
   - `Ingestion.ipynb`
   - `Exploratory Data Analysis.ipynb`
   - `Vendor Performance.ipynb` (optional deep dive)
5. Open Power BI and connect to `final_table.csv`

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you want to improve.

---