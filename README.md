# Project : Pizza Sales Analysis
### KPI’s REQUIREMENT:
We need to analyze key indicators for our pizza sales data to gain insights into our business performance. Specifically, we want to calculate the following metrics:
1.	Total Revenue: The sum of the total price of all pizza orders.
2.	Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
3.	Total Pizzas Sold: The sum of the quantities of all pizzas sold.
4.	Total Orders: The total number of orders placed.
5.	Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.
## Data Analysis using MySQL
#### A.	KPI’s
1.	Total Revenue:
```sql
SELECT SUM(total_price) AS total_revenue FROM pizza_sales;
```
2. Average Order Value:
```sql
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS avg_order_value FROM pizza_sales;
```
3.	Total Pizza Sold:
```sql
SELECT SUM(quantity) AS total_pizza_sold FROM pizza_sales;
```
4.	Total Orders:
```sql
SELECT COUNT(DISTINCT order_id) AS total_order FROM pizza_sales;
```
5.	Average Pizzas Per Order:
```sql
SELECT ROUND(SUM(quantity) / COUNT(DISTINCT order_id), 2) AS avg_pizza_per_order FROM pizza_sales;
```
#### B. Hourly Trend for Total Pizzas Sold
```sql
SELECT HOUR(order_time) AS order_hours, SUM(quantity) AS total_pizzas_sold
FROM pizza_sales
GROUP BY HOUR(order_time)
ORDER BY HOUR(order_time);
```
#### C.	Weekly Trend for Orders
```sql
SELECT WEEK(order_date, 3) AS WeekNumber, YEAR(order_date) AS Year,
      COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales
GROUP BY WEEK(order_date, 3), YEAR(order_date)
ORDER BY Year, WeekNumber;
```
#### D.	% of Sales by Pizza Category
```sql
SELECT pizza_category,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales 
GROUP BY pizza_category;
```
OR
```sql
SELECT pizza_category,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales
     WHERE MONTH(order_date) = 1), 2) AS PCT
 FROM pizza_sales
 WHERE MONTH(order_date) = 1
GROUP BY pizza_category;
```

#### E.	% of Sales by Pizza Size
```sql
SELECT pizza_size,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```
#### F.	Total Pizzas Sold by Pizza Category
```sql
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
-- WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```
#### G.	Top 5 Pizzas by Revenue
```sql
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM  pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC LIMIT 5;
```
#### H. Bottom 5 Pizzas by Revenue
```sql
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC LIMIT 5;
```
#### I. Top 5 Pizzas by Quantity
```sql
SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
 LIMIT 5;
```
#### J. Top 5 Pizzas by Total Orders
```sql
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
```
#### K. Bottom 5 Pizzas by Total Orders
```sql
SELECT 
    pizza_name, 
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
LIMIT 5;
```
## Tableau Dashboard
Created a comprehensive dashboard in Tableau featuring key metrics and charts, including Hourly Trend, Weekly Trend, Sales by Category, Sales by Size, Total Pizzas Sold by Category, Top 5 Best Sellers, and Bottom 5 Worst Sellers.
### KPI’S
-	Total Revenue
-	Total Orders 
-	Average Order Value 
-	Total Pizzas Sold
-	Average Pizzas Per Order
### DASHBOARD
  ![image](https://github.com/prathamj03/Pizza-Sales-Analysis-Project/blob/main/pizza%20sales/pizzasales1.png)
  ![image](https://github.com/prathamj03/Pizza-Sales-Analysis-Project/blob/main/pizza%20sales/pizzasales2.png)
