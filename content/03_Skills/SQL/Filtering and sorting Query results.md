#DISTINCT #ORDERBY #LIMIT


E.g.
Many different movies can be released the same year. In such cases, SQL provides a convenient way to discard rows that have a duplicate column value by using the `DISTINCT` keyword.

```sql
SELECT DISTINCT column, another_column, ...
FROM mytable
WHERE condition(s);
```
Since the `DISTINCT` keyword will blindly remove duplicate rows, we will learn in a future lesson how to discard duplicates based on specific columns using grouping and the `GROUP BY` clause.


## Ordering Results

Unlike our neatly ordered table in the last few lessons, most data in real databases are added in no particular column order. As a result, it can be difficult to read through and understand the results of a query as the size of a table increases to thousands or even millions rows.

To help with this, SQL provides a way to sort your results by a given column in ascending or descending order using the `ORDER BY` clause.

```sql
SELECT column, another_column, ...
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```
When an `ORDER BY` clause is specified, each row is sorted alpha-numerically based on the specified column's value. In some databases, you can also specify a collation to better sort data containing international text.


# Limiting results to a subset

Another clause which is commonly used with the `ORDER BY` clause are the `LIMIT` and `OFFSET` clauses, which are a useful optimization to indicate to the database the subset of the results you care about.  

The `LIMIT` will reduce the number of rows to return, and the optional `OFFSET` will specify where to begin counting the number rows from.
```sql
SELECT column, another_column, ...
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```













































