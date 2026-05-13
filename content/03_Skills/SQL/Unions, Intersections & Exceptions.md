#UNION #INTERSECT #EXCEPT

When working with multiple tables, the `UNION` and `UNION ALL` operator allows you to append the results of one query to another assuming that they have the same column count, order and data type. If you use the `UNION` without the `ALL`, duplicate rows between the tables will be removed from the result.

```sql
SELECT column, another_column 
	FROM mytable 
UNION / UNION ALL / INTERSECT / EXCEPT 
SELECT other_column, yet_another_column 
	FROM another_table 
ORDER BY column DESC 
LIMIT n;
```


In the order of operations as defined in [Lesson 12: Order of execution](https://sqlbolt.com/lesson/select_queries_order_of_execution "SQL Lesson 12: Order of execution"), the `UNION` happens before the `ORDER BY` and `LIMIT`. It's not common to use `UNION`s, but if you have data in different tables that can't be joined and processed, it can be an alternative to making multiple queries on the database.

Similar to the `UNION`, the `INTERSECT` operator will ensure that only rows that are identical in both result sets are returned, and the `EXCEPT` operator will ensure that only rows in the first result set that aren't in the second are returned. This means that the `EXCEPT` operator is query order-sensitive, like the `LEFT JOIN` and `RIGHT JOIN`.

Both `INTERSECT` and `EXCEPT` also discard duplicate rows after their respective operations, though some databases also support `INTERSECT ALL` and `EXCEPT ALL` to allow duplicates to be retained and returned.

# What is it used for ?

The `UNION` operator is used to combine the result-set of two or more `SELECT` statements

Requirements for `UNION`:
- Every `SELECT` statement within `UNION` must have the same number of columns
- The columns must also have similar data types
- The columns in every `SELECT` statement must also be in the same order



# What is SQL INTERSECT ?

The `INTERSECT` clause combine 2 `SELECT` statements but the dataset returned by the `INTERSECT` statement will be the intersection of the data sets of the 2 `SELECT` statement
- `INTERSECT` will return only those rows that will be common to both of the `SELECT` statement

Key characteristics of SQL INTERSECT:
- Returns only the common rows between 2 result sets.
- Ensures uniqueness by automatically removing duplicate rows
- Requires that both SELECT statements have the same number of columns.
- The data types of corresponding columns in both queries must be compatible



# What is SQL EXCEPT

The `EXCEPT` operator is used to return the rows from the first SELECT statement that are not present in the 2nd `SELECT` statement
- Allows you to return rows that exists in the first result but not in the second
- Useful for finding records in 1 table that do not have corresponding records in another table
- EXCEPT automatically removes duplicates, while EXCEPT ALL retains duplicates
- Requires both queries to have the same number of columns and compatible data types
- NOT supported in MySQL, while NOT IN can be used as an alternative
- Use EXCEPT when you need to exclude certain rows efficiently from the first result set, especially in larger datasets.

















































