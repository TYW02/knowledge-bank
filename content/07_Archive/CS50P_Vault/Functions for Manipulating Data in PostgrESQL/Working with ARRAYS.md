

# Before we get started
- CREATE TABLE example
```postgresql
CREATE TABLE my_first_table (
	first_column text,
	second_column integer
);
```
- INSERT example
```postgresql
INSERT INTO my_first_table
	(first_column, second_column) VALUES ('text value', 12);
```



# ARRAY a special type
Let's create a simple table with 2 array columns.
```postgresql
CREATE TABLE grades (
	student_id int, 
	email text[][].
	test_scores int[]
);
```



# INSERT statements with ARRAYS
- Example INSERT statement:
```postgresql
INSERT INTO grades
	VALUES (1,
	'{{"work", "work1@datacamp.com"}, {"other", "other1@datacamp.com"}}',
	'{92, 85, 96, 88}');
```



# Accessing ARRAYs
```postgresql
SELECT
	email[1][1] AS type
	email[1][2] AS address,
	test_scores[1]
FROM grades;
```

```postgresql
+------------------+--------------------------------+-----------------+
| type             | address                        | test_scores     |
|------------------|--------------------------------|-----------------|
| work             | work1@datacamp.com             | 92              |
| work             | work2@datacamp.com             | 76              |
+------------------+--------------------------------+-----------------+
```
Note that PostgreSQL array indexes start with one and not zero.



# Searching ARRAYs
```postgresql
SELECT
	email[1][1] AS type,
	email[1][2] AS address,
	test_scores[1]
FROM grades
WHERE email[1][1] = 'work';
```

```postgresql
+------------------+--------------------------------+-----------------+
| type             | address                        | test_scores     |
|------------------|--------------------------------|-----------------|
| work             | work1@datacamp.com             | 92              |
| work             | work2@datacamp.com             | 76              |
+------------------+--------------------------------+-----------------+
```



# ARRAY functions and operators
```postgresql
SELECT
	email[2][1] AS type,
	email[2][2] AS address,
	test_scores[1]
FROM grades
WHERE 'other' = ANY (email);
```

```postgresql
+------------------+--------------------------------+-----------------+
| type             | address                        | test_scores     |
|------------------|--------------------------------|-----------------|
| other            | other1@datacamp.com            | 92              |
| null             | null                           | 76              |
+------------------+--------------------------------+-----------------+
```


```postgresql
SELECT
	email[2][1] AS type,
	email[2][2] AS address,
	test_scores[1]
FROM grades
WHERE email @> ARRAY['other'];
```

```postgresql
+------------------+--------------------------------+-----------------+
| type             | address                        | test_scores     |
|------------------|--------------------------------|-----------------|
| other            | other1@datacamp.com            | 92              |
| null             | null                           | 76              |
+------------------+--------------------------------+-----------------+
```




















