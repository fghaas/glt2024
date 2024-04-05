# Was ist eine Photovoltaik-Anlage?

<!-- Note -->
Eine Photovoltaik-Anlage (PV-Anlage) macht aus Licht (Sonnenlicht) Strom.
Das funktioniert so, dass Licht auf Solarzellen (Photodioden, eine Art Halbleiter) fällt, die zu großen Paneelen zusammengefügt sind.

Wenn Licht auf die Solarzelle fällt, erzeugt sie eine kleine Menge Gleichstrom.
Und weil ein Solarpaneel ganz viele Solarzellen enthält, die alle in Serie geschaltet sind, produzieren die alle gemeinsam eine ganz ordentliche Menge Gleichstrom (so ca. 50 Volt pro Modul).


<!-- .slide: data-background-image="images/wechselrichter.jpg" data-background-size="contain" -->
## Wechselrichter <!-- .element class="hidden" -->

<!-- Note -->
Aber mit Gleichstrom fangen wir nix an, weil ja fast alle Geräte im Haus mit Wechselstrom funktionieren (auch die Wärmepumpe!).
Also brauchen wir einen **Wechselrichter,** der uns aus dem Gleichstrom Wechselstrom macht.

Damit können wir alle elektrischen Geräte in unserem Haus betreiben — aber nur wenn die Sonne scheint.


<!-- .slide: data-background-image="images/speicher.jpg" data-background-size="contain" -->
## Stromspeicher <!-- .element class="hidden" -->

<!-- Note -->
Damit wir auch Sonnenstrom verwenden können, wenn sie mal nicht scheint, brauchen wir einen **Stromspeicher.**
Der ist eigentlich nichts anderes als eine Batterie, allerdings eine ziemlich große.


<!-- .slide: data-background-image="images/Energiefluss_PVA_2.svg" data-background-size="contain" -->
## Netzbezug und Einspeisung <!-- .element class="hidden" -->

<!-- Note -->
Manchmal wird die Batterie auch leer — wenn mal länger nicht die Sonne scheint —, und wenn wir dann noch weiter Strom brauchen, dann ziehen wir den einfach aus dem Stromnetz.
Dazu haben wir wie früher eine **Stromleitung** mit einem Stromzähler (einem Smart Meter).

Und dann kann es uns natürlich auch passieren, dass wir alle elektrischen Geräte im Haus betreiben können *und* unsere Batterie komplett voll geladen haben und es scheint noch *immer* die Sonne, dann speisen wir ins Stromnetz ein.
Das funktioniert auch über dieselbe Stromleitung, und über einen eigenen Zählpunkt am Smart Meter.
Das nennt sich dann *Überschusseinspeisung.*

Bildquelle: <https://commons.wikimedia.org/wiki/File:Energiefluss_PVA_2.svg> ([CC0](https://creativecommons.org/publicdomain/zero/1.0/deed.de), Public Domain)


## Woraus besteht unsere PV-Anlage?

22 Module zu 465&nbsp;Wp == 10,23&nbsp;kWp <!-- .element class="fragment fade-in-then-semi-out" -->

15&nbsp;kW (DC) Wechselrichter <!-- .element class="fragment fade-in-then-semi-out" -->

9,2&nbsp;kWh Stromspeicher 
(max. 5&nbsp;kW Entladeleistung)  <!-- .element class="fragment fade-in-then-semi-out" -->

<!-- Note -->
Unsere PV-Anlage besteht aus 22 Solarmodulen, die jeweils *maximal* 465 Watt Leistung erzeugen können, das ergibt eine theoretische Gesamt-Maximalleistung von 10,23 Kilowatt-Peak (kWp).

Der Wechselrichter könnte noch etwa 50% mehr Kapazität liefern, wäre also noch durch zusätzliche Module ausbaufähig.

Der Stromspeicher hat 9.2 kWh *nutzbare* Kapazität, kann aber maximal 5 kW Entladeleistung liefern.
Auch die Ladeleistung ist begrenzt und liegt bei ca. 5,5kW.


<!-- .slide: data-background-image="images/energy-dashboard-202309.png" data-background-size="contain" -->
## Was leistet die PV-Anlage? <!-- .element class="hidden" -->

<!-- Note -->
So sieht die Leistung der PV-Anlage im September aus:

* 30-40&nbsp;kWh/Tag
* 40% Eigenbedarf, 60% ins Netz
* 10% Energieverlust im Speicher

September ist ein sehr energiesparender Monat für ein Haus mit Wärmepumpe: man heizt noch nicht und kühlt nicht mehr.


<!-- .slide: data-background-image="images/energy-dashboard-20230916.png" data-background-size="contain" -->
## Produktion tagsüber (Schönwetter) <!-- .element class="hidden" -->

<!-- Note -->
Typischer Verlauf an einem sonnigen Tag im September. (16. September)

Nachts minimaler Verbrauch aus der Batterie (wie erwähnt, wir heizen noch nicht).
Morgens ist die Batterie noch ca. 30-40% geladen.

Am Vormittag Eigenverbrauch (Wäsche, Geschirr, Kochen) und aufladen der Batterie (braucht ca. 3 Sonnenstunden).

Nachmittags praktisch ausschließlich Einspeisung.

Abends ab 20:00 dann Verbrauch aus der Batterie, für Warmwasseraufbereitung der Wärmepumpe.


<!-- .slide: data-background-image="images/charge-max.png" data-background-size="contain" -->
## Einspeisung beim Laden <!-- .element class="hidden" -->

<!-- Note -->
An sonnigen Tagen kann durchaus auch diese Situation hier vorkommen:

Vormittags ist der Speicher noch nicht voll geladen (30%), aber die PV-Anlage produziert mehr Strom, als der Speicher laden kann.

Dann geht der Überschuss einfach ins Netz.


<!-- .slide: data-background-image="images/energy-dashboard-20230903.png" data-background-size="contain" -->
## Produktion tagsüber (Schlechtwetter) <!-- .element class="hidden" -->

<!-- Note -->
Und so sieht ein Tag mit abwechselnd Wolken und Regen aus. (3. September)

Mit 7-8 wolkigen Stunden kriegen wir die morgens fast leer gewesene Batterie bis zum Nachmittag auch voll, speisen dann allerdings kaum ein.


<!-- .slide: data-background-image="images/energy-dashboard-202403.png" data-background-size="contain" -->
## Monatsproduktion März <!-- .element class="hidden" -->

<!-- Note -->
Hier noch eine Übersicht über Energieverbrauch und -Erzeugung im März.

Das ist ganz interessant, weil hier alles ganz schnell kippt:
zu Monatsbeginn hat die Wärmepumpe noch ordentlich zu tun, *und* es scheint weniger Sonne; am Monatsende heizt man kaum mehr und die Sonne ist da.

Führt dazu, dass man Anfang März noch ordentlich Strom zukauft, und am Monatsende bereits wieder Nettoeinspeiser ist.


<!-- .slide: data-background-image="images/per-module-peaks.png" data-background-size="contain" -->
## Produktionsspitzen März <!-- .element class="hidden" -->

<!-- Note -->
Auch das erwartet man so vielleicht nicht, das ist die Stromproduktion dividiert durch die Anzahl der Module, also Watt-pro-Modul.

Fällt jemandem was auf?

Die Spitzenwerte liegen hier deutlich *über* den nominellen maximal 465 Watt pro Modul.

Das liegt daran, dass die Module kalt sind.
Bei PV-Modulen ist es umgekehrt wie bei der Wärmepumpe, und die Effizienz *steigt* bei kühlen Temperaturen (ca. 1% pro 3K Temperaturunterschied).
Der Normwert bezieht sich auf 25°C.

Hat es also um die 0°C, obwohl die Sonne kräftig scheint (und geht vielleicht auch noch Wind, der die Module effizient kühlt), dann können wir 8% mehr aus den Modulen rausholen.
