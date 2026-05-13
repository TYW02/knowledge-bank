

# Exploring EXTRACT(), DATE_PART() and DATE_TRUNC() functions

- Transactional timestamp precision not useful for analysis
2005-05-13 08:53:53

- Often need to extract parts of timestamps
2005 or 5 or 2 or Friday

- Or convert / truncate timestamp precision to standardize
2005-05-13 00:00:00


- EXTRACT(*field* FROM *source*)
```postgresql
SELECT EXTRACT(quarter FROM timestamp '2005-01-24 05:12:00') AS quarter;
```

- DATE_PART('field', source)
```postgresql
SELECT DATE_PART('quarter', timestamp '2005-01-24 05:12:00') AS quarter;
```



# Extracting sub-fields from timestamp data

- Transactional data from DVD Rentals *payment* table
```postgresql
SELECT * FROM payment;
```

![[Pasted image 20230121120036.png]]



# Extracting sub-fields from timestamp data
- Data from *payment* table by year and quarter 
```postgresql
SELECT
	EXTRACT(quarter FROM payment_date) AS quarter,
	EXTRACT(year FROM payment_date) AS year,
	SUM(amount) AS total_payments
FROM
	payment
GROUP BY 1, 2;
```


Results
![[Pasted image 20230121120241.png]]



# Truncating timestamps using DATE_TRUNC()
- The DATE_TRUCT() function will truncate timestamp or interval data types.

- Truncate timestamp '2005-05-21 15:30:30' by year
```postgresql
SELECT DATE_TRUNC('year', TIMESTAMP '2005-05-21 15:30:30');
```
Result:: 2005:01:01 00:00:00

- Truncate timestamp '2005-05-21 15:30:30' by month
```postgresql
SELECT DATE_TRUNC('month', TIMESTAMP '2005-05-21 15:30:30');
```
Result: 2005:05:01 00:00:00










































