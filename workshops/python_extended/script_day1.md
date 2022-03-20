# Introduction into Python (Extended)

**Date** : February, 23rd / 24th 2022  
**Time** : 10-12 / 13-15  
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

### Task
- write the same functionality for product
- let the user choose the operation
- let the user choose if he wants to restart or quit the program

### Bonus Knowledge
- loops allows `continue`and `break`

## Functions

**Exercise:**
- Write a function `fibo(n)` which calculates the fibonacci number of n
- Add a obligatory parameter for returning a list
- Think of different ways for implementing `fibo` (list, iterative, recursive)

```python
def fibo_recursive(n):
    if n == 0 :
        return 0
    elif n == 1 :
        return 1
    else:
        return(fibo_recursive(n-1) + fibo_recursive(n-2))
    
def fibo_iterative(n):
    a = 0
    b = 1
    # a,b = 0,1
    if n == 0 : 
        return 0
    elif n == 1 :
        return 1
    else :
        for i in range(1,n):
            summe = a+b
            a = b
            b = summe
            # a, b = b, a+b
    return(b)
```

## Modules

```python
import fibonacci
import fibonacci as fibo
from fibonacci import fibo_recursive
```














