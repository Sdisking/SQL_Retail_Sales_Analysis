### SQL_Retail_Sales_Analysis

## Project Overview**

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. thr project involves setting up a retail sales database, performing exploratory data analysis(EDA) and answering specific business questions through SQL quersies. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in sql.

## Project Structure
**1. Database Setup**

Database Creation : the project starts by creating a database named "Retail_sales_Analysis"

Table Creation : A table named "Sales_data" is created to store the sales data. the table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, Age, Product category, quantity sold, price per unit, cost of goods sold (COGS), and Total sale amount.

```sql
Create database Retail_sales_Analysis;
use Retail_sales_Analysis;
CREATE TABLE Sales_data (
    Transaction_id INT PRIMARY KEY,
    Sale_date DATE,
    Sale_time TIME,
    customer_id INT,
    gender VARCHAR(20),
    age INT,
    Category VARCHAR(20),
    Quantity INT,
    Price_per_unit FLOAT,
    cogs FLOAT,
    Total_Sale FLOAT
);
```

### 2. Data Exploration & Cleaning

**Record Count** : Determine the total number of records in the dataset.

**Customer count** : Find out how many unique customers are in the dataset.

**category count** : Identify all unique product categories in the dataset.

**Null Value Check** : Check for any null values in the dataset and delete records with missing data.

```sql
select * from Sales_data;

select transaction_id from Sales_data;

select count(*) from Sales_data;

select total_sale from sales_data where total_sale is null;
```

 ### Exploratory Questions
**How many Sales we have?**

```sql
select count(transaction_id) as Total_sales from sales_data;
```

**how many customers we have?**

```sql
select count(distinct customer_id) as Total_Customers from sales_data;
```

**how many categories we have?**

```sql
select distinct category from sales_data;
```


### My Analysis and Findings
**Q.1 Write a SQL query to retrieve all columns for sales made on '2022-11-05**

```sql
select * from sales_data where sale_date ="2022-11-05";
```

**Q.2 Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 3 in the month of Nov-2022**

```sql
SELECT 
    *
FROM
    sales_data
WHERE
    category = 'clothing'
        AND sale_date BETWEEN '2022-11-01' AND '2022-11-30'
        AND quantity > 3;
```

**Q.3 Write a SQL query to calculate the total sales (total_sale) for each category.**

```sql
SELECT 
    category, SUM(total_sale) AS Total_Sales
FROM
    sales_data
GROUP BY category;
```

**Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**

```sql
SELECT 
    category, ROUND(AVG(age), 2) AS Avg_Age
FROM
    sales_data
WHERE
    category = 'beauty';
```

**Q.5 Write a SQL query to find all transactions where the total_sale is greater than 1000.**

```sql
SELECT 
    *
FROM
    sales_data
WHERE
    total_sale > 1000;
```

**Q.6 Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**

```sql
SELECT 
    category, gender, COUNT(transaction_id) AS Total_Transaction
FROM
    sales_data
GROUP BY gender , category
ORDER BY category;
```

**Q.7 Write a SQL query to calculate the average sale for each month. Find out best selling month in each year**

```sql
select year,month,avg_sale from (select year(sale_date) as Year,
monthname(sale_date) as month,
avg(total_sale) as Avg_sale,
rank() over(partition by year(sale_date) order by avg(total_sale) desc) as ranked 
from sales_data group by 1,2) as t1 where ranked =1;
```

**Q.8 Write a SQL query to find the top 5 customers based on the highest total sales**

```sql
SELECT 
    customer_id, SUM(total_sale) AS Total_sale
FROM
    sales_data
GROUP BY customer_id
ORDER BY total_sale DESC
LIMIT 5;
```

**Q.9 Write a SQL query to find the number of unique customers who purchased items from each category.**

```sql
SELECT 
    category, COUNT(DISTINCT (customer_id)) AS Unique_customer
FROM
    sales_data
GROUP BY category;
```

**Q.10 Write a SQL query to create each shift and number of orders (Example Morning <=12, Afternoon Between 12 & 17, Evening >17)**

```sql
select 
case 
when hour(sale_time) < 12 then "Morning"
when hour(sale_time) between 12 and 17 then "afternoon"
else "Evening"
end as shift,count(transaction_id) as No_of_orders
from Sales_data group by shift;
```

## End of Project

**Author - Suraj Das**

This is the first project in my portfolio, showcasing the SQL skills essential for data analyst roles.
