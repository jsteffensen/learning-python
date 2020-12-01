# Learning Python
Newbie Python examples

## Download python

Get 3.8 so we are compatible with TensorFlow
https://www.python.org/downloads/release/python-386/

## Using a virtual environment

https://www.youtube.com/watch?v=28eLP22SMTA

## Installing third party libraries

`C:\Users\myusername>pip install tensorflow`


you can then use it in your code like:

```
import tensorflow as tf
```

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

array2D = np.array([range(i, i+2) for i in array])
print(array2D)
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

## Pandas and files

```
import numpy as np
import pandas as pd

dataframe = pd.read_csv('C:/Users/root/Desktop/BTCUSD.csv', sep=',')

for i, j in dataframe.iterrows():
    print(i)
    print(j)
    print()

    if i > 1:
        break

print(dataframe.head(3))
```

produces

```
0
Date         20200526
Timestamp    00:00:00
Open           8843.4
High           8844.6
Low            8843.4
Close          8844.6
Volume         0.0975
Name: 0, dtype: object

1
Date         20200526
Timestamp    00:00:10
Open           8844.6
High           8844.6
Low            8844.5
Close          8844.5
Volume         0.0975
Name: 1, dtype: object

2
Date         20200526
Timestamp    00:00:20
Open           8844.6
High           8844.6
Low            8843.5
Close          8843.5
Volume          0.135
Name: 2, dtype: object

       Date Timestamp    Open    High     Low   Close  Volume
0  20200526  00:00:00  8843.4  8844.6  8843.4  8844.6  0.0975
1  20200526  00:00:10  8844.6  8844.6  8844.5  8844.5  0.0975
2  20200526  00:00:20  8844.6  8844.6  8843.5  8843.5  0.1350

```
