

# Numeric types: integer
![[Pasted image 20230124093733.png]]



# Numeric Types: decimal
![[Pasted image 20230124093756.png]]



# Division
```postgresql
-- integer division
SELECT 10/4;
```

```postgresql
-- numeric division
SELECT 10/4.0;
```



# Range: min and max
```postgresql
SELECT min(question_pct)
	FROM stackoverflow;
```

```postgresql
SELECT max(question_pct)
	FROM stackoverflow;
```



# Variance
 - Population Variance
 ```postgresql
 SELECT var_pop(question_pct)
	 FROM stackoverflow;
```

- Simple Variance
```postgresql
SELECT var_samp(question_pct)
	FROM stackoverflow;
```

```postgresql
SELECT variance(question_pct)
	FROM stackoverflow;
```



# Standard Deviation
- Sample Standard Deviation
```postgresql
SELECT stddev_samp(question_pct)
	FROM stackoverflow;
```

```postgresql
SELECT stddec(question_pct)
	FROM stackoverflow;
```


- Population Standard Deviation
```postgresql
SELECT stddev_pop(question_pct)
	FROM stackoverflow;
```



# Round
```postgresql
SELECT ROUND(42.1256, 2);
```



# Summarize by group
```postgresql
-- Summarize by group with GROUP BY
SELECT tag,
	min(question_pct),
	avg(question_pct),
	max(question_pct)
FROM stackoverflow
GROUP BY tag;
```



































