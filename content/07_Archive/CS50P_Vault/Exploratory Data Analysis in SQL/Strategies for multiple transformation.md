

# CASE WHEN
```postgresql
-- Case for each of :, -, and |
SELECT CASE WHEN category LIKE '%: %' THEN split_part(category, ': ', 1)
			WHEN category LIKE '% - %' THEN plit_part(category, ' - ', 1)
			ELSE split_part(category, ' | ', 1)
		END AS major_category, -- alias the result
		sum(businessess) -- also select number of business
	FROM naics
	GROUP BY major_category; -- Group by categories created above
```



# Recoding table
- Original values: fruit table
![[Pasted image 20230124153707.png]]

- Standardized values: recode table
![[Pasted image 20230124153732.png]]


# Step 1: CREATE TEMP TABLE
```postgresql
CREATE TEMP TABLE recode AS
	SELECT DISTINCT fav_fruit AS original, -- original, messy values
	fav_fruit AS standardized
	FROM fruit;
```


# Step 2: UPDATE values
```postgresql
-- All rows: lower case, remove white spaces on ends

UPDATE recode
	SET standardized=trim(lower(original));
```

```postgresql
-- Specific rows: correct a misspelling

UPDATE recode
	SET standardized='banana'
WHERE standardized LIKE '%nn%';
```

```postgresql
-- All row: remove any s

UPDATE recode
	SET standardized=rtrim(standardized, 's');
```


# Step 3: JOIN original and recode tables
- Original only
```postgresql
SELECT fav_fruit, count(*)
FROM fruit
GROUP BY fav_fruit;
```


- With recoded values
```postgresql
SELECT standardized,
	count(*)
FROM fruit
	LEFT JOIN records
	ON fav_fruit=original
GROUP BY standardized;
```


# Recap
1. CREATE TEMP TABLE with original values
2. UPDATE to create standardized values
3. JOIN original data to standarized data




















































