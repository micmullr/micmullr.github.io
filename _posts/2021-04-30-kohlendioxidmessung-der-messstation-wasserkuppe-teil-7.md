---
title: 'Visualisierung der Kohlendioxidmessung  Teil 7'
date: 2021-04-30
permalink: /beitrag/kohlendioxidmessung_wasserkuppe_teil7/
tags:
---

Die Konzentration ist im Mai auf der Nordhemisphäre am höchsten, da das im Frühling stattfindende Ergrünen zu dieser Zeit beginnt; sie erreicht ihr Minimum im Oktober, wenn die Photosynthese betreibende Biomasse am größten ist.

Stand: 27.04.2021


```python
import locale
locale.setlocale(locale.LC_ALL, 'de_DE')

import numpy as np
import matplotlib.pyplot as plt
import matplotlib.style as style
style.use('fivethirtyeight')
from calendar import month_abbr


df_vis = pd.read_csv('daten/wasserkuppe.csv')
df_vis.index = pd.to_datetime(df_vis.Datum)

df_vis
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
      <th>Datum</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
    </tr>
    <tr>
      <th>Datum</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-05-07 01:00:00</th>
      <td>05-07-00 01:00</td>
      <td>9.7</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-05-07 02:00:00</th>
      <td>05-07-00 02:00</td>
      <td>9.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-05-07 03:00:00</th>
      <td>05-07-00 03:00</td>
      <td>9.7</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-05-07 04:00:00</th>
      <td>05-07-00 04:00</td>
      <td>9.4</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-05-07 05:00:00</th>
      <td>05-07-00 05:00</td>
      <td>8.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-04-06 20:00:00</th>
      <td>04-06-20 20:00</td>
      <td>8.8</td>
      <td>994.0</td>
      <td>735.0</td>
    </tr>
    <tr>
      <th>2020-04-06 21:00:00</th>
      <td>04-06-20 21:00</td>
      <td>8.8</td>
      <td>995.0</td>
      <td>737.0</td>
    </tr>
    <tr>
      <th>2020-04-06 22:00:00</th>
      <td>04-06-20 22:00</td>
      <td>8.8</td>
      <td>995.0</td>
      <td>739.0</td>
    </tr>
    <tr>
      <th>2020-04-06 23:00:00</th>
      <td>04-06-20 23:00</td>
      <td>7.6</td>
      <td>995.0</td>
      <td>740.0</td>
    </tr>
    <tr>
      <th>2020-05-06 00:00:00</th>
      <td>05-06-20 00:00</td>
      <td>6.5</td>
      <td>995.0</td>
      <td>737.0</td>
    </tr>
  </tbody>
</table>
<p>174600 rows × 4 columns</p>
</div>




```python
df_vis = df_vis.resample('M').mean()
df_vis
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
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
    </tr>
    <tr>
      <th>Datum</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-31</th>
      <td>9.597414</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-02-29</th>
      <td>6.987156</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-03-31</th>
      <td>5.985321</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-04-30</th>
      <td>5.805000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-05-31</th>
      <td>6.943972</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-08-31</th>
      <td>5.670833</td>
      <td>1020.233333</td>
      <td>751.100000</td>
    </tr>
    <tr>
      <th>2020-09-30</th>
      <td>7.174167</td>
      <td>1014.941667</td>
      <td>745.800000</td>
    </tr>
    <tr>
      <th>2020-10-31</th>
      <td>5.693333</td>
      <td>1009.225000</td>
      <td>741.425000</td>
    </tr>
    <tr>
      <th>2020-11-30</th>
      <td>2.715833</td>
      <td>1012.291667</td>
      <td>745.200000</td>
    </tr>
    <tr>
      <th>2020-12-31</th>
      <td>2.384167</td>
      <td>1013.800000</td>
      <td>746.466667</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 3 columns</p>
</div>




```python
t = df_vis['Temperatur']
p = df_vis['Luftdruck']
mol = 44.01
mg2 = df_vis['Kohlendioxid']

df_vis['ppm'] = 10*mg2/mol*((8.31447*(t+273.15))/p)

df_vis
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
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
      <th>ppm</th>
    </tr>
    <tr>
      <th>Datum</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-31</th>
      <td>9.597414</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-02-29</th>
      <td>6.987156</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-03-31</th>
      <td>5.985321</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-04-30</th>
      <td>5.805000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-05-31</th>
      <td>6.943972</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-08-31</th>
      <td>5.670833</td>
      <td>1020.233333</td>
      <td>751.100000</td>
      <td>387.798992</td>
    </tr>
    <tr>
      <th>2020-09-30</th>
      <td>7.174167</td>
      <td>1014.941667</td>
      <td>745.800000</td>
      <td>389.157172</td>
    </tr>
    <tr>
      <th>2020-10-31</th>
      <td>5.693333</td>
      <td>1009.225000</td>
      <td>741.425000</td>
      <td>387.010451</td>
    </tr>
    <tr>
      <th>2020-11-30</th>
      <td>2.715833</td>
      <td>1012.291667</td>
      <td>745.200000</td>
      <td>383.661572</td>
    </tr>
    <tr>
      <th>2020-12-31</th>
      <td>2.384167</td>
      <td>1013.800000</td>
      <td>746.466667</td>
      <td>383.280561</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 4 columns</p>
</div>




```python
df_vis = df_vis.drop(columns=['Temperatur','Luftdruck','Kohlendioxid'])
df_vis
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
      <th>ppm</th>
    </tr>
    <tr>
      <th>Datum</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-31</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-02-29</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-03-31</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-04-30</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2000-05-31</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-08-31</th>
      <td>387.798992</td>
    </tr>
    <tr>
      <th>2020-09-30</th>
      <td>389.157172</td>
    </tr>
    <tr>
      <th>2020-10-31</th>
      <td>387.010451</td>
    </tr>
    <tr>
      <th>2020-11-30</th>
      <td>383.661572</td>
    </tr>
    <tr>
      <th>2020-12-31</th>
      <td>383.280561</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 1 columns</p>
</div>



Folgender Code war bei der Erstellung hilfreich [^1]


```python
co2_data = df_vis['2011':'2019']
n_years = co2_data.index.year.max() - co2_data.index.year.min()
z = np.ones((n_years +1 , 12)) * np.min(co2_data.ppm)
for d, y in co2_data.groupby([co2_data.index.year, co2_data.index.month]):
  z[co2_data.index.year.max() - d[0], d[1] - 1] = y.mean()[0]

plt.figure(figsize=(10, 14))
plt.pcolor(np.flipud(z), cmap='hot_r')
plt.yticks(np.arange(0, n_years+1)+.5,
           range(co2_data.index.year.min(), co2_data.index.year.max()+1));
plt.xticks(np.arange(13)-.5, month_abbr)
plt.xlim((0, 12))
plt.colorbar().set_label('Kohlendioxidmessung in mg/m³ der Messstation Wasserkuppe ')
plt.show()  

```


​    
![png](/images/kohlendioxidmessung/output_100_0.png)
​    


In der Abbildung sind die Kohlendioxidwerte für November 2011 am geringsten und im April 2018 am höchsten. Der Einfluss der Nordhemisphäre dominiert den jährlichen Zyklus der Schwankung der Kohlenstoffdioxidkonzentration, denn dort befinden sich weit größere Landflächen und somit eine größere Biomasse als auf der Südhemisphäre. Die Konzentration ist im Mai auf der Nordhemisphäre am höchsten, da das im Frühling stattfindende Ergrünen zu dieser Zeit beginnt; sie erreicht ihr Minimum im Oktober, wenn die Photosynthese betreibende Biomasse am größten ist.[^2]

## Minimale und maximale Werte

Anschließend werden die maximalen und minimalen Werte aufgelistet. 


```python
t = pd.to_datetime('11-11-30')
t

df_wasserkuppe_01_02_2002_12_0 = df_vis[(df_vis.index == '2011-11-30')]
df_wasserkuppe_01_02_2002_12_0
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
      <th>ppm</th>
    </tr>
    <tr>
      <th>Datum</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2011-11-30</th>
      <td>369.717896</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_wasserkuppe_01_02_2002_12_0 = df_vis[(df_vis.index == '2018-07-31')]
df_wasserkuppe_01_02_2002_12_0
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
      <th>ppm</th>
    </tr>
    <tr>
      <th>Datum</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-07-31</th>
      <td>393.254659</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_vis['ppm'].argmax()
```




    219




```python
df_vis.iloc[[df_vis['ppm'].argmax()]]
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
      <th>ppm</th>
    </tr>
    <tr>
      <th>Datum</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-04-30</th>
      <td>393.527525</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_vis.iloc[[df_vis['ppm'].argmin()]]
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
      <th>ppm</th>
    </tr>
    <tr>
      <th>Datum</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2011-11-30</th>
      <td>369.717896</td>
    </tr>
  </tbody>
</table>
</div>



Quellenangaben:
[^1]: Vettigli, G. (2019, 22. April). Visualizing Atmospheric Carbon Dioxide. Dzone.Com. https://dzone.com/articles/visualizing-atmospheric-carbon-dioxide

[^2]: U.K. (2016, 21. Januar). Florierende Vegetation verstärkt Kohlendioxid-Schwankungen. Max-Planck-Gesellschaft. https://www.mpg.de/9862783/co2-schwankung-vegetation-erderwaermung



