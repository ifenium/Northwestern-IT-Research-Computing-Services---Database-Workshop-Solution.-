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
SELECT film_id, c.category_id, name 
FROM film_category AS fc
INNER JOIN category AS c
ON fc.category_id = c.category_id 
WHERE c.category_id < 10;
```

## Joining and Grouping: Customer Spending

### Get a list of the names of customers who have spent more than $150, along with their total spending.

``` sql
SELECT first_name, last_name, SUM(amount) 
FROM customer AS c
INNER JOIN payment AS p 
ON c.customer_id = p.customer_id 
GROUP BY c.first_name, c.last_name 
HAVING SUM(amount) > 150;
```

### Who is the customer with the highest average payment amount?

``` sql 
SELECT c.customer_id, first_name, last_name, AVG(amount) 
FROM customer AS c
INNER JOIN payment AS p 
ON c.customer_id = p.customer_id 
GROUP BY c.customer_id, c.first_name, c.last_name 
ORDER BY AVG(amount) DESC
LIMIT 1;
```

## Joining for Better Addresses

### Create a list of addresses that includes the name of the city instead of an ID number and the name of the country as well.

``` sql
SELECT c.city, co.country 
FROM country AS co 
INNER JOIN city AS c ON co.country_id = c.country_id
INNER JOIN address AS a ON c.city_id = a.city_id;
```

## Joining Customers, Payments, and Staff

### Join the customer and payment tables together with an inner join; select customer id, name, amount, and date and order by customer id. Then join the staff table to them as well to add the staff’s name.

``` sql
SELECT c.customer_id, 
	   c.first_name AS "Customer First Name", 
	   c.last_name AS "Customer Last Name", 
	   s.first_name AS "Staff First Name", 
	   s.last_name AS "Staff Last Name", 
	   p.amount, 
	   p.payment_date 
FROM customer AS c
INNER JOIN payment AS p ON c.customer_id = p.customer_id
INNER JOIN staff AS s ON p.staff_id = s.staff_id 
ORDER BY customer_id; 
```

## Joining and Grouping: Films and Actors

### Repeating an exercise from Part 1, but adding in information from additional tables: Which film (by title) has the most actors? Which actor (by name) is in the most films?

``` sql 
SELECT COUNT(actor_id), f.title
FROM film_actor as fc
INNER JOIN film as f 
ON fc.film_id = f.film_id
GROUP BY f.film_id
ORDER BY COUNT(actor_id) DESC
LIMIT 1; 
```
> 15 | Lambs Cincinatti

#### Challenge: Which two actors have been in the most films together? 

``` sql 


```
