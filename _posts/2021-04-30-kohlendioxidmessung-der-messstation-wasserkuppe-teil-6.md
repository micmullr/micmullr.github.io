---
title: 'Streudiagramme Teil 6'
date: 2021-04-30
permalink: /beitrag/kohlendioxidmessung_wasserkuppe_teil6/
tags:
---

Im Streudiagramm erkennt man durch das Muster der Punkte Informationen über die Abhängigkeitsstruktur der beiden Merkmale.

Stand: 27.04.2021


```python
import matplotlib.pyplot as plt
import numpy as np
from pandas.plotting import scatter_matrix
#df['logarithm'] = np.log(df['Temperatur']) 
#dfny = df.dropna()
#scatter_matrix(df['logarithm'])

#df.plot.scatter(df, loglog=True)
scatter_matrix(df_wasserkuppedrop, figsize=(15,7))

```




    array([[<AxesSubplot:xlabel='Temperatur', ylabel='Temperatur'>,
            <AxesSubplot:xlabel='Luftdruck', ylabel='Temperatur'>,
            <AxesSubplot:xlabel='Kohlendioxid', ylabel='Temperatur'>,
            <AxesSubplot:xlabel='ppm', ylabel='Temperatur'>],
           [<AxesSubplot:xlabel='Temperatur', ylabel='Luftdruck'>,
            <AxesSubplot:xlabel='Luftdruck', ylabel='Luftdruck'>,
            <AxesSubplot:xlabel='Kohlendioxid', ylabel='Luftdruck'>,
            <AxesSubplot:xlabel='ppm', ylabel='Luftdruck'>],
           [<AxesSubplot:xlabel='Temperatur', ylabel='Kohlendioxid'>,
            <AxesSubplot:xlabel='Luftdruck', ylabel='Kohlendioxid'>,
            <AxesSubplot:xlabel='Kohlendioxid', ylabel='Kohlendioxid'>,
            <AxesSubplot:xlabel='ppm', ylabel='Kohlendioxid'>],
           [<AxesSubplot:xlabel='Temperatur', ylabel='ppm'>,
            <AxesSubplot:xlabel='Luftdruck', ylabel='ppm'>,
            <AxesSubplot:xlabel='Kohlendioxid', ylabel='ppm'>,
            <AxesSubplot:xlabel='ppm', ylabel='ppm'>]], dtype=object)




​    
![png](/images/kohlendioxidmessung/output_3_1.png)
​    



```python
dfco2m = dfco2m.drop(columns = ['MA3'])
dfco2m
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
      <th>2011-01-31</th>
      <td>9.861905</td>
      <td>1018.083333</td>
      <td>718.535714</td>
      <td>377.267934</td>
    </tr>
    <tr>
      <th>2011-02-28</th>
      <td>10.933333</td>
      <td>1015.166667</td>
      <td>718.979167</td>
      <td>380.087965</td>
    </tr>
    <tr>
      <th>2011-03-31</th>
      <td>10.738542</td>
      <td>1012.093750</td>
      <td>723.416667</td>
      <td>383.434028</td>
    </tr>
    <tr>
      <th>2011-04-30</th>
      <td>10.977660</td>
      <td>1008.351064</td>
      <td>724.648936</td>
      <td>385.891135</td>
    </tr>
    <tr>
      <th>2011-05-31</th>
      <td>8.386458</td>
      <td>1008.500000</td>
      <td>723.479167</td>
      <td>381.627605</td>
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
      <td>387.711256</td>
    </tr>
    <tr>
      <th>2020-09-30</th>
      <td>7.174167</td>
      <td>1014.941667</td>
      <td>745.800000</td>
      <td>389.088071</td>
    </tr>
    <tr>
      <th>2020-10-31</th>
      <td>5.693333</td>
      <td>1009.225000</td>
      <td>741.425000</td>
      <td>386.948444</td>
    </tr>
    <tr>
      <th>2020-11-30</th>
      <td>2.715833</td>
      <td>1012.291667</td>
      <td>745.200000</td>
      <td>383.644441</td>
    </tr>
    <tr>
      <th>2020-12-31</th>
      <td>2.384167</td>
      <td>1013.800000</td>
      <td>746.466667</td>
      <td>383.237839</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 4 columns</p>
</div>




```python
import matplotlib.pyplot as plt
import numpy as np
from pandas.plotting import scatter_matrix
#df['logarithm'] = np.log(df['Temperatur']) 
#dfny = df.dropna()
#scatter_matrix(df['logarithm'])

#df.plot.scatter(df, loglog=True)

scatter_matrix(dfco2m , figsize=(15,7))

```




    array([[<AxesSubplot:xlabel='Temperatur', ylabel='Temperatur'>,
            <AxesSubplot:xlabel='Luftdruck', ylabel='Temperatur'>,
            <AxesSubplot:xlabel='Kohlendioxid', ylabel='Temperatur'>,
            <AxesSubplot:xlabel='ppm', ylabel='Temperatur'>],
           [<AxesSubplot:xlabel='Temperatur', ylabel='Luftdruck'>,
            <AxesSubplot:xlabel='Luftdruck', ylabel='Luftdruck'>,
            <AxesSubplot:xlabel='Kohlendioxid', ylabel='Luftdruck'>,
            <AxesSubplot:xlabel='ppm', ylabel='Luftdruck'>],
           [<AxesSubplot:xlabel='Temperatur', ylabel='Kohlendioxid'>,
            <AxesSubplot:xlabel='Luftdruck', ylabel='Kohlendioxid'>,
            <AxesSubplot:xlabel='Kohlendioxid', ylabel='Kohlendioxid'>,
            <AxesSubplot:xlabel='ppm', ylabel='Kohlendioxid'>],
           [<AxesSubplot:xlabel='Temperatur', ylabel='ppm'>,
            <AxesSubplot:xlabel='Luftdruck', ylabel='ppm'>,
            <AxesSubplot:xlabel='Kohlendioxid', ylabel='ppm'>,
            <AxesSubplot:xlabel='ppm', ylabel='ppm'>]], dtype=object)




​    
![png](/images/kohlendioxidmessung/output_5_1.png)
​    



```python
dfco2m.plot.scatter(x='Temperatur', y='Luftdruck', loglog=False, alpha=1, figsize=(15,7))
plt.show()
```


​    
![png](/images/kohlendioxidmessung/output_6_0.png)
​    



```python
dfco2m.plot.scatter(x='Temperatur', y='ppm', loglog=False, alpha=1, figsize=(15,7))
plt.show()
```


​    
![png](/images/kohlendioxidmessung/output_7_0.png)
​    



```python
dfco2m.plot.scatter(x='Luftdruck', y='ppm', loglog=False, alpha=1, figsize=(15,7))
plt.show()
```


​    
![png](/images/kohlendioxidmessung/output_8_0.png)
​    


# 3D Streudiagramm




```python
#https://stackoverflow.com/questions/59232073/scatter-plot-with-3-variables-in-matplotlib

#https://www.advsofteng.com/doc/cdpydoc/threedscatter2.htm Dropline



import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import numpy as np

x = np.array(dfco2m['Temperatur'])
y = np.array(dfco2m['Luftdruck'])
z = np.array(dfco2m['ppm'])

fig = plt.figure(figsize=(20, 20))
ax = fig.add_subplot(111, projection='3d')
ax.scatter(x, y, z, 
           linewidths=1, alpha=.7,
           edgecolor='k',
           s = 200,
           c='green',
           )
plt.show()
```


​    
![png](/images/kohlendioxidmessung/output_10_0.png)
​    



```python
dfco2m.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 120 entries, 2011-01-31 to 2020-12-31
    Freq: M
    Data columns (total 4 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   Temperatur    120 non-null    float64
     1   Luftdruck     120 non-null    float64
     2   Kohlendioxid  120 non-null    float64
     3   ppm           120 non-null    float64
    dtypes: float64(4)
    memory usage: 4.7 KB



```python
x.shape
```




    (120,)




```python
y.shape
```




    (120,)




```python
z.shape
```




    (120,)



ToDO: Droplines
https://matplotlib.org/devdocs/gallery/mplot3d/stem3d_demo.html    
Siehe: https://support.minitab.com/de-de/minitab/19/help-and-how-to/graphs/3d-scatterplot/interpret-the-results/key-results/