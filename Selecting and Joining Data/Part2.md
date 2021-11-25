## Subqueries

### What films are actors with ids 129 and 195 in together?

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


