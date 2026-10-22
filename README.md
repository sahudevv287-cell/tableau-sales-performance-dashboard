# Sales Performance Dashboard (Tableau)

An interactive Tableau dashboard that analyzes retail sales across India. The project starts from a messy raw dataset, cleans it, and turns it into a dashboard with filters, a metric selector and linked charts that answer practical business questions: what sells, where, to whom, and how discounts affect profit.

> **Note:** The dataset is **simulated for learning purposes**. It does not represent a real company, and the insights below describe this sample data only.


**Live dashboard:** [View on Tableau Public](https://drive.google.com/file/d/1IldO3GjK1_Ei6CoOvgqJA1umtPhY5fFK/view?usp=drive_link)

---

## Key numbers

| Metric | Value |
|---|---|
| Total sales | ₹2.72M |
| Total profit | ₹200.9K |
| Total orders | 2,000 |
| Average profit per order | ₹100.04 |
| Profit ratio | 7.4% |

## Key insights

- **Laptops and Phones drive profit.** Together they generate about 89% of total profit (₹113.0K and ₹65.1K), while most other sub-categories contribute very little.
- **Medium discounts have the weakest margin.** Orders in the medium discount band have a profit ratio of 5.0%, compared with 8.0% (high) and 8.2% (low). Discounting is not a simple "more discount, less profit" pattern in this data.
- **Sales are spread across customer segments.** Consumer leads with ₹1,033.2K, followed by Corporate (₹992.8K) and Home Office (₹694.8K).
- **A few products lead sales.** Dell XPS 13 (₹23.6K) and HP Pavilion (₹17.2K) are the top two of the top five products by sales.

*(Update these figures if you change filters or data cleaning choices.)*

## Dashboard features

- **Four filters:** Region, Segment, Order Date and Category, applied to every chart
- **Metric selector:** switch key charts between Sales, Profit and Quantity using a parameter
- **Click-to-filter actions:** selecting a state or sub-category updates the other charts
- **Tooltips** with sales, profit and profit ratio
- **Eight linked visuals:**
  1. KPI cards (sales, profit, average profit, orders, profit ratio)
  2. Monthly sales vs profit (dual axis line chart)
  3. Sales map by state (filled map)
  4. Profit by sub-category
  5. Top 5 customers by sales
  6. Top 5 products by sales
  7. Profit ratio by discount band
  8. Sales by segment

## Dataset

| Item | Detail |
|---|---|
| File | `data/Superstore_India_Sales_RAW.csv` (raw), `data/Superstore_India_Sales_CLEANED.csv` (cleaned) |
| Size | 2,045 raw rows, 23 columns (2,000 orders after removing duplicates) |
| Period | January 2023 to September 2025 |
| Coverage | 4 regions, 11 states, multiple cities across India |
| Source | Simulated data generated for practice |

**Main columns:** Order ID, Order Date, Ship Date, Ship Mode, Customer ID and Name, Segment, Region, State, City, Category, Sub-Category, Product Name, Unit Price, Quantity, Discount, Sales, Profit, Payment Method, Sales Rep, Customer Rating.

## Data cleaning summary

The raw file was intentionally messy. Main issues and fixes:

| Issue | Fix |
|---|---|
| About 45 duplicate rows | Removed exact duplicates |
| Mixed date formats (`dd-mm-yyyy`, `mm/dd/yyyy`, `12 Mar 2024`, `yyyy/mm/dd`) | Standardized to a single date format |
| Inconsistent text (casing, extra spaces, variants like "Tech", "Office Supply") | Trimmed whitespace and mapped to standard categories |
| Old city names (Bombay, Calcutta, Bangalore) | Standardized to Mumbai, Kolkata, Bengaluru |
| Missing values in Sales, Quantity, Profit, City | Handled using filtering or documented rules |
| Discount as both `0.1` and `10%` | Converted to a consistent decimal |
| Currency symbols in Sales (`₹`) | Removed and converted to numbers |
| Negative quantities | Corrected to positive values |
| Ship dates before order dates | Flagged and corrected or excluded |
| Extreme Sales outliers | Reviewed and handled (document your choice) |

Full details are in [`docs/data-cleaning-log.md`](https://colab.research.google.com/drive/18ET0fyyVKyfT1UduROHadLXCvOD2wwZI).

## Calculated fields

| Field | Formula |
|---|---|
| Profit Ratio | `SUM([Profit]) / SUM([Sales])` |
| Discount Band | `IF [Discount] <= 0.1 THEN 'Low' ELSEIF [Discount] <= 0.2 THEN 'Medium' ELSE 'High' END` |
| Selected Metric | `CASE [Metric Selector] WHEN 'Sales' THEN SUM([Sales]) WHEN 'Profit' THEN SUM([Profit]) WHEN 'Quantity' THEN SUM([Quantity]) END` |

## Project structure

```
tableau-sales-performance-dashboard/
├── README.md
├── data/
│   ├── Superstore_India_Sales_RAW.csv
│   └── Superstore_India_Sales_CLEANED.csv
├── dashboard/
│   └── Sales_Performance_Dashboard.twbx
├── images/
│   └── dashboard-preview.png
└── docs/
    ├── data-cleaning-log.md
    └── data-dictionary.md
```

## How to open the project

1. Download `dashboard/Sales_Performance_Dashboard.twbx`.
2. Open it in **Tableau Desktop** or **Tableau Public** (free).
3. The workbook is packaged, so the data loads automatically.

Or view the interactive version online: [Tableau Public link](https://drive.google.com/file/d/1IldO3GjK1_Ei6CoOvgqJA1umtPhY5fFK/view?usp=drive_link).

## Tools and skills

- **Tableau** (dashboard design, dual-axis charts, filled maps, parameters, actions)
- **Data cleaning and preparation**
- **Calculated fields and parameters**
- **Data storytelling**

## Author

**DEV SAHU**
[LinkedIn](www.linkedin.com/in/sahudev) 

Feedback and suggestions are welcome.
