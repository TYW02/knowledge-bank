




# The LIKE operator

## _ wildcard: Used to match exactly one character
## % wildcard: Used to match zero or more character
```postgresql
SELECT title
FROM film
WHERE title LIKE 'ELF%';
```


```postgresql
SELECT title
FROM film
WHERE title LIKE '%ELF';
```


```postgresql
SELECT title
FROM film
WHERE title LIKE '%ELF%';
```



# LIKE versus full-text search
```postgresql
SELECT title, description
FROM film
WHILE to_tsvector(title) @@ to_tsquery('elf')
```



# What is full-text search ?
#### Full text search provides a means for performing natrual language queries of text data in your database.

- Stemming
- Spelling mistakes
- Ranking



# Full-text search syntax explained
```postgresql
SELECT title, description
FROM film
WHILE to_tsvector(title) @@ to_tsquery('elf')
```

Full text search can get complex but even a basic full text search query can be a very powerful tool. The example you see here is a basic technique for querying a document, in this case the column title, to match the characters elf. 

The WHERE clause of the query uses the match operator to compare the values returned by two built-in functions to perform the search, to_tsvector and to_tsquery. 

These functions convert text and string data to a tsvector data type which is a sorted list of words that have been normalized into variants of the same word. These variants are called `lexemes`.










































