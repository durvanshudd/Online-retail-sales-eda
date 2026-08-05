# Online Retail Sales Analysis

Exploratory data analysis of the Online Retail transactional dataset (~1.07M rows), focused on revenue drivers, seasonality, customer behavior, and geographic performance.

## Objective

To clean a real-world, messy transactional dataset and answer a set of practical business questions from it:

- Which products and customers actually drive revenue?
- How does revenue move across months, days of the week, and countries?
- Do repeat customers behave differently from one-time customers?

## Dataset

- **Source:** Online Retail dataset — transaction-level records from a UK-based online retailer, Dec 2010–Dec 2011
- **Size:** 1,067,371 rows × 8 columns (raw)
- **Columns:** `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `Customer ID`, `Country`

## Data Cleaning

| Step | Rows affected |
|---|---|
| Removed fully null rows | 247,389 |
| Removed duplicate rows | 34,335 |
| Removed non-positive `Quantity` and `Price` (cancellations / adjustments) | remainder filtered |
| **Final dataset** | **779,425 rows** |

`Revenue` was derived as `Quantity × Price` for all downstream analysis.

## Key Findings

**Products**
- Highest quantity and highest revenue product: *PAPER CRAFT, LITTLE BIRDIE* (80,995 units, ~£168,470 revenue) — the same item leads on both metrics.
- Widest price range in the catalog, from £0.001 (PADS) up to £10,953 for the single most expensive listed item.

**Time trends**
- **Total** revenue peaks in **November** (pre-holiday buying) and is lowest in **February**.
- **Average order value** peaks in **January** — despite January not being a high-volume month, the orders placed are larger on average.

**Geography**
- **United Kingdom** drives the overwhelming majority of both total revenue (~£14.39M) and customer count (**5,350 unique customers**) — expected, given this is a UK-based retailer.
- **Netherlands** posts the highest *average* revenue per transaction among all countries, suggesting fewer but larger (likely wholesale) orders.
- Nigeria sits at the bottom on both total and average revenue.

**Customers**
- Customer-level revenue varies widely: the top customer (ID 12346) generated ~£77,556 in total revenue across the dataset.
- Customers were split into **Repeat** vs **One-Time** based on transaction history. Repeat customers show a visibly higher average revenue than one-time customers.

## Visuals

Six charts were generated to support the above findings:
1. UK vs Non-UK total revenue
2. Average revenue by country
3. Average revenue by month
4. Average revenue by day of week
5. Top 10 products by quantity sold
6. One-time vs repeat customer average revenue

## Tools Used

`Python`, `pandas`, `numpy`, `matplotlib`

## Limitations / Next Steps

- Revenue comparisons (e.g. repeat vs one-time customers) are based on visual/mean comparison and have not yet been validated with a statistical significance test — flagged as a follow-up.
- Extreme-quantity orders (70,000+ units) are treated as outliers but not yet traced to specific accounts to check whether they represent wholesale/B2B buying skewing the averages.
- The ~23% of rows with missing Customer ID were dropped entirely; these are not yet confirmed as guest checkouts vs. another cause.
- Next planned notebook in this series: customer segmentation (RFM-style) on the cleaned dataset.

## How to Run

```bash
pip install pandas numpy matplotlib
jupyter notebook NoteBook.ipynb
```

Place `online_retail.csv` in the same directory before running.
