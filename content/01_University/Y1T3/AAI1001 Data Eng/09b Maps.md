---
title: 09b Maps
tags:
  - Choropleth_Map
  - geom_sf
---
# How to visualize geospatial data


### We will be using `sf` for the geospatial data
```R
countries <- select(World, iso_a3, name)
head(countries, 10)

countries <- st_drop_geometry(countries) # Removes column
slice_head(countries, n =10)
```

## Using `geom_sf()`
#geom_sf
```R
ggplot(World, aes(fill = continents)) + geom_sf()
```
![[Pasted image 20260711151737.png]]


## Common Simple-Feature(SF) Geometry Types

| Geometry           | Description                                               |
| ------------------ | --------------------------------------------------------- |
| POINT              | Single coordinate pair                                    |
| LINESTRING         | Sequence of points connected by lines                     |
| POLYGON            | Sequence of connected line segments forming a closed loop |
| MULTIPOINT         | Set of points, treated as a unit                          |
| MULTILINESTRING    | Set of line strings, treated as a unit                    |
| MULTIPOLYGON       | Set of polygons, treated as a unit                        |
| GEOMETRYCOLLECTION | Collection of one or more geometries of any type          |

```R
metro |> st_is("POINT") |> all() # Gets all POINTs

ggplot() + geom_sf(data = World) + geom_sf(data = metro) # plots worldmap + points
```
![[Pasted image 20260711152155.png]]

### Line String Example
```R
World_rivers |>
	filter(name == "Ismailiya Canal") |>
	st_coordinates()
	
ggplot() +
	geom_sf(data = World, color = "grey") +
	geom_sf(data = World_rivers, color - "navyblue")
```
![[Pasted image 20260711152354.png]]

### Plot map of single country
```R
World |> filer(name == "South Africa") |>
	ggplot() + geom_sf()
```


# Importing Geospatial Data as `sf` objects

## Common geospatial file types
- JSON
- Geojson
- shp

 > They can be imported using `sf::read_sf()`
 

### Checking what type is the data
```R
sgp_pa |> st_geometry_type() |> head(4)

"singapore_by_planning_area_since_1999.geojson" |>
read_sf(type = 5) |> st_geometry_type() |> head(4)
# The `type = 5` casts ALL geometris to MultiLineString
ggplot(sgp_pa_5) + geom_sf()
```


# Handling Common Issues with Geospatial Data
Inherently more complex than tabular data
Complexity leads to issues before data can be analyzed or visualized.
- Topological errors such as overlapping or self-intersecting polygon
- More points in line strings and polygons than necessary, causing large files and slow rendering

## Repairing Invalid Geometries
Overlapping or self-intersecting polygons are common topological errors
```R
self_intersecting_pgon <-
  rbind(c(0, 4), c(4, 1), c(4, 3), c(0, 0), c(0, 4)) |>
  list() |> st_polygon() |> st_sfc()
ggplot(self_intersecting_pgon) +
  geom_sf(color = "red", linewidth = 3) +
  geom_sf( # Add points to the plot
    data = st_cast(self_intersecting_pgon, "POINT"),
    size = 5,
    shape = 16 # Filled circles, see ?points
  )
```
![[Pasted image 20260711153253.png]]


## Checking for validity
```R
st_is_valid(self_intersecting_pgon) # Identifies self-intersecting polygon as INVALID
# Returns: FALSE
```


## Try converting into valid by inserting intersection point as a vertex
```R
# Intersecting Point is (2.666667, 2)
valid_mpgon <- st_make_valid(self_intersecting_pgon) # changes type to MULTIPOLYGON
st_geometry_type(valid_mpgon)

st_coordinates(valid_mpgon)
```
![[Pasted image 20260711153556.png]]

```R
ggplot(valid_mpgon) +
  geom_sf(color = "red", linewidth = 3) +
  geom_sf(
    data = st_cast(valid_mpgon, "POINT"),
    size = 5,
    shape = 16
  )
```
![[Pasted image 20260711154423.png]]


## Simplifying Line Strings and Polygons
A general rule of thumb is that maps typically do not require more than 10,000 boundary points
- The number of boundary points can be determined using `mapview::npts()`
```R
library(mapview)
npts(subzones) # 58797
```

Using `rmapshaper::ms_simplify()` can effectively reduce the number of points
```R
library(rmapshaper)
simplified <- ms_simplify(subzones)
npts(simplified) # 5365
```

> Drawbacks
> - Islands and some detail of shapes have been removed by the simplification
> - Overall, the differences between the 2 maps are barely visible
> - Simplifying can significantly reduce num of points, resulting in faster calculations and quicker rendering, **while** maintaining almost the same visual appearance

![[Pasted image 20260711154921.png]]


# Map Projection
Earth's surface is spherical
Any map displayed on flat 2D surface must be a mathematical projection
[Gauss's Theorema Egregium](https://en.wikipedia.org/wiki/Theorema_Egregium) states that there is no distortion-free projection that can flatten a sphere.

## Coordinate Reference Systems
Map projections are encoded using a Coordinate Reference System(CRS)
These parameters can be retrieved for a given `sf` object using `st_crs()` 
```R
st_crs(World, parameters = TRUE)[c("Name", "srid")]
# $Name "WGS 84"
# $srid "EPSG:4326"
```

> When plotting `sf` object with WGS 84 projection, longitude is mapped to x-axis and latitude to y-axis

Lines of constant longitude and latitude intersect at right angles on the map, latitude differences are scaled proportionally into y-coordinate differences, this is referred to as "equirectangular"
- This significantly distorts areas and shape.
Example: Greenland and Australia look comparable in area, **BUT** in reality Greenland only has 28% of Australia's land area.

```R
gg_world <- ggplot(World) +
  geom_sf() +
  geom_sf(
    aes(fill = name),
    data = filter(World, name %in% c("Greenland", "Australia"))
  ) +
  scale_fill_manual(values = c("Greenland" = "red", "Australia" = "blue")) +
  guides(fill = "none") +
  theme(
    panel.background = element_blank(),
    panel.grid = element_line(color = "black"),
    panel.ontop = TRUE
  )
gg_world + labs(title = "Equirectangular Pojection")
```
![[Pasted image 20260711155730.png]]

Equirectangular projection is suboptimal because area on map is uninterpretable as data value

It is **Preferable** to choose an equal-area projection (Projection that faithfully represents area proportions)

### List of equal-area projections
- Behrmann Projection (SRID ESRI:54017)
- Equal Earth Projection (SRID ESRI:54035)
- Eckert IV Projection (SRID ESRI:54012)
- Sinusoidal Projection (SRID ESRI:54008)
- Mollweide (SRID ESRI:54009)

## How to transform to an equal-area projection
```R
gg_world + labs(title = "Equirectangular Pojection")
gg_world + coord_sf(crs = "ESRI:54035") + labs(title = "Equal Earth Projection")
```
![[Pasted image 20260711160154.png]]


![[Pasted image 20260711160219.png]]
- Behrmann projection: The poles are stretched into horizontal lines and all parallels are equally long. Stark contrast with reality as poles are points without length.

- Equal Earth projection: The poles are stretched into horizontal lines but are shorter than the equator. Both antimeridians are curved, meeting the pole lines at an obtuse angle.

- Eckert IV projection: Similar to the Equal Earth projection, but the antimeridians smoothly merge into the pole lines without any sharp corners.

- Sinusoidal projection: The poles are correctly depicted as single points. The eastern and western antimeridian meet at the poles, forming a sharp corner.

- Mollweide projection: Similar to the sinusoidal projection, but the antimeridians merge into each other without any sharp corners at the poles.



# Choropleth Maps

Characteristics of #Choropleth_Map
Variable to be visualized consists of 1 number or category per region
Region **DO NOT** overlap
Region are filled with colors that **represent** the variable
Regions are determined before data are collected (division by country)
	- Opposite: Dasymetric Maps
Variable is (Categorical or quantitative), not expected to depend significantly on region's spatial extent
	Example:
	1. Ratio of 2 variable that both scale approximately into proportion to area (GDP per capita)
	2. Percentage of a subset from the total number of observations (percentage of unemployed individuals in population)
	3. Spatial density in units of inverse area (Number of solar panels per square kilometer)
	4. Rate of change in percent (Increase in GDP from 1 year to next)

### Example Data
```R
atm <-
  "API_FB.ATM.TOTL.P5_DS2_en_excel_v2_2342.xls" |>
  readxl::read_xls(skip = 3) |>
  select(
    country = `Country Name`,
    code = `Country Code`,
    atm_2021 = `2021`
  )
world <-
  World |>
  left_join(atm, by = c("iso_a3" = "code")) |>
  select(country, code = iso_a3, area, atm_2021)
```

### Plotting
```R
earth <- st_polygon(
  x = list(
    cbind(
      c(rep(-180, 181), rep(180, 181), -180), c(-90:90, 90:-90, -90)
    )
  )
) |>
  st_sfc() |>
  st_set_crs(4326) |> # Equirectangular projection
  st_as_sf()

gg_atm_2021 <-
  ggplot() +
  geom_sf(data = earth, fill = "lightblue1") +
  geom_sf(aes(fill = atm_2021), data = world, color = "black") +
  labs(
    fill = NULL,
    title = "Automated Teller Machines per 100,000 Adults in 2021"
  ) +
  coord_sf(crs = "ESRI:54035") +
  theme_void() +
  theme(
    legend.margin = margin(5, 0, 0, 0), # Increase margin above legend
    legend.key.width = unit(1.25, "cm"),
    legend.frame = element_rect(), # Add a frame around the colorbar
    legend.position = "top",
    plot.title = element_text(face = "bold", hjust = 0.5),
  )
gg_atm_2021
```


## Choosing a suitable palette
You can use palettes from [ColorBrewer website](https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3)

You can access palettes through `scale_fill_fermenter()` for ordinal and quantitative data
If data is nominal, use `scale_fill_brewer()`
```R
gg_atm_2021 <-
  gg_atm_2021 +
  scale_fill_fermenter(
    breaks = scales::breaks_log(n = 6), # log scaled because data is right-skewed
    palette = "Greens",
    direction = 1,
    na.value = "gray80"
  )
gg_atm_2021
```

### Guidelines for choosing suitable palette
- Opt for sequential palette if variable is non-negative and either ordinal or quantitative
- When displayed on white background, lighter colors should represent smaller values
- For variables with both positive and negative values, choose a diverging palette. Lightest color represents zero
- For nominal variables, use ColorBrewer's qualitative palettes


## Adding Missing Values to Legend
```R
# The fill color of this legend entry is set to the same color,
# `gray80`, as the missing values in the map.

# The `order` argument of the `guide_*()` functions is used to
# shift the missing value from the start to the end of the legend.

gg_atm_2021 <-
  gg_atm_2021 +
  aes(color = NA) +
  guides(
    fill = guide_colorsteps(order = 1),
    color = guide_legend(override.aes = list(fill = "gray80"), order = 2)
  )
gg_atm_2021


# To fine-tune the legend, "colour" should be removed, 
# and "NA" can be replaced by the more descriptive "Missing".

gg_atm_2021 <-
  gg_atm_2021 +
  labs(color = NULL) +
  scale_color_manual(labels = "Missing", values = "black") +
  theme(legend.text.position = "bottom")
gg_atm_2021
```


## Adding Labels
To improve readability, label **AT LEAST** the largest geographic units

Use `geom_sf_text()` 
The label color should be chosen such that it provides a clear contrast against the background color
```R
gg_atm_2021 <-
  gg_atm_2021 +
  geom_sf_text(
    aes(label = code),
    data = filter(
      world,
      min_rank(desc(area)) <= 20 & (is.na(atm_2021) | atm_2021 <= 30)
    ),
    color = "black",
    size = 1.7
  ) +
  geom_sf_text(
    aes(label = code),
    data = filter(
      world,
      min_rank(desc(area)) <= 20 & atm_2021 > 30
    ),
    color = "white",
    size = 1.7
  )
gg_atm_2021
```


