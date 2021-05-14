---
title: 'Gleitende Durchschnitte mit Python berechnen'
date: 2021-05-14
permalink: /beitrag/gleitende-durchschnitte/
tags:
  - operations management
---

Eine Bedarfskurve kann auf vier verschiedene Arten verlaufen: Sporadisch (unvorhersehbar), konstant (selbes Niveau), trendmäßig (steigend oder fallend) und saisonal (steigende und fallende Bereiche). 


| ![Verschiedene Arten von Bedarfsverläufe](/images/gleitende_durchschnitt/bedarfsverlauf.svg) |
| :----------------------------------------------------------: |
|      *Verschiedene Arten von Bedarfsverläufen*       |


# Konstantes Niveau

Bei einem konstanten Bedarf schwanken die Werte einer Zeitreihe unregelmäßig um ein konstantes Niveau. Es bieten sich zwei Instrumente zur Berechnung eines Prognosewertes an, den gleitenden Durchschnitt und die exponentielle Glättung erster Ordnung. 



Der gleitende Durchschnitt errechnet sich ähnlich wie der normale Mittelwert:

$${\frac {1}{n}}\sum _{i=1}^{n}{x_{i}}={\frac {x_{1}+x_{2}+\cdots +x_{n}}{n}}$$

oder

$$\hat{y}_{t+1} = \frac{1}{T}\sum^{t}_{\tau=t-T+1} y_t$$


Die Werte, aus denen der Mittelwert gebildet werden soll, werden addiert und die Summe wiederum durch die Anzahl der Werte geteilt. Die in die Prognose einbezogenen Vergangenheitswerte erhalten dieselbe Gewichtung.

# Problematiken
Während eine große Menge an Werten generell vorteilhaft ist, um Ausreißer herauszufiltern, ist dies bei der Bedarfsermittlung eher von Nachteil, da auch Vorperioden betrachtet werden in denen das Unternehmen anders ausgerichtet war oder einen geringeren Marktanteil hatte.



# Beispiel mit Python


```python
import pandas as pd
import numpy as np
df = pd.read_csv('../data/gleitende_durchschnitt/duschgel.csv',  sep = ';' ,decimal = ',', header = None )
df.columns = ['A', 'B']
df
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>106.8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>129.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>153.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>149.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>158.3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>132.9</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>149.8</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>140.3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>138.3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>152.2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>128.1</td>
    </tr>
  </tbody>
</table>
</div>



Man berechnet den Mittelwert, indem man die Summe der betrachteten Zahlen durch ihre Anzahl teilt.


```python
GD = (106.8 + 129.2 + 153.0) / 3
np.round(GD,1)
```




    129.7



Um dies zu implementieren, wird die iloc-Funktion von Pandas verwendet. Die Position der Bedarfsspalte wird in der iloc-Funktion festgelegt. Während die Zeile eine Variable i ist, welche solange iteriert, bis das Ende des Datenframe erreicht wird. Greife selektiv auf die Zeile 0 zu. Dazu verwende den Locator iloc.
loc ruft Zeilen (und/oder Spalten) mit bestimmten Bezeichnungen ab.
iloc holt Zeilen (und/oder Spalten) an ganzzahligen Positionen. Siehe: https://stackoverflow.com/questions/31593201/how-are-iloc-and-loc-different


```python
df.iloc[0]
```




    A      1.0
    B    106.8
    Name: 0, dtype: float64




```python
x1 = df.iloc[0,1]
print(x1)
x2 = df.iloc[1,1]
print(x2)
x3 = df.iloc[2,1]
print(x3)
```

    106.8
    129.2
    153.0



```python
df.loc[df.index[0 + 2]]
```




    A      3.0
    B    153.0
    Name: 2, dtype: float64




```python
for x in range(0,df.shape[0]-2):
    df.loc[df.index[x + 2], 'GD_3'] = np.round(((df.iloc[x, 1] + df.iloc[x + 1, 1] + df.iloc[x + 2, 1]) /3), 1)
```


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>GD_3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>106.8</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>129.2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>153.0</td>
      <td>129.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>149.1</td>
      <td>143.8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>158.3</td>
      <td>153.5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>132.9</td>
      <td>146.8</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>149.8</td>
      <td>147.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>140.3</td>
      <td>141.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>138.3</td>
      <td>142.8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>152.2</td>
      <td>143.6</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>128.1</td>
      <td>139.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
import matplotlib.pyplot as plt
%matplotlib inline
import matplotlib.style as style
style.use('fivethirtyeight')
```


```python
plt.figure(figsize=[15,10])
plt.grid(True)
plt.plot(df['B'],label='Bedarf',color='#30e67f')
plt.plot(df['GD_3'],label='GD T=3',color='#533E2D')
plt.legend(loc=2)
```




    <matplotlib.legend.Legend at 0x269d286c0c8>




​    
![png](/images/gleitende_durchschnitt/output_14_1.png)
​    


# Überprüfung der Ergebnisse

Wir überprüfen unser Vorgehen mit der eingebauten pandas Funktion rolling.


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>GD_3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>106.8</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>129.2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>153.0</td>
      <td>129.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>149.1</td>
      <td>143.8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>158.3</td>
      <td>153.5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>132.9</td>
      <td>146.8</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>149.8</td>
      <td>147.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>140.3</td>
      <td>141.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>138.3</td>
      <td>142.8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>152.2</td>
      <td>143.6</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>128.1</td>
      <td>139.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['Rolling'] = df['B'].rolling(3).mean()
df
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
      <th>A</th>
      <th>B</th>
      <th>GD_3</th>
      <th>Rolling</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>106.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>129.2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>153.0</td>
      <td>129.7</td>
      <td>129.666667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>149.1</td>
      <td>143.8</td>
      <td>143.766667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>158.3</td>
      <td>153.5</td>
      <td>153.466667</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>132.9</td>
      <td>146.8</td>
      <td>146.766667</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>149.8</td>
      <td>147.0</td>
      <td>147.000000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>140.3</td>
      <td>141.0</td>
      <td>141.000000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>138.3</td>
      <td>142.8</td>
      <td>142.800000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>152.2</td>
      <td>143.6</td>
      <td>143.600000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>128.1</td>
      <td>139.5</td>
      <td>139.533333</td>
    </tr>
  </tbody>
</table>
</div>



Quellen:
[1] https://www.ingenieurkurse.de/produktion/aggregierte-produktionsplanung/einstufige-produktionsprogrammplanung/einstufige-mehrperiodige-produktionsprogrammplanung/prognosen-zur-nachfrageentwicklung/methode-des-gleitenden-durchschnitts.html
    
[2]  https://otexts.com/fpp2/decomposition.html
    
[3] https://www.cmegroup.com/education/courses/technical-analysis/understanding-moving-averages.html

[4] https://www.uni-siegen.de/smi/aktuelles/bestandsmanagement_wolf.pdf

[5] https://de.wikibooks.org/wiki/Materialwirtschaft:_Beschaffung:_Bedarfsarten_und_Bedarfsermittlung

[6] https://www.datacamp.com/community/tutorials/moving-averages-in-pandas

