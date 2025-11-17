# Superstore-Dashboard
## 📝 Superstore Analytics — Project Story
This project is an end-to-end Business Intelligence workflow where I worked through the entire process:
**data cleaning** → **transformation** → **SQL modeling** → **analysis** → **DAX measures** → **dashboard design in Power BI.**
My goal was to simulate the real-world responsibilities of a Data Analyst / BI Analyst and produce a dashboard that communicates clear, actionable business insight.

---

## 1.) Starting with the Raw Data
**I began with the Superstore Sales dataset — a widely used multi-dimensional retail dataset containing:**
- Order information
- Sales, profit, quantity
- Product categories & sub-categories
- Customer segments
- Shipping details
- Regional/geographical information
- Multiple time-based columns
  
**The raw file had several issues:**
- Dates stored as text
- Missing and inconsistent values
- Mixed data types
- Lack of additional analytical columns (Year, Month, Margin, etc.)
- To clean and transform it effectively, I decided to work in Python (Google Colab).

---

## 2.) Cleaning & Enriching the Data with Python
Using pandas, I performed initial EDA and data preparation.

**Key steps I completed:**

✔ Loaded the raw CSV from Google Drive

✔ Checked column types, missing values, and duplicates

✔ Converted **Order Date** and **Ship Date** into proper datetime format

✔ Created new analytical features:
- OrderYear
- OrderMonth
- OrderQuarter
- StartOfMonth (for time intelligence in Power BI)

✔ Calculated ProfitMargin with outlier handling

✔ Verified distributions for Sales and Profit

The goal was to produce a dataset that Power BI could use immediately with minimal additional cleaning.

**The cleaned dataset was exported as:**
👉 superstore_clean.csv

---

## 3.) Building Analytical Views with SQL (SQLite)

To extend the analysis further and practice SQL, I loaded the cleaned dataset into a SQLite database.

I created a **fact_sales** table and built analytical SQL views such as:

- Monthly Sales View

- Sales by Region & Category

- Customer Lifetime (basic version)

**Example query:**


SELECT "Product Name",

       SUM(Sales) AS total_sales,
       
       SUM(Profit) AS total_profit
       
FROM fact_sales

GROUP BY "Product Name"

ORDER BY total_sales DESC

LIMIT 10;



This step helped validate the cleaned data and created aggregated tables for both EDA and Power BI.

---

## 4.) Data Modeling in Power BI

I imported **superstore_clean.csv** into Power BI.

**I built:**

- A Fact Table **(fact_sales)**

- A Date Dimension **(Dim_Date)** generated through Power Query, including:

- Year

- Month

- Quarter

- StartOfMonth (link to fact table)

**Relationship:**
fact_sales[StartOfMonth] → Dim_Date[StartOfMonth]


This enables powerful **time intelligence** functions using DAX.

---

## 5.) Creating DAX Measures (KPI + Time Intelligence)

To analyze sales trends and performance, I created a set of DAX measures including:

**📌 Core KPIs**

Total Sales = SUM(fact_sales[Sales])

Total Profit = SUM(fact_sales[Profit])

Total Orders = DISTINCTCOUNT(fact_sales[Order ID])

Profit Margin % = DIVIDE([Total Profit], [Total Sales])

Average Order Value = DIVIDE([Total Sales], [Total Orders])

**📌 Time Intelligence**

Sales LY =

CALCULATE(

    [Total Sales],
    
    DATEADD(Dim_Date[StartOfMonth], -1, YEAR)
    )

Sales YoY % =

DIVIDE([Total Sales] - [Sales LY], [Sales LY])

These measures allowed me to build dynamic KPIs, YoY comparisons, and historical trends.
