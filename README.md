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

## 2. Cleaning & Enriching the Data with Python
Using pandas, I performed initial EDA and data preparation.

**Key steps I completed:**

✔ Loaded the raw CSV from Google Drive

✔ Checked column types, missing values, and duplicates

✔ Converted Order Date and Ship Date into proper datetime format

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
