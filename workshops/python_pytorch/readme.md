# Introduction into Machine Learning with Python (PyTorch)

## Preps

## Start

### Basics Python

```python
mylist = [1,2,3]
mymatrix = [[1,2,3],[4,5,6],[7,8,9]]

mylist = ["hello","world",1,2.0,true]

```

### Basics Numpy

#### Arrays

```python
import numpy as np
# Lists to NumpyArrays
mylist = [1,2,3]
np.array(my_list)
mymatrix = [[1,2,3],[4,5,6],[7,8,9]]
np.array(mymatrix)
```

```python
np.arange(0,10) #Evenly Integers Array
np.arange(0,10,2)

np.linspace(0,10,3) #Evenly Intervals

np.zeros(3) #zero Arrays, analog np.ones
np.zeros(3,3)

np.random.seed(42)
np.random.rand(5,5) #Array with randoms
np.random.randn(5,5)
np.random.randint(1,100,10)

np.eye(4) #identity matrix
```

#### Array Methods

```python
arr = np.arange(25)
rndarray = np.random.randint(0,50,10)

arr.reshape(5,5) #vector to matrix
arr.reshape(1,25)
arr.reshape(25,1)
arr.shape
```

#### Data Types

```python
arr.dtype
```

#### Indexing & Slicing

```python
arr = np.arange(0,11)
arr[8]
arr[1:5]
arr[0:5]

slice_arr = arr[2:7]
slice_arr[:] = 0 #Check orriginal Array

arr_copy = arr[2:7]
```

#### Conditions on Array

```python
arr > 4
bool_arr = arr>4
arr[bool_arr]
```

### Operations

```python
arr = np.arange(0,10)
arr+arr # analog - * ( special /)
1/arr
arr*3 # watch dtype
.sqrt, .exp, .sin, .log, .sum(), .mean(), .max
```

## Pytorch Basics

Converting Arrays to Tensors

```python
import torch
import numpy as np
torch.__version__
arr = np.arange(1,6,5)
#print arr, arr.dtype, type(arr)

x = torch.from_numpy(arr)
print(x) # x.dtype x.type
arr[2] = 77
print(x) #tensor and array share memory!

x = torch.tensor(arr) #copy of array
```

Tensors have a lot of functions and methods analog zu numpy arrays. Such as torch.empty(), torch.zeros(), torch.rand(), torch.randn(), torch.randint(), .arange(), .linspace, etc...
Analog can tensors be reshaped and arithmetics

### Tensors in Application

Advantage of tensors is storing a sequence of operations or apply a derivative = Dynamical Computational Graph. Tensors are tracking all operations on it

```python
import torch

 x = torch.tensor(2.0, requires_grad=True)
 # f = 2x^4 + x^3 + 3x^2 + 5x + 1
 y = 2*x**4 + x**3 + 3*x**2 + 5*x+1 #Berechnung von y=f(2)
 print(y)
 y.backward # Calculate backdrop derivative of f' = 8x^3 + 3x^2+6x+5
 print(x.grad) # Berechnung von f'(2) = slope of polynomial f at (2,63)
```

```python
x = torch.tensor([1.,2,3],[3,2,1], requires_grad=True)
print(x)
# FIRST LAYER y = 3x+2
y = 2*x + 2
print(y)
# SECOND LAYER z = 2y^2
z = 2*y**2
print(z)
# OUTPUT LAYER
out = z.mean()
print(out)

# Backpropagate to find gradient of x w.r.t. to out
out.backward()
print(x.grad)
```

## Into Machine Learning

**What is Machine Learning?**

- data analysis for automated analytical model building
- learn insights without explicitely programming
- Applications
  - Prediction Equipment Failures
  - Classification
  - Pattern and Immge Recognition
  - Text Analysis
  - Fraud Detection
  - Recommondations
  - etc.
- Unsupervised Learning
  - labeled examples (spam vs. legitimate emails, cats vs dogs)
  - compare outputs to find errors and modify model accordingly
  1. Data Aqcuisition
  2. Clean Data
  3. Split into Training Data, Validation Data, Test Data (Metric)
  4. Model Training
  5. Model Testing
  6. Model Deployment
- Unsupervised, No labels at all
  - Clustering (Similarity)
  - Anomaly Detection
  - Dimensionlity Reduction
  1. Data Aquisition
  2. Data Cleaning
  3. Model Training/Building
  4. Transformation
  5. Model Deployment

**Overfitting**

- Over : model fits too much to the noise; results in low error on training sets but high error on test
- Under : does not fit the trend, low variance but high bias, model too simple
- Multidimensional Data: Check for Epoch(whole training set once)/Error Curve while Learning
- Compare Training and Test Data on Error Curve
  - normal Training slightly better than Test
  - Test drifts off : Overfitting (Find Overfit Epoch)
  - Test always bad : Underfitting

**Classification Metrics**

- Accuracy : Number of Correct Predictions / Total (problematic with unblanced data sets)
- Recall : relevant cases in data set: true positives / (true positives+false negatives)
- Precision: identify relevant data points
- F1-Score: combination of Recall of Precision (harmonic mean)
- Confusion Matrix
- "Good" Metrics depends on specific situation

**Regression Evaluation**

- Mean Absolute Error (MAE) (Absolute Difference) / wont punish large errors -> see image
- Mean Square Error (MSE) / squares Units as well
- Root Mean Square Error (RMSE)

### Theory of ANNs

#### Perceptron

- going back to Neuron
- Nucleus, Dendrites (Inputs), Axon (Output)
- Perzeptron 1958 Frank Rosenblatt / 1934 McCulloghPitts
- Inputs, Weights, Output, Bias
- Activation Function (Classification Tasks, Limit Outputs to 0 and 1)
  - Step Function ( 0, 1)
  - Sigmoid Function (0 - 1)
  - Hyperbolic Tangent (-1 - 1)
  - Rectified Linear Unit (ReLU) (Cut at 0)
  - Softmax (Multiclassification)
  - see Wikipedia Activatio Functions

#### Artificial Neural Network

- Input & Output Layers
- Hidden Layer (Fully Connected)
- Deep Neural Network (2 or more hidden layer)
- ANN Topologies
- can approximate **any (convex) continuous function** (Zhou Lu & Boris Hanin Universal Approximation Theorem)

#### Cost Functions and Gradient Descent

- measure Loss/Error by compare to training data -> single Value
- o(z) = a (o perceptron), y = real value
- C(W,B,S,E) huge function! [Link](https://stats.stackexchange.com/questions/154879/a-list-of-cost-functions-used-in-neural-networks-alongside-applications)
- how to minimize C(w1,w2,....b1,...)?
- Minimal Exercise with single Perceptron -> derivative for 0
- n-dimensional -> stochastic process of gradient descent
- step size, small -> takes long, too big -> overshoot = LEARNING RATE
- adaptive gradient descent, ADAM
- cross entropy and quadratic cost

#### Backpropagation

- Costfunction -> Update Weights
- Minimal Bsp 1 Neuron Network C(w1,b1,w2,b3,w3,b3)
- from Back to Front
- Chain Rule Derivative
- Hadamard Product (element by element)

### Linear Regression

```python
import torch
import torch.nn as nn
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

# Create Data
X = torch.linspace(1,50,50).reshape(-1,1)
torch.manual_seed(71)
e = torch.randint(-8,9,(50,1), dtype=torch.float) # Error Daten
y = 2*X+1+e

#Show Data
plt.scatter(X.numpy(), y.numpy())

```

```python
# Simple Linear Model
torch.manual_seed(59)
model = nn.Linear(in_features=1, out_features=1)
print(model.weight)
print(model.bias)
#without seeing any data the model sets to a random weight and bias
```

```python
# Model Class to get an Object
class Model(nn.Module):
  def __init__(self, in_features, out_features):
    super().__init__()
    self.linear = nn.Linear(in_features, out_features)

  def forward(self, x):
    y_pred = self.linear(x)
    return y_pred

   def print_params(self):
        for name, param in self.linear.named_parameters():
            print(name, '\t', param.item())
```

```python
# Simple Linear Model
torch.manual_seed(59)
model = Model(1,1)
print(model)
model.print_params()
model.forward(torch.tensor([2.0]))
#without seeing any data the model sets to a random weight and bias
```

```python
# Show Current Result
x1 = np.array([X.min(),X.max()])
w1,b1 = model.linear.weight.item(), model.linear.bias.item()
y1 = x1*w1 + b1

plt.scatter(X.numpy(), y.numpy())
plt.plot(x1,y1,'r')
```

```python
# LEARNING! (finally...)

# Setting criterion and optimizer
criterion = nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters(), lr=0.001)

# set reasonably large number of passes
epochts = 50
# create list to store loss values for evaluating the learning process
losses = []
for i in range(epochs):
  #Create prediction set bei running X trough current model
  y_pred = model.forward(X)
  #Calculate the loss and append to loss array
  loss = criterion(y.pred, y)
  losses.append(loss)
  #Print current status
  print("Epoch ",i," - Loss ", loss.item())
  # Reset optimizer and  backdrop
  optimizer.zero_grad()
  loss.backward()
  optimizer.step()

# Show Learning Curve
plt.plot(range(epochs), losses)
```

```python
# Show Current Result
x1 = np.array([X.min(),X.max()])
w1,b1 = model.linear.weight.item(), model.linear.bias.item()
y1 = x1*w1 + b1

plt.scatter(X.numpy(), y.numpy())
plt.plot(x1,y1,'r')
```

## Artificial Neural Network

The Iris Flower Data Setting

```python
import torch
import torch.nn as nn
import torch.nn.functional as F
from torch.utils.data import Dataset, DataLoader
from sklearn.model_selection import train_test_split

import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline

df = pd.read_csv('../Data/iris.csv')
df.head()
df.shape()

fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(10,7))
fig.tight_layout()

plots = [(0,1),(2,3),(0,2),(1,3)]
colors = ['b', 'r', 'g']
labels = ['Iris setosa','Iris virginica','Iris versicolor']

for i, ax in enumerate(axes.flat):
    for j in range(3):
        x = df.columns[plots[i][0]]
        y = df.columns[plots[i][1]]
        ax.scatter(df[df['target']==j][x], df[df['target']==j][y], color=colors[j])
        ax.set(xlabel=x, ylabel=y)

fig.legend(labels=labels, loc=3, bbox_to_anchor=(1.0,0.85))
plt.show()
```

Define Model

```python
class Model(nn.Module):
    def __init__(self, in_features=4, h1=8, h2=9, out_features=3):
        super().__init__()
        self.fc1 = nn.Linear(in_features,h1)    # input layer
        self.fc2 = nn.Linear(h1, h2)            # hidden layer
        self.out = nn.Linear(h2, out_features)  # output layer

    def forward(self, x):
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.out(x)
        return x
```

Prepare Data (Test/Training Split)

```python
X = df.drop('target',axis=1).values
y = df['target'].values

X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.2,random_state=33)

X_train = torch.FloatTensor(X_train)
X_test = torch.FloatTensor(X_test)
# y_train = F.one_hot(torch.LongTensor(y_train))  # not needed with Cross Entropy Loss
# y_test = F.one_hot(torch.LongTensor(y_test))
y_train = torch.LongTensor(y_train)
y_test = torch.LongTensor(y_test)


trainloader = DataLoader(X_train, batch_size=60, shuffle=True)
testloader = DataLoader(X_test, batch_size=60, shuffle=False)
```

Initialize Model

```python
torch.manual_seed(4)
model = Model()
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.01)
```

Training

```python
epochs = 100
losses = []

for i in range(epochs):
    i+=1
    y_pred = model.forward(X_train)
    loss = criterion(y_pred, y_train)
    losses.append(loss)

    # a neat trick to save screen space:
    if i%10 == 1:
        print(f'epoch: {i:2}  loss: {loss.item():10.8f}')

    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
```

Plot and Validate

```python
plt.plot(range(epochs), losses)

with torch.no_grad():
    y_val = model.forward(X_test)
    loss = criterion(y_val, y_test)
print(f'{loss:.8f}')

correct = 0
with torch.no_grad():
    for i,data in enumerate(X_test):
        y_val = model.forward(data)
        print(f'{i+1:2}. {str(y_val):38}  {y_test[i]}')
        if y_val.argmax().item() == y_test[i]:
            correct += 1
print(f'\n{correct} out of {len(y_test)} = {100*correct/len(y_test):.2f}% correct')
```

Save and Load

```python
torch.save(model.state_dict(), 'IrisDatasetModel.pt')
#---
new_model = Model()
new_model.load_state_dict(torch.load('IrisDatasetModel.pt'))
new_model.eval()
```

Classify unseen data

```python
mystery_iris = torch.tensor([5.6,3.7,2.2,0.5])

fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(10,7))
fig.tight_layout()

plots = [(0,1),(2,3),(0,2),(1,3)]
colors = ['b', 'r', 'g']
labels = ['Iris setosa','Iris virginica','Iris versicolor','Mystery iris']

for i, ax in enumerate(axes.flat):
    for j in range(3):
        x = df.columns[plots[i][0]]
        y = df.columns[plots[i][1]]
        ax.scatter(df[df['target']==j][x], df[df['target']==j][y], color=colors[j])
        ax.set(xlabel=x, ylabel=y)

    # Add a plot for our mystery iris:
    ax.scatter(mystery_iris[plots[i][0]],mystery_iris[plots[i][1]], color='y')

fig.legend(labels=labels, loc=3, bbox_to_anchor=(1.0,0.85))
plt.show()

with torch.no_grad():
    print(new_model(mystery_iris))
    print()
    print(labels[new_model(mystery_iris).argmax()])

```
