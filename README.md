# Assignment 3 - Gathering, Scraping, Munging and Cleaning Data
#### Queries to Create Tables:
```sql
CREATE DATABASE Grocery_Recommendation_System
```
#### Queries to Add Constraints to the Tables:
#### Adding Primary Keys and Unique Key:
```sql
ALTER TABLE Grocery_Recommendation_System.merchant ADD merchant_id INT NOT NULL AUTO_INCREMENT, ADD CONSTRAINT PRIMARY KEY(merchant_id);
ALTER TABLE Grocery_Recommendation_System.merchant ADD CONSTRAINT `Merchant_id` UNIQUE (merchant_id);

ALTER TABLE walmart_branch ADD COLUMN branch_id INT NOT NULL AUTO_INCREMENT, ADD CONSTRAINT PRIMARY KEY(branch_id);
ALTER TABLE walmart_branch ADD CONSTRAINT `Branch_id` UNIQUE (branch_id);
ALTER TABLE Grocery_Recommendation_System.walmart_branch ADD COLUMN merchant_id INT;
UPDATE Grocery_Recommendation_System.walmart_branch SET merchant_id = 1

ALTER TABLE Grocery_Recommendation_System.target_branch ADD COLUMN branch_id INT NOT NULL AUTO_INCREMENT, ADD CONSTRAINT PRIMARY KEY(branch_id);
ALTER TABLE Grocery_Recommendation_System.target_branch ADD CONSTRAINT `Branch_id` UNIQUE (branch_id);
ALTER TABLE Grocery_Recommendation_System.target_branch ADD COLUMN merchant_id INT;
UPDATE Grocery_Recommendation_System.target_branch SET merchant_id = 2

ALTER TABLE Grocery_Recommendation_System.samsclub_branch ADD COLUMN branch_id INT NOT NULL AUTO_INCREMENT, ADD CONSTRAINT PRIMARY KEY(branch_id);
ALTER TABLE Grocery_Recommendation_System.samsclub_branch ADD CONSTRAINT `Branch_id` UNIQUE (branch_id);
ALTER TABLE Grocery_Recommendation_System.samsclub_branch ADD COLUMN merchant_id INT;
UPDATE Grocery_Recommendation_System.samsclub_branch SET merchant_id = 3

ALTER TABLE Grocery_Recommendation_System.walmart_products ADD COLUMN prd_id BIGINT NOT NULL AUTO_INCREMENT, ADD CONSTRAINT PRIMARY KEY(prd_id);
ALTER TABLE Grocery_Recommendation_System.walmart_products ADD CONSTRAINT `Prd_id` UNIQUE (prd_id);

ALTER TABLE Grocery_Recommendation_System.target_products ADD COLUMN prd_id BIGINT NOT NULL AUTO_INCREMENT, ADD CONSTRAINT PRIMARY KEY(prd_id);
ALTER TABLE Grocery_Recommendation_System.target_products ADD CONSTRAINT `Prd_id` UNIQUE (prd_id);

ALTER TABLE Grocery_Recommendation_System.samsclub_products ADD COLUMN prd_id BIGINT NOT NULL AUTO_INCREMENT, ADD CONSTRAINT PRIMARY KEY(prd_id);
ALTER TABLE Grocery_Recommendation_System.samsclub_products ADD CONSTRAINT `Prd_id` UNIQUE (prd_id);
```

#### Use Cases:

1. Compare the price of variaties of mangoes available in Walmart and target

```sql
SELECT 
    walmart_products.grocery_name,
    walmart_products.product_price,
    target_products.product_price
FROM
    walmart_products
        INNER JOIN
    target_products ON walmart_products.zipcode = target_products.zipcode

```
2. Display the product ratings of walmart and target
```sql
SELECT 
    walmart_products.grocery_name,
    walmart_products.product_rating AS walmart_ratings,
    target_products.product_rating AS target_ratings
FROM
    walmart_products
        INNER JOIN
    target_products ON walmart_products.grocery_name = target_products.grocery_name;
```

3. Compare the prices of products in walmart and samsclub
```sql
SELECT 
    w.grocery_name,
    s.grocery_name,
    w.product_price,
    s.product_price
FROM
    walmart_products AS w
        INNER JOIN
    samsclub_products AS s ON w.grocery_name = s.grocery_name

```
4. List the groceries at target and walmart at 02338
```sql
SELECT 
    w.name AS walmart_groceries,
    t.name AS target_groceries,
    w.zipcode
FROM
    walmart_products AS w
        JOIN
    target_products AS t ON w.zipcode = '02338'

```
5. List the number of stores located near zipcode “01970”
```sql
SELECT 
    COUNT(DISTINCT walmart_branch.location) AS walmart_stores,
    COUNT(DISTINCT target_branch.location) AS target_stores
FROM
    target_branch
        INNER JOIN
    walmart_branch ON target_branch.zipcode = '01970';

```

6.  Display all the product link that is common in Walmart and target
```sql
SELECT 
    w.product_link AS walmart_product_link,
    t.product_link AS target_product_link
FROM
    walmart_products w
        INNER JOIN
    target_products t ON t.grocery_name = w.grocery_name;  
   ```
    
  7. Displaying all the categories in target and categories that is common in target and sams club
  ```sql
  SELECT 
    t.category
FROM
    target_products t
        LEFT JOIN
    samsclub_products s ON t.category = s.category;
 ```
 8. Displaying product links that have rating more than 2.0
```sql
SELECT 
    product_link
FROM
    walmart_products
WHERE
    product_rating > 2.0;
    
 ```
 9.Display all female employees in target and Walmart    
```sql
SELECT 
    w.first_name, t.first_name
FROM
    walmart_employees w,
    target_employees t
WHERE
    w.gender = 'Female'
        AND t.gender = 'Female'
ORDER BY w.emp_id , t.emp_id;
    
 ```
10. Display the total count of Diary products in target
```sql
SELECT 
    COUNT(grocery_name)
FROM
    target_products
WHERE
    category = 'Diary';
```
11.Get the address that has both Sam's club and Target
```sql
SELECT t.address
FROM target_branch t
INNER JOIN samsclub_branch s
ON t.zipcode = s.zipcode;
```
12.Display the list of products and its price which is available in both Instacart and target
```sql
SELECT 
    t.grocery_name, t.product_price
FROM
    target_products t
        INNER JOIN
    instacart_products i ON i.grocery_name = t.grocery_name;
```

13.Display the product link of products available for delivery on Dec 8th in Instacart
```sql
SELECT product_link 
FROM instacart_products
WHERE distance LIKE "%Delivery by Thu%";
```

14.Get the URL for Sam's Club
```sql
SELECT merchant_url
FROM merchant
WHERE mechant_name LIKE "%Sam%";
```

15.Get the address in which both Walmart and Target is Located
```sql
SELECT w.address
FROM walmart_branch w
INNER JOIN target_branch t
ON w.zipcode = t.zipcode;
```
16.	Display the employee details of walmart employees
```sql
SELECT 
    *
FROM
    walmart_employees
        INNER JOIN
    walmart_emp_salary ON walmart_employees.empid = walmart_emp_salary.empid
```
17.Display the list of employees from instacart employees whose salary is in between 40000 and 60000
```sql
select *
from instacart_employees
inner join instacart_emp_salary on instacart_employees.empid = instacart_emp_salary.empid
where salary between 40000 and 60000

```
18.Increment the salary of the employees of target by $10000 whose age is greater than 50.
```sql
select first_name, salary,  bonus = 10000, new_salary = salary + 10000 
from target_employees
inner join target_emp_salary on target_employees.empid = target_emp_salary.empid
where age > 50

```
