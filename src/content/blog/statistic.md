---
title: 'Statistics'
description: 'Measures of Position, Dispersion, and Shape'
pubDate: 'Nov 14 2025'
slug: 'statistic'
---

I use pandas for this analysis.

Import the library.


```python
import pandas as pd
pd.__version__
```




    '2.2.3'



Create a dictionary for this analysis.


```python
dict_data = {'age': [12, 13, 65, 43, 23, 44, 33, 12, 12, 32, 23], 'height': [1.2, 1.3, 1.65, 1.43, 2.3, 1.44, 1.33, 1.4, 1.54, 1.32, 2.3]}
dict_data
```




    {'age': [12, 13, 65, 43, 23, 44, 33, 12, 12, 32, 23],
     'height': [1.2, 1.3, 1.65, 1.43, 2.3, 1.44, 1.33, 1.4, 1.54, 1.32, 2.3]}



After that, create a DataFrame from the dictionary and display descriptive statistics.


```python
df_data = pd.DataFrame(dict_data)
df_data
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
      <th>age</th>
      <th>height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12</td>
      <td>1.20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13</td>
      <td>1.30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>65</td>
      <td>1.65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>43</td>
      <td>1.43</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>2.30</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44</td>
      <td>1.44</td>
    </tr>
    <tr>
      <th>6</th>
      <td>33</td>
      <td>1.33</td>
    </tr>
    <tr>
      <th>7</th>
      <td>12</td>
      <td>1.40</td>
    </tr>
    <tr>
      <th>8</th>
      <td>12</td>
      <td>1.54</td>
    </tr>
    <tr>
      <th>9</th>
      <td>32</td>
      <td>1.32</td>
    </tr>
    <tr>
      <th>10</th>
      <td>23</td>
      <td>2.30</td>
    </tr>
  </tbody>
</table>
</div>



## Measures

### Measures of Position

**Mean:** The average value of a dataset.


```python
df_data.mean()
```




    age       28.363636
    height     1.564545
    dtype: float64



**Median:** The middle value of a dataset.


```python
df_data.median()
```




    age       23.00
    height     1.43
    dtype: float64



**Mode:** The most frequently occurring value in a dataset.


```python
df_data.mode()
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
      <th>age</th>
      <th>height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12</td>
      <td>2.3</td>
    </tr>
  </tbody>
</table>
</div>



### Measures of Dispersion


```python
# Variance measures how spread out a dataset is.
df_data.var()
```




    age       293.254545
    height      0.146807
    dtype: float64




```python
# Standard deviation is the square root of the variance.
df_data.std()
```




    age       17.124677
    height     0.383154
    dtype: float64




```python
# The coefficient of variation is the ratio of the standard deviation to the mean.
df_data.std() / df_data.mean() * 100
```




    age       60.375462
    height    24.489820
    dtype: float64



### Asymmetry (Skewness) and Kurtosis

Skewness (also called asymmetry) measures how lopsided the distribution is:
- Positive skewness (> 0): long right tail.
- Zero skewness (= 0): perfectly symmetric distribution.
- Negative skewness (< 0): long left tail.

Kurtosis measures how heavy the tails are compared to a normal distribution:
- Positive kurtosis (> 0): leptokurtic, with heavier tails and a sharper peak.
- Zero kurtosis (= 0): mesokurtic, similar to the normal curve.
- Negative kurtosis (< 0): platykurtic, with lighter tails and a flatter peak.


```python
skew_values = df_data.skew()
kurtosis_values = df_data.kurtosis()

def classify_skew(value):
    if value > 0:
        return 'positively skewed (right tail)'
    if value < 0:
        return 'negatively skewed (left tail)'
    return 'approximately symmetric'

def classify_kurtosis(value):
    if value > 0:
        return 'leptokurtic (heavy tails)'
    if value < 0:
        return 'platykurtic (light tails)'
    return 'mesokurtic (normal tails)'

report_lines = []
for column in df_data.columns:
    report_lines.append(
        f"{column}: skewness={skew_values[column]:.3f} -> {classify_skew(skew_values[column])}; "
        f"kurtosis={kurtosis_values[column]:.3f} -> {classify_kurtosis(kurtosis_values[column])}"
    )

print('\n'.join(report_lines))
```

    age: skewness=0.954 -> positively skewed (right tail); kurtosis=0.481 -> leptokurtic (heavy tails)
    height: skewness=1.506 -> positively skewed (right tail); kurtosis=1.070 -> leptokurtic (heavy tails)
    
