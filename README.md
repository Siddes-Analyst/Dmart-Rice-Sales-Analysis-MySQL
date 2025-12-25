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

### <b> 📈 Q3. Location Performance Ranking:
#### *Rank all store locations based on total selling price using RANK () or DENSE_RANK ().*

```MySQL
select Location, 
sum(Total_Selling_Price) as "Total_Selling_Price",
RANK() over (order by sum(Total_Selling_Price)desc) as "Location_Rank"
from Rice_Sales 
group by Location;
```
## 📷 Output

![](Screenshots/03.png)

---

### <b> 📈 Q4. Month-wise Sales Growth Analysis:
#### For each year, calculate:
-	Current month sales
-	Previous month sales
-	Percentage growth or decline using LAG () window function

```MySQL
with Month_Wise as (
select Year, Month, 
sum(Total_Selling_Price) as Current_Month
from Rice_Sales
group by Year, Month
),
Lag_Month_Wise as (
select Year, Month, Current_Month,
LAG(Current_Month) over (partition by Year order by Month) as Previous_Month
from Month_Wise
)
select Year, Month,
Current_Month, Previous_Month,
case
when Previous_Month IS NULL or Previous_Month = 0 then Null
Else
Cast((Current_Month - Previous_Month) * 100.0/Current_Month as decimal(10,2))
end
as Percentage_Growth
from Lag_Month_Wise
order by Year, Month;
```
## 📷 Output

![](Screenshots/04.jpg)

---

### <b> 📈 Q5. Product-Level Profit Margin Analysis:
#### *Compute profit margin percentage for each product, Then display top 10 products with highest margin.*

```MySQL
select top 10 Product_Name, 
sum(Total_Selling_Price) as "Sales", 
sum(Profit) as "Profit",
cast(
(cast(sum(Profit) as decimal(10,2))
/ 
cast(sum(Total_Selling_Price) as decimal(10,2))
)* 100.0 as decimal(10,2)) as "Profit_Margin_Percentage"
from Rice_Sales
group by Product_Name
order by Profit_Margin_Percentage desc;
```
## 📷 Output

![](Screenshots/05.jpg)
