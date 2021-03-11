---
title: 'Der Kohlendioxidgehalt in Hessen Teil 1'
date: 2021-03-11
permalink: /beitrag/kohlendioxid-hessen-1/
tags:
  - cool posts
  - category1
  - category2
---

# Der Kohlendioxidgehalt in Hessen Teil 1

Die Rohdaten stellen uns vor folgenden Aufgaben:
1. Den Datentyp müssen wir von Objekt in Zahlen umwandeln.
2. Die Datumspalte und Zeitspalte in ein Datumsformat bringen ("%d-%m-%y %H:%M").

Pandas ist ein Framework.  Hauptbestandteil ist die Klasse DataFrame, mit der sich zweidimensionale Tabellen, die aus Zeilen und Spalten bestehen, aufbereiten und umarbeiten lassen.

Wir laden die pandas Bibliothek und kürzen sie mit pd ab.





```python
import pandas as pd
```

Die Datei *messwerte.txt*  liefert uns Hinweise, wie wir die Datei in Python laden.

**Dezimaltrennzeichen**

Deutschland verwendet ein Komma (,) als **Dezimaltrennzeichen**.

**Feldtrennzeichen** 

Die meisten europäischen Länder, trennen mit ';'' anstatt ',' und das Dezimaltrennzeichen ist ',' statt '.'

Die Messdaten einlesen (pd.read_csv) und die Zellen mit ';' trennen. Dezimaltrennzeichen ',' ( sep=';' , decimal=',').


Datum;Zeit;Kohlendioxid (CO2)[mg/m³];Temperatur[°C];Luftdruck[hPa]

01.12.2019;01:00;867;-3,5;1023

01.12.2019;02:00;885;-3,6;1023




```python
df= pd.read_csv('daten/messwerteb.txt', sep=';' ,decimal=',')
```

Mit der head-Methode erhalten wir eine Übersicht über die ersten fünf Zeilen. 


```python
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
      <th>Datum</th>
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.12.2019</td>
      <td>01:00</td>
      <td>867</td>
      <td>-3,5</td>
      <td>1023</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.12.2019</td>
      <td>02:00</td>
      <td>885</td>
      <td>-3,6</td>
      <td>1023</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.12.2019</td>
      <td>03:00</td>
      <td>890</td>
      <td>-3,2</td>
      <td>1022</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.12.2019</td>
      <td>04:00</td>
      <td>883</td>
      <td>-3,4</td>
      <td>1022</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.12.2019</td>
      <td>05:00</td>
      <td>891</td>
      <td>-3,6</td>
      <td>1022</td>
    </tr>
  </tbody>
</table>
</div>



Beim Einlesen von Daten versucht Pandas, die Daten automatisch in ein Zahlenformat (Integer oder Floats) zu konvertieren. Mit df.dtypes erhalten wir den entsprechenden Datentyp. Für die Messparameter und das Datum ist das nicht gelungen. Für die Verarbeitungsschritte, die uns noch bevorstehen, ist dieses Format ungeeignet. 


```python
df.dtypes
```




    Datum                        object
    Zeit                         object
    Kohlendioxid (CO2)[mg/m³]    object
    Temperatur[°C]               object
    Luftdruck[hPa]               object
    dtype: object



Wir tauschen die Dezimaltrennzeichen in Spalte Temperatur[°C]  ',' mit '.' und erstellen eine neue Spalte Temperatur (df['Temperatur']).


```python

df['Temperatur'] = [x.replace(',', '.') for x in df['Temperatur[°C]']]
```


```python
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
      <th>Datum</th>
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
      <th>Temperatur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.12.2019</td>
      <td>01:00</td>
      <td>867</td>
      <td>-3,5</td>
      <td>1023</td>
      <td>-3.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.12.2019</td>
      <td>02:00</td>
      <td>885</td>
      <td>-3,6</td>
      <td>1023</td>
      <td>-3.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.12.2019</td>
      <td>03:00</td>
      <td>890</td>
      <td>-3,2</td>
      <td>1022</td>
      <td>-3.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.12.2019</td>
      <td>04:00</td>
      <td>883</td>
      <td>-3,4</td>
      <td>1022</td>
      <td>-3.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.12.2019</td>
      <td>05:00</td>
      <td>891</td>
      <td>-3,6</td>
      <td>1022</td>
      <td>-3.6</td>
    </tr>
  </tbody>
</table>
</div>



Wir wandeln die Datenreihe Luftdruck[hPa], Temperatur und Kohlendioxid (CO2)[mg/m³] von object zu float um, und erstellen neue Spalten namens Luftdruck, Temperatur und Kohlendioxid.

WICHTIG: errors='coerce' wandelt '-' und alle weiteren Zeichen zu NaN um.


```python
df['Luftdruck'] = pd.to_numeric(df['Luftdruck[hPa]'], errors='coerce')

df['Temperatur'] = pd.to_numeric(df['Temperatur'], errors='coerce')

df['Kohlendioxid'] = pd.to_numeric(df['Kohlendioxid (CO2)[mg/m³]'], errors='coerce')
```


```python
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
      <th>Datum</th>
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.12.2019</td>
      <td>01:00</td>
      <td>867</td>
      <td>-3,5</td>
      <td>1023</td>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.12.2019</td>
      <td>02:00</td>
      <td>885</td>
      <td>-3,6</td>
      <td>1023</td>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.12.2019</td>
      <td>03:00</td>
      <td>890</td>
      <td>-3,2</td>
      <td>1022</td>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.12.2019</td>
      <td>04:00</td>
      <td>883</td>
      <td>-3,4</td>
      <td>1022</td>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.12.2019</td>
      <td>05:00</td>
      <td>891</td>
      <td>-3,6</td>
      <td>1022</td>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail()
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
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4147</th>
      <td>21.05.2020</td>
      <td>20:00</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4148</th>
      <td>21.05.2020</td>
      <td>21:00</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4149</th>
      <td>21.05.2020</td>
      <td>22:00</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4150</th>
      <td>21.05.2020</td>
      <td>23:00</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4151</th>
      <td>21.05.2020</td>
      <td>24:00</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.dtypes
```




    Datum                         object
    Zeit                          object
    Kohlendioxid (CO2)[mg/m³]     object
    Temperatur[°C]                object
    Luftdruck[hPa]                object
    Temperatur                   float64
    Luftdruck                    float64
    Kohlendioxid                 float64
    dtype: object



Für die weitere Verarbeitung der Daten brauchen wir ein bestimmtes **Datumsformat**. Zum Beispiel für FP Prophet.

Wir addieren zur Spalte 'Zeit' :00 und fügen eine neue Spalte 
'Sekundenformat' hinzu, ohne Sekundenformat gibt es eine Fehlermeldung, z.B. bei FP Prophet.



```python
df['Sekundenformat'] = df['Zeit'] + ':00'
```


```python
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
      <th>Datum</th>
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
      <th>Sekundenformat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.12.2019</td>
      <td>01:00</td>
      <td>867</td>
      <td>-3,5</td>
      <td>1023</td>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
      <td>01:00:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.12.2019</td>
      <td>02:00</td>
      <td>885</td>
      <td>-3,6</td>
      <td>1023</td>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
      <td>02:00:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.12.2019</td>
      <td>03:00</td>
      <td>890</td>
      <td>-3,2</td>
      <td>1022</td>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
      <td>03:00:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.12.2019</td>
      <td>04:00</td>
      <td>883</td>
      <td>-3,4</td>
      <td>1022</td>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
      <td>04:00:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.12.2019</td>
      <td>05:00</td>
      <td>891</td>
      <td>-3,6</td>
      <td>1022</td>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
      <td>05:00:00</td>
    </tr>
  </tbody>
</table>
</div>



Dieser Weg verursachte einen Fehler: 
Monat und Tag zu Beginn richtig aber zum Schluß falsch:
df['Datum2']=pd.to_datetime(df.Datum) + pd.to_timedelta(df.period)

df["Date"] = df["Datum2"].apply(lambda x: datetime.combine(x, datetime.min.time()))

df["Date"] = df["Datum"].dt.strftime("%d-%m-%y %H:%M")

Wir nutzen die Pandas-Funktion **to_datetime**. Um datumsspezifische Operationen durchführen zu können.


```python
df['DatumYDM']=pd.to_datetime(df.Datum)
```


```python
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
      <th>Datum</th>
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
      <th>Sekundenformat</th>
      <th>DatumYDM</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.12.2019</td>
      <td>01:00</td>
      <td>867</td>
      <td>-3,5</td>
      <td>1023</td>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
      <td>01:00:00</td>
      <td>2019-01-12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.12.2019</td>
      <td>02:00</td>
      <td>885</td>
      <td>-3,6</td>
      <td>1023</td>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
      <td>02:00:00</td>
      <td>2019-01-12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.12.2019</td>
      <td>03:00</td>
      <td>890</td>
      <td>-3,2</td>
      <td>1022</td>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
      <td>03:00:00</td>
      <td>2019-01-12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.12.2019</td>
      <td>04:00</td>
      <td>883</td>
      <td>-3,4</td>
      <td>1022</td>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
      <td>04:00:00</td>
      <td>2019-01-12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.12.2019</td>
      <td>05:00</td>
      <td>891</td>
      <td>-3,6</td>
      <td>1022</td>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
      <td>05:00:00</td>
      <td>2019-01-12</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.dtypes
```




    Datum                                object
    Zeit                                 object
    Kohlendioxid (CO2)[mg/m³]            object
    Temperatur[°C]                       object
    Luftdruck[hPa]                       object
    Temperatur                          float64
    Luftdruck                           float64
    Kohlendioxid                        float64
    Sekundenformat                       object
    DatumYDM                     datetime64[ns]
    dtype: object




Wir informieren Pandas, dass die zu lesenden Werte nacheinander Angaben zum Tag, Monat, Jahr beinhalten. 


```python
df["DatumMDY"] = df["DatumYDM"].dt.strftime("%d-%m-%y")
```

Wir wandeln Spalte Sekundenformat in 0 days 01:00:00 um. (zählt nur Stunden bis 24 und beginnt bei 0 Tage)


```python
df['Stundenzaehler']=pd.to_timedelta(df.Sekundenformat)
```


```python
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
      <th>Datum</th>
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
      <th>Sekundenformat</th>
      <th>DatumYDM</th>
      <th>DatumMDY</th>
      <th>Stundenzaehler</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.12.2019</td>
      <td>01:00</td>
      <td>867</td>
      <td>-3,5</td>
      <td>1023</td>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
      <td>01:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 01:00:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.12.2019</td>
      <td>02:00</td>
      <td>885</td>
      <td>-3,6</td>
      <td>1023</td>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
      <td>02:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 02:00:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.12.2019</td>
      <td>03:00</td>
      <td>890</td>
      <td>-3,2</td>
      <td>1022</td>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
      <td>03:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 03:00:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.12.2019</td>
      <td>04:00</td>
      <td>883</td>
      <td>-3,4</td>
      <td>1022</td>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
      <td>04:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 04:00:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.12.2019</td>
      <td>05:00</td>
      <td>891</td>
      <td>-3,6</td>
      <td>1022</td>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
      <td>05:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 05:00:00</td>
    </tr>
  </tbody>
</table>
</div>



Wir addieren zur Spalte DatumMDY die Spalte Stundenzaehler = 2019-12-01 01:00:00


```python
df['DatumStundenzaehler']=pd.to_datetime(df.DatumMDY) + pd.to_timedelta(df.Stundenzaehler)
```


```python
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
      <th>Datum</th>
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
      <th>Sekundenformat</th>
      <th>DatumYDM</th>
      <th>DatumMDY</th>
      <th>Stundenzaehler</th>
      <th>DatumStundenzaehler</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.12.2019</td>
      <td>01:00</td>
      <td>867</td>
      <td>-3,5</td>
      <td>1023</td>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
      <td>01:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 01:00:00</td>
      <td>2019-12-01 01:00:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.12.2019</td>
      <td>02:00</td>
      <td>885</td>
      <td>-3,6</td>
      <td>1023</td>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
      <td>02:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 02:00:00</td>
      <td>2019-12-01 02:00:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.12.2019</td>
      <td>03:00</td>
      <td>890</td>
      <td>-3,2</td>
      <td>1022</td>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
      <td>03:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 03:00:00</td>
      <td>2019-12-01 03:00:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.12.2019</td>
      <td>04:00</td>
      <td>883</td>
      <td>-3,4</td>
      <td>1022</td>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
      <td>04:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 04:00:00</td>
      <td>2019-12-01 04:00:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.12.2019</td>
      <td>05:00</td>
      <td>891</td>
      <td>-3,6</td>
      <td>1022</td>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
      <td>05:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 05:00:00</td>
      <td>2019-12-01 05:00:00</td>
    </tr>
  </tbody>
</table>
</div>




Das Datumsformat wird in 01-12-2019 01:00 umgwandelt


```python
df["DatumFinal"] = df["DatumStundenzaehler"].dt.strftime("%d-%m-%y %H:%M")
```


```python
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
      <th>Datum</th>
      <th>Zeit</th>
      <th>Kohlendioxid (CO2)[mg/m³]</th>
      <th>Temperatur[°C]</th>
      <th>Luftdruck[hPa]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
      <th>Sekundenformat</th>
      <th>DatumYDM</th>
      <th>DatumMDY</th>
      <th>Stundenzaehler</th>
      <th>DatumStundenzaehler</th>
      <th>DatumFinal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.12.2019</td>
      <td>01:00</td>
      <td>867</td>
      <td>-3,5</td>
      <td>1023</td>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
      <td>01:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 01:00:00</td>
      <td>2019-12-01 01:00:00</td>
      <td>01-12-19 01:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.12.2019</td>
      <td>02:00</td>
      <td>885</td>
      <td>-3,6</td>
      <td>1023</td>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
      <td>02:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 02:00:00</td>
      <td>2019-12-01 02:00:00</td>
      <td>01-12-19 02:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.12.2019</td>
      <td>03:00</td>
      <td>890</td>
      <td>-3,2</td>
      <td>1022</td>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
      <td>03:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 03:00:00</td>
      <td>2019-12-01 03:00:00</td>
      <td>01-12-19 03:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.12.2019</td>
      <td>04:00</td>
      <td>883</td>
      <td>-3,4</td>
      <td>1022</td>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
      <td>04:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 04:00:00</td>
      <td>2019-12-01 04:00:00</td>
      <td>01-12-19 04:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.12.2019</td>
      <td>05:00</td>
      <td>891</td>
      <td>-3,6</td>
      <td>1022</td>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
      <td>05:00:00</td>
      <td>2019-01-12</td>
      <td>12-01-19</td>
      <td>0 days 05:00:00</td>
      <td>2019-12-01 05:00:00</td>
      <td>01-12-19 05:00</td>
    </tr>
  </tbody>
</table>
</div>



Wir löschen die folgenden Spalten:


```python
df=df.drop(columns=['Datum', 'Zeit','Sekundenformat','Kohlendioxid (CO2)[mg/m³]','Temperatur[°C]','Luftdruck[hPa]','DatumYDM','DatumMDY','Stundenzaehler','DatumStundenzaehler'])
```


```python
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
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
      <th>DatumFinal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
      <td>01-12-19 01:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
      <td>01-12-19 02:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
      <td>01-12-19 03:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
      <td>01-12-19 04:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
      <td>01-12-19 05:00</td>
    </tr>
  </tbody>
</table>
</div>



Wir nennen Spalte DatumFinal in Datum um


```python
df=df.rename(columns={'DatumFinal': 'Datum'})
```


```python
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
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
      <th>Datum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
      <td>01-12-19 01:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
      <td>01-12-19 02:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
      <td>01-12-19 03:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
      <td>01-12-19 04:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
      <td>01-12-19 05:00</td>
    </tr>
  </tbody>
</table>
</div>



Wir setzen Spalte Datum als Index, dadurch können wir die  Vorzüge der Datumsklasse nutzen.



```python
df=df.set_index('Datum')
```


```python
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
      <th>01-12-19 01:00</th>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
    </tr>
    <tr>
      <th>01-12-19 02:00</th>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
    </tr>
    <tr>
      <th>01-12-19 03:00</th>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
    </tr>
    <tr>
      <th>01-12-19 04:00</th>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
    </tr>
    <tr>
      <th>01-12-19 05:00</th>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
    </tr>
  </tbody>
</table>
</div>



Das Ergebnis: Wir haben das Datum als nutzbares  Datumsformat umgewandelt. 
Die Temperatur, Luftdruck und Kohlendioxid sind im Zahlenformat und NaN Werte für fehlende Daten.


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
      <th>01-12-19 01:00</th>
      <td>-3.5</td>
      <td>1023.0</td>
      <td>867.0</td>
    </tr>
    <tr>
      <th>01-12-19 02:00</th>
      <td>-3.6</td>
      <td>1023.0</td>
      <td>885.0</td>
    </tr>
    <tr>
      <th>01-12-19 03:00</th>
      <td>-3.2</td>
      <td>1022.0</td>
      <td>890.0</td>
    </tr>
    <tr>
      <th>01-12-19 04:00</th>
      <td>-3.4</td>
      <td>1022.0</td>
      <td>883.0</td>
    </tr>
    <tr>
      <th>01-12-19 05:00</th>
      <td>-3.6</td>
      <td>1022.0</td>
      <td>891.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>21-05-20 20:00</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21-05-20 21:00</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21-05-20 22:00</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21-05-20 23:00</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22-05-20 00:00</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>4152 rows × 3 columns</p>
</div>




```python
 df.dtypes
```




    Temperatur      float64
    Luftdruck       float64
    Kohlendioxid    float64
    dtype: object




```python

```
