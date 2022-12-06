# Assignment 3 - Gathering, Scraping, Munging and Cleaning Data

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
6. Displaying product links that have rating more than 2.0
```sql
SELECT 
    product_link
FROM
    walmart_products
WHERE
    product_rating > 2.0;
    
 ```
    
7.  Display all the product link that is common in Walmart and target
```sql
SELECT 
    w.product_link AS walmart_product_link,
    t.product_link AS target_product_link
FROM
    walmart_products w
        INNER JOIN
    target_products t ON t.grocery_name = w.grocery_name;  
   ```
    
  8. Displaying all the categories in target and categories that is common in target and sams club
  ```sql
  SELECT 
    t.category
FROM
    target_products t
        LEFT JOIN
    samsclub_products s ON t.category = s.category;
 ```
    
    
  

