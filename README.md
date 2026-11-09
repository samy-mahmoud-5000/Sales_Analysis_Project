# Sales Analysis Project - End to End

End-to-end sales analysis from messy raw data to an interactive Power BI dashboard.

## Overview
Started with 20 raw orders full of errors. After cleaning, I ended with 17 valid orders, 36K in Total Sales, and a full dashboard that answers: which month, city, customer, and product drive the sales.

## 1. Data Cleaning - SQL
- Fixed inconsistent text with TRIM() and LOWER() for CustomerName, City, Product and Category
- Replaced NULLs and 'Unknown' values with CASE WHEN
- Fixed invalid dates like 01 January 1900
- Removed invalid rows with Quantity = 0
- Created the clean table: `End_To_End_Clean`

## 2. Data Analysis - SQL
- Calculated Total Sales: `UnitPrice * Quantity * (1 - Discount)`
- Customer Segmentation with CASE WHEN: VIP if Total Sales >= 5000, else Normal
- Monthly Performance with CTE + RANK() OVER (ORDER BY Sales DESC)
- Month Classification: Golden Month (Rank 1), Silver Month (Rank 2), Normal
- Sales Level: Excellent >= 20000, Good >= 10000, Normal

## 3. Data Modeling - Power BI
Built a model with 4 tables:
- `End_To_End_Clean_FACT` - Main fact table (20 rows raw)
- `Customer_Segmentation` - VIP / Normal customers
- `order_sales` - Sales by order
- `Master_Monthly_Sales_Performance` - Monthly ranking

DAX Measures:
- Total_Sales = SUMX(FACT, UnitPrice * Quantity * (1 - Discount))
- Total_Orders = COUNT(OrderID)
- AVG_Orders = DIVIDE([Total_Sales], [Total_Orders])

## 4. Dashboard - Power BI
- KPI Cards: Total Sales 36.00K, Total Orders 17
- Sales by Month (Column Chart)
- Sales by City, by Customer, by Product (Pie Charts)
- City Slicer for interactive filtering
- Key Insights box inside the dashboard

## Key Insights
- Best Month: March with 17.5K - more than January & February together
- Top City: Cairo with 16K (44.44% of sales)
- Top Customer: Mona with 11.3K (34.77% of sales) - VIP Customer
- Best Product: Monitor with 11K (34.92% of sales)

## Tools Used
SQL Server | Power BI | DAX | Data Modeling | Data Cleaning
