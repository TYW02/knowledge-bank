


# Count Values
```postgresql
SELECT unanswered_count, count(*)
	FROM stackoverflow
WHERE tag='amazon-ebs'
GROUP BY unanswered_count
ORDER BY unanswered_count;
```



# Truncate
```postgresql
SELECT trunc(42.1256, 2);
```

```postgresql
SELECT trunc(12345, -3);
```



# Truncating and grouping
```postgresql
SELECT trunc(unanswered_count, -1) AS trunc_ua,
	count(*)
	FROM stackoverflow
WHERE tag='amazon-ebs'
GROUP BY trunc_ua -- column alias
ORDER BY trunc_ua; -- column alias
```



# Generate
```postgresql
SELECT generate_series(1, 10, 2);
```

```postgresql
SELECT generate_series(0, 1, .1);
```



# Create bins: query
```postgresql
-- Create bins
WITH bins AS (
	SELECT generate_series(30, 60, 5) AS lower,
		generate_series(35, 65, 5) AS upper),
	-- Subset data to tag of integer
	ebs AS (
		SELECT unanswered_count
			FROM stackoverflow
		WHERE tag='amazon-ebs')
-- Count values in each bin
SELECT lower, upper, count(unanswered_count)
	-- left join keeps all bins
	FROM bins
		LEFT JOIN ebs
			ON unanswered_count >= lower
			AND unanswered_count < upper
-- Group by bin bounds to create the groups
GROUP BY lower, upper
ORDER BY lower;
```









































