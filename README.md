## Basics 

```
USE sql_store; 
SELECT * FROM customers 
WHERE state = ‘CA’ 
ORDER BY first_name 
LIMIT 3; 

```

* SQL is not a case-sensitive language.
* In MySQL, every statement must be terminated with a semicolon.  


## Comments 
We use comments to add notes to our code. 
—- This is a comment and it won’t get executed.

## SELECT Clause  

```
SELECT (points * 10 + 20) AS discount_factor
FROM customers 

```

Order of operations:
* Parenthesis  
* Multiplication / division 
* Addition / subtraction  

## —- Removing duplicates
```
SELECT DISTINCT state
FROM customers 

```

## WHERE Clause  

We use the WHERE clause to filter data.  
Comparison operators:  
* • Greater than: >   
* • Greater than or equal to: >= 
* • Less than: <  
* • Less than or equal to: <=  
* • Equal: = 
* • Not equal: <> 
* Not equal: !=  


## Logical Operators  

—- AND (both conditions must be True) 

```
SELECT * 
FROM customers 
WHERE birthdate > ‘1990-01-01’ AND points > 1000 

```
—- OR (at least one condition must be True) 

```
SELECT * 
FROM customers 
WHERE birthdate > ‘1990-01-01’ OR points > 1000 

```

—- NOT (to negate a condition) 

```
SELECT *
FROM customers 
WHERE NOT (birthdate > ‘1990-01-01’)

```

## IN Operator 

—- Returns customers in any of these states: VA, NY, CA

```
SELECT * 
FROM customers 
WHERE state IN (‘VA’, ‘NY’, ‘CA’)

```

## BETWEEN Operator 

```
SELECT * 
FROM customers 
WHERE points BETWEEN 100 AND 200

```

## LIKE Operator
—- Returns customers whose first name starts with b 

```
SELECT *
FROM customers 
WHERE first_name LIKE ‘b%’

```

* %: any number of characters 
* _: exactly one character 

## REGEXP Operator 
—- Returns customers whose first name starts with a 
```
SELECT * 
FROM customers  
WHERE first_name REGEXP ‘^a’

```
* ^: beginning of a string 
* $: end of a string 
* |: logical OR  
* [abc]: match any single characters 
* [a-d]: any characters from a to d 

## More Examples

—- Returns customers whose first name ends with EY or ON 
```
WHERE first_name REGEXP ‘ey$|on$’

```
—- Returns customers whose first name starts with MY 
—- or contains SE

```
WHERE first_name REGEXP ‘^my|se’

```
—- Returns customers whose first name contains B followed by  
—- R or U
```
WHERE first_name REGEXP ‘b[ru]’

```

## IS NULL Operator  

—- Returns customers who don’t have a phone number
```
SELECT *
FROM customers 
WHERE phone IS NULL

```

## ORDER BY Clause

—- Sort customers by state (in ascending order), and then
—- by their first name (in descending order) 

```
SELECT * 
FROM customers  
ORDER BY state, first_name DESC

```

## LIMIT Clause 
—- Return only 3 customers 

```
SELECT *
FROM customers  
LIMIT 3

```

—- Skip 6 customers and return 3 
```
SELECT * 
FROM customers  
LIMIT 6, 3

```

## Inner Joins
```
SELECT *
FROM customers c 
JOIN orders o  
   ON c.customer_id = o.customer_id

```  
## Exercise of Inner join with different table 

```
SELECT * 
FROM order_items oi
join products p ON oi.product_id = p.product_id

```
## Another Example

```
SELECT order_id, oi.product_id, quantity, oi.unit_price 
FROM order_items oi
join products p ON oi.product_id = p.product_id

```

## Joining Across Databases

```
USE sql_inventory;
SELECT *
FROM sql_store.order_items oi
JOIN products p
ON oi.product_id = p.product_id

```

## Self Join

```
USE sql_hr;
SELECT *
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id

```

## Another Exmaple of Self Join

```
USE sql_hr;
SELECT 
	e.employee_id,
    e.first_name,
    m.first_name AS manager
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id

```

##  Joining Multiple Table

```
USE sql_store;
SELECT *
FROM orders o 
JOIN customers c
	ON o.customer_id = c.customer_id
JOIN order_statuses os
	ON o.status = os.order_status_id

```
## Another example Of joining multiple table

```
USE sql_store;
SELECT 
	 o.order_id,
    o.order_date,
    c.first_name,
    c.last_name,
    os.name AS status
FROM orders o 
JOIN customers c
	ON o.customer_id = c.customer_id
JOIN order_statuses os
	ON o.status = os.order_status_id

```

## Exercise of joining multiple table

```
USE sql_invoicing;
SELECT *
FROM payments p
JOIN clients c
	ON p.client_id = c.client_id
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id

```

## Exercise of another joining multiple table

```
USE sql_invoicing;
SELECT 
	 p.date,
    p.invoice_id,
    p.amount,
    c.name,
    pm.name
FROM payments p
JOIN clients c
	ON p.client_id = c.client_id
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id

```

## Compound Join Conditions

```
USE sql_store;
SELECT *
FROM order_items oi
JOIN order_item_notes oin
	ON oi.order_id = oin.order_id
   AND oi.product_id = oin.product_id

```

## Outer Joins LEFT
```  
—- Return all customers whether they have any orders or not 
SELECT 
	c.customer_id,
    c.first_name,
    o.order_id
FROM customers c
LEFT JOIN orders o 
	ON c.customer_id = o.customer_id
ORDER BY c.customer_id
   
```

## Outer Joins RIGHT

```
—- Return all customers whether they have any orders or not 
SELECT 
	c.customer_id,
    c.first_name,
    o.order_id
FROM orders o
RIGHT JOIN customers c
	ON c.customer_id = o.customer_id
ORDER BY c.customer_id
   
```

## Outer Join Between Multiple Tables 

```
SELECT 
	 c.customer_id,
    c.first_name,
    o.order_id
FROM customers c
LEFT JOIN orders o 
	ON c.customer_id = o.customer_id
LEFT JOIN shippers sh
	ON o.shipper_id = sh.shipper_id
ORDER BY c.customer_id

```

## Outer Join Between Multiple Tables Exercise

```
SELECT 
	 o.order_id,
    o.order_date,
    c.first_name AS customer,
    sh.name AS shipper,
    os.name AS status
FROM orders o
JOIN customers c
	ON o.customer_id =c.customer_id
LEFT JOIN shippers sh
	ON o.shipper_id =sh.shipper_id
JOIN order_statuses os
	ON o.status = os.order_status_id

```

## outer SELF JOIN
```
USE sql_hr;
SELECT 
	 e.employee_id,
    e.first_name,
    m.first_name AS manager
FROM employees e
LEFT JOIN employees m
	ON e.reports_to = m.employee_id

```

## USING CLAUSE
```
SELECT *
FROM order_items oi
JOIN order_item_notes oin
	USING (order_id,product_id)

```

## USING Clause exercise

```
USE sql_invoicing;
SELECT 
	p.date,
    c.name AS client,
    p.amount,
    pm.name AS payment_method
    
FROM payments p
JOIN clients c USING (client_id)
JOIN payment_methods pm
	ON p.payment_method = pm.payment_method_id


```
## CROSS JOIN 

```
USE sql_store;
SELECT 
	c.first_name AS customer,
    p.name AS product
FROM customers c
CROSS JOIN products p
ORDER BY c.first_name


```

* DO a cross join between shippers and products
* Using the implicit sysntex
* and then using the explicit syntax

```
SELECT *
	sh.name AS shipper,
    p.name AS product

FROM shipper sh, products p
CROSS JOIN products p
ORDER BY sh.name

```

## UNION

```
SELECT 
	customer_id,
    first_name,
    points,
    'Bronze' AS type
FROM customers
WHERE points < 2000
UNION
SELECT 
	customer_id,
    first_name,
    points,
    'SILVER' AS type
FROM customers
WHERE points BETWEEN 2000 AND 3000


```

## INSERT TO ROWS DATA

```
INSERT INTO customers (
	first_name,
    last_name,
    birth_date,
    address,
    city,
    state)
VALUES (
    'John', 
    'Smith', 
    '1991-05-05',
	'address',
    'city',
    'CA'
    )

```

## Inserting Multiple Rows 

```
INSERT INTO products(name, quantity_in_stock, unit_price)
VALUES ('Product1',10,1.95),
	    ('Product2',11,1.95),
       ('Product3',12,1.95)

```

## Inserting Hierarchical Rows 

```
INSERT INTO orders(customer_id, order_date, status)
VALUES (1,'2022-04-04',1);

INSERT INTO order_items
VALUES
	 (LAST_INSERT_ID(), 1, 1, 2.95),
    (LAST_INSERT_ID(), 2, 1, 3.95)

```