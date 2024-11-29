# sqlpractice
Beginning of SQL journey 
# Retail Sales Analysis SQL Project

## Project Overview

**Project Title**: Retail Sales Analysis  
**Level**: Beginner  
**Database**: `p1_retail_db`

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in SQL.

## Objectives

1. **Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `p1_retail_db`.
- **Table Creation**: A table named `retail_sales` is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE DATABASE sqlpractice;

CREATE TABLE retailsales (

				    transactions_id INT PRIMARY KEY, 
         			    sale_date DATE, 
	                      	    sale_time TIME, 
				    customer_id INT,
							gender VARCHAR(15),
							age INT, 
							category VARCHAR(15),
							quantity INT, 
							price_per_unit float, 
							cogs float, 
							total_sale float
							);
--Data Cleaning
	SELECT  * 
    FROM retailsales

    WHERE 
		transactions_id is NULL
		OR 
		sale_date is NULL
		OR 
		customer_id is NULL
		OR 
		gender IS NULL
		OR
		category is NULL
		OR
		quantity is NULL
		OR
		price_per_unit is NULL
		OR
		cogs is NULL
		OR
		total_sale is NULL;
--Data Exploration 

-- How many sale we have had?

SELECT COUNT(*) 
       as total_sale FROM retailsales;

-- How many DISTINCT customers we have?

SELECT DISTINCT customer_id  
       FROM retailsales;

-- How many DISTINCT category we have?

SELECT DISTINCT category  
       FROM retailsales;

-- Data Analysis

-- 1. Write a query to retrieve all columns for sales made on 2022-11-05?

SELECT * FROM retailsales 
         WHERE sale_date = '2022-11-05';

-- Write a query to retrieve all transactions where the category is clothing and the quantity sold is more than
   10 in the month of November 2022?

SELECT * FROM retailsales
         WHERE category = 'Clothing' 
	 AND 
	TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
 	AND
	quantity >= 4;

-- Write a query to calculate total sales (total_sale) for each category 

SELECT SUM(total_sale) as totalsales,
       category
       FROM retailsales 
       GROUP BY category;

--Write a query to find the average age of customers who purchased items from the Beauty category?

SELECT 
     ROUND(AVG(age),2) as average_age
     FROM retailsales 
     WHERE category = 'Beauty';

--Write a query to find all transactons where the total_sale is greater than 1000?


SELECT *
       FROM retailsales
       WHERE total_sale > 1000;

-- Write a query to find the total number of transactions (transactions_id) made by each gender in 
   each category?

SELECT 
	   category,
	   gender, 
	   count (*) as total_no_transactions
           FROM retailsales
           GROUP BY category, gender
           ORDER BY 1;

-- Write a query to find out the average sale for each month. Find out the best selling month in each year.


SELECT * FROM
       (SELECT 
       EXTRACT (YEAR FROM sale_date) as year,
	   EXTRACT (MONTH from sale_date) as month,
	   AVG(total_sale) as avg_sale,
	   RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank 
	   FROM retailsales
	   GROUP BY 1,2
      ) as t1
	  WHERE rank = 1
	  
- Write  a query to fnd the top 5 customers based on the highest 
  total sales?

  SELECT 
          SUM(total_sale) AS sales,
 		  customer_id
		  FROM retailsales
		 GROUP BY customer_id
		 ORDER BY sales desc
		 LIMIT 5;
  
--Write a SQL query to find the number of unique customers who purchased
  iems from each category?

 
 SELECT 
          category,
 		  COUNT(DISTINCT customer_id) as distinct_customers
		  FROM retailsales
		  GROUP BY category
		  ORDER BY category, distinct_customers;
		  
-- Write a SQL query to create each shift and number of transactions done in each shift (shift as Morning, Afternoon
and Evening)

SELECT COUNT(transactions_id) AS number_of_Orders,
        CASE 
		WHEN EXTRACT (HOUR FROM sale_time) < 12 THEN 'Morning'
                WHEN EXTRACT (HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
	        ELSE 'Evening'
        END as shift
        FROM retailsales
        GROUP BY shift
	 ORDER BY shift, number_of_orders
	 
## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.

## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

## How to Use

1. **Clone the Repository**: Clone this project repository from GitHub.
2. **Set Up the Database**: Run the SQL scripts provided in the `database_setup.sql` file to create and populate the database.
3. **Run the Queries**: Use the SQL queries provided in the `analysis_queries.sql` file to perform your analysis.
4. **Explore and Modify**: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.

## Author - Zero Analyst

This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!

### Stay Updated and Join the Community

For more content on SQL, data analysis, and other data-related topics, make sure to follow me on social media and join our community:

- **YouTube**: [Subscribe to my channel for tutorials and insights](https://www.youtube.com/@zero_analyst)
- **Instagram**: [Follow me for daily tips and updates](https://www.instagram.com/zero_analyst/)
- **LinkedIn**: [Connect with me professionally](https://www.linkedin.com/in/najirr)
- **Discord**: [Join our community to learn and grow together](https://discord.gg/36h5f2Z5PK)

Thank you for your support, and I look forward to connecting with you!

