# Section 6: Advanced SQL Commands

### Timestamps
- Variable types:
    - TIME contains only time
    - DATE contains only date
    - TIMESTAMP contains date and time
    - TIMESTAMPTZ contains date, time and, timezone
- Functions:
    - TIMEZONE
    - NOW
    - TIMEOFDAY
    - CURRENT_TIME
    - CURRENT_DATE
```SQL
SHOW ALL -- Displays system runtime parameters
SHOW TIMEZONE 

SELECT NOW()
SELECT TIMEOFDAY()
SELECT CURRENT_TIME
SELECT CURRENT_DATE
```

### EXTRACT
- Obtain a sub-component of a date value
    - YEAR
    - MONTH
    - DAY 
    - WEEK
    - QUARTER
```SQL
SELECT EXTRACT(YEAR FROM payment_date) AS year 
FROM payment;

SELECT EXTRACT(MONTH FROM payment_date) AS pay_month 
FROM payment;

SELECT EXTRACT(QUARTER FROM payment_date) AS pay_quarter 
FROM payment;

SELECT COUNT(*)
FROM payment
WHERE EXTRACT(dow FROM payment_date) = 1
```

### AGE
- Calculates and returns the current age given a TIMESTAMP
```SQL
SELECT AGE(payment_date) FROM payment;
```

### TO_CHAR
- Convert data types to text
- Useful for TIMESTAMP formatting
```SQL
SELECT TO_CHAR(payment_date, 'YYYY-MM-DD') FROM payment;

SELECT TO_CHAR(payment_date, 'MONTH-YYYY') FROM payment;

SELECT TO_CHAR(payment_date, 'dd/MM/YYYY') FROM payment;

SELECT DISTINCT(TO_CHAR(payment_date, 'MONTH')) FROM payment;
```

### Mathematical Functions
[Mathematical Functions and Operators](https://www.postgresql.org/docs/9.5/functions-math.html)
```SQL
SELECT ROUND(rental_rate/replacement_cost,4)*100 AS percent_cost
FROM film;

SELECT 0.1*replacement_cost AS deposit
FROM film;
```

### String Functions
[String Functions and Operators](https://www.postgresql.org/docs/9.1/functions-string.html)
```SQL
SELECT LENGTH(first_name) FROM customer;

SELECT first_name || ' ' || last_name AS full_name 
FROM customer;

SELECT LOWER(LEFT(first_name,1)) || LOWER(last_name) || '@gmail.com' AS email 
FROM customer
```

### Subquery
- Construct complex queries
    - Performs a query on the results of another query
```SQL
SELECT title, rental_rate FROM film
WHERE rental_rate > (SELECT AVG(rental_rate) FROM film);

SELECT inventory.film_id 
FROM rental
INNER JOIN inventory 
ON inventory.inventory_id = rental.inventory_id
WHERE return_date BETWEEN '2005-05-29' AND '2005-05-30';

SELECT film_id, title FROM film
WHERE film_id IN 
(SELECT inventory.film_id 
FROM rental
INNER JOIN inventory 
ON inventory.inventory_id = rental.inventory_id
WHERE return_date BETWEEN '2005-05-29' AND '2005-05-30')
ORDER BY film_id;

SELECT first_name, last_name
FROM customer AS c
WHERE NOT EXISTS
(SELECT * FROM payment AS p
	WHERE p.customer_id = c.customer_id
	AND amount > 11);
```

### Self-Join
- Table is joined to itself
    - Useful for comparing values within the same table
```SQL
SELECT f1.title, f2.title, f1.length 
FROM film AS f1
INNER JOIN film AS f2
ON f1.film_id != f2.film_id 
AND f1.length = f2.length;
```