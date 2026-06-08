---

---

## 11. R Type Coercion Hierarchy

When a vector contains mixed types, R automatically promotes everything to the most flexible type.

### The Hierarchy

```
logical → integer → numeric → character
(least flexible)              (most flexible)
```

### Example Questions

```r
c(TRUE, FALSE, 1L, 2.5)   # numeric  — 2.5 forces everything to numeric
c(TRUE, FALSE, 1L)         # integer  — 1L forces logical up to integer
c(TRUE, FALSE, "hello")    # character — "hello" forces everything to character
c(1L, 2L, 3.5)             # numeric  — 3.5 forces integers to numeric
```

### Watch Out For

- `L` suffix means integer, NOT character — `1L` is the integer 1
- `TRUE`/`FALSE` become `1`/`0` when coerced to integer or numeric
- The whole vector takes the type of its most flexible element

---

## 12. Type Casting — `as.integer()` and `as.numeric()`

R's casting behaviour is different from Python and other languages.

### `as.integer()` — Truncates, Never Rounds


```r
as.integer(3.9)    # 3 — NOT 4, decimal is chopped off
as.integer(3.1)    # 3
as.integer(-3.9)   # -3 — toward zero, not -4

# If you want rounding, do it explicitly first
as.integer(round(3.9))   # 4
```

> **Memory trick:** `as.integer()` is a chainsaw — it cuts cleanly with no rounding.

### `as.numeric()` On Strings — Returns NA With Warning, Never Errors


```r
as.numeric("hello")   # NA — with warning: NAs introduced by coercion
as.numeric("3.14")    # 3.14 — works if string looks like a number
as.numeric("1e3")     # 1000 — scientific notation also works
```

> **Key insight:** R never crashes on bad conversions — it returns `NA` silently. This is why NA handling is so critical.

### Watch Out For

- `as.integer()` truncates — never assume it rounds
- Failed `as.numeric()` conversions produce `NA` with a warning, not an error
- Always check for `NA` after casting from character to numeric

---

## 13. NA Behaviour — Complete Reference

### The Core Rules


```r
NA == NA              # NA  — never TRUE, use is.na() instead
is.na(NA)             # TRUE — correct way to check for NA
mean(c(1, 2, NA))     # NA  — contagious by default
sum(c(1, 2, NA))      # NA  — contagious by default
mean(c(1, 2, NA), na.rm = TRUE)   # 1.5 — removes NA first
sum(c(1, 2, NA),  na.rm = TRUE)   # 3   — removes NA first
```

### na.rm Parameter


```r
na.rm = FALSE   # default — keeps NA, result is NA
na.rm = TRUE    # removes NA before calculating
```

> Works the same way for `sum()`, `mean()`, `min()`, `max()`, `sd()`

### Watch Out For

- `NA == NA` is a classic trap — always returns `NA`, never `TRUE`
- `na.rm = FALSE` is the default — always add `na.rm = TRUE` when data may have NAs
- `as.numeric()` on non-numeric strings silently creates NAs

---

## 14. Quarto — Render Order and Key Advantages

### Render Order

```
.qmd file
   ↓
knitr     → executes all R code chunks → produces .md file
   ↓
pandoc    → converts .md into finished format (HTML, PDF, Word, etc.)
   ↓
finished output
```

> **Memory trick:** Knitr runs the **K**ode first. Pandoc just prints it.

### Quarto vs Traditional Word Processors

|Quarto|Traditional (MS Word, Google Docs)|
|---|---|
|Separated content and formatting|Coupled content and formatting|
|Reproducible document|Static document|
|Combines text + code + output|Limited code integration|
|Markdown portable plain text|Portability issues|
|Efficient version control (Git)|Not version control friendly|
|Output: HTML, PDF, Word, Revealjs|Output: Word, PDF only|

### Watch Out For

- Quarto does NOT fix grammar, check spelling, or write content
- knitr always comes before pandoc — never the other way around
- `.qmd` extension is specific to Quarto documents

---

## 15. Time Series Components

### The Four Components

```
Trend      → long-term direction (upward, downward, flat)
Seasonal   → fixed, predictable repeating pattern
             e.g. sales spike every December
Cyclical   → irregular wave-like fluctuations over longer periods
             e.g. economic boom/bust over years
Residual   → random noise left after removing the above three
```

### Seasonal vs Cyclical — Common Confusion

```
Seasonal  → fixed interval (every year, every quarter)
Cyclical  → irregular interval, longer duration (years to decades)
```

### What Is NOT A Component

- **Stationarity** — a property of the series, not a component
- **Autocorrelation** — a statistical measure, not a component

---

## 16. Stationarity and Random Walk

### Stationarity

> A stationary time series has **constant mean, constant variance, and no trend** over time. It looks statistically the same regardless of when you observe it.

```
Stationary     → constant mean, constant variance
Non-stationary → drifting mean or growing variance (e.g. random walk)
```

### Random Walk — Critical Definition

```
Y(t) = Y(t-1) + ε(t)

where ε(t) = random error (white noise)
```

> **Common misconception:** A random walk is NOT purely random. Each value depends on the previous value plus a random shock. The "random" part is only the change, not the value itself.

```
Random walk  → NOT stationary (mean drifts, variance grows)
White noise  → IS stationary (each value truly independent)
```

> **Memory trick:** Random walk = **yesterday + surprise**. White noise = **pure surprise**.

---

## 17. ARIMA Model — Definition and Parameters

### ARIMA(p, d, q)

|Parameter|Name|Meaning|
|---|---|---|
|p|AutoRegressive order|How many past **values** to include|
|d|Integrated (differencing) order|How many times to difference to achieve stationarity|
|q|Moving Average order|How many past **errors** to include|

### What Each Parameter Does

r

```r
# AR — current value depends on past values
ARIMA(2,0,0): Y(t) = Y(t-1) + Y(t-2) + error

# I — difference the series to make it stationary
d=1: use Y(t) - Y(t-1) instead of Y(t)
d=0: series is already stationary

# MA — current value depends on past errors
ARIMA(0,0,2): Y(t) = error(t) + error(t-1) + error(t-2)
```

### Memory Trick

```
p → "Past values"     (autoregressive)
d → "Differencing"    (make stationary)
q → "eQuation error"  (moving average of past errors)
```

### Special Cases

```
ARIMA(0,1,0) → random walk (one differencing, no AR, no MA)
ARIMA(1,0,0) → AR(1) model
ARIMA(0,0,1) → MA(1) model
```

---

## 18. ACF and PACF — Model Selection

### What They Measure

```
ACF  (AutoCorrelation Function)
     → correlation with past values INCLUDING indirect effects
     → used to identify q (MA order)

PACF (Partial AutoCorrelation Function)
     → correlation with past values EXCLUDING indirect effects
     → used to identify p (AR order)
```

### Memory Trick

```
PACF → P → tells you p
ACF  → what's left → tells you q
```

### How To Read The Plots

```
"Cuts off at lag n" means significant spikes stop after lag n
→ use n as your order

PACF cuts off after lag 1 → p = 1
PACF cuts off after lag 2 → p = 2
ACF cuts off after lag 1  → q = 1
ACF cuts off after lag 2  → q = 2
```

### Watch Out For

- PACF cuts off at lag 1 → p = **1**, not p = 2
- ACF → q, PACF → p — never mix these up
- d is determined by how many differences are needed, not from ACF/PACF