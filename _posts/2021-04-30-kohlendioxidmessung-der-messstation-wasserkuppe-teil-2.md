---
title: 'Messstellenstandort Wasserkuppe mit Geopandas Teil 2'
date: 2021-04-30
permalink: /beitrag/kohlendioxidmessung_wasserkuppe_teil2/
tags:
---

Welchen Einfluss hat der Messstellenstandort Wasserkuppe auf die Messdaten? Vor allem die anthropogen Einflüsse der näheren Umgebung. Die Visualisierung wird mit geopandas umgesetzt. Geopandas ist eine Pythonbibliothek für die Arbeit mit Geodaten. 

Für eine visuelle Eingrenzung liefert eine Shapefile, ein Format für vektorielle Geodaten, Polygondaten mit Bundesländer und Postleitzahlengebiete. Im weiteren Verlauf wird der Umgang mit dem Koordinatenbezugssystem beschrieben, den Installationsblauf von Geopandas gezeigt und eine OpenStreetMap als Basiskarte eingebunden.

Das Koordinatenreferenzsystem oder Koordinatenbezugsystem (KBS), engl. coordinate reference system, international mit CRS abgekürzt, beschreibt die Lage eines Koordinatensystems zur Angabe einer Position auf der Erde.

Stand: 27.04.2021

## EPSG-Codes
Der EPSG-Code ist ein System weltweit eindeutiger, 4- bis 5-stelliger Schlüsselnummern für Koordinatenreferenzsysteme und andere geodätische Datensätze, wie Referenzellipsoide oder Projektionen.


  	

 	 	 

 	



|Code   |Koordinatenreferenzsystem   |Bemerkung   |
|:-:|:-:|:-:|
|4326|WGS-84 / Geographische Koordinaten|weltweites System für GPS-Geräte, OpenStreetMap Datenbank|
|3857|WGS 84 / Pseudo-Mercator|Google Maps, OpenStreetMap|
|31467|DHDN / Gauß-Krüger Zone 3|passend für Baden-Württemberg und Hessen.|
|   |   |   |

## Installation

Es wurde Python 3.7 genutzt. Die folgende Installationsreihenfolge ist wichtig. Microsoft Visual C++ 14.0 oder höher wird benötigt. Dieses kann unter https://visualstudio.microsoft.com/de/visual-cpp-build-tools/ runtergeladen werden.

* pip install numpy
* pip install pandas
* pip install shapely
* pip install pipwin 
* pipwin install gdal
* pipwin install fiona
* pip install pyproj
* pip install six
* pip install rtree
* pip install geopandas

* pip install matplotlib
* pip contextily ---> lieferte den Fehler: A GDAL API version must be specified. Provide a path to gdal-config using a GDAL_CONFIG environment variable or use a GDAL_VERSION environment variable.

Deswegen:
* conda install contextily --channel conda-forge

## Shapefile Deutschland

Die benötigte Shapefile wurde von folgender Seite runtergeladen:
www.suche-postleitzahl.org/downloads. Die folgende Seite war dabei sehr hilfreich.[^1]


- plz-gebiete.shp: Die Datei enthält die Polygone der einzelnen Postleitzahlenbereiche 
- zuordnung_plz_ort.csv: Die zugehörige Postleitzahl als Bezeichner für Ort und Bundesland. Das Dateiformat ist im CSV-Format. 


​    


```python
import geopandas as gpd
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('fivethirtyeight')

%matplotlib inline
```

Die Postleitzahlen müssen als String gelesen werden. Sonst wird eine 01 beginnende PLZ mit 1 geparst. Die shapefile wird geladen und das CRS ausgegeben. Alle vier Dateien mit den Endungen, .dbf , prj , shp , shx sollten im selben Ordner sein. 


```python
dtl_shapefile_df = gpd.read_file('plz-gebiete.shp', dtype={'plz': str}, encoding="utf-8")

dtl_shapefile_df


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
      <th>plz</th>
      <th>note</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52538</td>
      <td>52538 Gangelt, Selfkant</td>
      <td>POLYGON ((5.86632 51.05110, 5.86692 51.05124, ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>47559</td>
      <td>47559 Kranenburg</td>
      <td>POLYGON ((5.94504 51.82354, 5.94580 51.82409, ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>52525</td>
      <td>52525 Waldfeucht, Heinsberg</td>
      <td>POLYGON ((5.96811 51.05556, 5.96951 51.05660, ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>52074</td>
      <td>52074 Aachen</td>
      <td>POLYGON ((5.97486 50.79804, 5.97495 50.79809, ...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>52531</td>
      <td>52531 Übach-Palenberg</td>
      <td>POLYGON ((6.01507 50.94788, 6.03854 50.93561, ...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>8720</th>
      <td>02899</td>
      <td>02899 Ostritz, Schönau-Berzdorf</td>
      <td>POLYGON ((14.85296 51.06854, 14.85449 51.06859...</td>
    </tr>
    <tr>
      <th>8721</th>
      <td>02929</td>
      <td>02929 Rothenburg/O.L.</td>
      <td>POLYGON ((14.85491 51.32895, 14.85608 51.33004...</td>
    </tr>
    <tr>
      <th>8722</th>
      <td>02827</td>
      <td>02827 Görlitz</td>
      <td>POLYGON ((14.91168 51.14243, 14.91571 51.14571...</td>
    </tr>
    <tr>
      <th>8723</th>
      <td>02828</td>
      <td>02828 Görlitz</td>
      <td>POLYGON ((14.93413 51.16084, 14.93451 51.16123...</td>
    </tr>
    <tr>
      <th>8724</th>
      <td>02826</td>
      <td>02826 Görlitz</td>
      <td>POLYGON ((14.95374 51.14703, 14.95393 51.14814...</td>
    </tr>
  </tbody>
</table>
<p>8725 rows × 3 columns</p>
</div>




```python
dtl_shapefile_df.crs
```




    {'init': 'epsg:4326'}




```python
plz_ort_df = pd.read_csv(
    'zuordnung_plz_ort.csv', 
    sep=',', 
    dtype={'plz': str}
)

plz_ort_df.drop('osm_id', axis=1, inplace=True)

plz_ort_df.head()
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
      <th>ort</th>
      <th>plz</th>
      <th>bundesland</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aach</td>
      <td>78267</td>
      <td>Baden-Württemberg</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aach</td>
      <td>54298</td>
      <td>Rheinland-Pfalz</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aachen</td>
      <td>52062</td>
      <td>Nordrhein-Westfalen</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aachen</td>
      <td>52064</td>
      <td>Nordrhein-Westfalen</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aachen</td>
      <td>52066</td>
      <td>Nordrhein-Westfalen</td>
    </tr>
  </tbody>
</table>
</div>



Verbinde die .shape-Datei mit der csv-Datei, nutze dabei die Postleitzahlen. Dies ist ein typischer Excel sverweis. 


```python
deutschland_df = pd.merge(
    left=dtl_shapefile_df, 
    right=plz_ort_df, 
    on='plz',
    how='inner'
)

deutschland_df.drop(['note'], axis=1, inplace=True)

deutschland_df.head()
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
      <th>plz</th>
      <th>geometry</th>
      <th>ort</th>
      <th>bundesland</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52538</td>
      <td>POLYGON ((5.86632 51.05110, 5.86692 51.05124, ...</td>
      <td>Gangelt</td>
      <td>Nordrhein-Westfalen</td>
    </tr>
    <tr>
      <th>1</th>
      <td>52538</td>
      <td>POLYGON ((5.86632 51.05110, 5.86692 51.05124, ...</td>
      <td>Selfkant</td>
      <td>Nordrhein-Westfalen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47559</td>
      <td>POLYGON ((5.94504 51.82354, 5.94580 51.82409, ...</td>
      <td>Kranenburg</td>
      <td>Nordrhein-Westfalen</td>
    </tr>
    <tr>
      <th>3</th>
      <td>52525</td>
      <td>POLYGON ((5.96811 51.05556, 5.96951 51.05660, ...</td>
      <td>Heinsberg</td>
      <td>Nordrhein-Westfalen</td>
    </tr>
    <tr>
      <th>4</th>
      <td>52525</td>
      <td>POLYGON ((5.96811 51.05556, 5.96951 51.05660, ...</td>
      <td>Waldfeucht</td>
      <td>Nordrhein-Westfalen</td>
    </tr>
  </tbody>
</table>
</div>



# Messstellenstandort Wasserkuppe 


```python
import shapely
import contextily as ctx
```


```python
wasserkuppe_df = deutschland_df.query(('plz == "36129"'))
wasserkuppe_df = wasserkuppe_df.to_crs(epsg=3857)

df = pd.DataFrame({'city': ['Wasserkuppe'],
                   'latitude': [50.49768412],
                   'longitude': [9.9358506]})
gdf = gpd.GeoDataFrame(df.drop(['latitude', 'longitude'], axis=1),
                       crs = {'init': 'epsg:4326'},
                       geometry = [shapely.geometry.Point(xy)
                                 for xy in zip(df.longitude, df.latitude)])
gdf = gdf.to_crs(epsg = 3857)
print(gdf)
fig = plt.figure(figsize = (15,15))
ax = plt.subplot()
ax.text(x = 1106053.829, y = 6532916.278 - 715, s ='Messstelle Wasserkuppe', size = 18) 
wasserkuppe_df = wasserkuppe_df.plot(color='none',edgecolor='black', linewidth=3, ax = ax)
                                                                         
ax.set_axis_off()                                    

gdf.plot(ax = wasserkuppe_df, marker = 'o', color = 'red', markersize = 150)

ctx.add_basemap(ax = ax, source=ctx.providers.OpenTopoMap)
```

              city                         geometry
    0  Wasserkuppe  POINT (1106053.829 6532916.278)




![png](/images/kohlendioxidmessung/output_13_1.png)
    


Der rote schraffierte Bereich ist das Sperrgebiet Truppenübungsplatz Wildflecken.

Quellenangaben:


[^1]: Orduz, J. C. (2020, 7. Januar). Open Data: Germany Maps Viz. Dr. Juan Camilo Orduz. https://juanitorduz.github.io/germany_plots/


Quellenangaben Sonstiges:

https://stackoverflow.com/questions/51621615/which-geopandas-datasets-maps-are-available

https://github.com/geopandas/geopandas/blob/master/doc/source/gallery/plotting_basemap_background.ipynb

https://geopandas.org/gallery/plotting_basemap_background.html