
SQL also supports the use of aggregate expressions (or functions) that allow you to summarize information about a group of rows of data.

With the Pixar database that you've been using, aggregate functions can be used to answer questions like, "How many movies has Pixar produced?", or "What is the highest grossing Pixar film each year?".

```sql
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, ...
FROM mytable
WHERE constraint_expression;
```

Without a specified grouping, each aggregate function is going to run on the whole set of result rows and return a single value. And like normal expressions, giving your aggregate functions an alias ensures that the results will be easier to read and process.

## Common aggregate functions

| Function                                | Description                                                                                                                                                                                     |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **COUNT(*****)**, **COUNT(**column**)** | A common function used to counts the number of rows in the group if no column name is specified. Otherwise, count the number of rows in the group with non-NULL values in the specified column. |
| **MIN(**column**)**                     | Finds the smallest numerical value in the specified column for all rows in the group.                                                                                                           |
| **MAX(**column**)**                     | Finds the largest numerical value in the specified column for all rows in the group.                                                                                                            |
| **AVG(**column)                         | Finds the average numerical value in the specified column for all rows in the group.                                                                                                            |
| **SUM(**column**)**                     | Finds the sum of all numerical values in the specified column for the rows in the group.                                                                                                        |


## Grouped aggregate functions
In addition to aggregating across all the rows, you can instead apply the aggregate functions to individual groups of data within that group (ie. box office sales for Comedies vs Action movies).  
This would then create as many results as there are unique groups defined as by the `GROUP BY` clause.
```sql
SELECT AGG_FUNC(_column_or_expression_) AS aggregate_description, … 
FROM mytable 
WHERE constraint_expression 
GROUP BY column;
```
The `GROUP BY` clause works by grouping rows that have the same value in the column specified.



# Queries with aggregates (Pt.2)

Our queries are getting fairly complex, but we have nearly introduced all the important parts of a `SELECT` query. 
One thing that you might have noticed is that if the `GROUP BY` clause is executed after the `WHERE` clause (which filters the rows which are to be grouped), then how exactly do we filter the grouped rows?

Luckily, SQL allows us to do this by adding an additional `HAVING` clause which is used specifically with the `GROUP BY` clause to allow us to filter grouped rows from the result set.
```sql
SELECT group_by_column, AGG_FUNC(_column_expression_) AS aggregate_result_alias, … 
FROM mytable 
WHERE condition 
GROUP BY column 
HAVING group_condition;
```
The `HAVING` clause constraints are written the same way as the `WHERE` clause constraints, and are applied to the grouped rows. With our examples, this might not seem like a particularly useful construct, but if you imagine data with millions of rows with different properties, being able to apply additional constraints is often necessary to quickly make sense of the data.


















































