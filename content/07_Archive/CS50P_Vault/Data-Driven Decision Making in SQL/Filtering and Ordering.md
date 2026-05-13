

# WHERE 
```postgresql
SELECT *
FROM customers
WHERE country = 'Italy';
```



# Operators in the WHERE clause
- Comparison operators:
	- Equal =
	- Not Equal <>
	- Less than <
	- Less than or equal to <=
	- Greater than >
	- Greater than or equal to >=
- BETWEEN operator
- IN operator
- IS NULL and IS NOT NULL operators



# Example comparison operators
```postgresql
SELECT *
FROM movies
WHERE genre <> 'Drama';
```

- Select all columns from movies where the price for renting is larger equal 2
```postgresql
SELECT *
FROM movies
WHERE renting_price >= 2;
```



# Example: BETWEEN operator
- Select all columns of customers where the date when the account was created is between 2018-01-01 and 2018-08-31
```postgresql
SELECT *
FROM customers
WHERE date_account_start BETWEEN '2018-01-01' AND '2018-09-31';
```



# Example: IN operator
```postgresql
SELECT *
FROM actors
WHERE nationality IN ('USA', 'Australia')
```



# Example: NULL operator
```postgresql
SELECT *
FROM renting
WHERE rating IS NULL
```

- Select all columns from renting where rating is not NULL
```postgresql
SELECT *
FROM renting
WHERE rating IS NOT NULL
```



# Boolean operators AND
- Select customer name and the date when they created their account for customers who are from Itay AND who created an account between 2018-01-01 and 2018-08-31
```postgresql
SELECT name, date_account_start
FROM customers
WHERE country = 'Italy'
AND date_account_start BETWEEN '2018-01-01' AND '2018-08-31';
```


# Boolean operators OR
- Select customer name and the date when they created their account for customers who are from Italy _OR_ who created an account between 2018-01-01 and 2018-08-31.
```postgresql
SELECT name, date_account_start
FROM customers
WHERE country = 'Italy'
OR date_account_start BETWEEN '2018-01-01' AND '2018-08-31';
```


# ORDER BY
- Order the result of a query by rating
```postgresql
SELECT *
FROM renting
WHERE rating IS NOT NULL
ORDER BY rating;
```



# ORDER BY ...DESC
```postgresql
SELECT *
FROM renting
WHERE rating IS NOT NULL
ORDER BY rating DESC;
```























