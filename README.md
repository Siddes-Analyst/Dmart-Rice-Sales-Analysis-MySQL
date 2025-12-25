# 🛒 Dmart-Rice-Sales-Analysis-MySQL

## 📊 Project Overview
This project analyzes D-Mart rice brand sales data using MySQL. 15 business-oriented SQL queries were solved to extract insights such as
- Sales Performance
- Revenue Contribution
- Fake Discount Detection
- Top-Performing Products
- Location-Wise Trends
  
---

## 📌 General Topics
- #### *Database_Name - D_Mart_Rice_Brand*
- #### *Table_Name - Rice_Sales*
![](Screenshots/00.png)

---
### <b> 📈 Q1. Year-wise Revenue and Profit Trend:
#### *Write a query to calculate total sales revenue, total profit, and total units sold for each year.  Order the result by profit in descending order.*

```MySQL
select Year, 
SUM(Unit_Sold) as "Unit_Sold",
SUM(Total_Selling_Price) as "Total_Sales_Revenue",
SUM(Profit) as "Profit"
FROM Rice_Sales 
group by Year order by Profit desc;
```
## 📷 Output

![](Screenshots/01.png)

---

### <b> 📈 Q2. Top 5 Most Profitable Rice Brands:
#### *Find the top 5 rice brands that generated the highest total profit across all years.*

```MySQL
select top 5 Rice_Brand,
sum(Profit) as "Total_Profit"
from Rice_Sales 
GROUP BY Rice_Brand order by Total_Profit desc;
```
## 📷 Output

![](Screenshots/02.png)

---
