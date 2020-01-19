---
title: "Time series in Prophet"
published: true
---

Prophet is a tool published by facebook that can be used for forecasting data like time series.

We will be forecasting stock data for apple today. It can be tough to predict stock data because it is so noisy.

## Getting the data

Head to [this](https://finance.yahoo.com/quote/AAPL/history/) link and download the `csv` file by clicking the "Download Data" link on the page. It is a little hard to spot.

## Installing Prophet

```
pip install fbprophet
```

Just run the following command to install Prophet. Make sure that you have python installed and you should run this code in a Jupyter Notebook (or jupyterlab).

## Using Prophet

Importing libraries

```python
import pandas as pd
from fbprophet import Prophet
```

We are loading the `csv` file here. We call it `AAPL.csv`. You should have downloaded this data in the earlier section titled "Getting the data"

```python
df = pd.read_csv("AAPL.csv")
df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
        vertical-align: top;
    }
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-01-20</td>
      <td>107.839996</td>
      <td>108.970001</td>
      <td>106.500000</td>
      <td>108.720001</td>
      <td>99.893822</td>
      <td>49899900</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015-01-21</td>
      <td>108.949997</td>
      <td>111.059998</td>
      <td>108.269997</td>
      <td>109.550003</td>
      <td>100.656441</td>
      <td>48575900</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-01-22</td>
      <td>110.260002</td>
      <td>112.470001</td>
      <td>109.720001</td>
      <td>112.400002</td>
      <td>103.275063</td>
      <td>53796400</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015-01-23</td>
      <td>112.300003</td>
      <td>113.750000</td>
      <td>111.529999</td>
      <td>112.980003</td>
      <td>103.807991</td>
      <td>46464800</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015-01-26</td>
      <td>113.739998</td>
      <td>114.360001</td>
      <td>112.800003</td>
      <td>113.099998</td>
      <td>103.918228</td>
      <td>55615000</td>
    </tr>
  </tbody>
</table>
</div>

We have to rename the columns to `ds` and `y` so that we can train it using Prophet.
```python
d2 = df[["Date", "High"]]
d2.columns = ["ds", "y"]
d2.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
        vertical-align: top;
    }
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ds</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-01-20</td>
      <td>108.970001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015-01-21</td>
      <td>111.059998</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-01-22</td>
      <td>112.470001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015-01-23</td>
      <td>113.750000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015-01-26</td>
      <td>114.360001</td>
    </tr>
  </tbody>
</table>
</div>

We are just training prophet on our dataframe just like that.
```python
m = Prophet() # We train Prophet here
m.fit(d2)
```

### Predicting the future

```python
future = m.make_future_dataframe(periods=365)
future.tail() # Goes up to 01-16-2021
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ds</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1619</th>
      <td>2021-01-12</td>
    </tr>
    <tr>
      <th>1620</th>
      <td>2021-01-13</td>
    </tr>
    <tr>
      <th>1621</th>
      <td>2021-01-14</td>
    </tr>
    <tr>
      <th>1622</th>
      <td>2021-01-15</td>
    </tr>
    <tr>
      <th>1623</th>
      <td>2021-01-16</td>
    </tr>
  </tbody>
</table>
</div>

We actually predict the future in the following cell.

```python
forecast = m.predict(future)
forecast[['ds', 'yhat', 'yhat_lower', 'yhat_upper']].tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ds</th>
      <th>yhat</th>
      <th>yhat_lower</th>
      <th>yhat_upper</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1619</th>
      <td>2021-01-12</td>
      <td>421.165426</td>
      <td>295.498040</td>
      <td>559.937322</td>
    </tr>
    <tr>
      <th>1620</th>
      <td>2021-01-13</td>
      <td>421.603917</td>
      <td>300.204687</td>
      <td>557.991950</td>
    </tr>
    <tr>
      <th>1621</th>
      <td>2021-01-14</td>
      <td>421.868835</td>
      <td>296.781987</td>
      <td>559.755712</td>
    </tr>
    <tr>
      <th>1622</th>
      <td>2021-01-15</td>
      <td>422.064133</td>
      <td>296.079828</td>
      <td>559.776385</td>
    </tr>
    <tr>
      <th>1623</th>
      <td>2021-01-16</td>
      <td>419.793294</td>
      <td>293.032000</td>
      <td>559.370520</td>
    </tr>
  </tbody>
</table>
</div>


```python
# (Optional)
%config InlineBackend.figure_format = 'retina'
# Makes the quality of the figure better.
```


Here is a plot of the figure.

```python
fig1 = m.plot(forecast)
```

![png](/assets/images/2020-01-19/output_7_0.png)


And there you have it! We used facebook's Prophet tool to train a forecaster model and we forecasted future prices of apple's stock with it.