

# Determining the length of a string
```postgresql
SELECT
	title,
	CHAR_LENGTH(title)
FROM film;
```

```postgresql
SELECT
	title,
	LENGTH(title)
FROM film;
```

```postgresql
+------------------------------+-----------------------+
| title                        | CHAR_LENGTH(title)    |
|------------------------------|-----------------------|
| ACADEMY DINOSAUR             | 16                    |
| ACE GOLDFINGER               | 14                    |
| ADAPTATION HOLES             | 16                    |
+------------------------------+-----------------------+
```


# Finding the position of a character in a string
```postgresql
SELECT
	email,
	POSITION('@' IN email)
FROM customer;
```

- Returns position where '@' is located


# Parsing string data
```postgresql
SELECT
	LEFT(description, 50)
FROM film;
```
- The LEFT function allows you to extract the first 'n' characters of a string.


```postgresql
SELECT
	RIGHT(description, 50)
FROM film;
```
- RIGHT function is similar but it extracts the last 'n' character of a string.


# Extracting substrings of character data
```postgresql
SELECT
	SUBSTRING(description, 10, 50)
FROM film AS f;
```
- SUBSTRING allows us to do pretty much exactly what its name implies - extract a substring from text data.
	- The substring functions takes 3 parameters. The first is the source string or column,
	- This is followed by an integer representing the starting position of the source string or in this case the number 10. 
	- Finally, we include another integer to specify the length of the substring that we want to extract. In this case, the number 50.



# Extracting substrings of character data
```postgresql
SELECT
	SUBSTRING(email FROM 0 FOR POSITION('@' IN email))
FROM
	customer;
```


```postgresql
SELECT
	SUBSTRING(email FROM POSITION('@' IN email)+1 FOR CHAR_LENGTH(email))
FROM
	customer;
```

- In this example, we use the POSITION function as the second parameter of SUBSTRING to determine the starting position in the string and the CHAR_LENGTH to determine the last position which is a nice trick for determining the last position of a string. 
- The POSITION function will return the integer value of the position of the at sign in the string. To exclude the at sign from the result, we need to add one to the starting position.


# Extracting substrings of character data
```postgresql
SELECT
	SUBSTR(description, 10, 50)
FROM 
	film AS f;
```

























