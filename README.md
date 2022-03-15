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