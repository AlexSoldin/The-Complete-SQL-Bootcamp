# Section 10: Conditional Expressions

### CASE
- Conditional statement
```SQL
SELECT customer_id,
CASE
	WHEN (customer_id <= 100) THEN 'Premium'
	WHEN (customer_id BETWEEN 100 AND 200) THEN 'Plus'
	ELSE 'Normal'
END AS customer_class
FROM customer; 

SELECT customer_id,
CASE customer_id
	WHEN 2 THEN 'Winner'
	WHEN 5 THEN 'Second Place'
	ELSE 'Normal'
END	AS raffle_results
FROM customer; 

SELECT
SUM(CASE rental_rate
	WHEN 0.99 THEN 1
	ELSE 0
END) AS number_of_bargains,
SUM(CASE rental_rate
	WHEN 2.99 THEN 1
	ELSE 0
END) AS regular,
SUM(CASE rental_rate
	WHEN 4.99 THEN 1
	ELSE 0
END) AS premium
FROM film;

SELECT
SUM(CASE rating
	WHEN 'R' THEN 1
	ELSE 0
END) AS r,
SUM(CASE rating
	WHEN 'PG' THEN 1
	ELSE 0
END) AS pg,
SUM(CASE rating
	WHEN 'PG-13' THEN 1
	ELSE 0
END) AS pg13
FROM film;
```

### COALESCE
- Perform operations on tables with NULL values
	- If discount is NULL then 0 will be used as the default
```SQL
-- Not in the database
SELECT item, (price - COALESCE(discount, 0)) AS final
FROM table
```

### CAST
- Convert from one data type to another 
	- These conversions will need to be within reason
```SQL
SELECT CAST('5' AS INTEGER) as new_int; 

SELECT '5'::INTEGER as new_int; 

SELECT inventory_id, CHAR_LENGTH(CAST(inventory_id AS VARCHAR)) FROM rental;
```

### NULLIF
- Takes in two inputs and returns NULL if both are equal, otherwise it returns the first argument passed
```SQL
SELECT (
	SUM(CASE WHEN department = 'A' THEN 1 ELSE 0 END)/
	NULLIF(SUM(CASE WHEN department = 'B' THEN 1 ELSE 0 END), 0)
) AS department_ratio 
FROM depts
```

### Views
- Database object that is actually a stored query
```SQL
CREATE VIEW customer_info AS
SELECT first_name, last_name, address FROM customer
INNER JOIN address
ON customer.address_id = address.address_id;

SELECT * FROM customer_info;

CREATE OR REPLACE VIEW customer_info AS
SELECT first_name, last_name, address, district FROM customer
INNER JOIN address
ON customer.address_id = address.address_id;

DROP VIEW customer_info;

DROP VIEW IF EXISTS customer_info;

ALTER VIEW customer_info RENAME TO c_info;
```

### Imports and Exports
- Import does not create a table for you
	- Assumes a table is already created
```SQL

```