# Kohlendioxidmessung der Messstation Wasserkuppe

Stand: 16.03.2021

![grafik.png](attachment:grafik.png)

Der Boden als Kohlenstoffspeicher ist keine Konstante, sondern reagiert äußerst dynamisch auf veränderte Konzentrationen von Treibhausgasen in der Atmosphäre. Darum ist es wichtig den Kohlendioxidgehalt zu verfolgen. Das Hessische Landesamt für Naturschutz, Umwelt und Geologie, liefert aktuelle Messwerte der Kohlendioxid-Konzentrationen von zwei Stationen in Hessen. Diese befinden sich in Linden und Wasserkuppe.1 

Für die Jahre 2001-2018, siehe obige Abbildung, wurden die Daten nach Monat gruppiert. Jedes Element 
der Matrix stellt den monatlichen Mittelwert der Kohlendioxidmessung der Messstation Wasserkuppe dar. 
Die Angaben als Massenkonzentrationen in $mg/m^3$ gelten nur für die bestimmten Bedingungen von Druck und Temperatur. Daten als Volumenmischungsverhältnisse in ppm sind unabhängig von Druck und Temperatur. [2]

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

In diesem Abschnitt wird der Datensatz bearbeitet. Die Daten befinden sich noch im Rohzustand, für eine weitere Verarbeitung, werden sie in bestimmte Formate umgewandelt. Anschließend analysieren wir die Messdaten mit Python.

Für die Umsetzung wird das Pandas Framework genutzt. Hauptbestandteil ist die Klasse DataFrame, mit der sich zweidimensionale Tabellen, die aus Zeilen und Spalten bestehen, aufbereiten und umarbeiten lassen.

Die Datei messwerte.txt liefert Hinweise, wie die Datei in Python geladen werden soll. Deutschland verwendet ein Komma (,) als Dezimaltrennzeichen. Die meisten europäischen Länder, trennen mit ‚;“ anstatt ‚,‘ und das Dezimaltrennzeichen ist ‚,‘ statt ‚.‘ Die Messdaten einlesen (pd.read_csv) und die Zellen mit ‚;‘ trennen. Dezimaltrennzeichen ‚,‘ ( sep=‘;‘ , decimal=‘,‘).

Datum;Zeit;Kohlendioxid (CO2)[mg/m³];Temperatur[°C];Luftdruck[hPa]

01.12.2019;01:00;867;-3,5;1023

01.12.2019;02:00;885;-3,6;1023

Die Rohdaten stellen folgenden Aufgaben:

    Der Datentyp muss von Objekt in Zahl umwgewandelt werden.
    Die Datumspalte und Zeitspalte in ein Datumsformat bringen („%d-%m-%y %H:%M“).

Die pandas Bibliothek wird geladen und mit mit pd abgekürzt.


```python
import pandas
```



Quellenangabe:

Giuseppe Vettigli
Visualizing Atmospheric Carbon Dioxide
Apr. 22, 19
https://dzone.com/articles/visualizing-atmospheric-carbon-dioxide


[2] https://www.hlnug.de/fileadmin/dokumente/luft/externe_fachveranstaltungen/vorlesungen/jacobi/02_Grundlagen_der_Luftreinhaltung.pdf

