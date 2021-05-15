---
title: 'Verarbeitung und Vorverarbeitung vom Datensatz Teil 4'
date: 2021-04-30
permalink: /beitrag/kohlendioxidmessung_wasserkuppe_teil4/
tags:
---
In diesem Abschnitt wird der Datensatz bearbeitet. Die Daten befinden sich noch im Rohzustand, für eine weitere Verarbeitung, werden sie in bestimmte Formate umgewandelt. 

Anschließend werden die Messdaten mit Python analysiert. Für die Umsetzung wird das Pandas Framework genutzt. Hauptbestandteil ist die Klasse DataFrame, mit der sich zweidimensionale Tabellen, die aus Zeilen und Spalten bestehen, aufbereiten und umarbeiten lassen. Die Datei messwerte.txt liefert Hinweise, wie die Datei in Python geladen werden soll. Deutschland verwendet ein Komma (,) als Dezimaltrennzeichen. Die meisten europäischen Länder, trennen mit ‚;“ anstatt ‚,‘ und das Dezimaltrennzeichen ist ‚,‘ statt ‚.‘ 

Datum;Zeit;Kohlendioxid (CO2)[mg/m³];Temperatur[°C];Luftdruck[hPa]

01.12.2019;01:00;867;-3,5;1023

01.12.2019;02:00;885;-3,6;1023

Die Rohdaten stellen folgenden Aufgaben:

Der Datentyp muss von Objekt in Zahl umwgewandelt werden. 
Die Datumspalte und Zeitspalte in ein Datumsformat bringen („%d-%m-%y %H:%M“).

Die pandas Bibliothek wird geladen und mit mit pd abgekürzt.

Stand: 27.04.2021


```python
import pandas as pd
```

Die Messdaten einlesen (pd.read_csv) und die Zellen mit ‚;‘ trennen. Dezimaltrennzeichen ‚,‘ ( sep=‘;‘ , decimal=‘,‘).


```python
df_wasserkuppe = pd.read_csv('daten/messwerte_wasserkuppe.txt', sep = ';' , decimal = ',')
```

Die head-Methode liefert eine Übersicht über die ersten fünf Zeilen.


```python
df_wasserkuppe.head()
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
      <th>Windgeschwindigkeit[m/s]</th>
      <th>Windrichtung[Grad]</th>
      <th>Niederschlag[mm/30min]</th>
      <th>Globalstrahlung[W/m²]</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>05.07.2000</td>
      <td>01:00</td>
      <td>-</td>
      <td>9,7</td>
      <td>-</td>
      <td>12,6</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>05.07.2000</td>
      <td>02:00</td>
      <td>-</td>
      <td>9,8</td>
      <td>-</td>
      <td>10,8</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>05.07.2000</td>
      <td>03:00</td>
      <td>-</td>
      <td>9,7</td>
      <td>-</td>
      <td>11,0</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>05.07.2000</td>
      <td>04:00</td>
      <td>-</td>
      <td>9,4</td>
      <td>-</td>
      <td>12,8</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05.07.2000</td>
      <td>05:00</td>
      <td>-</td>
      <td>8,8</td>
      <td>-</td>
      <td>12,6</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



Beim Einlesen von Daten versucht Pandas, die Daten automatisch in ein Zahlenformat (Integer oder Floats) zu konvertieren. Mit df.dtypes erhalten wir den entsprechenden Datentyp. Für die Messparameter und das Datum ist das nicht gelungen. Für die Verarbeitungsschritte, die uns noch bevorstehen, ist dieses Format ungeeignet.


```python
df_wasserkuppe.dtypes
```




    Datum                        object
    Zeit                         object
    Kohlendioxid (CO2)[mg/m³]    object
    Temperatur[°C]               object
    Luftdruck[hPa]               object
    Windgeschwindigkeit[m/s]     object
    Windrichtung[Grad]           object
    Niederschlag[mm/30min]       object
    Globalstrahlung[W/m²]        object
    dtype: object



Die Dezimaltrennzeichen in Spalte Temperatur[°C] ',' mit '.' tauschen und erstelle eine neue Spalte Temperatur (df['Temperatur']). (x.replace)


```python
df_wasserkuppe['Temperatur'] = [x.replace(',' , '.') for x in df_wasserkuppe['Temperatur[°C]']]
```


```python
df_wasserkuppe.head()
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
      <th>Windgeschwindigkeit[m/s]</th>
      <th>Windrichtung[Grad]</th>
      <th>Niederschlag[mm/30min]</th>
      <th>Globalstrahlung[W/m²]</th>
      <th>Temperatur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>05.07.2000</td>
      <td>01:00</td>
      <td>-</td>
      <td>9,7</td>
      <td>-</td>
      <td>12,6</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>9.7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>05.07.2000</td>
      <td>02:00</td>
      <td>-</td>
      <td>9,8</td>
      <td>-</td>
      <td>10,8</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>9.8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>05.07.2000</td>
      <td>03:00</td>
      <td>-</td>
      <td>9,7</td>
      <td>-</td>
      <td>11,0</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>9.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>05.07.2000</td>
      <td>04:00</td>
      <td>-</td>
      <td>9,4</td>
      <td>-</td>
      <td>12,8</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>9.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05.07.2000</td>
      <td>05:00</td>
      <td>-</td>
      <td>8,8</td>
      <td>-</td>
      <td>12,6</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>8.8</td>
    </tr>
  </tbody>
</table>
</div>



Die Datenreihe Luftdruck[hPa], Temperatur und Kohlendioxid (CO2)[mg/m³] von object zu float umwandeln, und erstelle eine neue Spalten namens Luftdruck, Temperatur und Kohlendioxid. (pd.to_numeric) Der Parameter errors='coerce' wandelt '-' und andere Parsingfehler zu NaN (Not a Number) um.

Pandas-Operationen wie to_numeric arbeiten standardmäßig nicht "in-place". Deswegen werden die Ergebnisse, einer neuen Spalte zugewiesen.



```python
df_wasserkuppe['Luftdruck'] = pd.to_numeric(df_wasserkuppe['Luftdruck[hPa]'], errors = 'coerce')

df_wasserkuppe['Temperatur'] = pd.to_numeric(df_wasserkuppe['Temperatur'], errors = 'coerce')

df_wasserkuppe['Kohlendioxid'] = pd.to_numeric(df_wasserkuppe['Kohlendioxid (CO2)[mg/m³]'], errors = 'coerce')
```


```python
df_wasserkuppe.head()
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
      <th>Windgeschwindigkeit[m/s]</th>
      <th>Windrichtung[Grad]</th>
      <th>Niederschlag[mm/30min]</th>
      <th>Globalstrahlung[W/m²]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>05.07.2000</td>
      <td>01:00</td>
      <td>-</td>
      <td>9,7</td>
      <td>-</td>
      <td>12,6</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>9.7</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>05.07.2000</td>
      <td>02:00</td>
      <td>-</td>
      <td>9,8</td>
      <td>-</td>
      <td>10,8</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>9.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>05.07.2000</td>
      <td>03:00</td>
      <td>-</td>
      <td>9,7</td>
      <td>-</td>
      <td>11,0</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>9.7</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>05.07.2000</td>
      <td>04:00</td>
      <td>-</td>
      <td>9,4</td>
      <td>-</td>
      <td>12,8</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>9.4</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05.07.2000</td>
      <td>05:00</td>
      <td>-</td>
      <td>8,8</td>
      <td>-</td>
      <td>12,6</td>
      <td>-</td>
      <td>-</td>
      <td>1</td>
      <td>8.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_wasserkuppe.tail()
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
      <th>Windgeschwindigkeit[m/s]</th>
      <th>Windrichtung[Grad]</th>
      <th>Niederschlag[mm/30min]</th>
      <th>Globalstrahlung[W/m²]</th>
      <th>Temperatur</th>
      <th>Luftdruck</th>
      <th>Kohlendioxid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>174595</th>
      <td>04.06.2020</td>
      <td>20:00</td>
      <td>735</td>
      <td>8,8</td>
      <td>994</td>
      <td>4,9</td>
      <td>-</td>
      <td>0,0</td>
      <td>18</td>
      <td>8.8</td>
      <td>994.0</td>
      <td>735.0</td>
    </tr>
    <tr>
      <th>174596</th>
      <td>04.06.2020</td>
      <td>21:00</td>
      <td>737</td>
      <td>8,8</td>
      <td>995</td>
      <td>5,4</td>
      <td>-</td>
      <td>-</td>
      <td>3</td>
      <td>8.8</td>
      <td>995.0</td>
      <td>737.0</td>
    </tr>
    <tr>
      <th>174597</th>
      <td>04.06.2020</td>
      <td>22:00</td>
      <td>739</td>
      <td>8,8</td>
      <td>995</td>
      <td>5,9</td>
      <td>-</td>
      <td>0,4</td>
      <td>1</td>
      <td>8.8</td>
      <td>995.0</td>
      <td>739.0</td>
    </tr>
    <tr>
      <th>174598</th>
      <td>04.06.2020</td>
      <td>23:00</td>
      <td>740</td>
      <td>7,6</td>
      <td>995</td>
      <td>7,4</td>
      <td>-</td>
      <td>0,2</td>
      <td>1</td>
      <td>7.6</td>
      <td>995.0</td>
      <td>740.0</td>
    </tr>
    <tr>
      <th>174599</th>
      <td>04.06.2020</td>
      <td>24:00</td>
      <td>737</td>
      <td>6,5</td>
      <td>995</td>
      <td>6,6</td>
      <td>-</td>
      <td>0,0</td>
      <td>1</td>
      <td>6.5</td>
      <td>995.0</td>
      <td>737.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_wasserkuppe.dtypes
```




    Datum                         object
    Zeit                          object
    Kohlendioxid (CO2)[mg/m³]     object
    Temperatur[°C]                object
    Luftdruck[hPa]                object
    Windgeschwindigkeit[m/s]      object
    Windrichtung[Grad]            object
    Niederschlag[mm/30min]        object
    Globalstrahlung[W/m²]         object
    Temperatur                   float64
    Luftdruck                    float64
    Kohlendioxid                 float64
    dtype: object



Für die weitere Datenverarbeitung, zum Beispiel für FP Prophet, wird ein bestimmtes Datumsformat benötigt. 
Zur 'Zeit'spalte wird ":00" hinzugeügt, ohne Sekundenformat gibt es eine Fehlermeldung. [^1]

Prophet ist eine Open-Source-Software, die vom Core Data Science-Team von Facebook veröffentlicht wurde. 
Prophet ist für die Prognose von Zeitreihendaten geeignet.



```python
df_wasserkuppe['Sekundenformat'] = df_wasserkuppe['Zeit'] + ':00'
```

Die Pandas-Funktion to_datetime wird genutzt, um datumsspezifische Operationen durchführen zu können.


```python
df_wasserkuppe['DatumYDM'] = pd.to_datetime(df_wasserkuppe.Datum)
```

Pandas wird informiert, dass die zu lesenden Werte nacheinander Angaben zum Tag, Monat, Jahr beinhalten.


```python
df_wasserkuppe["DatumMDY"] = df_wasserkuppe["DatumYDM"].dt.strftime("%d-%m-%y")
```

Die Spalte Sekundenformat in 0 Tage 01:00:00 wird umgewandelt. (zählt Stunden bis 24 und beginnt bei 0 Tage)


```python
df_wasserkuppe['Stundenzaehler'] = pd.to_timedelta(df_wasserkuppe.Sekundenformat)
```

Zur Spalte DatumMDY die Spalte Stundenzaehler addiert = 2019-12-01 01:00:00


```python
df_wasserkuppe['DatumStundenzaehler'] = pd.to_datetime(df_wasserkuppe.DatumMDY) + pd.to_timedelta(df_wasserkuppe.Stundenzaehler)
```

Das Datumsformat wird in 01-12-2019 01:00 umgwandelt


```python
df_wasserkuppe["DatumFinal"] = df_wasserkuppe["DatumStundenzaehler"].dt.strftime("%d-%m-%y %H:%M")
```

Die folgenden Spalten werden gelöscht:


```python
df_wasserkuppe = df_wasserkuppe.drop(columns = ['Datum', 'Zeit','Sekundenformat','Kohlendioxid (CO2)[mg/m³]','Temperatur[°C]','Luftdruck[hPa]','DatumYDM','DatumMDY','Stundenzaehler','DatumStundenzaehler'])
df_wasserkuppe = df_wasserkuppe.drop(columns=['Windgeschwindigkeit[m/s]', 'Windrichtung[Grad]','Niederschlag[mm/30min]','Globalstrahlung[W/m²]'])
```

Die Spalte DatumFinal in Datum umbenennen.


```python
df_wasserkuppe = df_wasserkuppe.rename(columns={'DatumFinal' : 'Datum'})
```

Die Spalte Datum als Index setzen, dadurch werden die Vorzüge der Datumsklasse genutzt.


```python
df_wasserkuppe = df_wasserkuppe.set_index('Datum')
```

Das Ergebnis: Das Datum wurde als nutzbares Datumsformat umgewandelt. Die Temperatur, Luftdruck und Kohlendioxid sind im Zahlenformat und NaN Werte für fehlende Daten.


```python
df_wasserkuppe.head()
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
      <th>05-07-00 01:00</th>
      <td>9.7</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>05-07-00 02:00</th>
      <td>9.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>05-07-00 03:00</th>
      <td>9.7</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>05-07-00 04:00</th>
      <td>9.4</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>05-07-00 05:00</th>
      <td>8.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_wasserkuppe.dtypes
```




    Temperatur      float64
    Luftdruck       float64
    Kohlendioxid    float64
    dtype: object




```python
df_wasserkuppe.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 174600 entries, 2000-05-07 01:00:00 to 2020-05-06 00:00:00
    Data columns (total 4 columns):
     #   Column        Non-Null Count   Dtype  
    ---  ------        --------------   -----  
     0   Datum         174600 non-null  object 
     1   Temperatur    173564 non-null  float64
     2   Luftdruck     76646 non-null   float64
     3   Kohlendioxid  154136 non-null  float64
    dtypes: float64(3), object(1)
    memory usage: 6.7+ MB


Zusammenfassung:


```python
df_wasserkuppe['Temperatur'] = [x.replace(',', '.') for x in df_wasserkuppe['Temperatur[°C]']]
df_wasserkuppe['Luftdruck'] = pd.to_numeric(df_wasserkuppe['Luftdruck[hPa]'], errors='coerce')
df_wasserkuppe['Temperatur'] = pd.to_numeric(df_wasserkuppe['Temperatur'], errors='coerce')
df_wasserkuppe['Kohlendioxid'] = pd.to_numeric(df_wasserkuppe['Kohlendioxid (CO2)[mg/m³]'], errors='coerce')
df_wasserkuppe['Sekundenformat'] = df_wasserkuppe['Zeit'] + ':00'
df_wasserkuppe['DatumYDM'] = pd.to_datetime(df_wasserkuppe.Datum)
df_wasserkuppe["DatumMDY"] = df_wasserkuppe["DatumYDM"].dt.strftime("%d-%m-%y")
df_wasserkuppe['Stundenzaehler'] = pd.to_timedelta(df_wasserkuppe.Sekundenformat)
df_wasserkuppe['DatumStundenzaehler'] = pd.to_datetime(df_wasserkuppe.DatumMDY) + pd.to_timedelta(df_wasserkuppe.Stundenzaehler)
df_wasserkuppe["DatumFinal"] = df_wasserkuppe["DatumStundenzaehler"].dt.strftime("%d-%m-%y %H:%M")
df_wasserkuppe = df_wasserkuppe.drop(columns=['Datum', 'Zeit','Sekundenformat','Kohlendioxid (CO2)[mg/m³]','Temperatur[°C]','Luftdruck[hPa]','DatumYDM','DatumMDY','Stundenzaehler','DatumStundenzaehler'])
df_wasserkuppe = df_wasserkuppe.drop(columns=['Windgeschwindigkeit[m/s]', 'Windrichtung[Grad]','Niederschlag[mm/30min]','Globalstrahlung[W/m²]'])
df_wasserkuppe = df_wasserkuppe.rename(columns={'DatumFinal': 'Datum'})
df_wasserkuppe = df_wasserkuppe.set_index('Datum')
df_wasserkuppe.head()
```

Die Ergebnisse als csv speichern.


```python
df_wasserkuppe.to_csv('daten/wasserkuppe.csv')
```

Quellenangaben:

[^1]: Webseite: https://facebook.github.io/prophet/

