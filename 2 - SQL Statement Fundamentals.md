# Section 2: SQL Statement Fundamentals

### SELECT 
```SQL
SELECT first_name, last_name, email FROM customer;
```

### DISTINCT
```SQL
SELECT DISTINCT(release_year) FROM film;

SELECT DISTINCT(rental_rate) FROM film;

SELECT DISTINCT(rating) FROM film;

SELECT DISTINCT(district) FROM address;
```

### COUNT
```SQL
SELECT COUNT(*) FROM payment;

SELECT COUNT(DISTINCT(amount)) FROM payment;

SELECT COUNT(DISTINCT(district)) FROM address;
```

### SELECT WHERE
```SQL
SELECT * FROM customer 
WHERE first_name = 'Jared';

SELECT title FROM film 
WHERE rental_rate > 4 AND replacement_cost >= 19.99 AND rating='R';

SELECT COUNT(*) FROM film 
WHERE rental_rate > 4 AND replacement_cost >= 19.99 AND rating='R';

SELECT COUNT(*) FROM film 
WHERE rating='R' OR rating='PG-13';

SELECT * FROM film 
WHERE rating!='R';

SELECT email FROM customer 
WHERE first_name='Nancy' AND last_name='Thomas';

SELECT description FROM film 
WHERE title='Outlaw Hanky';

SELECT phone FROM address 
WHERE address='259 Ipoh Drive';

SELECT COUNT(*) FROM payment
WHERE amount > 5;
```

### ORDER BY
- Default is ASC
```SQL
SELECT store_id, first_name, last_name FROM customer
ORDER BY store_id, first_name ASC;

SELECT store_id, first_name, last_name FROM customer
ORDER BY store_id DESC, first_name ASC;
```

### LIMIT
```SQL
SELECT * FROM payment
LIMIT 1;

SELECT * FROM payment
WHERE amount != 0.00
ORDER BY payment_date DESC
LIMIT 5;

SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10;

SELECT title, length FROM film
ORDER BY length ASC
LIMIT 5;

SELECT title, length FROM film
ORDER BY length ASC
LIMIT 5;

SELECT COUNT(title) FROM film
WHERE length <= 50;
```

### BETWEEN
- BETWEEN is inclusive
- NOT BETWEEN is exclusive
- Date format is YYYY-MM-DD
    - Considers up to 00:00 hour mark instead of 24:00
```SQL
SELECT COUNT(*) FROM payment
WHERE amount NOT BETWEEN 8 AND 9;

SELECT COUNT(*) FROM film
WHERE rating='R' AND replacement_cost BETWEEN 5 AND 15;
```

### IN
```SQL
SELECT COUNT(*) FROM payment
WHERE amount NOT IN (0.99, 1.98, 1.99)

SELECT * FROM customer
WHERE first_name IN ('John', 'Jake', 'Julie');
```

### LIKE
- Percent %
    - Matches any sequence of characters
- Underscore _
    - Matches any single character
- LIKE is case-sensitive 
- ILIKE is case-insensitive
```SQL
SELECT * FROM customer
WHERE first_name LIKE 'J%' AND last_name LIKE 'S%';

SELECT * FROM customer
WHERE first_name ILIKE 'j%' AND last_name ILIKE 's%';

SELECT * FROM customer
WHERE first_name LIKE '_her%';

SELECT * FROM customer
WHERE first_name LIKE 'A%' AND last_name NOT LIKE 'B%'
ORDER BY last_name;

SELECT COUNT(*) FROM actor
WHERE first_name LIKE 'P%';

SELECT COUNT(*) FROM film
WHERE title LIKE '%Truman%'
```