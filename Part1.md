## Describe Commands

### 1. Get a list of the tables in the database.

``` console
/dt
```


## Select

### 1. Get a list of actors with the first name Julia.

``` sql 
SELECT * 
FROM actor 
WHERE first_name = 'Julia';
```

### 2. Get a list of actors with the first name Chris, Cameron, or Cuba.

``` sql 
SELECT * 
FROM actor 
WHERE first_name IN ('Chris', 'Cameron', 'Cuba');
```

### 3. Select the row from customer for customer named Jamie Rice.
 
``` sql
SELECT * 
FROM customer
WHERE first_name = 'Jamie' AND last_name = 'Rice';
```

### 4. Select amount and payment_date from payment where the amount paid was less than $1.
``` sql 
SELECT amount, payment_date 
FROM payment 
WHERE amount < 1;
```

## Distinct

### 1. What are the different rental durations that the store allows?

``` sql 
SELECT DISTINCT rental_duration 
FROM film;
```

## Order By

### 1. What are the IDs of the last 3 customers to return a rental?

``` sql 
SELECT customer_id 
FROM rental
WHERE return_date IS NOT NULL 
ORDER BY return_date DESC LIMIT 3;
```

## Counting

### 1. How many films are rated NC-17? How many are rated PG or PG-13?

``` sql 
SELECT COUNT(*)
FROM film 
WHERE rating IN ('PG', 'PG-13');
```

```sql 
SELECT COUNT(*) 
FROM film 
WHERE rating = 'NC-17';
``` 

#### Challenge: How many different customers have entries in the rental table? 

```sql
SELECT COUNT(DISTINCT customer_id) 
FROM rental;
```

## Group By 

### 1. Does the average replacement cost of a film differ by rating?

``` sql 
SELECT AVG(replacement_cost) AS "Average Replacement Cost", rating
FROM film 
GROUP BY rating;
```


#### Challenge: Are there any customers with the same last name? 
> NO 

``` sql
SELECT COUNT(last_name), last_name
FROM customer
GROUP BY last_name
HAVING count(last_name) > 1;
```


## Functions 

### 1. What is the average rental rate of films? Can you round the result to 2 decimal places?

``` sql 
SELECT ROUND(AVG(rental_rate), 2)
FROM film;
```

#### Challenge: What is the average time that people have rentals before returning? Hint: the output you’ll get may include a number of hours > 24. You can use the function justify_interval on the result to get output that looks more like you might expect.

``` sql 
SELECT justify_interval(AVG(return_date-rental_date)) 
FROM rental;
```

#### Challenge 2:  Select the 10 actors who have the longest names (first and last name combined).

``` sql 
SELECT concat(first_name, last_name), length(concat(first_name, last_name))
FROM actor
ORDER BY length(concat(first_name, last_name)) DESC
LIMIT 10;
```

## Count, Group, and Order

### 1. Which film (id) has the most actors? Which actor (id) is in the most films?

``` sql
SELECT COUNT(actor_id), film_id
FROM film_actor
GROUP BY film_id
ORDER BY COUNT(actor_id) DESC;
```
> film_id: 508

``` sql 
SELECT COUNT(film_id), actor_id
FROM film_actor
GROUP BY actor_id
ORDER BY COUNT(film_id) DESC;
```
> actor_id: 107 
