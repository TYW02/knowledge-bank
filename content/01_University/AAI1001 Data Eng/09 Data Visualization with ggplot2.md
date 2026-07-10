---
title: 09 Data Visualization with ggplot2
tags:
  - ggplot2
---
The basic idea of #ggplot2 is to build a plot layer by layer, starting with the `data` and `aesthetics` then adding `geometric object (geom)` to represent data visually

- geom: Geometric object that represent data in the plot
- Aesthetic Mapping: Relationship between statistical variable and the visual representation (e.g. Body mass to x-axis, taxonomic order to point shape)
- Annotation: Textual or graphical element providing background information about plot or element. There are **Data Annotation** & **Plot Annotation**
- Scale: How variable values are translated into visual appearance
- Guide: Feature in a plot that enables reader to convert visual appearance into statistical values
- Theme: Collection of layout choices on overall plot appearance, such as background color, font family

![[Pasted image 20260710183046.png]]
Plot Annotation: Things that tell you about the plot
Data Annotation: Things that tell you about the data


# Scatter plot
#Scatter_Plot
Display the relationship between 2 quantitative variables.
Useful for identifying patterns, trends, and potential correlations in the data.

# ggplot basics
- `ggplot2` is built on the concept of layers
- `ggplot()` function initializes a plot
- `aes()` function maps aesthetics to variable
- `geom()` functions add plot layers

### Example data to be plotted
```R
dfr <- tribble(
	~x, ~y,
	3, -1, 
	0, -2,
	1, 2
)
gg <- ggplot(dfr, aes(x=x, y=y)) # This only creates the plot with X, y axis no data is plotted yet
class(gg)
```


## Point
#geom_point
```R
gg + geom_point()
```
![[Pasted image 20260710183552.png]]

## Path & Lines
```R
gg + geom_path() + labs(title = "Path")
gg + geom_line() + labs(title = "Lines")
```
![[Pasted image 20260710183652.png]]

### What is the difference ?
Main difference is how they connect the dots.

`geom_line()` sorts data by x-axis values from left to right before connecting points
`geom_path()` connects points sequentially in the **EXACT** order they appear in your data frame. (In this example it goes from (3,-1) -> (0,-2) -> (1,2))

## Combining Points with Path/Lines
```R
gg + geom_point() + geom_path() + labs(title = "Points and Path")
gg + geom_point() + geom_line() + labs(title = "Points and Line")
```


### Example data
```R
michelle <- 
	storms |>
	filter(name == "Michelle") |>
	mutate(obs = row_number()) |>
	select(long, lat, wind, pressure, month, day, hours, obs) |>
	head(michelle, 3) |> gt()
```
`gt()` Creates a visual table 
![[Pasted image 20260710184402.png]]

## Plotting with color
```R
gg_long_lat <-
	ggplot(michells, aes(long, lat, color = obs)) +
	geom_point() +
	labs(
		x = "Longitude (0)",
		y = "Latitude (0)",
		color = "obs"
	)
```

```R
gg_long_lat +
	geom_path() +
	labs(title = "Path")
```
![[Pasted image 20260710184624.png]]

### Adding caption
#ggplot_caption
```R
gg_pressure_wind_point <-
	ggplot(michelle, aes(pressure, wind)) +
	geom_point() +
	labs(
		x = "Pressure (hPa)",
		y = "Wind (knots)",
		caption = "Source: National Hurricane Center"
	)
```
![[Pasted image 20260710184820.png]]

# Dealing with Overplotting
#Overplotting

Occurs when multiple points are plotted at the same or extremely close positions
- Can be problematic since it is impossible to discern overplotted data points

**Mitigation Strategies** include jittering combined with partial transparency and representing counts by symbol areas

```R
gg_pressure_wind_line <- ggplot(michelle, aes(pressure, wind)) +
	geom_line() +
	labs(x = "Pressure(hPa)", y = "Wind (knots)", caption = "Source: National Hurricane Center")
```

#Jitter
```R
gg_pressure_wind_line +
	geom_jitter(alpha = 0.5) +
	labs(title = "Jitter")
```

#Count 
```R
gg_pressure_wind_line +
	geom_count(alpha = 0.5) + # Counts num of points directly on top of each other
	labs(size = "Obs", title = "Count") +
	scale_size_area()
```
![[Pasted image 20260710185308.png]]

By connecting all observed values, `geom_line()` tends to accentuate details influenced by randomness rather than the underlying process (Like the random stuttering of data points)
- Alternative is `geom_smooth()`, which fits smooth curve to data, not necessarily passing through all observed points

Default method for curve fitting is locally estimated scatter-plot smoothing (**LOESS**) if there are fewer than 1,000 data points

In fitted curve, the dark grey surrounding ribbon represents the estimated 95% confidence interval for a given x-coordinate

```R
gg_pressure_wind_count <- ggplot(michelle, aes(pressure, wind)) + geom_count(alpha = 0.5) + scale_size_area() + labs(x = "Pressure (hPa)", y = "Wind (Knots)", caption = "Source: National Hurricane Center")
```

```R
gg_pressure_wind_count +
	geom_smooth(
		method = "loess"
	) +
	labs(
		title = "Default Smoothing"
	)
	
	
gg_pressure_wind_count +
	geom_smooth(
		method = "lm"
	) +
	labs(
		title = "Linear Model"
	)
	

gg_pressure_wind_count +
	geom_smooth(
		span = 0.3
	) +
	labs(
		title = "Wiggly Smoothing"
	)
	
	
gg_pressure_wind_count +
	geom_smooth(
		span = 1.0
	) +
	labs(
		title = "Steady Smoothing"
```

In `geom_smooth()` the `span` argument is specifically used when smoothing method is set to `loess`
- The lower the span value the more "Wigglier" the line
**Smaller** span makes the `blue` line wigglier while a **larger** span makes it straighter
**Smaller** span makes `grey ribbon` wider and wavy because model uses fewer data points per segment. **Larger** span becomes narrower and smoother because model uses more data to calculate trend.
![[Pasted image 20260710190230.png]]

### Basic `geom` summary

| geom_                              | Description                                                                                                                                 |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `geom_point()`                     | Plots points at x and y coordinates. Corresponding numbers are retrieved from data frame columns specified as arguments to `aes()` function |
| `geom_path()`                      | Connects points in the order they appear in the data frame                                                                                  |
| `geom_line()`                      | Connects points in order of the X variable                                                                                                  |
| `geom_jitter()`                    | Adds a small amount of randomness to coordinates, mitigating the effect of overplotting                                                     |
| `geom_count() + scale_size_area()` | Represents the multiplicity of overlapping points by the area of the point symbols                                                          |
| `geom_smooth()`                    | Adds a smooth trend curve to the plot                                                                                                       |
 
# Visualizing Ungrouped Quantitative Distribution
Can be visualized using
- Histogram
- Frequency Polygons
- Rug Plots
- Smoothed Density Estimates
- Box Plots

These plots help to understand the distribution of a single quantitative variable without grouping it by any categorical variable.

# Histogram
#Histogram

```R
gg_hist_bins <- function(n_bins) {
	ggplot(iris, aes(x = .data$Sepal.Length)) +
	geom_histogram(bins = n_bins) +
	labs(
		x = "Sepal Length (cm)",
		y = "Count",
		title = str_c("Histogram Using", n_bins, " Bins"), # String Concatenate
		caption = "Source: Anderson (1935)"
	)
}
```

```R
gg_color_hist <- function(n_bins, arg_fill = NA, arg_color = "black"){
	ggplot(iris, aes(x = .data$Sepal.Length)) +
	geom_histogram(bins = n_bins, fill = arg_fill, color = arg_color) +
	labs(
		x = "Sepal Length (cm)",
		y = "Count",
		title = str_c("Histogram Using", n_bins, " Bins"), # String Concatenate
		caption = "Source: Anderson (1935)"
	)
}
```

### Example Usage
```R
gg_color_hist(
	40,
	arg_fill = "yellow",
	arg_color = "darkblue"
)
```

![[Pasted image 20260710193159.png]]
> `Fill` is the color of the inner side of histogram
> `Color` is the line color of the histogram


# Frequency Polygons
#Frequency_Polygons

```R
gg_freqpoly_bins <- function(n_bins){
	ggplot(iris, aes(x = .data$Sepal.Length)) +
	geom_freqpoly(bins = n_bins, color = "darkblue") +
	labs(
		x = "Sepal Length (cm)",
		y = "Count",
		title = str_c("Frequency Polygon Using ", n_bins, " Bins"),
	),
	caption = "Source: Anderson (1935)"
	)
}
```
![[Pasted image 20260710193529.png]]
Line-based alternative to a histogram

# Rug Plots
#Rug_Plots

Histogram or frequency polygon provide insight into distribution of data points, they obscure the precise position of **individual** data points inside the bins.

Rug Plots reveal exact positions by representing each data points using a short line perpendicular to the coordinate axis.

```R
gg_color_hist(20) +
	geom_rug() +
	labs(title = "Histogram with Rug Plot")
	
gg_color_hist(20) +
	geom_rug(
		aes(y = 0), # We did not specify y in gg_color_hist
		position = position_jitter(height = 0), # Jitter the rug points
		alpha = 0.5,
		sides = "lrbt" # draw marks on Left, Right, Bottom, Top of plot
	) +
	labs(title = "Histogram with Jittered Plot")
	

gg_freqpoly_bins(20) +
	geom_rug(
		aes(y = 0),
		position = position_jitter(height = 0),
		alpha = 0.5,
		sides = "b" # Rug will only show on bottom of plot
	) +
	labs(title = "Frequency Polygon with Jittered Rug")
```


# Smoothed Density Estimates
Approximate the empirical distribution with smooth Probabilistic Density Function
Smoothed density is normalized so that area under curve is 1

```R
ggplot(iris, aes(Sepal.Length)) +
  geom_histogram(aes(y = after_stat(density)), bins = 20, fill = NA, color = "gray25") +
  geom_density(adjust = 0.5, color = "darkblue", linewidth = 1.5) +
  geom_rug(
    aes(y = 0),
    position = position_jitter(height = 0),
    alpha = 0.5,
    sides = "b"
  ) +
  labs(title = "Smoothed Estimate (Adjust = 0.5)")
```
![[Pasted image 20260710194839.png]]

```R
ggplot(iris, aes(Sepal.Length)) +
  geom_histogram(aes(y = after_stat(density)), bins = 20, fill = NA, color = "gray25") +
  geom_density(adjust = 1.5, color = "darkblue", linewidth = 1.5) +
  geom_rug(
    aes(y = 0),
    position = position_jitter(height = 0),
    alpha = 0.5,
    sides = "b"
  ) +
  labs(title = "Smoothed Estimate (Adjust = 1.5)")
```
![[Pasted image 20260710194847.png]]

> `adjust` is a multiplicative multiplier for smoothing bandwidth. Let's you fine tune how jagged or smooth your density curve appears
> `after_stat(density)` scales your y-axis of your histogram to represent density rather than raw counts.


# Box Plots
#Box_Plot

### Example data used
```R
IQR <- IQR(dfr_norm$values)
quantiles <- quantile(dfr_norm$values, c(0.25, 0.50, 0.75)) |> t() |> round(4) |> data.frame()
colnames(quantiles) <- c("0.25", "0.50", "0.75")

min_include_outliers <- min(dfr_norm$values) |> round(4)
min_exclude_outliers <- (quantile(dfr_norm$values, 0.25) - 1.5 * IQR)[["25%"]] |> round(4)
max_exclude_outliers <- (quantile(dfr_norm$values, 0.75) + 1.5 * IQR)[["75%"]] |> round(4)
max_include_outliers <- max(dfr_norm$values) |> round(4)

quantiles <- quantiles |>
  add_column(.before = "0.25", "min\\outliers" = min_exclude_outliers) |>
  add_column(.before = "min\\outliers", "min" = min_include_outliers) |>
  add_column(.after = "0.75", "max\\outliers" = max_exclude_outliers) |>
  add_column(.after = "max\\outliers", "max" = max_include_outliers)
quantiles |> gt()
```

## Plotting Box Plot
```R
ggplot(dfr_norm, aes(x = values)) +
  geom_boxplot(fill = "lightyellow", color = "darkblue") +
  labs(title = "Box Plot of Samples from Normal Distribution")
```
![[Pasted image 20260710195346.png]]


# Visualizing Grouped Quantitative Distributions
Grouped Distributions involve a categorical variable that divides the data into groups.
This allows comparisons between groups, revealing differences in their distributions. Color coding and faceting are often used to distinguish between groups

## Grouped Distribution Histogram
```R
ggplot(iris, aes(Sepal.Length, fill = Species)) +
  geom_histogram(bins = 20, color = "gray") +
  labs(
      x = "Sepal Length (cm)",
      y = "Count", 
      title = "Stacked Histogram. Source: Anderson (1935)."
    )
    
ggplot(iris, aes(Sepal.Length, fill = Species)) +
  geom_histogram(bins = 20, position = "dodge") + # Separate bins horizontally
  labs(
      x = "Sepal Length (cm)",
      y = "Count", 
      title = "Stacked Histogram. Source: Anderson (1935)."
    )
    
ggplot(iris, aes(Sepal.Length, fill = Species)) +
  geom_histogram(bins = 20, fill = NA, color = "gray") +
  geom_histogram(bins = 20, position = "dodge") +
  labs(
      x = "Sepal Length (cm)",
      y = "Count", 
      title = "Stacked Histogram. Source: Anderson (1935)."
    )
```
![[Pasted image 20260710195603.png]]


## Grouped Distribution Faceting
```R
ggplot(iris, aes(Sepal.Length)) +
  geom_histogram(bins = 20, fill = NA, color = "black") +
  facet_wrap(vars(Species), ncol = 1) + # Create small subplots based on cat data
  labs(
      x = "Sepal Length (cm)",
      y = "Count", 
      title = "Faceted Histogram. Source: Anderson (1935)."
  )
  
ggplot(iris, aes(Sepal.Length)) +
  geom_histogram(bins = 20, fill = NA, color = "black") +
  geom_rug(
    aes(y = 0),
    position = position_jitter(height = 0),
    alpha = 0.5,
    sides = "b"
  ) +
  facet_wrap(vars(Species), ncol = 1) +
  labs(
      x = "Sepal Length (cm)",
      y = "Count", 
      title = "Faceted Histogram with Rug Plot. Source: Anderson (1935)."
  )
```
![[Pasted image 20260710195752.png]]

# Grouped Data Distribution Frequency Polygon and Density

```R
ggplot(iris, aes(Sepal.Length)) +
  geom_freqpoly(bins = 20) +
  facet_wrap(vars(Species), ncol = 1) +
  geom_rug(aes(y = 0), position = position_jitter(height = 0), alpha = 0.5, sides = "b") +
  geom_vline(aes(xintercept = mean(Sepal.Length)), color = "red", linetype = "dashed") +
  labs(x = "Sepal Length (cm)", y = "Count")
  
  
ggplot(iris, aes(Sepal.Length)) +
  geom_density() +
  facet_wrap(vars(Species), ncol = 1) +
  geom_rug(aes(y = 0), position = position_jitter(height = 0), alpha = 0.5, sides = "b") +
  geom_vline(aes(xintercept = mean(Sepal.Length)), color = "red", linetype = "dashed") +
  labs(x = "Sepal Length (cm)", y = "Density")
```
![[Pasted image 20260710202739.png]]


# Grouped Data Distribution Box and Violin Plots
#Violin_Plots are axially symmetric [[09 Data Visualization with ggplot2#Smoothed Density Estimates | Density Plots]] which are created using `geom_violin()`

Violin plots should only be used for grouped data, For ungrouped data, `geom_density()` should be used instead.
```R
ggplot(iris, aes(Sepal.Length, Species)) +
  geom_violin()
  
ggplot(iris, aes(Sepal.Length, Species)) +
  geom_violin() +
  geom_boxplot(aes(fill = Species), width = 0.2)
```
![[Pasted image 20260710203021.png]]
![[Pasted image 20260710203027.png]]

## Box plots
```R
ggplot(iris, aes(Sepal.Length)) +
  geom_boxplot(aes(fill = Species)) +
  # remove y axis labels
  scale_y_continuous(breaks = NULL)
  
ggplot(iris, aes(Sepal.Length, Species)) +
  geom_boxplot()
```
![[Pasted image 20260710203100.png]]
![[Pasted image 20260710203106.png]]
