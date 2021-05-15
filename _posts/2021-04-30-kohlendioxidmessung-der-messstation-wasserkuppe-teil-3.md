---
title: 'Einfluss des Messstellenstandort auf die Messdaten Teil 3'
date: 2021-04-30
permalink: /beitrag/kohlendioxidmessung_wasserkuppe_teil3/
tags:
---
Die Lichter der Erde bei Nacht sind hauptsächlich vom Menschen gemacht. Dieses wird genutzt um die nährere Umgebung des Standortes auf die anthropogenen Einflüsse einzuschätzen. 

Hierfür werden Satellitenbilder genutzt. Vom Visible-Infrared-Imaging-Radiometer-Suite-Instrument (VIIRS) auf dem Suomi-NPP-Satelliten, der am 28. Oktober 2011 von NASA und NOAA (National Oceanic and Atmospheric Administration) gestartet worden ist.

Das VIIRS-Instrument wurde speziell entwickelt, um die Erde tagsüber statt nachts zu beobachten. Seine Empfindlichkeit reicht aus, um das Licht eines einzelnen Schiffes auf der Erdoberfläche zu erfassen.[^1]

Stand: 27.04.2021


```python
wasserkuppe_df = deutschland_df
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
fig = plt.figure(figsize = (20,20))
ax = plt.subplot()
ax.text(x = 1106053.829 - 47150, y = 6532916.278 + 5915, s ='Messstelle Wasserkuppe', size = 28, color = 'white') 
wasserkuppe_df = wasserkuppe_df.plot(color='none',edgecolor='gray', linewidth=0, ax = ax)
                                                                         
ax.set_axis_off()                                    

gdf.plot(ax = wasserkuppe_df, marker = 'o', color = 'red', markersize = 150)

ctx.add_basemap(ax = ax, source=ctx.providers.NASAGIBS.ViirsEarthAtNight2012)
```

              city                         geometry
    0  Wasserkuppe  POINT (1106053.829 6532916.278)




![png](/images/kohlendioxidmessung/output_2_1.png)
    



```python
wasserkuppe_df = deutschland_df.query(('bundesland == "Hessen"'))
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
fig = plt.figure(figsize = (25,25))
ax = plt.subplot()
ax.text(x = 1106053.829 - 47150, y = 6532916.278 + 5915, s ='Messstelle Wasserkuppe', size = 18, color = 'white') 
wasserkuppe_df = wasserkuppe_df.plot(color='none',edgecolor='gray', linewidth=1, ax = ax)
                                                                         
ax.set_axis_off()                                    

gdf.plot(ax = wasserkuppe_df, marker = 'o', color = 'red', markersize = 150)

ctx.add_basemap(ax = ax, source=ctx.providers.NASAGIBS.ViirsEarthAtNight2012)
```

              city                         geometry
    0  Wasserkuppe  POINT (1106053.829 6532916.278)


    C:\Users\mm\anaconda3\lib\site-packages\contextily\tile.py:632: UserWarning: The inferred zoom level of 9 is not valid for the current tile provider (valid zooms: 1 - 8).
      warnings.warn(msg)




![png](/images/kohlendioxidmessung/output_3_2.png)
    



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
ax.text(x = 1106053.829 - 2700, y = 6532916.278 + 515, s ='Messstelle Wasserkuppe', size = 18, color = 'white') 
wasserkuppe_df = wasserkuppe_df.plot(color='none',edgecolor='gray', linewidth=3, ax = ax)
                                                                         
ax.set_axis_off()                                    

gdf.plot(ax = wasserkuppe_df, marker = 'o', color = 'red', markersize = 150)

ctx.add_basemap(ax = ax, source=ctx.providers.NASAGIBS.ViirsEarthAtNight2012)
```

              city                         geometry
    0  Wasserkuppe  POINT (1106053.829 6532916.278)


    C:\Users\mm\anaconda3\lib\site-packages\contextily\tile.py:632: UserWarning: The inferred zoom level of 13 is not valid for the current tile provider (valid zooms: 1 - 8).
      warnings.warn(msg)




![png](/images/kohlendioxidmessung/output_4_2.png)
    


Die verschiedenen Zoomlevel um die Region der Messstelle zeigen wenige Lichter bei Nacht. Hier kann man eine ländliche Region erkennen. Das bedeutet der Datensatz sollte geringe anthropogen Einflüsse der näheren Umgebung haben. 

Quellenangaben:

[^1]: Hattenbach, J. (2012, 6. Dezember). Das neue Bild der Erde - bei Nacht. SciLogs - Wissenschaftsblogs. https://scilogs.spektrum.de/himmelslichter/das-neue-bild-der-erde-bei-nacht/


Quellenangaben Sonstiges:

https://stackoverflow.com/questions/51621615/which-geopandas-datasets-maps-are-available

https://github.com/geopandas/geopandas/blob/master/doc/source/gallery/plotting_basemap_background.ipynb

https://geopandas.org/gallery/plotting_basemap_background.html