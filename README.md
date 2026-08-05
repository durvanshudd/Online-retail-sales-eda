# Online Retail Sales Analysis

Exploratory data analysis of the Online Retail transactional dataset (~1.07M rows), focused on revenue drivers, seasonality, customer behavior, and geographic performance.

## Objective

To clean a real-world, messy transactional dataset and answer a set of practical business questions from it:

- Which products and customers actually drive revenue?
- How does revenue move across months, days of the week, and countries?
- Do repeat customers behave differently from one-time customers?

## Dataset

- **Source:** This project uses the Online Retail dataset. Download it from https://www.kaggle.com/datasets/tunguz/online-retail  — transaction-level records from a UK-based online retailer, Dec 2010–Dec 2011
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
   <img width="640" height="480" alt="UK VS Non UK Comparision on basis of total Revenue" src="https://github.com/user-attachments/assets/d272ecef-3102-4a52-83dd-b564a4d14365" />
2. Average revenue by country
   <img width="1500" height="600" alt="Average Revenue of each country" src="https://github.com/user-attachments/assets/4dd4aa34-ff67-49f6-b99f-d57a8ea0e558" />
3. Average revenue by month
   <img width="1000" height="600" alt="Average Revenue per month" src="https://github.com/user-attachments/assets/b39fd70e-9393-42b7-a27a-e2211bdc6be8" />
4. Average revenue by day of week
   <img width="800" height="600" alt="Average Revenue of each day of week" src="https://github.com/user-attachments/assets/748fd7f2-d600-4067-8e25-ce99171e1d45" />
5. Top 10 products by quantity sold
   <img width="640" height="480" alt="Top 10 products by quantity" src="https://github.com/user-attachments/assets/5d277d71-d08c-4b27-a680-1b2b2dc014bc" />
6. One-time vs repeat customer average revenue
   <img width="640" height="480" alt="Customer Type VS Revenue" src="https://github.com/user-attachments/assets/de9483c6-bfba-4a75-84a7-523de08f825d" />

## Tools Used

`Python`, `pandas`, `numpy`, `matplotlib`

## Limitations / Next Steps

- Revenue comparisons (e.g. repeat vs one-time customers) are based on visual/mean comparison and have not yet been validated with a statistical significance test — flagged as a follow-up.
- Extreme-quantity orders (70,000+ units) are treated as outliers but not yet traced to specific accounts to check whether they represent wholesale/B2B buying skewing the averages.
- The ~23% of rows with missing Customer ID were dropped entirely; these are not yet confirmed as guest checkouts vs. another cause.
- Next planned notebook in this series: customer segmentation (RFM-style) on the cleaned dataset.

