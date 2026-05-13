
# Converting Case
```postgresql
SELECT lower('abc DeFg 7-')
```

```postgresql
SELECT upper('aBc DeFg 7-')
```



# Case insensitive comparisons
```postgresql
SELECT *
FROM fruit;
```

```postgresql
SELECT *
FROM fruit
WHERE lower(fav_fruit)='apple';
```



# Case insensitive searches
```postgresql
-- USING LIKE

SELECT *
FROM fruit
-- "apple" in value
WHERE fav_fruit LIKE '%apple%';
```


```postgresql
-- USING ILIKE

SELECT *
FROM fruit
--ILIKE for case insensitive
WHERE fav_fruit ILIKE '%apple%';
```



# Trimming spaces
```postgresql
SELECT trim('   abc   ');
```
- trim or btrim: both ends
	- trim('   abc   ') = 'abc'
- rtrim: right end
	- rtrim('   abc   ') = '   abc'
- ltrim: left start
	- ltrim('   abc   ') = 'abc   '


# Trimming other values
```postgresql
SELECT trim('Wow!', '!');

SELECT trim('Wow!', '!wW')
```



# Combining functions
```postgresql
SELECT trim(lower('Wow!'), '!w');
```















































