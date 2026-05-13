

# Syntax 
- Create Temp Table Syntax
```postgresql
-- Create table as
CREATE TEMP TABLE new_tablename AS
-- Query results to store in the table
SELECT column1, column2
	FROM table;
```

- Select Into Syntax
```postgresql
-- Select existing columns
SELECT column1, column2
	-- Cluase to direct results to a new temp table
	INTO TEMP new_tablename
	-- Existing table with existing columns
	FROM table;
```



# Create a table
```postgresql
CREATE TEMP TABLE top_companies AS 
SELECT rank,
	title
	FROM fortune500
WHERE rank <= 10;
```



# Insert into table
```postgresql
INSERT INTO top_companies
SELECT rank, title
FROM  fortune500
WHERE rank BETWEEN 11 AND 20;
```


# Delete (drop) table
```postgresql
DROP TABLE top_companies;

DROP TABLE IF EXISTS top_companies;
```
















































