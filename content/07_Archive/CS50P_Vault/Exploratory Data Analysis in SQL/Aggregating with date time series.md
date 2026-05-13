
# Generate series
```postgresql
SELECT generate_series('2018-01-01',
					  '2018-01-02',
					  '5 hours'::interval);
```



# Generate series from the beginning
```postgresql
SELECT generate_series('2018-01-31',
					  '2018-12-31',
					  '1 momnth'::interval);
```


```postgresql
-- Subtract 1 day to get end of month
SELECT generate_series('2018-02-01',
					  '2019-01-01',
					  '1 month'::interval) - '1 day'::interval;
```



# Normal aggregation
```postgresql
SELECT * FROM sales;
```

```postgresql
SELECT date_trunc('hour', date)
	AS hour,
	count(*)
GROUP BY hour
ORDER BY hour;
```


# Aggregation with series
```postgresql
-- Create the series as a table called hour_series
WITH hour_series AS (
	SELECT generate_series('2018-04-23 09:00:00', -- 9am
							'2018-04-23 14:00:00', --2pm
							'1 hour'::interval) AS hours)
-- hours from series, count date (NOT *) to count non-NULL
SELECT hours, count(date)

	-- Join series to sales data
	FROM hour_series
		LEFT JOIN sales
			ON hours=date_trunc('hour', date)
GROUP BY hours
ORDER BY hours;
```



# Aggregation with bins
```postgresql
-- Create bins
WITH bins AS (
	SELECT generate_series('2018-04-23 09:00:00',
							'2018-04-23 15:00:00',
							'3 hours'::interval) AS lower,
			generate_series('2018-04-23 12:00:00',
							'2018-04-23 18:00:00',
							'3 hours'::interval) AS upper)

-- Count value in each bin
SELECT lower, upper, count(date)

	--left join keeps all bins
	FROM bins
		LEFT JOIN sales
			ON date >= lower
			AND date < upper
-- Group by bin bounds to create the group
GROUP BY lower, upper
ORDER BY lower;
```















































