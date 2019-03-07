First we need to create a common way to compare, we want to use Jupyter

```bash
conda create --name datamining
conda install jupyter
conda install -c r r-irkernel
```
Also we need to install pandas for python
```bash
conda install pandas
```
First we’re going  to read a csv in R
```R
read.csv("ejemplo.csv")
```
And with Python
```python
import pandas as pd
pd.read_csv("ejemplo.csv”)
```

Now to read data with excel
With r first install

```R
install.packages("gdata")
```

```R
library(gdata)
read.xls("ejemplo.xls”)
# Or read a custom sheet
read.xls("ejemplo.xls", sheet="mtcars")
```

With python

First install
```
pip install xlrd
```
Then
```
pd.read_excel("ejemplo.xls”)
# Or a sheet
pd.read_excel(“ejemplo.xls", sheet_name="mtcars")
```

Now to access data R treats data frames  values as a matrix, so you can access using the [  ] accesors

```R
mtcars = read.csv("ejemplo.csv”)
mtcars[3,5]
```
Python needs to know that you’re accusing data as matrix using the values operand
```python
mtcars = read.csv("ejemplo.csv”)
mtcars.values[0,4]
```
This lead to a big difference and is that R is 1 indexed and python is 0 indexed

To access tabular data just use the column name in both R and Python,
```python
mtcars["hp"]
```
The main difference is R returns a data frame but python returns an array, opposite to
```python
mtcars[["hp"]]
```
Where R returns a array while Python return a data frame

To access all tabular data in R, you need to specify
```R
mtcars[c("mpg", "cyl”)]
```
While in python you need to use double square brackets and the column names
```python
mtcars[["mpg", "cyl"]]
```
Accesing via column indexes is posible

R
```R
mtcars[1:2]
```
In python you need to specify the iloc property (index location)
```python
mtcars.iloc[:,0:2]
```
And to access a single row

R
```R
mtcars[1,]
```
In Python indexes can’t be mixed with locations, to specify a location by its integer index you need to specify the .iloc property
```python
mtcars.iloc[[1]]
```
Both seems different but to select multiples rows

R
```R
mtcars[c(1,3,5),]
```
Python
```python
mtcars.iloc[[0,2,4]]
```
With this syntaxes we can access sub segments of the data frame using array notation or slice notation

R
```R
mtcars[c(1,3,5),c(1,3,5)]
mtcars[1:3,1:3]
```
Python

```python
mtcars.iloc[[0,2,4], [0,2,4]]
mtcars.iloc[0:3,0:3]
```