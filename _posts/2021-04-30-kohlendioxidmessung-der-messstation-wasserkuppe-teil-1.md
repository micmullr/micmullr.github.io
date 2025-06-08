---

title: 'Kohlendioxidmessung der Messstation Wasserkuppe Teil 1'
date: 2021-04-30
permalink: /beitrag/kohlendioxidmessung_wasserkuppe_teil1/
tags:

---

Kohlendioxid (CO₂) spielt als zentrales Treibhausgas eine entscheidende Rolle im globalen Klima. Die Analyse seiner zeitlichen und regionalen Konzentrationsverläufe liefert wertvolle Erkenntnisse über klimatische Prozesse und menschlichen Einfluss. Diese Untersuchung konzentriert sich auf die Messstation auf der Wasserkuppe – einem repräsentativen Standort im hessischen Luftmessnetz des HLNUG.

In diesem mehrteiligen Beitrag werden zunächst die Rohdaten aufbereitet. Dafür setzen wir Python und Pandas ein, um Rohdaten wie Temperatur, Luftdruck und CO₂-Werte korrekt zu formatieren und in eine zeitlich strukturierte Datenreihe zu überführen. Anschließend wandeln wir CO₂-Massenkonzentrationen (mg/m³) mithilfe physikalischer Formeln in das Volumenmischungsverhältnis (ppm) um.

Zur Veranschaulichung der räumlichen Einbettung verwenden wir GeoPandas und GIS-Daten, wodurch der Einfluss des Messstandorts – etwa durch nahe Verkehrswege oder militärisch wie das Sperrgebiet Wildflecken – verstanden werden kann.

Auf dieser Grundlage analysieren wir saisonale Schwankungen im CO₂-Verlauf und identifizieren Trends über zwei Jahrzehnte. Mittels Streu- und Zeitreihenplots werden Zusammenhänge zwischen CO₂, Temperatur und Luftdruck sichtbar, ergänzt durch rollierende Mittelwerte zur Trendglättung.

Stand: 27.04.2021

| ![Kohlendioxidmessung der Messstation Wasserkuppe](/images/kohlendioxidmessung/kohlendioxidmessung_messstation_wasserkuppe.png) |
|:-------------------------------------------------------------------------------------------------------------------------------:|
|                                                                                                                                 |
| *Kohlendioxidmessung der Messstation Wasserkuppe*                                                                               |

Das Hessische Landesamt für Naturschutz, Umwelt und Geologie liefert aktuelle Messwerte der Kohlendioxidkonzentrationen von zwei Stationen in Hessen. Diese befinden sich in Linden und auf der Wasserkuppe.[^1] 

Für die Jahre 2001 bis 2018 (siehe obige Abbildung) wurden die Daten nach Monaten gruppiert. Jedes Element der Matrix stellt den monatlichen Mittelwert der Kohlendioxidmessung an der Station Wasserkuppe dar. Die Angaben als Massenkonzentrationen in mg/m³ gelten nur für bestimmte Bedingungen von Druck und Temperatur. Daten als Volumenmischungsverhältnisse in ppm sind hingegen unabhängig von Druck und Temperatur.[^2]

In der Abbildung erkennt man den Photosyntheseeffekt der Vegetation: In den Wintermonaten ist der Kohlendioxidgehalt der Atmosphäre höher, weil die Assimilation kaum stattfindet. Bei der Assimilation werden aufgenommene, fremde anorganische und organische Stoffe aus der Umwelt in Bestandteile des Organismus umgewandelt, meist unter Energiezufuhr. Ein Beispiel dafür ist die Bildung von Glucose:

$$6 H_2O + 6 CO_2 → C_6 H_{12} O_6 + 6 O_2$$

Durch die Photosynthese der Landpflanzen wird in den folgenden Monaten Kohlendioxid aus der Atmosphäre entfernt. Dies lässt sich gut in den Monaten von Mai bis September erkennen; dort ist die Kohlendioxidkonzentration am geringsten.

Der Mittelwert war von 2001 bis 2004 relativ konstant, ab 2005 jedoch gestiegen. Bedingt durch umfangreiche anthropogene Freisetzungen wird der natürliche Treibhauseffekt verstärkt, was eine Klimaänderung zur Folge hat.

# Der Datensatz

Der Datensatz stammt vom Hessischen Landesamt für Naturschutz, Umwelt und Geologie (HLNUG). Er wurde von folgender Webseite heruntergeladen: [Luftmessstelle Wasserkuppe | Messdatenportal](http://www.hlnug.de/messwerte/datenportal/messstelle/2/1/0801/7,11,20)

Für die Analyse wurden folgende Einstellungen gewählt: Luft, Luftmessnetz, Wasserkuppe. Es wurden die drei Parameter Kohlendioxid (CO₂), Luftdruck und Temperatur sowie der Stundenmittelwert ausgewählt. Temperatur und Luftdruck sind notwendig, um die Messwerte in das Volumenmischungsverhältnis (ppm) umzurechnen. Der Download erfolgte am 05.06.2020 *für den Zeitraum* 05.07.2000 bis 04.06.2020.

| ![Standort der Messstation Wasserkuppe](/images/kohlendioxidmessung/standort_der_messstation_wasserkuppe.png) |
|:-------------------------------------------------------------------------------------------------------------:|
| *Standort der Messstation Wasserkuppe*                                                                        |

**Quellenangaben:**

[^1]: Webseite: https://www.hlnug.de/themen/luft/luftschadstoffe/kohlendioxid

[^2]: Jacobi, S. (o.D.). Grundlagen der Luftreinhaltung [Vorlesungsfolien]. Hessisches Landesamt für Naturschutz, Umwelt und Geologie Wiesbaden. https://www.hlnug.de/fileadmin/dokumente/luft/externe_fachveranstaltungen/vorlesungen/jacobi/02_Grundlagen_der_Luftreinhaltung.pdf . Abgerufen am 17. März 2021.
