# Learning Python
Newbie Python examples


## Machine learning primer

https://classroom.udacity.com/courses/ud187

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


## Binance client

```
import pandas as pd
import math
import os.path
import time
from binance.client import Client
from datetime import timedelta, datetime
from dateutil import parser

binance_api_key = 'api_key'
binance_api_secret = 'api_secret'

binsizes = {"1m": 1, "5m": 5, "1h": 60, "1d": 1440}
batch_size = 750
binance_client = Client(api_key=binance_api_key, api_secret=binance_api_secret)


def minutes_of_new_data(symbol, kline_size, data, source):
    if len(data) > 0:  old = parser.parse(data["timestamp"].iloc[-1])
    elif source == "binance": old = datetime.strptime('1 Jan 2017', '%d %b %Y')
    elif source == "bitmex": old = bitmex_client.Trade.Trade_getBucketed(symbol=symbol, binSize=kline_size, count=1, reverse=False).result()[0][0]['timestamp']
    if source == "binance": new = pd.to_datetime(binance_client.get_klines(symbol=symbol, interval=kline_size)[-1][0], unit='ms')
    if source == "bitmex": new = bitmex_client.Trade.Trade_getBucketed(symbol=symbol, binSize=kline_size, count=1, reverse=True).result()[0][0]['timestamp']
    return old, new

def get_all_binance(symbol, kline_size, save = False):
    filename = '%s-%s-data.csv' % (symbol, kline_size)
    if os.path.isfile(filename): data_df = pd.read_csv(filename)
    else: data_df = pd.DataFrame()
    oldest_point, newest_point = minutes_of_new_data(symbol, kline_size, data_df, source = "binance")
    delta_min = (newest_point - oldest_point).total_seconds()/60
    available_data = math.ceil(delta_min/binsizes[kline_size])
    if oldest_point == datetime.strptime('1 Jan 2017', '%d %b %Y'): print('Downloading all available %s data for %s. Be patient..!' % (kline_size, symbol))
    else: print('Downloading %d minutes of new data available for %s, i.e. %d instances of %s data.' % (delta_min, symbol, available_data, kline_size))
    klines = binance_client.get_historical_klines(symbol, kline_size, oldest_point.strftime("%d %b %Y %H:%M:%S"), newest_point.strftime("%d %b %Y %H:%M:%S"))
    data = pd.DataFrame(klines, columns = ['timestamp', 'open', 'high', 'low', 'close', 'volume', 'close_time', 'quote_av', 'trades', 'tb_base_av', 'tb_quote_av', 'ignore' ])
    data['timestamp'] = pd.to_datetime(data['timestamp'], unit='ms')
    if len(data_df) > 0:
        temp_df = pd.DataFrame(data)
        data_df = data_df.append(temp_df)
    else: data_df = data
    data_df.set_index('timestamp', inplace=True)
    if save: data_df.to_csv(filename)
    print('Done.')
    return data_df
```
