# Section 3: GROUP BY Statements

### Aggregate Functions
- Only occur in the SELECT or HAVING clauses
- Functions:
    - AVG() returns average value
        - ROUND(value, decimalPoints) 
    - COUNT() returns number of values
    - MAX() returns maximum value
    - MIN() returns minimum value
    - SUM() returns sum of all values
```SQL
SELECT ROUND(AVG(replacement_cost),2) FROM film;

SELECT MAX(replacement_cost), MIN(replacement_cost) FROM film;

SELECT SUM(replacement_cost) FROM film;
```

### GROUP BY
```SQL
SELECT rating, SUM(replacement_cost) FROM film
GROUP BY rating;

SELECT rating, rental_rate, SUM(replacement_cost) AS sum_replacement FROM film
GROUP BY rating, rental_rate
ORDER BY sum_replacement;

SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC;

SELECT customer_id, COUNT(amount) FROM payment
GROUP BY customer_id
ORDER BY COUNT(amount) DESC;

SELECT staff_id, customer_id, SUM(amount) FROM payment
GROUP BY staff_id, customer_id
ORDER BY staff_id, customer_id;

SELECT DATE(payment_date), SUM(amount) FROM payment
GROUP BY DATE(payment_date)
ORDER BY SUM(amount) DESC;

SELECT staff_id, COUNT(*) FROM payment
GROUP BY staff_id;

SELECT rating, AVG(replacement_cost) FROM film
GROUP BY rating;

SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(AMOUNT) DESC
LIMIT 5;
```

### HAVING
```SQL
SELECT store_id, COUNT(customer_id) FROM customer
GROUP BY store_id
HAVING COUNT(customer_id) > 300;

SELECT customer_id, COUNT(amount) FROM payment
GROUP BY customer_id
HAVING COUNT(*) >= 40;

SELECT customer_id, SUM(amount) FROM payment
WHERE staff_id = 2
GROUP BY customer_id
HAVING SUM(amount) > 100;
```