
Variables with measured or count data might have thousands of distinct values. A basic step in exploring your data is getting a “typical value” for each feature (variable): an estimate of where most of the data is located (i.e., its central tendency).

> [! Key Terms for Estimates of Location]
> 	Mean
> 		The sum of all values divided by the number of values.
> 		Synonym
> 			Average
> 	Weighted Mean
> 		The sum of all values times a weight divided by the sum of the weights.
> 		Synonym
> 			Weighted Average
> 	Median
> 		The value such that one-half of the data lies above and below
> 		Synonym
> 			50th Percentile
> 	Percentile
> 		The value such that P percent of the data lies below.
> 		Synonym
> 			Quantile
>	Weighted Median
>		The value such that one-half of the sum of the weights lies above and below the sorted data.
>	Trimmed Mean
>		The average of all values after dropping a fixed number of extreme values.
>		Synonym
>			Truncated Mean
>	Robust
>		Not sensitive to extreme values.
>		Synonym
>			Resistant
>	Outlier
>		A data value that is very different from most of the data.
>		Synonym
>			Extreme Value.


## Mean
The most basic estimate of location is the mean, or average value. The mean is the sum of all values divided by the number of values. 

You will encounter the symbol $\bar{x}$ ("x-bar") being used to represent the mean of a sample from a population.
The formula to compute the mean for a set of n values $x_1,x_2,...,x_n$ is:

Mean = $\bar{x}$ = $\frac{\sum^{n}_{i=1}x_i}{n}$

- N (or n) refers to the total number of records or observations.

## Trimmed Mean

A variation of the mean is a trimmed mean, which you calculate by dropping a fixed number of sorted values at each end and then taking an average of the remaining values.

Representing the sorted values by $x_{(1)},x_{(2)},...,x_{(n)}$ where $x_{(1)}$ is the smallest value and $x_{(n)}$ the largest, the formula to compute the trimmed mean with p smallest and largest values omitted is:

Trimmed Mean = $\bar{x}$ = $\frac{\sum^{n-p}_{i=p+1}x_{(i)}}{n-2p}$

- A trimmed mean eliminates the influence of extreme values.

For example, in international diving the top score and bottom score from five judges are dropped, and the final score is the average of the scores from the three remaining judges.
This makes it difficult for a single judge to manipulate the score

## Weighted Mean

Another type of mean is a _weighted mean_ which you calculate by multiplying each data value $x_i$ by a user_specified weight $w_i$ and diving their sum by the sum of the weights.

Weighted Mean = $\bar{x_w}$ = $\frac{\sum^{n}_{i=1}W_iX_i}{\sum^{n}_{i=1}W_i}$ 

Main motivation for using weighted mean:
- Some values are intrinsically more variable than others, and highly variable observations are given a lower weight.
	- For example, if we are taking the average from multiple sensors and one of the sensors is less accurate, then we might downweight the data from that sensor
- The data collected does not equally represent the different groups that we are interested in measuring.
	- For example, because of the way an online experiment was conducted, we may not have a set of data that accurately reflects all groups in the user base. To correct that, we can give a higher weight to the values from the groups that were underrepresented.


## Median and Robust Estimates













































