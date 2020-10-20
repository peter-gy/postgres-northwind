# Exercises and solutions

## 1. Which shippers do we have?

We have a table called `shippers`. Return all the fields from shippers.

```sql
SELECT
    *
FROM shippers;
```

## 2. Certain fields from Categories

In the Categories table, selecting all the fields using this SQL:

```sql
SELECT
    *
FROM categories;
```

will return 4 columns. We only want to see two columns, category_name and description.

```sql
SELECT
    category_name,
    description
FROM categories;
```

## 3. Sales Representatives

We’d like to see just the `first_name`, `last_name`, and `hire_date` of all the employees with the title of Sales Representative. Write a SQL statement that returns only those employees.

```sql
SELECT
    first_name,
    last_name,
    hire_date
FROM employees
WHERE
    title='Sales Representative';
```

## 4. Sales Representatives in the United States

Now we’d like to see the same columns as above, but only for those employees that both have the `title` of Sales Representative, and also are in the United States.

```sql
SELECT
    first_name,
    last_name,
    hire_date
FROM employees
WHERE
    title='Sales Representative' AND country='USA';
```

## 5. Orders placed by specific `employee_id`

Show all the `orders` placed by a specific `employee`. The `employee_id` for this `employee` (Steven Buchanan) is 5.

```sql
SELECT
    *
FROM orders
WHERE
    employee_id=5;
```

## 6. `suppliers` and `contact_titles`

In the `suppliers` table, show the `supplier_id`, `contact_name`, and `contact_title` for those `suppliers` whose `contact_title` is not Marketing Manager.

```sql
SELECT
    supplier_id,
    contact_name,
    contact_title
FROM suppliers
WHERE
    contact_title!='Marketing Manager';
```

## 7. `products` with "queso" in `product_name`

```sql
SELECT
    product_id,
    product_name
FROM products
WHERE
    LOWER(product_name) LIKE '%queso%';
```

Note that the use of `LOWER` in this problem is necessary, to execute a case-insensitive search.

## 8. `orders` shipping to France or Belgium

Looking at the `orders` table, there’s a field called `ship_country`. Write a query that shows the `order_id`, `customer_id`, and `ship_country` for the orders where the `ship_country` is either France or Belgium.

```sql
SELECT
    order_id,
    customer_id,
    ship_country
FROM orders
WHERE
    ship_country='France' or ship_country='Belgium';
```

## 9. Orders shipping to any country in Latin America

Now, instead of just wanting to return all the `orders` from France of Belgium, we want to show all the orders from any Latin American country. But we don’t have a list of Latin American countries in a table in the Northwind database. So, we’re going to just use this list of Latin American countries that happen to be in the `orders` table:

- Brazil
- Mexico
- Argentina
- Venezuela

It doesn’t make sense to use multiple `OR` statements anymore, it would get too convoluted. Use the `IN` statement.

```sql
SELECT
    order_id,
    customer_id,
    ship_country
FROM orders
WHERE
    ship_country IN ('Brazil', 'Mexico', 'Argentina', 'Venezuela');
```

## 10. Employees, in order of age

For all the `employees` in the `employees` table, show the `first_name`, `last_name`, `title`, and `birth_date`. Order the results by `birth_date`, so we have the oldest `employees` first.

```sql
SELECT
    first_name,
    last_name,
    title,
    birth_date
FROM employees
ORDER BY birth_date;
```

## 11. Showing only the `date` with a `date_time` field

In the output of the query above, showing the `employees` in order of `birth_date`, we see the time of the `birth_date` field, which we don’t want. Show only the date portion of the `birth_date` field.

Not applicable to my dataset.

## 12. Employees full name

Show the `first_name` and `last_name` columns from the `employees` table, and then create a new column called `full_name`, showing `first_name` and `last_name` joined together in one column, with a space inbetween.

Using Postgres way of concat:

```sql
SELECT
    first_name || ' ' || last_name
AS full_name
FROM employees;
```

Using general way of concat:

```sql
SELECT
    CONCAT(first_name, ' ', last_name)
AS full_name
FROM employees;
```

## 13. `order_details` amount per line item

In the `order_details` table, we have the fields `unit_price` and `quantity`. Create a new field, `total_price`, that multiplies these two together. We’ll ignore the `discount` field for now.

In addition, show the `order_id`, `product_id`, `unit_price`, and `quantity`. Order by `order_id` and `product_id`.

```sql
SELECT
    order_id,
    product_id,
    unit_price,
    quantity,
    unit_price * quantity AS total_price
FROM order_details
ORDER BY
    order_id,
    product_id
```

## 14. How many customers?

How many `customers` do we have in the `customers` table? Show one value only, and don’t rely on getting the recordcount at the end of a resultset.

```sql
SELECT
    COUNT(customer_id) AS customer_count
FROM customers;
```

Note that any column from the `customers` table could be used.

## 15. When was the first order?

Show the date of the first `order` ever made in the `orders` table.

```sql
SELECT
    MIN(order_date) AS first_order
FROM orders;
```

## 16. Countries where there are customers

Show a list of countries where the Northwind company has customers.

Using `DISTINCT`:

```sql
SELECT DISTINCT
    country
FROM
    customers
ORDER BY
    country
```

Using `GROUP BY`:

```sql
SELECT
    country
FROM
    customers
GROUP BY
    country
ORDER BY
    country
```
