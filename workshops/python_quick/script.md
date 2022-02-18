# Introduction into Python (Quick)

**Date** : February, 19th 2022  
**Time** : 9am - 12  
**Place** : ACP SR2, online

## Sources
* [Official Python Documentation](https://docs.python.org/3/)
* [Python Guide](https://docs.python-guide.org/)  
* [Write Python with Style](https://docs.python-guide.org/writing/style/)  
* [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)  

## Workshop Prep
* Download and Install [Anaconda](https://www.anaconda.com/products/individual)
* [ ] Download Data Package and prepare a workshop folder 

---
# Script

## Prior Workshop
- content = basic concepts of Input, Output, Calculations, Conditions, Repititions
- goal: learn how to program and work in a basic science data workflow
- no extended data structures, loops, conditions, objects, lambdas, libraries, user interfaces, compact code etc.
- use ressources:
  - online guides (see above)
  - youTube tutorials
  - stack overflow (google error messages)
- Practice! Practice! Practice!

## Introduction
- Programming a von-Neumann-architecture
- machine and high level programming
- script languages
- history of Python

## Python Usage
- command line
  - interactive mode
  - run Python file
- spyder
  - Editor
    - AutoComplete
    - Syntax Highlighting
    - Context help
  - Console Window
  - Variables Overview

## Syntax, Error Handling and Basics on In- and Output
- [Syntax](https://www.w3schools.com/python/python_syntax.asp)
  - line by line
  - intended blocks
  - [comments](https://www.w3schools.com/python/python_comments.asp)
- Variables
```python
# This is a comment
message = "Hello World" 
print(message)
```
- Input
```python
# Asking for user name
name = input("What's your name?") 
print("Hello "+ name)
```
- Handling error messages
  - which file
  - which line
  - kind of error

## Variables and Types
```python
number1 = 21
number2 = 19
sum = number1 + number2
print(sum)
```
- variables are dynamically typed
- Using Python [Operators](https://www.w3schools.com/python/python_operators.asp)
  - different meanings based on data type (for example plus) 
- check for types after input and before output = [TypeCasting](https://www.w3schools.com/python/python_casting.asp)

```python
number1 = input("Please enter first number: ")
number2 = input("Please enter second number: ")
sum = float(number1) + float(number2) # int or float
print("The sum is "+str(sum))
```

### Bonus Knowledge
- simple [data types](https://www.w3schools.com/python/python_datatypes.asp) in python
  - **numeric** : int(eger), float, complex
  - **text** : str(ing)
  - **boolean** : bool(ean)
  - **binary** : bytes, bytearray, memoryview
- [Fancy ways](https://docs.python.org/3/tutorial/inputoutput.html) of string formatting

## [Conditions](https://www.w3schools.com/python/python_conditions.asp)
```python
number1 = float(input("Please enter first number: "))
number2 = float(input("Please enter second number: "))
if number1 < number2:
  print("First is smaller then second number")
elif number1 > number2:
  print("First is larger then second number")
else:
  print("Both numbers are equal")
```
- Conditions evaluate to boolean value (True/False) `type(2<5)` -> `bool`
- arithmic compare ops : `==, !=, <, >, >=, <= `
- boolean ops: and, or, not

### Bonus Knowledge
- short one liner if statement `x=('yes' if True else 'no')`

### Task
- write a little calculator where one can select operations (+, -, *, /)

## Complex Data Types ([Lists](https://www.w3schools.com/python/python_lists.asp))
- define: `a=[1,"hello",2,4.0]`
- access: `a[0]`
- data types: `type(a[1])`
- complex data types come with [methods](https://www.w3schools.com/python/python_ref_list.asp)
  - append()
  - clear()
  - sort()
  - reverse()
  - etc.

### Bonus Knowledge
- complex data types in Python:
  - **sequence types** : [tuple](https://www.w3schools.com/python/python_tuples.asp), range
  - **mapping types**: [dict](https://www.w3schools.com/python/python_dictionaries.asp)
  - **set types**: [set](https://www.w3schools.com/python/python_sets.asp), frozenset



## Loops
- [while](https://www.w3schools.com/python/python_while_loops.asp) loop:
```python
currentInput = ""
numbers = []
while (currentInput != "n"):
  currentInput = input("Add a number? (n for none) : ")
  if currentInput != "n":
    numbers.append(float(currentInput))
    print("You now have entered "+len(numbers)+" numbers")
```

-[for](https://www.w3schools.com/python/python_for_loops.asp) loop:
```python
for x in [1,2,3,4,5]:
  print(x)
```
- you can use any object for counting, most common `range(start, stop, step)`
- `even = [x for x in range(1,10) if x%2 == 0 ]`

```python
result = 0
for x in numbers
  result = result + x
```

## Task
- write the same functionality for product
- let the user choose the operation
- let the user choose if he wants to restart or quit the program

### Bonus Knowledge
- loops allows `continue`and `break`


# Data Science Stack
- Python Modules
  - [Pandas](https://pandas.pydata.org/) ([Tutorial](https://www.w3schools.com/python/pandas/default.asp))
  - [Numpy](https://numpy.org/) ([Tutorial](https://www.w3schools.com/python/numpy/default.asp))
  - [MatPlotLib](https://matplotlib.org/) ([Tutorial](https://www.w3schools.com/python/matplotlib_intro.asp))
  - [SciKit](https://scikit-learn.org/stable/)

## Numpy Arrays
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
- initialize numpy arrays
  - np.array(x)
  - np.zeros
  - np.ones
- methods
  - .mean()
  - .min()
  - .max()

-filter numpy arrays
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
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression

x = np.arange(-10,10,2)
y = (x-4)**2 + x -10 + np.random.normal(0,1,x.shape)

plt.figure(figsize=(10,6))
plt.scatter(x, y)
plt.show()

poly = PolynomialFeatures(degree=2, include_bias=False)
poly_features = poly.fit_transform(x.reshape(-1, 1))

poly_reg_model = LinearRegression()
poly_reg_model.fit(poly_features, y)
y_predicted = poly_reg_model.predict(poly_features)

plt.figure(figsize=(10, 6))
plt.title("Your first polynomial regression – congrats! :)", size=16)
plt.scatter(x, y)
plt.plot(x, y_predicted, c="red")
plt.show()

//https://data36.com/polynomial-regression-python-scikit-learn/
```










