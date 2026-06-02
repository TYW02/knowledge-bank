---
title: Practice
tags:
  - R
  - Summarise
  - Encoding
---
# Summarise
#Summarise 

> `summarise()` always collapses to 1 row **per group**. Without `group_by()` there is only 1 group, the whole table.
> 
> With `group_by()` you define how many groups exists, so `summarise()` produces that many rows

A Clean way to think about it:
```R
group_by(lifeboats, boat_name)   # "here are my 20 groups"
summarise(passenger_count = n())  # "Give me 1 row per group" -> 20 rows
```


# Identifying Relationships

Look at the 2 tables you are joining and ask this question for each side:
> "For one value of the key, how many matching rows exist on this side ?"

## One-to-One
Each key value appears once on both sides
```R
shareholder <-> traded_companies (joined on name)
LaughingStock   LaughingStock
LOL Finance    LOL Finance
# each name appears exactly once on each side
```

## One-to-Many
Key appears once on the left, multiple times on the right
```R
traded_companies <-> products (Joined on comp_id)
comp_id 6    comp_id 6 -> HyperMagneto Flying Drone
              comp_id 6 -> NebulaForce Magnetic Motor
# 1 company, many products
```

## Many-to-Many
Key appears multiple times on **BOTH** sides
```R
shareholders <-> traded_companies (Joined on country)
Singapore    Singapore -> Absurd Assets
Singapore    Singapore -> LOL Finance
# Multiple shareholders in Singapore, multiple companies in Singapore
```


# Encoding Categorical to Numerical
#Encoding
```R
people |>
	mutate(
	numeric_class = case_when(
		class == "1st" ~ 1,
		class == "2nd" ~ 2,
		class == "3rd" ~ 3,
		class == "4th" ~ 4,
		TRUE ~ NA_real_
	))
```