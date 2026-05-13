#INNERJOIN  


Database normalization is useful because it minimizes duplicate data in any single table, and allows for data in the database to grow independently of each other (ie. Types of car engines can grow independent of each type of car). 

As a trade-off, queries get slightly more complex since they have to be able to find data from different parts of the database, and performance issues can arise when working with many large tables.

In order to answer questions about an entity that has data spanning multiple tables in a normalized database, we need to learn how to write a query that can combine all that data and pull out exactly the information we need.


## Multi-table queries with JOINs

Tables that share information about a single entity need to have a _primary key_ that identifies that entity _uniquely_ across the database. One common primary key type is an auto-incrementing integer (because they are space efficient), but it can also be a string, hashed value, so long as it is unique


Using the `JOIN` clause in a query, we can combine row data across two separate tables using this unique key. The first of the joins that we will introduce is the `INNER JOIN`.
```sql
SELECT column, another_table_column, ...
FROM mytable
INNER JOIN another_table
	ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, ... ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

The `INNER JOIN` is a process that matches rows from the first table and the second table which have the **same key** (as defined by the `ON` constraint) to create a result row with the combined columns from both tables. After the tables are joined, the other clauses we learned previously are then applied.




# OUTER JOIN
#LEFTJOIN #RIGHTJOIN #FULLJOIN


`INNER JOIN` we used last lesson might not be sufficient because the resulting table only contains data that belongs in **both of the tables**.

If the two tables have asymmetric data, which can easily happen when data is entered in different stages, then we would have to use a `LEFT JOIN`, `RIGHT JOIN` or `FULL JOIN` instead to ensure that the data you need is not left out of the results.

```sql
SELECT column, another_column, ...
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table
	ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, ... ASC/DESC
LIMIT num_limit OFFSET num_offset;
```


### LEFT JOIN
When joining table A to table B, a `LEFT JOIN` simply includes rows from A regardless of whether a matching row is found in B

### RIGHT JOIN
The `RIGHT JOIN` is the same, but reversed, keeping rows in B regardless of whether a match is found in A

### FULL JOIN
Finally, a `FULL JOIN` simply means that rows from both tables are kept, regardless of whether a matching row exists in the other table.








































