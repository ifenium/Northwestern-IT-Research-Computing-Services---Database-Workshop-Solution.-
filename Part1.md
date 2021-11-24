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


### 

``` sql 

```



### 

``` sql 

```


### 

``` sql 

```
