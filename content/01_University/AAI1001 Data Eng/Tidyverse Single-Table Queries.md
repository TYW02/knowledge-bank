---
tags:
  - R
  - dplyr
  - SELECT
  - Filter
---
# Importing Data
#R
To import data into R use the `read_csv()` function from the `readr` package. To do so, we can load either `tidyverse` or `readr` into the current session.
```R
library(tidyverse)

library(readr)
```

Next, we import the data
```R
# import the data from the .csv file
people <- read_csv("data_lecture/titanic/people.csv", show_col_types=FALSE)
tickets <- read_csv("data_lecture/titanic/tickets.csv", show_col_types=FALSE)
lifeboats <- read_csv("data_lecture/titanic/lifeboats.csv", show_col_types=FALSE)
```


# Glance at dplyr
#dplyr

| Row-Wise   |                                     |
| ---------- | ----------------------------------- |
| filter()   | Chooses rows based on column values |
| distinct() | Chooses unique rows                 |
| count()    | Count Rows                          |
| slice()    | Chooses rows based on location      |
| arrange()  | Changes the order of the rows       |

| Column-Wise |                                                       |
| ----------- | ----------------------------------------------------- |
| select()    | Changes whether or not a column is included           |
| rename()    | Changes the name of columns                           |
| mutate()    | Changes the values of columns and creates new columns |

| Group-Wise  |                                     |
| ----------- | ----------------------------------- |
| summarise() | Collapses a group into a single row |

# Selecting Columns
#SELECT 
```R
people |>
	select(fam_name, given_name) |>
	head(3)
	
people |>
	select(ends_with("name")) |>
	head(3)
	
people |>
	select(contains("_")) |>
	head(3)
	
people |>
	select(age:ticket) |>
	head(3)
```


# Counting Rows and Columns
#Count
```R
count(
	people,
	missing = if_else(
		is.na(age),
		"yes",
		"no"
	)
)

count(
	people,
	missing = if_else(
		is.na(age),
		"yes",
		"no"
	),
	gender = sex,
	name = "num"
)
```

The `name` parameter here allows you to rename the resulting column name.

# Filtering and Sorting Rows
#Filter
`filter()` mirrors *WHERE* clause in SQL
```R
filter(people, (age <= 20 & class == "3rd")) |>
	select(fam_name, given_name, age) |>
	head(4)
```


`arrange()` mirrors *ORDER BY* clause in SQL (default is ascending)
```R
arrange(engineer_bodies, age) |> head(7)

arrage(engineer_bodies, desc(age), recovered_body) |> head(6)
```

Ranking functions:
- row_number()
- min_rank()
- dense_rank()

```R
engineer_bodies |>
	select(fam_name, given_name, age) |>
	arrange(desc(age)) |>
	mutate(
		row_number = row_number(desc(age)),
		min_rank = min_rank(desc(age)),
		dense_rank = dense_rank(desc(age))
	) |>
	head(5)
```

> [!NOTE]
> `mutate()` creates new columns that are functions of existing variables. It can also modify and delete columns
> [Documentation](https://dplyr.tidyverse.org/reference/mutate.html)

# Summarizing Data by Group
```R
people |>
	summarize(
		n_people = n(),
		mean_age = round(mean(age, na.rm = TRUE)),
		sd_age = sd(age, na.rm = TRUE),
		.by = c(sex, class, survived)
	) |>
	filter(class != "Crew", survived == TRUE) |>
	arrange(sex, class)
```

> [!NOTE]
> `summarize()` creates a new data frame. It returns 1 row for each combination of grouping variables. If there are no grouping variables, the output will have a single row summarising all observation in the input. It will contain 1 column for each grouping variable and 1 column for each of the summary statistics that you have specified.
> [Documentation](https://dplyr.tidyverse.org/reference/summarise.html)


# Pivoting

Pivoting is the process of transforming a table from a long format (more rows than columns) to a wide format (more columns than rows) or vice versa. [Maybe like Transpose]
`tidyr::pivot_longer()` and `tidyr::pivot_wider()` are used to pivot data frames
```R
job_per_port <-
	people |>
	filter(!is.na(job_on_board)) |>
	count(embarkation_port, job_on_board, name = "num")
job_per_port
```


### pivot_wider()
```R
pivot_wider(
	job_per_port,
	names_from = embarkation_port,
	values_from = num,
	values_fill = 0
)
```


```R
age_status <-
	people |>
	summarize(
		min = min(age, na.rm = TRUE),
		lower_quartile = quartile(age, 0.25, na.rm = TRUE),
		median = median(age, na.rm = TRUE),
		upper_quartile = quantile(age, 0.75, na.rm = TRUE),
		max = max(age, na.rm = TRUE),
		.by = class
	)
age_status
```

### pivot_longer()
```R
pivot_longer(
	age_status,
	cols = c(
		min,
		lower_quartile,
		median,
		upper_quartile,
		max
	),
	names_to = "stat",
	values_to = "value"
) |>
arrange(class, value) |>
gt()
```