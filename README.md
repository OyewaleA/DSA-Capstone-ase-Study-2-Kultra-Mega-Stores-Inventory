# DSA-Capstone-ase-Study-2-Kultra-Mega-Stores-Inventory

## Table of Contents
* [Description](Description)
* [Dataset Overview](Dataset-Overview)
* [File](File)
* [Tools Used](Tools-Used)
* [Analysis](Analysis)
* [Recommendations](Recommendations)
## Description
This project contains SQL analysis for Kultra Mega Stores (KMS), focused on their **Abuja division** from 2009–2012. As a Business Intelligence Analyst, your role is to provide actionable insights based on historical order data.

### Dataset Overview

The dataset includes:
- Order details: sales, shipping cost, shipping mode, and priority.
- Customer information: names, order totals.
- Timeframe: 2009–2012.

### File:

[ data/kms_orders_2009_2012.xlsx
](https://github.com/OyewaleA/DSA-Capstone-ase-Study-2-Kultra-Mega-Stores-Inventory/blob/3e0519cdce85ff844df1ae714815c13d39d21bee/KMS%20Sql%20Case%20Study.csv)

[order status](https://github.com/OyewaleA/DSA-Capstone-ase-Study-2-Kultra-Mega-Stores-Inventory/blob/main/Order_Status.csv)

### 🛠 Tools Used

- SQL (SQL Server Management Studio) [download](https://www.microsoft.com/en/sql-server/sql-server-downloads)
- Excel [download](https://microsoft-excel.en.softonic.com/download)

## Analysis

**1. Which product category had the highest sales?**
```
SELECT TOP 1 (Product_Category),
       SUM(Sales) As [Total sale]
FROM [KMS Sql Case Study]
group by Product_Category
```
**2. What are the Top 3 regions in terms of sales?**
```
SELECT TOP 3 (Region),
       SUM(Sales) As [Total sale]
FROM [KMS Sql Case Study]
group by Region
order by [Total sale] desc;
```

**bottom 3 region in terms of sale**
```
SELECT TOP 3 (Region), 
       SUM(Sales) As [Total sale]
FROM [KMS Sql Case Study]
group by Region
order by [Total sale] asc;
```


**3. What were the total sales of appliances in Ontario?**
```
select Region,
       SUM(Sales) As [Total sale]
from [KMS Sql Case Study]
where Region ='Ontario'
group by Region;
```
**4. Who are the most valuable customers, and what products or services do they typically purchase?**
```
select top 10 profit, 
       sales, 
       Product_Name, 
       Customer_Name
from [KMS Sql Case Study]
order by Profit desc;
```

**5. Which small business customer had the highest sales?**

```
select top 1 (Customer_Name),
       Customer_Segment,  
       Sales
from [KMS Sql Case Study]
where Customer_Segment = 'Small Business'
order by Sales desc;
```

## Recommendations
**How can KMS increase revenue from the bottom 10 customers**

```
select top 10 Customer_Name,
       Product_Category,
       Region,
       Shipping_Cost,
       Unit_Price,Discount
fROM [dbo].[KMS Sql Case Study]
order by Profit
```


-  reduce shipping cost and unit price

- increase discount and advert


**Is shipping cost aligned with order priority?**

```
Select ship_mode, 
     		sum (shipping_cost) as shipping_cost_per_shipping_mode, 
		     count (order_priority) as No_of_Order_priority
from [KMS Sql Case Study]
group by Ship_Mode
order by shipping_cost_per_shipping_mode;

select ship_mode,  sum(profit)  as [Total profit]
from [KMS Sql Case Study]
group by Ship_Mode;

select ship_mode,  (sum(profit) -  sum (shipping_cost)) as Revenue
from [KMS Sql Case Study]
group by Ship_Mode
```
- Base on the above analysis, i observed that people placed more orders (1146) using delivery truck as the mode of shipping than Express Air (983),
and if we subtract the Total shipping cost of each of the shipping mode from the Total profit, 
Express Air shipping mode has the profit of 1,060,144.61 compared to Delivery Truck which has the profit of 218,696.93.
Therefore the company made appropriate spending.


