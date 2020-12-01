# Learning Python
Newbie Python examples

## Download python

Get 3.8 so we are compatible with TensorFlow
https://www.python.org/downloads/release/python-386/

## Using a virtual environment

https://www.youtube.com/watch?v=28eLP22SMTA

## Installing third party libraries

`C:\Users\myusername>pip install tensorflow`


you can then use it like:

```
import tensorflow as tf
``

# Code samples

## Hello world

```
print('Hello world!')
```

produces

```
Hello world!
```

## Array and 2D array

```
import numpy as np

array = np.array(range(1, 10))
print(array)

print('\n')

array = np.array([range(i, i+2) for i in array])
print(array)
```

produces

```
[1 2 3 4 5 6 7 8 9]


[[ 1  2]
 [ 2  3]
 [ 3  4]
 [ 4  5]
 [ 5  6]
 [ 6  7]
 [ 7  8]
 [ 8  9]
 [ 9 10]]
```
