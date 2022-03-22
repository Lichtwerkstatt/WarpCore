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


# Prior Workshop
- content = basic concepts of Input, Output, Calculations, Conditions, Repititions
- goal: learn how to program and work in a basic science data workflow
- no extended data structures, loops, conditions, objects, lambdas, libraries, user interfaces, compact code etc.
- use ressources:
  - online guides (see above)
  - youTube tutorials
  - stack overflow (google error messages)
- Practice! Practice! Practice!

# Introduction
- Programming a von-Neumann-architecture
  - Memory, BUS, CPU
  - ALU, operators, parameters
- machine code, high level programming and compilers
- script languages (Bash, R, JS, ...)
- history of Python
- Python Modules

## Python Usage
- command line
  - interactive mode
    - print, assign operator, arithm. operator
    - evaluation of variables and terms
    - _
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
  - line by line (Exception ;)
  - intended blocks
  - [comments](https://www.w3schools.com/python/python_comments.asp)
  - Capitals matter
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

- Debugging

# Variables 

## Strings
```python
'spam eggs'
"spam eggs"
"'spam' eggs"
'\'spam\' eggs'
"Hello \n World!"
"hello" + "world"
```

## Integer
2+2
50-5*6

## Operators
```python
#Arithm. Operators
8/5
17//3
17%3
2**7
8/2 #division returns float
```
**Task**
- Guess what `**`, `//` and `%` does
- find out order in which operators are applied ((), **, +-, \*/%//, + - )
- what does 1j mean? -> 1j**2
- is 10/2 the same as 2+3 ? -> 5 is 5.0

**Tip**: In interactive Mode `_` returns last value

```python
# Assign Operator
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
- show step by step
- breakpoints
- int input
- str output
- float inputs

**Exercise:** Write a tax calculator, returning the price inkl. MwSt. (16%)

### Bonus Knowledge
- simple [data types](https://www.w3schools.com/python/python_datatypes.asp) in python
  - **numeric** : int(eger), float, complex
  - **text** : str(ing)
  - **boolean** : bool(ean)
  - **binary** : bytes, bytearray, memoryview
- [Fancy ways](https://docs.python.org/3/tutorial/inputoutput.html) of string formatting  
  print(f'Hallo {a} und {b}')
- Assign operators +=, -=, ...
- Combined Assign a, b = 2, 4

# [Conditions](https://www.w3schools.com/python/python_conditions.asp)

## Comparison Operators
```python
true
false
3 > 2
x==5
x > 5
x > 5 and x < 10
not x > 5
x is 5
```

-combinations with `and`, `or`, `not`

## if then else

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
- find out if number is odd or even
- is a number the square root of another number
- write a little calculator where one can select operations (+, -, *, /)

# Complex Data Types ([Lists](https://www.w3schools.com/python/python_lists.asp))
- define: `a=[1,"hello",2,4.0]`
- access: `a[0]`
- data types: `type(a[1])`
- complex data types come with [methods](https://www.w3schools.com/python/python_ref_list.asp)
  - append()
  - clear()
  - sort()
  - reverse()
  - etc.
- comparison op `in`

### Bonus Knowledge
- complex data types in Python:
  - **sequence types** : [tuple](https://www.w3schools.com/python/python_tuples.asp), ()
  - **mapping types**: [dict](https://www.w3schools.com/python/python_dictionaries.asp) {:}
  - **set types**: [set](https://www.w3schools.com/python/python_sets.asp), frozenset {}



# Loops
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

### Task
Sum up all Elements
```python
result = 0
for x in numbers
  result = result + x
```
### Task
Reverse a String

### Task
- Guessing ganme
- Guess Number
- larger, smaller
- count rounds until number guessed correctly

```python
import random

userInput = -1
randomNumber = random.randint(0, 100)
count = 0
while (userInput != randomNumber):
    count += 1
    userInput = int(input("Die Zahl für deinen "+str(count)+"-ten Versuch: "))
    if userInput > randomNumber:
        print("zu hoch!")
    elif userInput < randomNumber:
        print("zu niedrig!")
    else:
        print("Gewonnen!")
        print(str(userInput)+" war die richtige Zahl!")
        print("Du hast nur "+ str(count)+ " Versuche gebraucht...")
```

### Task
Sort all members of a List

### Bonus Knowledge
- loops allows `continue`and `break`

## Functions

```python
def myFunction():
  print("Hello!")
  
def myFunction(param):

def myFunction(param = "Default")

*args # Argument List

def myFunction(c3, c2, c1): ...
myFunction(c1="1", c2="2", c3="3"

**kwargs # Argument Dictionary

```

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
    
def fibo_withOptionalList(n, *list):
    result = [0,1]
    if n < 2:
        return result[0:n+1]
    else :
        for i in range(2,n+1):
            result.append(result[i-1]+result[i-2])
    if list and list[0]:
        return result
    else :
        return result[n]
```

## Modules

```python
import fibonacci
import fibonacci as fibo
from fibonacci import fibo_recursive
```














