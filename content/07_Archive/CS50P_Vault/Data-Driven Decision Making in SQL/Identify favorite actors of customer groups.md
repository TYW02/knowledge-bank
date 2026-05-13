

# Combining SQL statements in one query
- LEFT JOIN
- WHERE
- GROUP BY
- HAVING
- ORDER BY


# From renting records to customer and actor information

- Our question: Who is the favorite actor for a certain customer group ?

Join table renting with tables
- customers
- actsin
- actors

```postgresql
SELECT *
FROM renting AS r
LEFT JOIN customers AS c
ON r.customer_id = c.customer_id
LEFT JOIN actsin as ai
ON r.movie_id = ai.movie_id
LEFT JOIN actors AS a
ON ai.actor_id = a.actor_id;
```


# Male customers
- Actors which play most often in movies watched by male customers
```postgresql
SELECT a.name,
	COUNT(*)
FROM renting AS r
LEFT JOIN customers AS c
ON r.customer_id = c.customer_id
LEFT JOIN actsin AS ai
ON r.movie_id = ai.movie_id
LEFT JOIN actors AS a
ON ai.actor_id = a.actor_id

WHERE c.gender = 'male'
GROUP BY a.name;
```



# Who is the favorite actor ?
- Actor being watched most often
- Best average rating when being watched.

```postgresql
SELECT a.name,
	COUNT(*) AS number_views,
	AVG(R.rating) AS avg_rating
FROM renting AS r
LEFT JOIN customers AS c
ON r.customer_id = c.customer_id
LEFT JOIN actsin AS ai
ON r.movie_id = ai.movie_id
LEFT JOIN actors AS a
ON ai.actor_id = a.actor_id
```



# Add HAVING and ORDER BY
```postgresql
SELECT a.name,
	COUNT(*) AS number_views,
	AVG(R.rating) AS avg_rating
FROM renting AS r
LEFT JOIN customers AS c
ON r.customer_id = c.customer_id
LEFT JOIN actsin AS ai
ON r.movie_id = ai.movie_id
LEFT JOIN actors AS a
ON ai.actor_id = a.actor_id

WHERE c.gender = 'male'
GROUP BY a.name
HAVING AVG(r.rating) IS NOT NULL
ORDER BY avg_rating DESC, number_views DESC;
```


































