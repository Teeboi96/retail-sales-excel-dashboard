# Retail Sales Excel Dashboard

This project is an end-to-end retail sales analysis built in **Excel Online**.  
It covers data cleaning, feature creation, PivotTables, and a final interactive-style dashboard that summarizes sales, profit, customer segments, and regional performance.

The goal was simple: start from a raw Excel file and turn it into something a manager could actually use to understand the business.

---

## 📂 Project Structure

```text
.
├── data/
│   └── retailsalescleaned.csv        # Cleaned dataset exported from Excel
├── excel/
│   └── RetailSalesDashboard.xlsx     # Main workbook (data, pivots, dashboard)
├── images/
│   ├── dashboardfull.png              # Final dashboard screenshot
│   ├── trendchart.png
│   ├── categorysales.png
│   ├── profitbycategory.png
│   ├── customertype.png
│   └── statecity.png
└── README.md
```

## 🎯 Objectives

- Clean and standardize a multi-year retail dataset.

- Create calculated fields such as Total Sales and numeric Profit.

- Build PivotTables for different analytical views:

  - Time series (Year/Month)

  - Product categories

  - Profitability

  - Customer types

  - Regions (State & City)

- Design a clean, symmetric dashboard using Excel charts.

All work was done in Excel Online, which comes with a few missing features that required workarounds (explained below).

## 🧱 Data Preparation

Key data cleaning and preparation steps:

1. Convert to Excel Table

  - Ctrl + T → "My table has headers".

  - Enables structured references and automatic expansion.

2. Freeze Headers

  - View → Freeze Panes → Freeze Top Row

  - Keeps column names visible while scrolling.

3. Date Formatting

  - Order Date and Ship Date formatted as Short Date.

  - This ensures Excel treats them as true dates instead of text.

4. Numeric Formatting

  - Financial fields (Cost Price, Retail Price, Sub Total, Order Total, Shipping Cost, Total) formatted as Number (2 decimals).

  - Discount % formatted as Percentage.

5. Standardized Sales Metric

Created a new column:

  `=[@[Retail Price]] * [@[Order Quantity]]`


This Total Sales field is used across all analysis and charts.

6. Fixing Profit Field

The original Profit Margin column actually contained profit amounts stored as text.

  - Created Profit Numeric using:

    `=VALUE([@[Profit Margin]])`


  - Formatted as Number and used this field in PivotTables.

7. Sanity Checks

  - Looked for blanks in key columns (Order No, Order Date, Product Name, Product Category, Retail Price, Order Quantity, Total Sales).

  - Verified that numeric columns contained valid numbers (no random text or extreme outliers).

  - Ensured date columns sorted chronologically, confirming they were recognized as dates.

After these steps, the dataset was consistent and ready for analysis.

## 📊 PivotTables & Analytical Views

Several PivotTables were created, each on its own sheet:

 1. Sales Trend (Year & Month)

  - Rows: Year, Month

  - Values: Total Sales
 
  ⚠️ Excel Online limitation:
  The usual Group by Month/Year option was not available for dates.

  ✅ Workaround:
  Added helper columns in the table:

   `Year  = YEAR([@[Order Date]])`
   `Month = TEXT([@[Order Date]], "MMMM")`


 2. Sales by Product Category

  - Rows: Product Category

  - Values: Total Sales (aggregation changed from COUNT to SUM in Value Field Settings).

 3. Profit by Product Category

  - Rows: Product Category

  - Values: Profit Numeric (SUM).

 4. Sales by Customer Type

  - Rows: Customer Type

  - Values: Total Sales.

 5. Sales by State

  - Rows: State

  - Values: Total Sales.

 6. Sales by City

  - Rows: City

  - Values: Total Sales.

Each PivotTable was formatted with:

 - Light PivotTable style

 - Number formatting with thousand separators

 - Clear, readable headers

These pivots feed the charts used on the dashboard.

## 📈 Dashboard & Visual Design

The Dashboard sheet brings everything together in a clean layout.

### KPI Cards

At the top of the dashboard:

 - Total Sales

 - Total Profit

 - Top Product Category

 - Top Performing State

These are displayed as “cards” with centered text and light borders for quick scanning.

### Charts

The dashboard uses six charts:

 1. Monthly Sales Trend – Line chart based on Year/Month.

 2. Sales by Product Category – Column chart.

 3. Profit by Product Category – Column chart.

 4. Sales by Customer Type – Column chart.

 5. Sales by State – Horizontal bar chart (for readability with text labels).

 6. Sales by City – Horizontal bar chart.

### Layout Choices

 - Charts arranged in a 3 × 2 grid (left and right columns, three rows).

 - Left column and right column have equal chart widths for symmetry.

 - Gridlines are removed on the dashboard sheet for a cleaner, report-style look.

 - Fonts and colors are kept minimal and consistent to keep the focus on the data, not decoration.

## ⚙️ Challenges & Workarounds

Working in Excel Online surfaced a few issues:

 1. No Date Grouping in PivotTables

   - The usual right-click → Group option for dates didn’t appear.

   - Fix: Created explicit Year and Month columns in the dataset and used them in the rows area.

 2. COUNT Instead of SUM

   - Some PivotTables defaulted to COUNT when summarizing fields.

   - Fix: Opened Value Field Settings and changed the summary function to SUM.

 3. Text-Stored Numbers

   - Profit values were stored as text, so SUM returned 0.

   - Fix: Used VALUE() to convert text to numeric and built pivots off the new column.

 4. Pivot Field List Not Updating

   - After adding new columns, PivotTables initially didn’t see them.

   - Fix: Refreshed and recreated PivotTables to ensure all fields were available.

These workarounds mirror real-world scenarios where tools have limitations but the analysis still needs to get done.

## 🔍 Key Insights (from the dashboard)

- Office Supplies is the dominant revenue category in this dataset.

- One state (e.g. NSW) clearly leads in total sales.

- Corporate customers generate the highest total sales among segments.

- Profit and sales are not evenly distributed across categories, which may inform pricing or promotion strategy.

- The time-series view shows noticeable peaks in specific months, suggesting seasonal effects.

(Note: Exact values depend on the underlying dataset and filters.)

## 🚀 How to Use This Project

   1. Download the workbook

      - Open excel/Retail_Sales_Dashboard.xlsx from this repo.

      - Click Download.

   2. Open in Excel (Desktop or Online)

      - Enable editing if prompted.

      - Navigate between sheets:

         - RetailData – main table

         - Pivot_ sheets – pivot sources

         - Dashboard – final view

   3. Modify or Extend

      - Swap in a different but similarly structured retail dataset.

      - Add more KPIs (e.g. average discount, profit margin percentage).

      - Extend visuals with slicers or additional charts.

## 🛠 Tools

- Excel Online (data cleaning, calculations, PivotTables, dashboard)

- CSV / Excel format for data

## 👤 Author

Project built by Treasure (Tee) as part of a personal analytics and dashboarding portfolio.

Feel free to open an issue or reach out if you have suggestions or questions.

