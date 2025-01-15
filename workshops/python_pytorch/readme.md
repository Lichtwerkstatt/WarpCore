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

#### Artificial Neural Network 
- Input & Output Layers
- Hidden Layer (Fully Connected)
- Deep Neural Network (2 or more hidden layer)
- ANN Topologies

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
