# 📊 Star Schema Sales Dashboard — Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Star Schema](https://img.shields.io/badge/Data%20Model-Star%20Schema-blueviolet?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📌 Project Overview

This project is an **interactive sales analytics dashboard** built in Microsoft Power BI using a **Star Schema data model**. It analyzes retail sales transactions across multiple Indian states, product categories, sub-products, payment modes, and sales managers — covering the period **January 2021 to May 2021**.

The dashboard answers a core business question:

> **"Which products are selling the most, in which states, through which payment methods, and which managers are driving the most revenue — and why?"**

This is the **data analyst equivalent of a deployed web application** — just as a web developer shows a live, interactive website, this dashboard is a live, filterable report that any stakeholder can explore in a browser.

---

## 📸 **Dashboard Preview:** 

![dashboard_preview](./screenshots/dashboard_preview.png)

---

## 🗂️ Repository Structure

```
star-schema-dashboard-powerbi/
│
├── 📁 data/
│   ├── Sales_Data.xlsx          # Fact table — core transactions
│   ├── ProductTable.xlsx        # Dimension — product categories
│   ├── SubProductTable.xlsx     # Dimension — sub-products
│   ├── StateTable.xlsx          # Dimension — Indian states
│   └── Payment_Table.xlsx       # Dimension — payment modes
│
├── 📁 report/
│   └── Star_schema_Dashboard.pbix   # Power BI Desktop file
│
├── 📁 screenshots/
│   └── dashboard_preview.png    # Dashboard screenshot
│
└── README.md
```

---


## 🗃️ Data Model — Star Schema

This project uses a **Star Schema**, the industry-standard data modelling approach for analytics. One central **Fact Table** is connected to multiple **Dimension Tables**.

```
                    ┌─────────────────┐
                    │  ProductTable   │
                    │ (Product Code,  │
                    │  Product Name)  │
                    └────────┬────────┘
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
┌─────────┴──────┐  ┌────────▼────────┐  ┌──────┴──────────┐
│  StateTable    │  │   FACT TABLE    │  │ SubProductTable  │
│ (State Code,   ├──►  Sales_Data     ◄──┤ (Sub Product     │
│  State Name)   │  │                 │  │  Code, Name)     │
└────────────────┘  │ • Date          │  └─────────────────-┘
                    │ • Product Code  │
          ┌─────────┤ • Sub Product   ├──────────┐
          │         │ • State Code    │          │
┌─────────┴──────┐  │ • Payment Code  │          │
│ Payment_Table  │  │ • Order Qty     │          │
│ (Payment Code, ◄──┤ • Price         │          │
│  Description)  │  │ • Sales Amount  │          │
└────────────────┘  │ • Manager       │          │
                    └─────────────────┘          │
                                                 │
                              (Manager is stored directly in Fact Table)
```

**Why Star Schema?**
- Faster query performance in Power BI
- Cleaner, easier-to-understand relationships
- Enables efficient slicing and dicing across dimensions

---

## 📊 Dataset Description

**Time Period:** January 2021 — May 2021
**Geography:** 5 Indian States
**Transactions:** Daily sales records

### Fact Table — `Sales_Data.xlsx`

| Column | Description |
|---|---|
| `Date` | Transaction date |
| `Month` | Month name |
| `Product Code` | Links to ProductTable |
| `Sub Product Code` | Links to SubProductTable |
| `State Code` | Links to StateTable |
| `Payment Mode Code` | Links to Payment_Table |
| `Order Qty` | Number of units ordered |
| `Price` | Unit price (₹) |
| `Sales Amount` | Total revenue = Price × Qty (₹) |
| `Manager` | Sales manager responsible |

### Dimension Tables

**ProductTable** — 6 Categories: Mobile, Books, Furniture, Electronics, Fashion, Stationary

**SubProductTable** — 27 Sub-Products across all categories, including:
- Furniture: Storage, Dining Table, Chairs, Single Bed, Double Bed
- Mobile: Oppo, Apple, OnePlus, Xiaomi, Realme, Micromax, Lava
- Electronics: Refrigerator, Washing Machine, TV, Air Conditioner
- Fashion: T-Shirt, Shirt, Jeans
- Books: Master in Python, Pythonista, Excel 1000 Tricks, Python Automate Everything
- Stationary: School Set, Office Set, Color Set

**StateTable** — Gujarat, Uttar Pradesh, Maharashtra, Madhya Pradesh, Tamil Nadu

**Payment_Table** — Net Banking, Cash on Delivery, Credit Card, UPI (Unified Payment Interface), Wallet

**Sales Managers** — Kuldeep Pandey, Harshit Patel, Chahal Singh, Shashikala, Alok Sindhe

---

## 📈 Dashboard Features & Visuals

| Visual | Type | What It Shows |
|---|---|---|
| **KPI Cards** | Card | Total Sales (4M), Total Order Qty (7245), Total Price (339K) |
| **Sales by Product Name** | Bar Chart | Which product category earns the most |
| **Sales by State** | Map (Bing Maps) | Geographic distribution of sales across India |
| **Sales by Sub Product** | Horizontal Bar | Granular product-level performance |
| **Sales by Payment Mode** | Bar Chart | Which payment method drives the most revenue |
| **Sales by Manager** | Bar Chart | Individual manager performance comparison |
| **Order Qty by State** | Pie Chart | State-wise volume distribution |
| **Price by Product** | Pie Chart | Price contribution by category |
| **Date Slicer** | Range Slider | Filter entire dashboard by date range |
| **State Slicer** | Dropdown | Filter entire dashboard by state |

---

## 🔍 Problem Solved & Business Story

### ❓ The Business Problem

A retail company operating across 5 Indian states sells products in 6 categories through 5 different payment modes, managed by 5 regional sales managers. The leadership team had **no single view** of:

- Which states and products were driving revenue
- Which payment methods customers preferred
- Which managers were performing vs. underperforming
- Whether any product categories or regions were lagging

Data was scattered across multiple Excel files with no unified model. Decision-making was slow and gut-driven.

### ✅ What Was Built

A unified **Star Schema data model** was designed connecting all tables, and an interactive Power BI dashboard was built on top of it — giving leadership a **single source of truth** they could filter by state, date, product, and more.

### 📢 Key Findings & Insights

1. **Gujarat leads in sales volume** — it consistently appears as the top-performing state by both order quantity and sales amount, driven by strong performance across multiple product categories.

2. **Uttar Pradesh is the highest order-volume state** — with 2K orders, UP drives the largest quantity of transactions, suggesting a high-frequency, possibly lower-ticket market.

3. **Mobile and Books are the top revenue categories** — despite Books having lower unit prices, high order frequency pushes them near the top; Mobile drives the highest per-transaction value.

4. **T-Shirts dominate sub-product sales** — within Fashion, T-Shirts are by far the most sold sub-product, indicating strong demand in that segment.

5. **Net Banking and Cash on Delivery are the preferred payment modes** — both contribute around ₹1M each, suggesting customers are split between digital and traditional payment preferences. Wallet adoption is the lowest.

6. **Kuldeep Pandey is the top-performing manager** — leading in Sales Amount with ~₹1M+, followed closely by Harshit Patel. Alok Sindhe shows the lowest numbers, flagging a potential area for coaching or territory review.

7. **Price distribution is relatively uniform across products** — each category contributes approximately 16–17% of total price, suggesting balanced pricing strategy across the portfolio.

8. **The Jan–May 2021 window shows consistent daily activity** — no dramatic seasonal spikes, indicating steady business operations without heavy promotional cycles.

### 💼 Business Recommendations

- **Double down on Gujarat and UP** — highest volume states; focus inventory and manager bandwidth here.
- **Investigate Alok Sindhe's territory** — underperformance may be due to market conditions, product mix, or support needs.
- **Push Wallet adoption** — it's the lowest used payment mode; a small incentive campaign could improve digital payment penetration.
- **Expand Mobile sub-products** — currently only Oppo is listed; adding more SKUs like Apple and OnePlus variants could significantly grow revenue.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Power BI Desktop** | Data modelling, DAX measures, dashboard design |
| **Power Query (M Language)** | Data cleaning, column type fixes, table joins |
| **DAX** | Custom KPIs and calculated measures |
| **Microsoft Excel** | Source data (Fact + Dimension tables) |
| **Star Schema Design** | Data architecture pattern for analytics |
| **Bing Maps** | Geographic visualization by Indian state |

---

## 📐 DAX Measures Used

```dax
-- Total Sales Amount
Total Sales = SUM('Sales_Data'[Sales Amount])

-- Total Order Quantity
Total Orders = SUM('Sales_Data'[Order Qty])

-- Total Price
Total Price = SUM('Sales_Data'[Price])

-- Sales by Manager (used in bar chart)
Sales by Manager = CALCULATE([Total Sales], ALLEXCEPT('Sales_Data', 'Sales_Data'[Manager]))
```


## ❓ Frequently Asked Interview Questions About This Project

**Q: What problem did you solve?**

Ans: Fragmented sales data across 5 Excel files with no unified view. Built a Star Schema model and dashboard so management can track sales by product, state, manager, and payment mode in real time.

**Q: Why did you use a Star Schema?**

Ans: Star Schema separates facts (transactions) from dimensions (products, states, payments), which makes Power BI queries faster, relationships cleaner, and the model easier to maintain and scale.

**Q: What insights did you find?**

Ans: Gujarat leads in revenue, Kuldeep Pandey is the top manager, T-Shirts are the best-selling sub-product, and Net Banking + COD are dominant payment methods.

**Q: How is this different from just making charts in Excel?**

Ans: Power BI with a Star Schema creates a relational model — all 5 tables are connected. A single slicer (e.g., State = Gujarat) filters every visual simultaneously, which is impossible to replicate cleanly in Excel.

**Q: What would you improve if given more data?**

Ans: Add a full year of data to detect seasonality, include a customer dimension for cohort analysis, and build a forecasting model using Power BI's AI visuals.

## 📄 License

Data used in this project is a sample dataset created for educational and portfolio demonstration purposes.

---

> ⭐ If this project helped you, consider giving it a star on GitHub!w
