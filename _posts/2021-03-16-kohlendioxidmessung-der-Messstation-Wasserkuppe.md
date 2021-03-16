Stand: 16.03.2021

![grafik.png](attachment:grafik.png)

| ![Kohlendioxidmessung der Messstation Wasserkuppe](images/co2hessen/kohlendioxidmessung_messstation_wasserkuppe.png) | 
|:--:| 
| *Kohlendioxidmessung der Messstation Wasserkuppe* |

Der Boden als Kohlenstoffspeicher ist keine Konstante, sondern reagiert äußerst dynamisch auf veränderte Konzentrationen von Treibhausgasen in der Atmosphäre. Darum ist es wichtig den Kohlendioxidgehalt zu verfolgen. Das Hessische Landesamt für Naturschutz, Umwelt und Geologie, liefert aktuelle Messwerte der Kohlendioxid-Konzentrationen von zwei Stationen in Hessen. Diese befinden sich in Linden und Wasserkuppe.[^1] 

Für die Jahre 2001-2018, siehe obige Abbildung, wurden die Daten nach Monat gruppiert. Jedes Element 
der Matrix stellt den monatlichen Mittelwert der Kohlendioxidmessung der Messstation Wasserkuppe dar. 
Die Angaben als Massenkonzentrationen in $mg/m^3$ gelten nur für die bestimmten Bedingungen von Druck und Temperatur. Daten als Volumenmischungsverhältnisse in ppm sind unabhängig von Druck und Temperatur. [^2]

In der Abbildung erkennt man den Photosyntheseeffekt der Vegetation. In den Wintermonaten ist der Kohlendioxidgehalt der Atmosphäre  höher, da eine Assimilation kaum vorhanden ist. Bei der Assimilation werden aufgenommene, fremde anorganische und organische Stoffe aus der Umwelt in Bestandteile des Organismus umgewandelt, meistens unter Energiezufuhr. Ein Beispiel dafür ist die Bildung von Glucose.

$$6 H_2O + 6 CO_2 → C_6 H_{12} O_6 + 6 O_2$$

Durch die Photosynthese von Landpflanzen werden in den weiteren Monaten Kohlendioxid entzogen, dies kann man gut in den Monaten von Mai bis September erkennen, dort ist die Kohlendioxidmessung am geringsten. 

Der Mittelwert ist von 2001-2004 konstant und ab 2005 gestiegen. Bedingt durch umfangreiche anthropogene Freisetzung wird der natürliche Treibhauseffekt verstärkt, welches eine Klimaänderung zur Folge hat.


# Der Datensatz

Der Datensatz stammt vom Hessisches Landesamt für Naturschutz, Umwelt und Geologie (HLNUG). Dieser wurde von folgender Webseite runtergeladen. http://www.hlnug.de/messwerte/datenportal/messstelle/2/1/0801/7,11,20

Folgendes wurde gewählt: Luft, Luftmessnetz, Wasserkuppe. Mit den drei ausgewählten Parametern Kohlendioxid (CO₂), Luftdruck, Temperatur und dem Stundenmittelwert. Temperatur und Luftdruck sind notwendig um die Messwerte in das Volumenmischungsverhältnis ppm umzurechnen. Der Download fand am 05.06.2020 statt, für diesem Zeitraum: 05.07.2000 - 04.06.2020. 

![grafik.png](attachment:grafik.png)

$$Abbildung: \:Messstation\:Wasserkuppe$$


# Verarbeitung und Vorverarbeitung vom Datensatz

In diesem Abschnitt wird der Datensatz bearbeitet. Die Daten befinden sich noch im Rohzustand, für eine weitere Verarbeitung, werden sie in bestimmte Formate umgewandelt. Anschließend analysieren wir die Messdaten mit Python. Für die Umsetzung wird das Pandas Framework genutzt. Hauptbestandteil ist die Klasse DataFrame, mit der sich zweidimensionale Tabellen, die aus Zeilen und Spalten bestehen, aufbereiten und umarbeiten lassen. Die Datei messwerte.txt liefert Hinweise, wie die Datei in Python geladen werden soll. Deutschland verwendet ein Komma (,) als Dezimaltrennzeichen. Die meisten europäischen Länder, trennen mit ‚;“ anstatt ‚,‘ und das Dezimaltrennzeichen ist ‚,‘ statt ‚.‘ Die Messdaten einlesen (pd.read_csv) und die Zellen mit ‚;‘ trennen. Dezimaltrennzeichen ‚,‘ ( sep=‘;‘ , decimal=‘,‘).

Datum;Zeit;Kohlendioxid (CO2)[mg/m³];Temperatur[°C];Luftdruck[hPa]

01.12.2019;01:00;867;-3,5;1023

01.12.2019;02:00;885;-3,6;1023

Die Rohdaten stellen folgenden Aufgaben:

Der Datentyp muss von Objekt in Zahl umwgewandelt werden. 
Die Datumspalte und Zeitspalte in ein Datumsformat bringen („%d-%m-%y %H:%M“).

Die pandas Bibliothek wird geladen und mit mit pd abgekürzt.


```python
import pandas as pd
```


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



Für die weitere Datenverarbeitung, zum Beispiel für FP Prophet, brauchen wir ein bestimmtes Datumsformat. 
Zur 'Zeit'spalte wird ":00" hinzugeügt. Ohne Sekundenformat gibt es eine Fehlermeldung, z.B. bei FP Prophet.

Prophet ist eine Open-Source-Software, die vom Core Data Science-Team von Facebook veröffentlicht wurde. 
Prophet ist ein Verfahren zur Vorhersage von Zeitreihendaten, das auf einem additiven Modell basiert, bei dem nichtlineare Trends mit jährlicher, wöchentlicher und täglicher Saisonalität sowie Ferieneffekten angepasst werden. Es funktioniert am besten mit Zeitreihen, die starke saisonale Effekte und mehrere Saisons historischer Daten haben. Prophet ist robust gegenüber fehlenden Daten und Verschiebungen im Trend und kommt typischerweise gut mit Ausreißern zurecht.


https://facebook.github.io/prophet/


```python
df['Sekundenformat'] = df['Zeit'] + ':00'
```

Wir nutzen die Pandas-Funktion to_datetime. Um datumsspezifische Operationen durchführen zu können.


```python
df['DatumYDM'] = pd.to_datetime(df.Datum)
```

Wir informieren Pandas, dass die zu lesenden Werte nacheinander Angaben zum Tag, Monat, Jahr beinhalten.


```python
df["DatumMDY"] = df["DatumYDM"].dt.strftime("%d-%m-%y")
```

Wir wandeln Spalte Sekundenformat in 0 days 01:00:00 um. (zählt nur Stunden bis 24 und beginnt bei 0 Tage)


```python
df['Stundenzaehler'] = pd.to_timedelta(df.Sekundenformat)
```

Wir addieren zur Spalte DatumMDY die Spalte Stundenzaehler = 2019-12-01 01:00:00


```python
df['DatumStundenzaehler'] = pd.to_datetime(df.DatumMDY) + pd.to_timedelta(df.Stundenzaehler)
```

Das Datumsformat wird in 01-12-2019 01:00 umgwandelt


```python
df["DatumFinal"] = df["DatumStundenzaehler"].dt.strftime("%d-%m-%y %H:%M")
```

Wir löschen die folgenden Spalten:


```python
df = df.drop(columns = ['Datum', 'Zeit','Sekundenformat','Kohlendioxid (CO2)[mg/m³]','Temperatur[°C]','Luftdruck[hPa]','DatumYDM','DatumMDY','Stundenzaehler','DatumStundenzaehler'])
```

Wir nennen Spalte DatumFinal in Datum um


```python

```


```python

```


```python

```


```python

```


```python

```

Für die weitere Verarbeitung der Daten brauchen wir ein bestimmtes Datumsformat. Zum Beispiel für FP Prophet.

Wir addieren zur Spalte 'Zeit' :00 und fügen eine neue Spalte 'Sekundenformat' hinzu, ohne Sekundenformat gibt es eine Fehlermeldung, z.B. bei FP Prophet.



```python
#Eine neue Temperaturspalte(df['Temperatur']) wird angehangen.
#In der Temperatur[°C]spalte wird das Dezimaltrennzeichen ',' mit '.' getauscht. (x.replace)


df_wasserkuppe['Temperatur'] = [x.replace(',', '.') for x in df_wasserkuppe['Temperatur[°C]']]

#Wir wandeln die Datenreihen; Luftdruck[hPa], Temperatur und Kohlendioxid (CO2)[mg/m³] von object zu float um. (pd.to_numeric)
#Der Parameter errors='coerce' wandelt '-' und andere Parsingfehler zu NaN (Not a Number) um.

df_wasserkuppe['Luftdruck'] = pd.to_numeric(df_wasserkuppe['Luftdruck[hPa]'], errors='coerce')

df_wasserkuppe['Temperatur'] = pd.to_numeric(df_wasserkuppe['Temperatur'], errors='coerce')

df_wasserkuppe['Kohlendioxid'] = pd.to_numeric(df_wasserkuppe['Kohlendioxid (CO2)[mg/m³]'], errors='coerce')

#Für die weitere Datenverarbeitung, zum Beispiel für FP Prophet, brauchen wir ein bestimmtes Datumsformat. 
#Zur 'Zeit'spalte wird ":00" hinzugeügt. 
#ohne Sekundenformat gibt es eine Fehlermeldung, z.B. bei FP Prophet.

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


```python
df_wasserkuppe.to_csv('daten/wasserkuppe.csv')
```


```python

```


```python

```


```python

```

[^1]: This is the first footnote.

[^2]: This is the first footnote.

Quellenangabe:

Giuseppe Vettigli
Visualizing Atmospheric Carbon Dioxide
Apr. 22, 19
https://dzone.com/articles/visualizing-atmospheric-carbon-dioxide


[2] https://www.hlnug.de/fileadmin/dokumente/luft/externe_fachveranstaltungen/vorlesungen/jacobi/02_Grundlagen_der_Luftreinhaltung.pdf

