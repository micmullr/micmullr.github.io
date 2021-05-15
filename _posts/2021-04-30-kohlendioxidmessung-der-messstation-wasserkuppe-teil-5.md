---
title: 'Umrechnung $𝑚𝑔/𝑚^3$ in ppm Teil 5'
date: 2021-04-30
permalink: /beitrag/kohlendioxidmessung_wasserkuppe_teil5/
tags:
---
Der $CO_2$-Gehalt in der Luft wird in parts per million (Anteile pro Million), kurz ppm, oder in Prozent (%), beziehungsweise Volumenprozent (Vol.-%) angegeben. 

Zu Beginn der Industrialisierung, um 1750 lag die $CO_2$-Konzentration bei 278 ppm.[^6] [^7] Diese historischen Daten sind in ppm, die Messtelle gibt die Kohlendioxidangaben in $𝑚𝑔/𝑚^3$ an. Um die Massenkonzentrationen und Volumenmischungsverhältnisse besser vergleichen zu können, werden sie in diesem Abschnitt umgewandelt. Die Angaben als Massenkonzentrationen in $𝑚𝑔/𝑚^3$ gelten nur für die bestimmten Bedingungen von Druck und Temperatur. Der Befehl df_wasserkuppe.info() liefert uns das maximal 76646 Werte ppm berechnen könnten. Da nur für 76646 Luftdruckwerte vorhanden sind.

Stand: 27.04.2021


```python
df_wasserkuppe = pd.read_csv('daten/wasserkuppe.csv')
df_wasserkuppe.index = pd.to_datetime(df_wasserkuppe.Datum)
```


```python
df_wasserkuppedrop = df_wasserkuppe.dropna()
df_wasserkuppedrop = df_wasserkuppedrop.drop(columns=['Datum'])

df_wasserkuppedrop
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
      <th>2011-01-09 12:00:00</th>
      <td>13.4</td>
      <td>1014.0</td>
      <td>724.0</td>
    </tr>
    <tr>
      <th>2011-01-09 13:00:00</th>
      <td>14.6</td>
      <td>1014.0</td>
      <td>726.0</td>
    </tr>
    <tr>
      <th>2011-01-09 14:00:00</th>
      <td>15.6</td>
      <td>1014.0</td>
      <td>729.0</td>
    </tr>
    <tr>
      <th>2011-01-09 15:00:00</th>
      <td>15.6</td>
      <td>1013.0</td>
      <td>720.0</td>
    </tr>
    <tr>
      <th>2011-01-09 16:00:00</th>
      <td>15.6</td>
      <td>1013.0</td>
      <td>721.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-04-06 20:00:00</th>
      <td>8.8</td>
      <td>994.0</td>
      <td>735.0</td>
    </tr>
    <tr>
      <th>2020-04-06 21:00:00</th>
      <td>8.8</td>
      <td>995.0</td>
      <td>737.0</td>
    </tr>
    <tr>
      <th>2020-04-06 22:00:00</th>
      <td>8.8</td>
      <td>995.0</td>
      <td>739.0</td>
    </tr>
    <tr>
      <th>2020-04-06 23:00:00</th>
      <td>7.6</td>
      <td>995.0</td>
      <td>740.0</td>
    </tr>
    <tr>
      <th>2020-05-06 00:00:00</th>
      <td>6.5</td>
      <td>995.0</td>
      <td>737.0</td>
    </tr>
  </tbody>
</table>
<p>75072 rows × 3 columns</p>
</div>



## Umrechnungsformel

mg = 0.1*ppm1*mol/((8.31447*(t+273.15))/p)

ppm = 10*mg2/mol*((8.31447*(t+273.15))/p)


mg2...ist die Massenkonzentration des Messwertes Kohlendioxid in mg/m3 

p...ist der Bezugsdruck. Der Normdruck wäre 1013,25 mbar.

mol...die molare Masse von Kohlendioxid in g/mol:
44,01 g/mol

10 ergibt sich als Umrechnungsfaktor, da keine konsistenten Einheiten verwendet werden[^10]

R ist die Universelle Gaskonstante = 8,314472 J/(K·mol)



```python
t= 13.4
p=1013.25
mol=44.01
mg2=724

ppm = 10*mg2/mol*((8.31447*(t+273.15))/p)
ppm
```




    386.8170144884977



Berechnung der Werte 2011-01-09 12:00:00 und 2020-05-06 00:00:00


```python
t= 6.5
p=995
mol=44.01
mg2=737

ppm = 10*mg2/mol*((8.31447*(t+273.15))/p)
ppm
```




    391.32936019874427




```python
t= 13.4
p=1014
mol=44.01
mg2=724

ppm = 10*mg2/mol*((8.31447*(t+273.15))/p)
ppm
```




    386.5309072292606




```python
t = df_wasserkuppedrop['Temperatur']
p = df_wasserkuppedrop['Luftdruck']
mol = 44.01
mg2 = df_wasserkuppedrop['Kohlendioxid']

df_wasserkuppedrop['ppm'] = 10*mg2/mol*((8.31447*(t+273.15))/p)

df_wasserkuppedrop['ppm']
```




    Datum
    2011-01-09 12:00:00    386.530907
    2011-01-09 13:00:00    389.221839
    2011-01-09 14:00:00    392.188422
    2011-01-09 15:00:00    387.728965
    2011-01-09 16:00:00    388.267478
                              ...    
    2020-04-06 20:00:00    393.873041
    2020-04-06 21:00:00    394.547875
    2020-04-06 22:00:00    395.618561
    2020-04-06 23:00:00    394.467844
    2020-05-06 00:00:00    391.329360
    Name: ppm, Length: 75072, dtype: float64




```python
df_wasserkuppedrop
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
      <th>2011-01-09 12:00:00</th>
      <td>13.4</td>
      <td>1014.0</td>
      <td>724.0</td>
      <td>386.530907</td>
    </tr>
    <tr>
      <th>2011-01-09 13:00:00</th>
      <td>14.6</td>
      <td>1014.0</td>
      <td>726.0</td>
      <td>389.221839</td>
    </tr>
    <tr>
      <th>2011-01-09 14:00:00</th>
      <td>15.6</td>
      <td>1014.0</td>
      <td>729.0</td>
      <td>392.188422</td>
    </tr>
    <tr>
      <th>2011-01-09 15:00:00</th>
      <td>15.6</td>
      <td>1013.0</td>
      <td>720.0</td>
      <td>387.728965</td>
    </tr>
    <tr>
      <th>2011-01-09 16:00:00</th>
      <td>15.6</td>
      <td>1013.0</td>
      <td>721.0</td>
      <td>388.267478</td>
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
      <td>8.8</td>
      <td>994.0</td>
      <td>735.0</td>
      <td>393.873041</td>
    </tr>
    <tr>
      <th>2020-04-06 21:00:00</th>
      <td>8.8</td>
      <td>995.0</td>
      <td>737.0</td>
      <td>394.547875</td>
    </tr>
    <tr>
      <th>2020-04-06 22:00:00</th>
      <td>8.8</td>
      <td>995.0</td>
      <td>739.0</td>
      <td>395.618561</td>
    </tr>
    <tr>
      <th>2020-04-06 23:00:00</th>
      <td>7.6</td>
      <td>995.0</td>
      <td>740.0</td>
      <td>394.467844</td>
    </tr>
    <tr>
      <th>2020-05-06 00:00:00</th>
      <td>6.5</td>
      <td>995.0</td>
      <td>737.0</td>
      <td>391.329360</td>
    </tr>
  </tbody>
</table>
<p>75072 rows × 4 columns</p>
</div>




```python
dfco2m = df_wasserkuppedrop.resample('M').mean()
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
import matplotlib.style as style

dfco2m['ppm'].plot(label = 'ppm', figsize=(15,7))
dfco2m['MA3'] = dfco2m['ppm'].rolling(3).mean()
dfco2m['MA3'].plot(label='MA3')
style.use('fivethirtyeight')
plt.legend()
```




    <matplotlib.legend.Legend at 0x172fbda4988>




​    
![png](/images/kohlendioxidmessung/output_14_1.png)
​    


Quellenangaben:

[^1]: Kohlendioxid-Konzentration – Klimawandel. (2019). bildungsserver. https://wiki.bildungsserver.de/klimawandel/index.php/Kohlendioxid-Konzentration

[^2]: Wikipedia-Autoren. (2007, 16. Mai). Kohlenstoffdioxid in der Erdatmosphäre. Wikipedia. https://de.wikipedia.org/wiki/Kohlenstoffdioxid_in_der_Erdatmosph%C3%A4re


[^3]: ppm in mg/m3. (2019). NABU Eibelshausen. http://www.nabu-eibelshausen.de/Rechner/ppm.html