# Intermediate-Assessment-Codeathon-PowerBI
Power BI Intermediate Assessment-Codeathon – Sales data cleaning, transformation, DAX calculations, interactive dashboard development, and business insights using Power BI.

## Project Overview

This repository contains my **Intermediate Assessment-Codeathon** completed as part of the *Program in AI-Driven Data Analytics*.

The project focuses on analysing sales data using Microsoft Power BI, covering data cleaning, transformation, data quality management, DAX calculations, data visualization, and interactive dashboard development.

The objective was to transform a raw sales dataset containing inconsistencies and missing values into a structured dataset and develop an interactive dashboard to identify regional order distribution, top-performing products, and profit trends over time.

## Tools & Technologies

- **Microsoft Power BI Desktop** – Data modelling, DAX calculations, and dashboard development.
- **Power Query Editor** – Data cleaning and transformation.
- **DAX (Data Analysis Expressions)** – Calculated tables, calculated columns, and measures.

## Project Workflow

### 1. Data Import & Cleaning

- Imported the raw CSV dataset into Power BI using Get Data.
- Inspected data quality using Column Quality, Column Distribution, and Column Profile.
- Handled missing text values by replacing nulls with `Unknown`.
- Handled missing numerical values using calculated replacements based on existing data relationships.
- Removed exact duplicate records and resolved repeated OrderIDs by retaining the most complete records.
- Standardised the OrderDate column using the appropriate date format and locale.
- Imputed the remaining missing OrderDate using the median date.
- Applied appropriate data types and loaded the cleaned dataset into Power BI.

### 2. Data Transformation Formulas

**Missing text values:**
```
if [CustomerName] = null
then "Unknown"
else [CustomerName]
```

The same approach was applied to the Region and Product columns.

**Missing numerical values:**
```
// Unit Price
if [UnitPrice] = null
then [Sales] / [Quantity]
else [UnitPrice]

// Sales
if [Sales] = null
then [Quantity] * [UnitPrice_Clean]
else [Sales]

// Cost
if [Cost] = null
then [Sales_Clean] - [Profit]
else [Cost]

// Profit
if [Profit] = null
then [Sales_Clean] - [Cost_Clean]
else [Profit]
```

**Duplicate record completeness check:**
```
List.NonNullCount(Record.FieldValues(_))
```

**Missing OrderDate imputation:**
```
if [OrderDate] = null
then #date(1998, 12, 15)
else [OrderDate]
```

### 3. Data Visualization & Dashboard Development

Created the following visualizations to present key sales insights:

| Visualization          | Analysis                               |
| ---------------------- | -------------------------------------- |
| Pie Chart              | Order Distribution by Region           |
| Clustered Column Chart | Top 5 Trending Products by Order Count |
| Line Chart             | Profit Trend Over Time                 |

Additional dashboard components:

- KPI Cards – Total Orders, Total Profit, and East Region Orders.
- Interactive Slicers – Region, Product, Category, and OrderDate.

### 4. DAX Calculations

**Calculated Table – East Region Orders**
```
East Region Orders =
FILTER(
    Sales_Data,
    Sales_Data[Region] = "East"
)
```

**Calculated Column – Profit Cost Difference**
```
Profit Cost Difference =
Sales_Data[Profit_Clean] - Sales_Data[Cost_Clean]
```

**Measure – Total Profit**
```
Total Profit =
SUM(Sales_Data[Profit_Clean])
```

### 5. Key Results & Insights

- Processed and cleaned the sales dataset to obtain 1,000 unique order records.
- Identified East as the region with the highest order count (263).
- Identified Monitor as the most frequently ordered product (132 orders).
- Calculated total profit of **₹5.036586**.
- Developed an interactive dashboard to analyse regional sales distribution, product demand, and profit trends.

## Project Deliverables

- Original sales dataset.
- Questions (.docx file)
- Summative Assessment_Power BI (`.pbix` file).
- Power BI Dashboard (.pdf file)
- Assessment methodology and step-by-step documentation.(.docx file)

## Conclusion

This assessment demonstrates the practical application of Power BI for data preparation, transformation, DAX-based calculations, and interactive data visualization. The project converts raw sales data into meaningful business insights that support better data-driven decision-making.

**Course:** Program in AI-Driven Data Analytics\
**Assessment:** Intermediate Assessment-Codeathon\
**Tool:** Microsoft Power BI
