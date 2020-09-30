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
```

### COUNT
```SQL
SELECT COUNT(*) FROM payment;

SELECT COUNT(DISTINCT(amount)) FROM payment;
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
```SQL

```

### IN
```SQL

```

### LIKE
```SQL

```