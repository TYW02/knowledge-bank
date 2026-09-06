---
title: "R Tidyverse Quiz — Areas To Watch Out For"
subject: "AAI1001 Data Engineering and Visualization"
topics: ["tidyverse", "dplyr", "joins", "single-table queries", "group_by", "summarise"]
created: "2026-06-02"
type: "study-notes"
---

# R Tidyverse Quiz — Areas To Watch Out For

---

## 1. Verb Order In A Pipe Chain

The most common source of errors. Each verb only sees what the previous step left behind.

### The Rule
> Any column you need in a later step must not be dropped by an earlier step.

### Example Question
Will this code run?
```r
people |>
  select(fam_name, given_name, survived) |>
  mutate(death_index = age + 10)
```

**Answer:** No. `select()` dropped `age` before `mutate()` needed it. R throws `Error: object 'age' not found`.

**Fix — Option 1:** Include `age` in `select()`
```r
select(fam_name, given_name, survived, age)
```

**Fix — Option 2:** `mutate()` first, then `select()`
```r
mutate(death_index = age + 10) |>
select(fam_name, given_name, survived, death_index)
```

### Watch Out For
- `mutate()` using a column that was dropped by an earlier `select()`
- `summarise()` referencing a column removed mid-chain
- `arrange()` on a column that no longer exists

---

## 2. `mutate()` vs `summarise()` — Row-Level vs Group-Level

A very common trick question area.

### The Rule
| Verb | When To Use | Output Rows |
|---|---|---|
| `mutate()` | Row-level computation | Same number of rows as input |
| `summarise()` | Group-level aggregation | One row per group |

### Example Question
What is wrong with this code?
```r
people |>
  group_by(class) |>
  mutate(survival_rate = mean(survived))
```

**Answer:** The code runs but is misleading. `mutate()` computes `mean(survived)` per group but **repeats the value on every row** rather than collapsing to one row per group. If you want one row per class, use `summarise()` instead.

### Watch Out For
- Using `mutate()` when you want aggregated output
- Using `summarise()` when you want to keep all rows but add a new column

---

## 3. `group_by()` Must Come Before `summarise()`

### The Rule
> `summarise()` always collapses to one row per group. Without `group_by()`, the entire data frame is one group — you get exactly 1 row back.

### Example Question
How many rows does this return?
```r
people |>
  summarise(
    survival_rate = mean(survived),
    mean_age = mean(age, na.rm = TRUE)
  )
```

**Answer:** 1 row. No `group_by()` means the entire table is treated as a single group.

### Example Question
How many rows does this return?
```r
people |>
  group_by(class, sex) |>
  summarise(count = n())
```

**Answer:** At most 8 rows (4 classes × 2 sexes). Could be fewer if some combinations have no passengers.

### Watch Out For
- Missing `group_by()` before `summarise()` — always gives 1 row
- More columns in `group_by()` = more specific groups = more output rows
- Filtering before `group_by()` can reduce the number of groups

---

## 4. Filtering Joins Never Add Columns

One of the most tested conceptual distinctions.

### The Rule
| Join Type | Adds Columns From y? | Affects Rows? |
|---|---|---|
| `inner_join()` | ✅ Yes | ✅ Yes — only matching rows |
| `left_join()` | ✅ Yes | ✅ Yes — keeps all of x |
| `right_join()` | ✅ Yes | ✅ Yes — keeps all of y |
| `full_join()` | ✅ Yes | ✅ Yes — keeps all rows |
| `semi_join()` | ❌ No | ✅ Yes — keeps matching rows from x |
| `anti_join()` | ❌ No | ✅ Yes — keeps non-matching rows from x |

### Example Question
How many columns does this return?
```r
shareholders |>
  anti_join(shares, join_by(sh_holder_id))
```

**Answer:** 4 columns — exactly the columns of `shareholders` (`sh_holder_id`, `sh_holder_name`, `country`, `is_indiv`). `anti_join` never adds columns from `shares`.

### Watch Out For
- Expecting `semi_join` or `anti_join` to add columns — they never do
- The output of a filtering join always has the same columns as the left table

---

## 5. Identifying Join Relationships

### The Framework
For each table being joined, ask: *"For one value of the key, how many matching rows exist on this side?"*

| Relationship | Left Side | Right Side | Example |
|---|---|---|---|
| One-to-One | 1 match | 1 match | shareholders ↔ traded_companies on name |
| One-to-Many | 1 match | Many matches | traded_companies ↔ products on comp_id |
| Many-to-Many | Many matches | Many matches | shareholders ↔ traded_companies on country |

### The Practical Test
```r
# Run this before writing your join
table_x |> count(key_column) |> arrange(desc(n))
table_y |> count(key_column) |> arrange(desc(n))

# If both have n > 1 for any value → many-to-many
# If only right side has n > 1 → one-to-many
# If both always have n = 1 → one-to-one
```

### Watch Out For
- Using wrong relationship type causes a warning or error
- Always verify from the data, not just intuition

---

## 6. `case_when()` — Missing Catch-All

### The Rule
Always include a `TRUE ~` catch-all at the end of `case_when()`. Without it, unmatched rows silently return `NA`.

### Example Question
What happens to passengers with missing `age` here?
```r
mutate(
  age_group = case_when(
    age < 18  ~ "Minor",
    age >= 18 ~ "Adult"
  )
)
```

**Answer:** Passengers with `NA` age match no condition and are silently assigned `NA` for `age_group`. This can corrupt downstream calculations like `mean()`.

**Fix:**
```r
mutate(
  age_group = case_when(
    age < 18  ~ "Minor",
    age >= 18 ~ "Adult",
    TRUE ~ NA_character_   # explicit catch-all
  )
)
```

### Watch Out For
- `NA_real_` for numeric outputs, `NA_character_` for character outputs
- `case_when()` evaluates top to bottom — first matching condition wins

---

## 7. `mean()` On Logical Vectors

### The Rule
> R treats `TRUE` as 1 and `FALSE` as 0 in arithmetic. So `mean(survived)` gives the **proportion** of TRUE values — i.e. survival rate.

```r
mean(c(TRUE, FALSE, TRUE, TRUE))  # returns 0.75
```

This is intentional and useful — no need to convert logical to numeric first.

### Watch Out For
- `NA` values will make `mean()` return `NA` unless you add `na.rm = TRUE`
```r
mean(age, na.rm = TRUE)  # ignores NA values
```

---

## 8. Redundant Operations — Code Smell

### Example Question
Will this code run, and is there anything wrong with it?
```r
people |>
  filter(sex == "Female") |>
  group_by(sex) |>
  summarise(count = n())
```

**Answer:** It runs, but `group_by(sex)` is redundant — after filtering for only "Female", there is only one possible group. The output will always be exactly 1 row regardless. Remove the `group_by()` or broaden the filter.

### Watch Out For
- `filter()` to a single value then `group_by()` that same column
- `arrange()` after `summarise()` when you only have 1 row

---

## 9. Row And Column Count — Quick Reference

| Verb | Rows | Columns |
|---|---|---|
| `filter()` | Decreases or stays same | Unchanged |
| `select()` | Unchanged | Decreases or stays same |
| `mutate()` | Unchanged | Increases |
| `arrange()` | Unchanged | Unchanged |
| `group_by()` | Unchanged | Unchanged (adds invisible metadata) |
| `summarise()` | One per group | Only grouping cols + new computed cols |
| `inner_join()` | Only matching rows | x cols + y cols (minus duplicate key) |
| `left_join()` | All of x | x cols + y cols (minus duplicate key) |
| `semi_join()` | Matching rows from x only | x cols only |
| `anti_join()` | Non-matching rows from x only | x cols only |

---

## 10. Group-Level Filtering Pattern

A common pattern for questions like *"how many groups satisfy condition X?"*

```r
data |>
  group_by(key) |>
  summarise(
    group_size  = n(),
    flag        = any(condition)
  ) |>
  filter(flag == TRUE & group_size >= 2) |>
  nrow()
```

### Example
*How many ticket groups lost at least one member?*
```r
people |>
  group_by(ticket) |>
  summarise(
    group_size  = n(),
    lost_member = any(survived == FALSE)
  ) |>
  filter(lost_member == TRUE & group_size >= 2) |>
  nrow()
```

### Watch Out For
- Solo entries (group_size == 1) may need to be excluded depending on the question
- `any()` returns TRUE if **at least one** row in the group meets the condition
- `all()` returns TRUE only if **every** row in the group meets the condition
