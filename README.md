# Mobile-Sales
This Power BI dashboard provides insights into mobile sales with KPIs on total sales (769M), transactions (4K), and quantity (19K). It highlights sales by city, day, brand, and model, along with payment methods and customer ratings. Interactive filters enable analysis by month, brand, and model.
Nice — here’s a full, structured deep-dive into your **mobile sales** Power BI dashboard (the one with tiger logo, map, KPIs and charts).

# Executive summary

Top-level KPIs show strong aggregate volume: **Total sales = 769M**, **Transactions = 4K**, **Average sale ≈ 40K**, **Total quantity = 19K**. The dashboard breaks performance down by day-of-month/day-name, city, brand and model, payment method and customer ratings — so you can spot which locations, products and days drive revenue and where quality/ratings might be a problem.

# Top KPI cards (what to read from each)

* **Total-sales (769M):** overall revenue — use as baseline for all comparisons.
* **Transaction (4K):** number of orders/receipts; combine with total sales to compute basket size.
* **Average (40K):** average sale value (TotalSales / Transactions).
* **Total-Quality (19K):** likely sum of items or quality-flagged units — verify definition (e.g., quantity vs quality score).

# Filters / slicers (left + right)

* **Month selector** (left vertical): lets you focus on a single month; good for seasonal analysis.
* **Brand / Mobile Model** slicers (right): drill into a brand or model to see its city spread, day trends, payment mix and rating profile.

# Visual-by-visual explanation

**Top-right — Total-Quality by Day (line)**

* Shows daily trend across the month for the “quality” measure (19K total). Useful to spot day-specific dips/spikes in product quality or returns. The end-of-month dip suggests either lower shipments or higher returns/quality issues on those days.

**Upper-middle — Total-sales by Day Name (area/line)**

* Aggregates sales by weekday name (Saturday → Wednesday shown). Chart shows a gentle decline across the week (e.g., \~115M → 105M). Use this to plan promotions and staffing (weekend vs weekday patterns).

**Left-center — Map: Total-sales by City**

* City bubbles show concentration of sales in metros (New Delhi, Mumbai, Bangalore, Hyderabad, Chennai, Kolkata, etc.). Bigger bubbles = higher sales. Use for geo-targeted marketing, logistics or inventory allocation.

**Lower-left — Brand table (Brand / Total-sales / Total-Quality)**

* Top brands by sales appear to be:

  * **Apple \~161.6M**
  * **Samsung \~160.0M**
  * **OnePlus \~153.7M**
  * **Vivo \~150.0M**
  * **Xiaomi \~143.8M**
* Table + map together show which brands sell best in which cities.

**Center (below day charts) — Transaction by Payment Method (donut)**

* Payment types (UPI, Debit, Credit, etc.) appear to have near-equal transaction counts (\~1K each, \~24% slices). That indicates no single dominant payment method and room for targeted payment campaigns.

**Center-right — Total-sales by Mobile Model (bar)**

* Highest-selling models (example labels shown): **iPhone SE \~60M**, **OnePlus Nord \~58M**, **Galaxy Note 20 \~56M**, **Vivo Y51 \~55M**. Useful for inventory and promotional focus.

**Far-right — Customer Ratings**

* Visual shows distribution of ratings (1–5) with counts and percentages (5-star slice is largest: \~1.49K). Use to identify models/brands with poor ratings for quality or returns investigation.

# Key findings / business insights

1. **Revenue leaders are focused in a handful of cities** — concentrate supply and promotions there.
2. **Brands are close in revenue** (Apple vs Samsung) — small shifts in share matter; track promotions closely.
3. **Top models drive a large chunk of sales** — optimize inventory, warranty and replacement policies for those SKUs.
4. **Payment mix is balanced** — consider incentives for lower-cost payment channels or loyalty offers.
5. **Day-of-week decline** suggests lower weekday demand or need for midweek promotions.
6. **Quality dips at month end** may signal fulfillment/logistic bottlenecks or returns — investigate operational logs.
7. **Ratings concentrate at top** but deeper drill (by model + city) may reveal pockets of poor satisfaction.

# Recommended actions (immediate & tactical)

* **Inventory / supply:** increase stock for iPhone SE / OnePlus Nord in top metro hubs.
* **Marketing:** run mid-week promos or flash sales to flatten the weekday decline.
* **Quality/returns:** investigate day-wise quality dips (logistics, vendor batches) and remediate.
* **Payments:** run a small discount for a strategic payment method to reduce transaction fees.
* **Customer care:** analyze 1–3 star reviews by model/city and prioritize fixes (software/returns/refund process).

# Suggested improvements to the report (UX & clarity)

* **Label units clearly** on KPI cards (e.g., “769M INR” or “769,200,000”).
* **Sort day names** properly (Mon→Sun) by adding DayOfWeek sort column in Calendar table.
* **Map:** add clustering and tooltip with revenue & units; use bubble size = total sales, color = avg rating or return rate.
* **Clarify “Total-Quality”** — is it quantity sold, quality score, or returns? Rename to `Total Quantity` if it is quantity.
* **Standardize number formatting** (M for millions or full numbers but consistent).
* **Dynamic titles** that show current slicer selections (e.g., “Total Sales — January — Apple”).
* **Make the bar chart labels readable** (rotate/trim labels or use tooltips).

# Useful DAX measures (copy/paste — adapt table/column names)

```dax
-- basic measures (replace 'Sales' and column names with your model)
Total Sales = SUM( Sales[SalesAmount] )

Total Quantity = SUM( Sales[Quantity] )

Transactions = DISTINCTCOUNT( Sales[TransactionID] )  -- or COUNTROWS if each row = transaction

Average Sale = DIVIDE( [Total Sales], [Transactions], 0 )

Average Rating = AVERAGE( Sales[CustomerRating] )

-- percent share for a payment type in donut
Payment Txns = COUNTROWS( Sales )
Payment % = DIVIDE( [Payment Txns], CALCULATE( [Payment Txns], ALL( Sales[PaymentMethod] ) ), 0 )

-- percent of 5-star ratings
Pct 5 Star = DIVIDE( CALCULATE( COUNTROWS( Sales ), Sales[CustomerRating] = 5 ), [Transactions], 0 )
```

# Tech tips (sorting & calendar)

* Create a **Calendar** table with `DayName` and `DayOfWeekNumber = WEEKDAY([Date],2)` then sort `DayName` by `DayOfWeekNumber`.
* For month slicer labels order, use MonthNumber to sort MonthName.
* For map accuracy, have Lat/Long or use city->region lookups.

# Final note

This dashboard is already strong — it gives a 360° view (KPI → geography → product → payments → ratings). The immediate wins are sharpening definitions (what exactly is Total-Quality), cleaning number formats, and adding small DAX measures for % shares and dynamic titles. If you want, I can:

* produce the **exact DAX you need** for dynamic titles, day sorting, and % measures using your column names,
* or create a **concise 340-character portfolio description** for this dashboard.

Which of those would you like next?
