
# Lead and lag
```postgresql
SELECT date,
	lag(date) OVER (ORDER BY date),
	lead(date) OVER (ORDER BY date)
FROM sales;
```


```postgresql
SELECT date,
	date - lag(date) OVER (ORDER BY date) AS gap
FROM sales;
```


# Average time between events
```postgresql
SELECT avg(gap)
FROM (SELECT date - lag(date) OVER (ORDER BY date) AS gap
	 FROM sales) AS gaps;
```


# Chnage in a time series
```postgresql
SELECT date,
	amount,
	lag(amount) OVER (ORDER BY date),
	amount - lag(amount) OVER (ORDER BY date) AS change
FROM sales;
```



























































