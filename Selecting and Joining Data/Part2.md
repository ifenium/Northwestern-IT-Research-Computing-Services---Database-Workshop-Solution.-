## Subqueries

### What films are actors with ids 129 and 195 in together?

> Wasteland Divine and License Weekend

``` sql
SELECT title 
FROM film 
WHERE film_id IN (
	SELECT film_id 
	FROM film_actor 
	WHERE actor_id=129
	AND film_id IN 
		(SELECT film_id 
		FROM film_actor 
		WHERE actor_id=195));
```


#### Challenge: How many actors are in more films than actor id 47? Hint: this takes 2 subqueries (one nested in the other). Work inside out: 1) how many films is actor 47 in; 2) which actors are in more films than this? 3) Count those actors.

> 144

``` sql 
SELECT count(actor_id) FROM 
	(SELECT actor_id, COUNT(film_id)
	FROM film_actor 
	GROUP BY actor_id
	HAVING COUNT(actor_id) > (SELECT COUNT(*)
				  FROM film_actor 
				  WHERE actor_id=47)) poo;
```


## Inner Joins 

### Select first_name, last_name, amount, and payment_date by joining the customer and payment tables. 

``` sql
SELECT first_name, last_name, amount, payment_date 
FROM customer 
INNER JOIN payment
ON payment.customer_id = customer.customer_id;
```


### Select film_id, category_id, and name from joining the film_category and category tables, only where the category_id is less than 10.

```sql
SELECT film_id, category_id, name 
FROM film_category 
INNER JOIN category 
ON film_category.category_id = category.category_id 
WHERE category_id < 10;
```
