---
title: 10 Geoms
tags:
  - Geoms
---
# Geoms for Bar Charts

## Single-Category Bar Chart
```R
gss_cat_labs <- function(...) {
  ggplot2::labs(
    x = "Count",
    y = "Response",
    title = "Party Affiliation of GSS Participants",
    caption = 'Source: R package "forcats"',
    ...
  )
}
ggplot(gss_cat, aes(y = partyid)) +
  geom_bar() +
  gss_cat_labs()
```

![[Pasted image 20260716074639.png]]


### Bar Chart Frequency sort, Alphabetical Order
```R
ggplot(gss_cat, aes(y = fct_infreq(partyid))) +
  geom_bar(fill = NA, color = "darkblue") +
  gss_cat_labs()
  
  
ggplot(gss_cat, aes(y = as.character(partyid))) +
  geom_bar(fill = NA, color = "darkblue") +
  gss_cat_labs()
```
![[Pasted image 20260716074837.png]]

![[Pasted image 20260716074845.png]]


## 2-Category Bar Chart
```R
ggplot(gss_cat, aes(y = partyid, fill = marital)) + # Here the fill is marital
  geom_bar(color = "darkblue") + # Bar outline is darkblue
  gss_cat_labs(fill = "Marital status") # Legend
  

ggplot(gss_cat, aes(y = partyid, fill = marital)) +
  geom_bar(position = "dodge") + # This makes the bar split into diff category
  gss_cat_labs(fill = "Marital status")
  
  
ggplot(gss_cat, aes(y = partyid)) +
  geom_bar(aes(fill = marital), position = "dodge") + # Split the bar
  geom_bar(fill = NA, color = "darkblue") + # Color the outline
  gss_cat_labs(fill = "Marital status")
```

![[Pasted image 20260716075004.png]]
![[Pasted image 20260716075010.png]]
![[Pasted image 20260716075016.png]]


## Bar Chart for Already Counted Data

```R
gss_by_partyid <- count( # Since partyid is already counted here
  gss_cat, 
  partyid, 
  name = "count")
gss_by_partyid
```

```R
ggplot(gss_by_partyid, aes(count, partyid)) +
  geom_col(fill = NA, color = "black") + gss_cat_labs()
```
![[Pasted image 20260716075201.png]]

> [!NOTE]
> Use `geom_col()` instead of `geom_bar()` if data are already counted.
> (If your data in dataframe is already counted)


# Geom for Heatmap & Contour Plots
#Heatmap #Countour_Plot

Static 3D plots are challenging to visualize in 2D surfaces such as computer screens.
Heatmaps and contour plots are more suitable for visualizing 3 variables on 2D surfaces.

### Example Data Used
```R
str_c("`volcano` class is: ", class(volcano)[1], 
      ", dimension is: ", dim(volcano)[1], " by ", dim(volcano)[2])
      
volcano_dfr <-
  tibble(elevation = c(volcano)) |>
  mutate(
    x = 10 * (row_number() - 1) %% nrow(volcano), # modulo
    y = 10 * (row_number() - 1) %/% nrow(volcano) # integer division
  )
str(volcano_dfr)


volcano_labs <- function(...) {
  ggplot2::labs(
    x = "x (m)",
    y = "y (m)",
    caption = 'R data set "volcano"',
    ...
  )}
```

> [!NOTE]
> `geom_raster()` is a fast special case of `geom_tile()` when all tiles are the same size

```R
ggplot(volcano_dfr, aes(x, y, fill = elevation)) + geom_tile() +
  volcano_labs(fill = "Elevation (m)", title = "Heatmap of Maunga Whau")
  
ggplot(volcano_dfr, aes(x, y, fill = elevation)) + geom_raster() +
  volcano_labs(fill = "Elevation (m)", title = "Heatmap of Maunga Whau")
```
![[Pasted image 20260716075849.png]]
Both outputs are the same just a matter of performance.


# Contour Plots
```R
ggplot(volcano_dfr, aes(x, y, z = elevation)) +
  geom_contour() +
  volcano_labs(title = "Basic Contours")
```
![[Pasted image 20260716075956.png]]

## Contour Lines
```R
ggplot(volcano_dfr, aes(x, y, z = elevation, color = after_stat(level))) +
  geom_contour() +
  volcano_labs(color = "Elevation (m)", title = "Contour Lines")
```
![[Pasted image 20260716080021.png]]

### Why use `after_stat()`
`ggplot` expects you to map aesthetics of `x`, `y`, `fill`... to raw columns existing in your original dataframe. However, many geometries such as `geom_bar()`, `geom_histogram()`, `geom_density()` internally compute new variables before rendering.

`after_stat()` tells `ggplot` to look at this freshly calculated data instead of your original dataframe.

> [!IMPORTANT]
> `after_stat()` can **ONLY** be placed inside the `aes()` function of a plot layer.
> 
> "Does the value I want to plot exist as a column in my original dataframe ?"
> IF answer is NO, and `ggplot` has to calculate that value for you behind the scenes, you need `after_stat()`
> 


## Filled Contours
```R
ggplot(volcano_dfr, aes(x, y, z = elevation)) +
  geom_contour_filled() +
  volcano_labs(fill = "Elevation (m)", title = "Filled Contours")
```
![[Pasted image 20260716080908.png]]


## Contour Lines with Text
```R
ggplot(volcano_dfr, aes(x, y, z = elevation, color = after_stat(level))) +
  geom_contour() + metR::geom_label_contour() + guides(color = "none") +
  volcano_labs(color = "Elevation (m)", title = "Contour Lines")
```
![[Pasted image 20260716080927.png]]

## How to change color scheme and customize levels in `geom_contour_filled()`
```R
ggplot(volcano_dfr, aes(x, y, z = elevation)) +
  geom_contour_filled(bins = 12) +
  scale_fill_viridis(discrete = TRUE, option = "B") +
  geom_contour(color = "white", bins = 12) +
  metR::geom_label_contour() +
  volcano_labs(fill = "Elevation (m)", title = "Heatmap of Maunga Whau")
```
![[Pasted image 20260716081020.png]]


# Geom for Text
Text in data visualization establishes immediate semantic relationships, which helps to enhance clarity, highlight key data points, and improve the overall visualization.

`geom_text()` generates text only

`geom_label()` adds rectangle and optional background colors
> Both require `x`, `y`, and `label` in `aes()`

### Example Data Used
```R
dfr <- tribble(
  ~x, ~y, ~word,
  0, -1, "1. This",
  2, 2, "2. That",
  1, -2, "3. Other",
  3, 0, "4. Same",
  1, 1, "5. Different"
)
gg <- ggplot(
  dfr, 
  aes(x, y, label = word)
)
gg + geom_text()
```
![[Pasted image 20260716185758.png]]
Note that in this graph the word "4. Same" is outside the graph

`ggplot2` does not automatically choose axis limits for text.
Use `xlim()` and `ylim()` to adjust axis limits.


## Using `geom_label()`
```R
gg + geom_label()
```
![[Pasted image 20260716190031.png]]

### Adjusted Text Label
```R
gg + 
  geom_label() + 
  xlim(-0.2, 3.3) + 
  ylim(-2.2, 2.2)
```
![[Pasted image 20260716185932.png]]

### Additional aesthetic for text
```R
mutate(dfr,
  class = c("i", "i", "ii", "ii", "iii"),
  extent = c(1, 2, 2, 3, 3),
  font_family = c("serif", "sans", "serif", "mono", "mono")
) |>
  ggplot(aes(x, y, label = word, color = class, size = extent, family = font_family)) +
  xlim(-1, 4) +
  ylim(-2.5, 2.5) + 
  geom_label() +
  scale_size_area()
```
![[Pasted image 20260716190058.png]]

## Aligning, Nudging, and Resizing Text
- Text by default is centered horizontally and vertically
- `hjust` and `vjust` adjust the alignment, termed justification
- Both arguments accept values between 0 and 1, bottom left to top right
```R
gg_partyid <-
  ggplot(gss_by_partyid, aes(count, partyid, label = count)) +
  geom_col(fill = NA, color = "darkblue") +
  labs(
    x = "Count",
    y = "Response",
    title = "Party Affiliation of GSS Participants",
    caption = 'Source: R package "forcats"'
  ) +
  xlim(0, 4500)
gg_partyid + geom_text()
```
![[Pasted image 20260716190222.png]]

### Aligning text label
```R
gg_partyid + 
  geom_text(hjust = 0)
```
![[Pasted image 20260716190339.png]]

Use `nudge_x` and `nudge_y` to shift text by a specified distance
```R
gg_partyid + 
  geom_text(hjust = 0, nudge_x = 75, size = 3)
```
![[Pasted image 20260716190420.png]]


Use `guides(... = "none")` to remove an axis or legend
Use `labs(... = NULL)` to remove an axis label or legend title
```R
gg_partyid +
  geom_text(hjust = 0, nudge_x = 75, size = 3) +
  labs(x = NULL, y = NULL) +
  guides(x = "none")
```
![[Pasted image 20260716190531.png]]

## Dodged Bar Charts
```R
count(gss_cat, partyid, marital, name = "count") |>
  ggplot(aes(marital, count, fill = partyid, label = count)) +
  geom_col(position = "dodge") +
  gss_cat_labs() + labs(x = NULL, y = NULL) + guides(y = "none") + ylim(0, 2000) +
  geom_text(aes(color = partyid), hjust = 0, vjust = 0.5, size = 4, angle = 90, position = ggpp::position_dodgenudge(width = 0.9, y = 20))
```
![[Pasted image 20260716190632.png]]


# Reduce Overplotting of Text through Repulsion
- When plotting a large number of text elements, they often overlap, making them unreadable
- To mitigate this issue, use `ggrepel::geom_text_repel()` to reduce text overplotting
- `max.overlaps` (default 10) is used to control the number of text elements that can overlap.

```R
michelle <-
  storms |>
  filter(name == "Michelle") |>
  mutate(observation = row_number()) |>
  select(wind, pressure, observation)
gg_michelle <-
  ggplot(michelle, aes(
    pressure, 
    wind, 
    color = observation, 
    label = observation
  )) +
  geom_point(alpha = 0.5) +
  geom_line(color = "black") +
  labs(
    x = "Pressure (hPa)",
    y = "Wind (knots)",
    title = "Hurricane Michelle",
    caption = "Source: National Hurricane Center"
  ) +
  guides(color = "none")
  
gg_michelle + 
  geom_text()
```
![[Pasted image 20260716190920.png]]


### Using repel
```R
gg_michelle + 
  geom_text_repel(max.overlaps = 50)
```
![[Pasted image 20260716190937.png]]


### Example 2
```R
count(gss_cat, partyid, marital, name = "count") |>
  mutate(
    partyid = fct_collapse( # Combine minor categories
      partyid,
      "Other/Missing" = c("No answer", "Don't know", "Other party")
    )
  ) |>
  ggplot(aes(
    count, 
    partyid, 
    fill = marital, 
    colour = marital, 
    label = count
    )
  ) +
  geom_col(width = 0.1) +
  ggrepel::geom_text_repel(
    max.overlaps = 100,
    position = position_stack(vjust = 0.5), size = 3, direction = "both") +
  labs(
    x = NULL,
    y = NULL,
    fill = "Marital Status",
    color = "Marital Status",
    title = "Party Affiliation of GSS Participants",
    caption = 'Source: R package "forcats"'
  )
```
![[Pasted image 20260716191014.png]]


# Text for Groups of Data Points
- Use `directlabels::geom_dl()` to print group labels in close proximity to the corresponding data points and remove the corresponding legend.
- Use `ggforce::geom_mark_ellipse()` to draw enclosing ellipses around data point groups
- Use `ggforce::geom_mark_hull()` to draw nearly convex hulls around data point groups

```R
gg_iris <-
  ggplot(
    iris,
    aes(
      Petal.Length, 
      Petal.Width, 
      colour = Species, 
      label = Species
    )
  ) +
  geom_jitter(alpha = 0.5) +
  labs(
    x = "Petal Length (cm)",
    y = "Petal Width (cm)",
    caption = "Source: Edgar Anderson (1935)"
  )
  
gg_iris + 
  labs(title = "Category Names in the Legend")
```
![[Pasted image 20260716192810.png]]

```R
gg_iris + directlabels::geom_dl(method = "smart.grid") +
  labs(title = "Category Names in the Plot") + guides(color = "none")
```
![[Pasted image 20260716192822.png]]

```R
gg_iris + xlim(0.8, 7.3) + ylim(-0.1, 2.7) +
  ggforce::geom_mark_ellipse() + guides(colour = "none") +
  labs(title = "Group Label and Enclosing Ellipse")
```
![[Pasted image 20260716193028.png]]



```R
gg_iris + xlim(0.8, 7.3) + ylim(-0.1, 2.7) +
  ggforce::geom_mark_hull() + guides(colour = "none") +
  labs(title = "Group Label and Hull")
```
![[Pasted image 20260716193033.png]]




