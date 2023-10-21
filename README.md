# Unveiling_Data_Insights_in_Pizza_Sales_through_SQL

Leveraged **SQL** to extract valuable insights to fuel data-driven business strategies.

**Tasks**
--------------------------------------------------------------------------------------------------------------------------
1.) What is the total revenue?

2.) What is the average order value?

3.) How many pizzas were sold in total?

4.) How many orders were placed in total?

5.) What is the average number of pizzas per order?

6.) Can you provide a daily trend for the total number of orders?

7.) Can you provide a monthly trend for the total number of orders?

8.) What is the percentage of sales contributed by each pizza category (e.g., Margherita, Pepperoni, Vegetarian)?

9.) What is the percentage of sales contributed by each pizza size (e.g., Small, Medium, Large)?

10.) What are the top 5 pizzas based on revenue generated?

11.) What are the bottom 5 pizzas based on revenue generated?

12.) What are the top 5 pizzas based on the quantity sold?

13.) What are the bottom 5 pizzas based on the quantity sold?

14.) What are the top 5 pizzas based on the total number of orders they were a part of?

15.) What are the bottom 5 pizzas based on the total number of orders they were a part of?


**Analysis**
--------------------------------------------------------------------------------------------------------------------------

1.)	**What is the total revenue?** 

--Calculating the total revenue from the 'orders' table.

**SELECT ROUND(SUM**(total_price),2) **AS** Revenue

**FROM** orders

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/34083fc9-e5eb-4bce-bc0e-b8ca1c49e278)


2.)	**What is the average order value?**

--Calculating the average value of each order in the 'orders' table.

--Step 1: Adding the total prices of all orders using SUM Function.

--Step 2: Counting the distinct order_ids.

**SELECT ROUND(SUM**(total_price) / **COUNT(DISTINCT** order_id),2) **AS** Average_Order_Value

**FROM** orders

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/d3298ba3-002a-4355-92c8-f3d17d7fc6ac)


3.)	**How many pizzas were sold in total?**

--Calculating the total pizzas sold from the 'orders' table.

**SELECT SUM**(quantity) **AS** Total_Pizzas_Sold

**FROM** orders

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/8aac627e-d464-43a3-9ff0-ef1df488ed05)


4.)	**How many orders were placed in total?**

--Calculating the total orders from the 'orders' table.

**SELECT COUNT(DISTINCT** order_id) **AS** Total_Orders

**FROM** orders
     
![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/b10bf7de-7626-4e70-a6df-5af0f34b6388)

5.)	**What is the average number of pizzas per order?**

--Calculating the Average Pizzas Per order from the 'orders' table.

--Step 1: Calculating the total quantity of orders placed.

--Step 2: Calculating the count of distinct order_id's.

**SELECT SUM**(quantity)/**COUNT(DISTINCT** order_ID) **AS** Average_Pizzas_Per_Order

**FROM** orders
         
![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/d0d5c64c-31d8-415f-a703-aade79f1a7b3)

6.)	**Daily Trend for Total Orders**

--We will use the DATENAME function to extract the day of the week from the order_date column.

--We will count the distinct order_id to identify the total orders placed.

**SELECT DATENAME**(DW, order_date) **AS** Order_Day, **COUNT(DISTINCT** order_id) **AS** Total_Orders

**FROM** orders

--As we have used an aggregate function and another column in our query, we use group by clause to obtain the results.

**GROUP BY DATENAME**(DW, order_date)

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/24822893-1cc7-4a03-9b81-07bf506846b6)


7.)	**Month trend for Total Orders**

--We will use the DATENAME function to extract the month from the orders_date column.

--We will count the distinct order_id to identify the total orders placed.

**SELECT DATENAME**(Month, order_date) **AS** Month, **COUNT(DISTINC**T order_id) **AS** Total_Orders

**FROM** orders

--As we have used an aggregate function and another column in our query, we used group by clause to obtain the results.

**GROUP BY DATENAME**(Month, order_date)

--Ordering the results of the Total_orders placed in descending order to know which month has the highest order.

**ORDER BY** Total_Orders **DESC**

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/935df269-1a86-4359-a918-053b950bc94b)

8.)	**What is the percentage of sales contributed by each pizza category ?** (

--Calculating the percentage of the total price for each pizza category relative to the overall total price of all orders.

--Selecting the pizza category and calculating the percentage.

**SELECT** pizza_category,

--Calculating the percentage as the sum of total prices for the pizza category divided by the total price of all orders.

**ROUND(SUM**(total_price) * 100 / (**SELECT SUM**(total_price) **FROM** orders), 2) **AS** Percentage_of_pizza_category

--Retrieving data from the 'orders' and 'pizza' tables.

**FROM** orders 

--Using the Left join to connect the pizza table and the orders table using the order_details_id.

**LEFT JOIN** pizza 

**ON** orders.order_details_id = pizza.order_details_id

--Grouping the results by pizza category.

**GROUP BY** pizza_category;

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/340c7c9e-2c45-4842-9f05-f693e40d7425)

9.)	**What is the percentage of sales contributed by each pizza size (e.g., Small, Medium, Large)?**

--Selecting the pizza_size and calculating the percentage of it

**SELECT** pizza_size, 

--Calculating the percentage as the sum of the total_price as per pizza size divided by the total price of all orders 

**ROUND(SUM**(total_price) * 100 / (**SELECT SUM**(total_price) **FROM** orders),2) **AS** Percentage_of_pizza_size

**FROM** orders

--Using Left join to connect the pizza and orders table using the order_details_id column

**LEFT JOIN** pizza

**ON** orders.order_details_id = pizza.order_details_id

--Grouping by pizza_size

**GROUP BY** pizza_size

--Ordering the results as per the highest order

**ORDER BY** Percentage_of_pizza_size **DESC**;
       
![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/66780955-f3b2-4e83-9a14-7dd0efbea341)

10.) **What are the top 5 pizzas based on revenue generated?**

--Selecting pizza_name and calculating the total_price from the pizza table and the orders table.

--Selecting the top 5 pizza names.

**SELECT TOP 5** pizza_name, **SUM**(total_price) **AS** Total_Revenue

**FROM** pizza

--Using Left Join to connect the orders table and pizza table using the order_details_id column.

**LEFT JOIN** orders

**ON** orders.order_details_id = pizza.order_details_id

--Grouping the results by pizza_name.

**GROUP BY** pizza_name

--Ordering the results of total_revenue in descending order.

**ORDER BY** Total_Revenue **DESC**;

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/073abda2-3d90-401f-8489-4b2d1fedf921)

11.)	**What are the bottom 5 pizzas based on revenue generated?**

--Selecting pizza_name and calculating the total_price from the pizza table and the orders table.

--Selecting the Bottom 5 pizza names # Here we won't be ordering with DESC.

**SELECT TOP 5** pizza_name, **ROUND(SUM**(total_price),2) **AS** Total_Revenue

**FROM** pizza

--Using Left Join to connect the orders table and pizza table using the order_details_id column.

**LEFT JOIN** orders

**ON** orders.order_details_id = pizza.order_details_id

--Grouping the results by pizza_name.

**GROUP BY** pizza_name

--Ordering the results of total_revenue in ascending order.

**ORDER BY** Total_Revenue ASC;

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/d2e550f3-b23f-4c69-8792-d7f9acc12bb7)

12.)	**What are the top 5 pizzas based on the quantity sold?**

--Selecting pizza_name and calculating the total_quantity from the pizza table and the orders table.

--Selecting the Top 5 pizza names.

**SELECT TOP 5** pizza_name, **SUM**(quantity) **AS** Total_Quantity

**FROM** pizza

--Using Left Join to connect the orders table and pizza table using the order_details_id column.

**LEFT JOIN** orders

**ON** orders.order_details_id = pizza.order_details_id

--Grouping the results by pizza_name.

**GROUP BY** pizza_name

--Ordering the results of total_quantity in descending order.

**ORDER BY** Total_Quantity **DESC**;

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/d042c62e-a96a-47a4-8fba-8dec5073f416)

13.)	**What are the bottom 5 pizzas based on the quantity sold?**

--Selecting pizza_name and calculating the total_quantity from the pizza table and the orders table.

--Selecting the Bottom 5 pizza names.

**SELECT TOP 5** pizza_name, **SUM**(quantity) **AS** Total_Quantity

**FROM** pizza

--Using Left Join to connect the orders table and pizza table using the order_details_id column.

**LEFT JOIN** orders

**ON** orders.order_details_id = pizza.order_details_id

--Grouping the results by pizza_name.

**GROUP BY** pizza_name

--Ordering the results of total_quantity in ascending order.

**ORDER BY** Total_Quantity **ASC**;

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/9ac61587-1e1e-4e5e-b092-6019e0e90cdf)

14.)	**What are the top 5 pizzas based on the total number of orders they were a part of?**

--Selecting pizza_name and calculating the total quantity from the pizza table and the orders table.

--Selecting the top 5 pizza names.

**SELECT TOP 5** pizza_name, **COUNT(DISTINCT** order_id) **AS** Total_orders 

--Retrieving data from the 'pizza' and 'orders' tables.

**FROM** pizza

Grouping the results by pizza_name.

**GROUP BY** pizza_name

--Ordering the results by the count of distinct orders in descending order.

--Ordering in descending order to get the top 5

**ORDER BY** Total_orders **DESC**

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/4cd35f3b-b948-40c3-9abe-9fa6a8447702)

15.)	**What are the bottom 5 pizzas based on the total number of orders they were a part of?**

--Selecting pizza_name and calculating the total quantity from the pizza table and the orders table.

--Selecting the bottom 5 pizza names.

**SELECT TOP 5** pizza_name, **COUNT(DISTINCT** order_id) **AS** Total_orders

--Retrieving data from the 'pizza' and 'orders' tables.

--Retrieving data from the 'pizza' table

**FROM** pizza 

-- Group the results by pizza_name. 

**GROUP BY** pizza_name

--Ordering the results by the count of distinct orders in descending order.

--Ordering in ascending order to get the bottom 5

**ORDER BY** Total_orders **ASC**;

![image](https://github.com/AbhishekTheAnalyst/Unveiling_Data_Insights_in_Pizza_Sales_through_SQL/assets/109465334/77aa7347-7545-48ce-869b-ee85e475fb98)
