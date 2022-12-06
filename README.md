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
