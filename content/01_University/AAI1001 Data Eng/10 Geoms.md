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





