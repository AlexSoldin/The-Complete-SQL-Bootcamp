# Section 5: JOINS

[SQL JOINS Explained with Venn Diagrams](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)

### AS 
- Executed at the end of the query
    - Only used in the SELECT statement and cannot be referenced in the rest of the query
```SQL
SELECT amount AS rental_price FROM payment;

SELECT SUM(amount) AS net_revenue FROM payment;

SELECT customer_id, SUM(amount) AS total_spent 
FROM payment
GROUP BY customer_id
HAVING SUM(amount) > 100; -- SUM(amount) instead of total_spent

SELECT customer_id, amount AS new_name 
FROM payment
WHERE amount > 2;
```

### Inner Joins
- Result in the set of records that match in both tables
- Intersection of the two tables
    - Order is not important as it is symmetrical
```SQL
SELECT * FROM payment
INNER JOIN customer
ON payment.customer_id = customer.customer_id;

SELECT payment_id, payment.customer_id, first_name 
FROM payment
INNER JOIN customer
ON payment.customer_id = customer.customer_id;

SELECT district, email
FROM customer
INNER JOIN address
ON address.address_id = customer.address_id
WHERE district = 'California';

WITH actor_table AS (SELECT film_id, first_name, last_name FROM actor
INNER JOIN film_actor
ON film_actor.actor_id = actor.actor_id
WHERE first_name = 'Nick' AND last_name = 'Wahlberg')
SELECT title, first_name, last_name FROM film
INNER JOIN actor_table
ON actor_table.film_id = film.film_id;

SELECT title, first_name, last_name FROM film_actor
INNER JOIN actor
ON film_actor.actor_id = actor.actor_id
INNER JOIN film
ON film_actor.film_id = film.film_id
WHERE first_name = 'Nick' AND last_name = 'Wahlberg';
```

### Full Outer Joins
- Results in the all the records from both tables
- Fills uncommon data with null values
```SQL
SELECT * FROM customer
FULL OUTER JOIN payment
ON customer.customer_id = payment.customer_id
WHERE customer.customer_id IS null
OR payment.payment_id IS null;
```

### Left Outer Joins 
- Results in the set of records that are in the left table
- If there is no match with the right table, the results are null
```SQL
SELECT film.film_id, film.title, inventory_id, store_id
FROM film
LEFT JOIN inventory ON
inventory.film_id = film.film_id
WHERE inventory.film_id IS null;
```

### Right Outer Joins 
- Same thing as a LEFT OUTER JOIN but tables are switched around
```SQL
SELECT film.film_id, film.title, inventory_id, store_id
FROM film
RIGHT JOIN inventory ON
inventory.film_id = film.film_id
WHERE inventory.film_id IS null;
```

### UNION 
- Used to combine the result set of two or more SELECT statements