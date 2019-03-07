In this folder are two notebooks, one for R and another for R running
each example of this file, also in this folder in ejemplo.* are the mtcars
database

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

Now to access data R treats data frames  values as a matrix, so you can
access using the [  ] accesors

```R
mtcars = read.csv("ejemplo.csv”)
mtcars[3,5]
```
Python needs to know that you’re accusing data as matrix using the values
operand
```python
mtcars = read.csv("ejemplo.csv”)
mtcars.values[0,4]
```
This lead to a big difference and is that R is 1 indexed and python is 0
indexed

To access tabular data just use the column name in both R and Python,
```python
mtcars["hp"]
```
The main difference is R returns a data frame but python returns an array,
opposite to
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
In Python indexes can’t be mixed with locations, to specify a location
by its integer index you need to specify the .iloc property
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
With this syntaxes we can access sub segments of the data frame using
array notation or slice notation

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

Now let's play directly with operators, with both Python and R we can do
element wise operations with dataframes, for example

R

```R
mtcars[4] > 200
```

And with Python

```python
mtcars["hp"]> 200
```

Both operations take a dataframe column and compare each value with
the integer value, building a new dataframe with the same indexes and
a boolean value, representing the operation result.

We can nest this operation with an accesor operation, filtering all the
dataframe

R
```R
mtcars[mtcars[4] > 200,]
```

python

```python
mtcars[(mtcars["hp"]> 200)]
```

And more interesting , logical operators like and (&) or (|) and not (~)
can also be used.

R
```R
mtcars[4] > 200 & mtcars[10] > 3
```

```python
(mtcars["hp"]> 200) & (mtcars["gear"] > 3)
```

A natural consequence is that we can have nested operations in our queries

R
```R
mtcars[mtcars[4] > 200 & mtcars[10] > 3,]
```

Python
```
mtcars[(mtcars["hp"]> 200) & (mtcars["gear"] > 3)]
```

We can also append new columns to our dataframe

R
```R
mtcars["i_like"] = mtcars[4] > 200 & mtcars[10] > 3
```
Python
```python
mtcars["i_like"] = (mtcars["hp"]> 110) & (mtcars["cyl"] > 10)
```


And more, we can set values to our filter column
R
```
mtcars[mtcars["i_like"]==TRUE,"i_like"] = "I like it"
mtcars[mtcars["i_like"]==FALSE,"i_like"] = "I dont like it"
```

```python
mtcars.loc[mtcars["i_like"] == True, "i_like"] = "I like it"
mtcars.loc[mtcars["i_like"] == False, "i_like"] = "I dont like it"
```