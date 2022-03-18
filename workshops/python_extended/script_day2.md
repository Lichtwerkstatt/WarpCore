# Data Science Stack
- Python Modules
  - [Pandas](https://pandas.pydata.org/) ([Tutorial](https://www.w3schools.com/python/pandas/default.asp))
  - [Numpy](https://numpy.org/) ([Tutorial](https://www.w3schools.com/python/numpy/default.asp))
  - [MatPlotLib](https://matplotlib.org/) ([Tutorial](https://www.w3schools.com/python/matplotlib_intro.asp))
  - [SciKit](https://scikit-learn.org/stable/)

# Introduction into Jupyter Notebooks


# Introduction into Numpy 

## Comparison between Fields and Arrays

- compare lists and arrays
```python
x = [a for a in range(1,10)]
x*2
x**2
```
```python
import numpy as np
n = np.arange(10)
n*2
n**2
```

## Initialize Numpy Arrays
- initialize numpy arrays
  - np.array(x)
  - np.zeros
  - np.ones
- methods
  - .mean()
  - .min()
  - .max()

## Filter Numpy Arrays
```python
a = np.arange(10)
a[1:4]
a[1:-3]
a[-5:]
c = a>=5
a[c]
a[a<5]
```

## Read Data with Pandas
- different ways of processing text files: 
```python
with open("datei.csv") as file:
    for line in file:
        data = line.strip().split(";")
        print(data[0] + ": " + data[1])
```
- convinient for CSV and Exsel is the Pandas Module:
```python
import pandas as pd
df = pd.read_csv("../data/astronauts.csv")
# df = pd.read_csv("../data/astronauts.csv", delimiter=";")
```
- accessing dataframe like numpy arrays:
```python
df.head()
len(df)
df["Name"]
df["Name"][20]
for name in df["name"]:
  print(name)

#accessing row:
df.iloc[21]
df.iloc[4:8]
df.iloc[21]["Name"]
type(df.iloc[20]["Gender"])
```

## Rebuilding Data Structures based on DataFrame
```python
for row in df.iterrows():
  pos = row[0]
  data = row[1]
  print(pos)
  print(data)
#shorter:
for pos, data in df.iterrows():
  print(pos)
  print(data)
```

## Filtering Data in Pandas
```python
df["Year"]
df["Year"] < 1990
df[df["Year"] < 1990]
# combine filters
df2 = df[df["Year"] < 1990]
df3 = df[df["Gender"] == "Male"]

# combine with boolean operators
filter1 = df["Year"] == 1990
filter2 = df["Year"] < 1960
df[(filter1)|(filter2)] # use bitwise boolean operators & | ^ ~ 
```

## Sort Data in Pandas
```python
dfSort= df.sort_values("Name", ascending=False)
names = [] 
for name in dfSort["Name"]:
    names.append(name) # build fields out of DataFrames
pd.DataFrame(names) #build DataFrames out of fields
```

## Matplotlib
```python
import matplotlib.pyplot as plt
plt.plot([1,2,3],[-3,4,5], color="#ff0000", linestyle="dashed", marker="o", label="Value 1")
plt.plot([1,2,4],[3,2,1], color="#00ff00", label="Value 2")
plt.legend()
plt.show()
```
- other plot types in matplotlib
  - **basic** : plot, scatter, bar,...
  - **fields** : contour, colormesh, quiver, steamplot, ...
  - **statistics** : histogram, boxplot, pie charts
  - **unstructured** : tricontour, triplot

```python
excel = pd.read_excel("daten.xlsx")
year = df["Jahr"]
sales = df["Umsatz"]
plt.plot(year,sales)
plt.show()
```

```python
df = pd.read_csv("../data/names.csv")
df2 = df[df["Name"] == "Anna"]
df3 = df2[df2["Gender"] == "F"]
df4 = df3[df3["State"] == "CA"]
df5 = df4.sort_values("Year")
plt.plot(df5["Year"], df5["Count"])
plt.legend()
plt.show()
```

## Linear and Polynomial Regression

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn import linear_model

x = np.arange(0,5,0.1)
y = 2.2*x+3.3 + np.random.normal(0,1,x.shape)

x = x.reshape((-1,1))

regr = linear_model.LinearRegression()
regr.fit(x,y)
print(regr.intercept_, regr.coef_)
y_pred = regr.predict(x)

y_eval = regr.coef_[0]*x + regr.intercept_

plt.scatter(x,y)
plt.plot(x,y_pred, color="red")
plt.plot(x,y_eval, color="yellow")
plt.show()
```

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression

x = np.arange(-10,10,2)
y = (x-4)**2 + x -10 + np.random.normal(0,1,x.shape)

poly = PolynomialFeatures(degree=2, include_bias=False)
poly_features = poly.fit_transform(x.reshape(-1, 1))

poly_reg_model = LinearRegression()
poly_reg_model.fit(poly_features, y)
print(poly_reg_model.intercept_, poly_reg_model.coef_)
y_predicted = poly_reg_model.predict(poly_features)

plt.figure(figsize=(10, 6))
plt.title("Your first polynomial regression – congrats! :)", size=16)
plt.scatter(x, y)
plt.plot(x, y_predicted, c="red")
plt.show()
```