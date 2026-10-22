# Olist E-Commerce Analysis (Excel)

End-to-end analysis of Brazilian e-commerce data (Olist) in Excel: **Power Query → Data Model → DAX → Pivot Tables → Interactive Dashboard**.


**[Download the Excel file]([PASTE-YOUR-LINK-HERE](https://docs.google.com/spreadsheets/d/1poq0YHqxMaI0mby6FpXPcEjhZTOQwdo7/edit?usp=sharing&ouid=114748847181758586771&rtpof=true&sd=true))**

The dashboard has 3 pages: **Sales**, **Reviews**, and **Delivery**.

---

## Key Insights

**Sales**
- Credit card is the most used payment method.
- São Paulo is the top city for seller sales.
- Heavier products cost more to ship (positive relationship between weight and freight).
- Sales grew through 2017, with a clear spike in **November 2017** (Black Friday).
- 2016 only has data from October, because data collection had just started.

**Reviews**
- Orders delivered **on time** score noticeably higher than **late** orders, so late delivery directly hurts customer satisfaction.
- Review scores stay stable across months, with no unusual spikes.

**Delivery**
- Most orders are delivered in **6–10 days**.
- The majority arrive within **15 days**.
- Delivery rate is about **97%**.
- When order volume rises sharply, delivery performance drops slightly.

---

## Project Workflow

**1. Data Cleaning (Power Query)**
- Fixed city names that contained numbers or unreadable characters (customers, sellers, geolocation).
- Removed 4 invalid rows with negative or missing prices.
- Replaced 610 missing product categories with `Unclassified`.
- Corrected invalid photo counts (one value matched against an identical product, two set to null).
- Removed duplicates in geolocation, then loaded it twice to link with both customers and sellers.
- Kept delivery-date blanks as null, since they belong to canceled or unavailable orders.
- Used `review_score` only, because review text is optional and inconsistent.

**2. Data Model**
- 9 tables connected with one-to-many relationships: Orders, Order Items, Customers, Sellers, Products, Payments, Reviews, Category Translation, and Geolocation.

**3. Calculated Columns (Orders table)**

| Column | Purpose |
|---|---|
| Purchase_Year / Purchase_Month / Month_Number | Trends by month, correctly ordered |
| Is Late | On Time vs Late |
| Delivery Days | Days from purchase to delivery |
| Delivery Bucket | Groups delivery time (0-5, 6-10, 11-15 days...) |

**4. DAX Measures**

`Total Sales` · `Total Revenue` · `Total Orders` · `Total Customers` · `Total Sellers` · `Total Reviews` · `% Late Deliveries` · `% Negative Reviews` · `Delivery Rate` · `Avg Delivery Time` · `Avg Estimated Time` · `Avg Processing Time` · `Total Delivered Orders`

Example:
```dax
Avg Delivery Time (Days) :=
AVERAGEX(
    olist_orders_dataset,
    DATEDIFF(
        olist_orders_dataset[order_purchase_timestamp],
        olist_orders_dataset[order_delivered_customer_date],
        DAY
    )
)
```

---

## Tools

Excel · Power Query · Data Model · DAX · Pivot Tables & Charts

---
