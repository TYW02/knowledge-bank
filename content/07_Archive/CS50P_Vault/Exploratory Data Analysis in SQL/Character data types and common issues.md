

# PostgreSQL character types

character(n) or char(n)
- Fixed length n
- trailing spaces ignored in comparisons

character varying(n) or varchar(n)
- variable length up to a maximum of n

text or varchar
- unlimited length



# Types of text data

### Categorical
Tues, Tueday, Mon, TH
shirts, shoes, hats, pants
satisfied, very satisfied, unsatisfied
0349-938, 1254-001, 5477-651
red, blue, green, yellow

### Unstructured Text
I really like this product. I use it every day. It's my favorite color.

We've redesigned your favorite t-shirt to make it even better. You'll love...

Four score and seven years ago our fathers brought forth on this continent, a new nation, conceived in Liverty, and dedicated to the proposition that all men are created equal...



# Grouping and Counting
```postgresql
SELECT category, -- categorical variable
	count(*) -- count rows for each category
FROM product -- table
GROUP BY category; -- categorical variable
```



# Order: most frequent values
```postgresql
SELECT category, -- categorical variable
	count(*) -- count rows for each category
FROM product -- table
GROUP BY category -- categorical variable
ORDER BY count DESC; -- show most frequent values first
```



# Order: category value
```postgresql
SELECT category, -- categorical variable
	count(*) -- count rows for each category
FROM product -- table
GROUP BY category -- categorical variable
ORDER BY category; -- order by categorical variable
```



# Common issues

### Case matters
'apple' != 'Apple'

### Empty strings aren't null
' ' != NULL

### Spaces count
'   apple   ' != 'apple'
' ' != '     '

### Punctuation differences
'to-do' != 'to-do '










































