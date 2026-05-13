

# Correlation Function
```postgresql
SELECT corr(assets, equity)
	FROM fortune500;
```


# Percentile functions
```postgresql
SELECT percentile_disc(percentile) WITHIN GROUP (ORDER BY column_name)
FROM table;

-- percentile between 0 and 1
```
- Returns a value from column


```postgresql
SELECT percentile_cont(percentile) WITHIN GROUP (ORDER BY column_name)
FROM table;
```
- Interpolates between values



# Percentile examples
```postgresql
SELECT percentile_disc(.5) WITHIN GROUP (ORDER BY val),
	percentile_count(.5) WITHIN GROUP (ORDER BY val)
FROM nums;
```


# Common issues
- Error codes
	- Examples: 9, 99, -99
- Missing values codes
	- Na, NaN, N/A, # N/A
	- 0 = missing or 0 ?
- Outlier (extreme) values
	- Really high or low ?
	- Negative values ?
- Not really a number
	- Examples: zip codes, survey response categories






















































