#Pandas 

To apply deep learning in the wild we must extract messy data stored in arbitrary formats, and preprocess it to suit our needs.


## Reading the Dataset

Comma-separated values (CSV) files are ubiquitous for the storing of tabular (spreadsheet-like) data.

To demonstrate how to load CSV files with `pandas`, we create a CSV file below `../data/house_tiny.csv`. This file represents a dataset of homes, where each row corresponds to a distinct home and the columns correspond to the number of rooms (`NumRooms`), the roof type (`RoofType`), and the price (`Price`).
```python
# Creating Dataset
import os

os.makedirs(os.join('..', 'data'), exists_ok=True)
data_file = os.path.join('..', 'data', 'house_tiny.csv')
with open(data_file, 'w') as f:
	f.write('''NumRooms,RoofType,Price
	NA,NA,127500
	2,NA,106000
	4,Slate,178100
	NA,NA,140000''')
```


```python 
# Reading Dataset
import pandas as pd

data = pd.read_csv(data_file)
print(data)

#    NumRooms RoofType   Price
# 0       NaN      NaN  127500
# 1       2.0      NaN  106000
# 2       4.0    Slate  178100
# 3       NaN      NaN  140000
```


## Data Preparation

In supervised learning, we train models to predict a designated _target_ value, given some set of _input_ values
- Our first step in processing the dataset is to separate out columns corresponding to input versus target values. We can select columns either by name or via integer-location based indexing (`iloc`).

Depending upon the context, missing values might be handled either via _imputation_ or _deletion_. 
- Imputation replaces missing values with estimates of their values  
- Deletion simply discards either those rows or those columns that contain missing values.


For categorical input fields, we can treat `NaN` as a category.

Since the `RoofType` column takes values `Slate` and `NaN`, `pandas` can convert this column into two columns `RoofType_Slate` and `RoofType_nan`.
A row whose roof type is `Slate` will set values of `RoofType_Slate` and `RoofType_nan` to 1 and 0, respectively. The converse holds for a row with a missing `RoofType` value.

```python
inputs, targets = data.iloc[:, 0:2], data.iloc[:, 2]
inputs = pd.get_dummies(inputs, dummy_na=True)
prints(inputs)

#    NumRooms  RoofType_Slate  RoofType_nan
# 0       NaN           False          True
# 1       2.0           False          True
# 2       4.0            True         False
# 3       NaN           False          True
```

> [!MY NOTE]
> inputs = data.iloc[:, 0:2] gets all features except the target value of Price 
> (Rows All, Cols idx 0-1)
> 
> targets = data.iloc[:, 2] gets only the Price 
> (Rows All, Cols idx 2 ONLY)
> 
> pd.get_dummies Converts categorical variable into dummy variable
> dummy_na=True Adds a col to indicate NaNs
> [Pandas.get_dummies](https://pandas.pydata.org/docs/reference/api/pandas.get_dummies.html)


For missing numerical values, one common heuristic is to replace the `NaN` entries with the mean value of the corresponding column.
```python
inputs = inputs.fillna(inputs.mean())
prints(inputs)

#    NumRooms  RoofType_Slate  RoofType_nan
# 0       3.0           False          True
# 1       2.0           False          True
# 2       4.0            True         False
# 3       3.0           False          True
```


## Conversion to Tensor Format
#Tensor 

Now that all the entries in `inputs` and `targets` are numerical, we can load them into a tensor
```python
import torch

X = torch.tensor(inputs.to_numpy(dtype=float))
y = torch.tensor(targets.to_numpy(dtype=float))
X, y

# (tensor([[3., 0., 1.],
#          [2., 0., 1.],
#          [4., 1., 0.],
#          [3., 0., 1.]], dtype=torch.float64),
#  tensor([127500., 106000., 178100., 140000.], dtype=torch.float64))
```







































