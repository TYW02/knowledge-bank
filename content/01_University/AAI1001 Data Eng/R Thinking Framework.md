---
title: R Thinking Framework
tags:
  - R
---
# 1. Identify your tables
> "Which table do I need ?"
> "Do I need to join them first ?"

# 2. Identify your output
> "What column names in the output ?"
> "How many rows roughly ?"
> "Is it 1 row per group or 1 row per observation"

# 3. Identify your transformation
> "Do I need to filter ?"
> "New computed column ?"
> "Need to group and aggregate ?"
> "Need to Reshape (Pivot)"
> "Need to sort ?"

# 4. Order your verbs
> Golden Rule: Can only use what exist at that point
> Ask: "Does this step have everything it needs from previous step"

# 5. Check your output
> Right number of rows ?
> Right column names ?
> Any unexpected NAs ?
> Does it make sense in the real world ?


# Verb Ordering Rule
## Rule 1: Create before you use
> `mutate()` before`filter()` uses it
> `mutate()` before `select()` keeps it

## Rule 2: Filter rows you don't need before you aggregate
> `filter()` rows you don't need before `group_by` / `summarise()` reduces computation and avoids wrong group size
> E.g. `filter(!is.na(values))`


## Rule 3: Aggregate before you filter group
> `group_by()` + `summarise()` FIRST then `filter()` on aggregated result
> `summarise(total = sum(value)) |> filter(total >500)`


## Rule 4: Join before everything else
> Get your complete table first THEN filter, mutate, group, select
> 


## Rule 5: Select() almost always last
> Keep only what you need for the final output
> if you `select()` too early you lose column you need later.


# Mutate() vs Summarise()

## Mutate()

| name    | class | score | class_avg |
| ------- | ----- | ----- | --------- |
| Alice   | A     | 80    | 80        |
| Bob     | A     | 90    | 80        |
| Charlie | A     | 70    | 80        |
| Diana   | B     | 60    | 80        |
| Eve     | B     | 100   | 80        |
| Frank   | B     | 80    | 80        |
`mutate()`: Adds columns and keep every row
```r
students |>
	group_by(class) |>
		mutate(class_avg = mean(score))
```

### When to use
"Keep all my rows but ADD info about group"
"Compare each row to group"


## Summarise()

| class | class_avg |
| ----- | --------- |
| A     | 80        |
| B     | 80        |
- All 3 records of A collapses into 1 row

`summarise()`: Collapse group into 1 row
```r
students |>
	group_by(class) |>
		summarise(
			class_avg = mean(score)
		)
```

### When to use
"I want ONE row per group as my final output"
"I want a summary NOT individual record"