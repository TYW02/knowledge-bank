
# Different names for the same thing ?
- Considerable overlap
- but not identical
	- There is a lot of overlap between use cases for joins, subqueries, and common table expressions. 
	- Many questions that you answer can use these techniques interchangeably without sacrificing query run time or the accuracy of your output. 
	- But these techniques are not identical.



# Differentiating Techniques

## Joins
- Combine 2+ tables
	- Simple Operations / Aggregations

## Correlated Subqueries
- Match Subqueries & tables
	- Avoid limits of joins
	- High Processing time

## Multiple/Nested Subqueries
- Muti-step transformations
	- Improve accuracy and reproducibility

## Common Table Expressions
- Organize subqueries sequentially



# So which do I use ?
- Depends on your database/question
- The technique that best allows you to:
- Use and reuse your queries



# Different Use Cases

## Joins
- 2+ Tables (What is the total sales per employee ?)


## Correlated Subqueries
- Who does each employee report to in a company ?


## Mutiple/Nested Subqueries
- What is the average deal size closed by each sales representative in the quarter ?


## Common Table Expressions
- How did the marketing, sales, growth, & engineering teams perform on key metrics ?

























