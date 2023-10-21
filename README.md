# Unveiling_Data_Insights_in_Pizza_Sales_through_SQL
Leveraged SQL to extract valuable insights to fuel data-driven business strategies.

1.)	Total Revenue 

--Calculating the total revenue from the 'orders' table.
SELECT ROUND(SUM(total_price),2) AS Revenue
FROM orders
 
