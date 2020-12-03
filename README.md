# Learning Python
Newbie Python examples


## Machine learning primer

https://classroom.udacity.com/courses/ud187

## Download python

Get 3.8 so we are compatible with TensorFlow
https://www.python.org/downloads/release/python-386/

Install to C:\Users\root\AppData\Local\Programs\Python\Python38

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

print()

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

## Structured array

```
import numpy as np

label = ['Lorem', 'Ipsum', 'Dolor']
minutes = [34, 45, 56]
weight = [180.6, 125.9, 170.0]

size = len(label)

structured_array = np.zeros(size, dtype={'names':('label', 'minutes', 'weight'), 'formats': ('U10', 'i4', 'f8')})

structured_array['label'] = label
structured_array['minutes'] = minutes
structured_array['weight'] = weight

print(structured_array)
```

produces

```
[('Lorem', 34, 180.6) ('Ipsum', 45, 125.9) ('Dolor', 56, 170. )]
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


## Add field to dataframe

```
import numpy as np
import pandas as pd

dataframe = pd.read_csv('C:/Users/root/Desktop/BTCUSD.csv', sep=',')

dataframe['bool'] = dataframe['Open'] > 10000

print(dataframe)
```

produces

```
             Date Timestamp     Open  ...    Close    Volume   bool
0        20200526  00:00:00   8843.4  ...   8844.6  0.097500  False
1        20200526  00:00:10   8844.6  ...   8844.5  0.097500  False
2        20200526  00:00:20   8844.6  ...   8843.5  0.135000  False
3        20200526  00:00:30   8843.5  ...   8840.5  0.023190  False
4        20200526  00:00:40   8840.4  ...   8837.8  0.000667  False
...           ...       ...      ...  ...      ...       ...    ...
1272844  20201125  23:59:10  18711.1  ...  18713.9  0.000235   True
1272845  20201125  23:59:20  18713.9  ...  18715.1  0.000168   True
1272846  20201125  23:59:30  18715.6  ...  18714.9  0.000220   True
1272847  20201125  23:59:40  18714.9  ...  18704.1  0.000319   True
1272848  20201125  23:59:50  18704.4  ...  18704.6  0.000221   True

[1272849 rows x 8 columns]
```
