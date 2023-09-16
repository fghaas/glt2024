# Wie nutzt unser Haus Strom?

<!-- Note -->
* Gelernt: man sollte wissen, wie der eigene Haushalt Energie nutzt. (danke, [Kris](https://blog.koehntopp.info/2022/05/02/a-solar-roof-2.html)!)

Wir wollen also vor allem 3 Dinge wissen:

* Wie viel Strom verbrauchen wir pro Tag insgesamt? (Um Gas brauchen wir uns ja nicht mehr zu kümmern.)
* Wie entwickelt sich dieser Verbrauch übers Jahr?
* Wie verteilt sich dieser Verbrauch auf einzelne Geräte?


## Stromverbrauch

<!-- Note -->
Schritt 1: Rausfinden, wieviel Energie unser Haus pro Tag (noch besser: pro Stunde) verbraucht.

In einem Haus, das *keine* PV-Anlage hat, ist das erstmal einfach, weil der Strom ja nur auf einem Weg ins Haus reinkommt, nämlich aus dem Netz.


<!-- .slide: data-background-image="images/e450.jpg" data-background-size="contain" -->
### Smart Meter <!-- .element class="hidden" -->

<!-- Note -->
Also: wir können unser Smart Meter anzapfen.

In unserem Zählerkasten findet sich ein [Landis+Gyr E450](https://www.landisgyr.eu/product/landisgyr-e450/).

* In Europa (nicht nur Österreich) weit verbreitetes Smart Meter.
* Auch in der Schweiz und den Niederlanden im Einsatz.


<!-- .slide: data-background-image="images/e450-kundenschnittstelle.jpg" data-background-size="contain" -->
### Kundenschnittstelle <!-- .element class="hidden" -->

<!-- Note -->
Aufgrund gesetzlicher Richtlinien muss ein Smart Meter eine Schnittstelle haben, über die Kunden jederzeit Verbrauchsdaten auslesen können.
Sinn davon ist offensichtlich, dass man als Kunde den eigenen Stromverbrauch nicht nur aus der Stromrechnung herausfinden können soll.

Das E450 ist mit mehreren Kundenschnittstellen-Optionen erhältlich.

* Die eigentliche Standard-Option ist eine RJ12-Schnittstelle.
  Das wäre praktisch, denn dafür gibt es den [Slimmelezer+](https://www.zuidwijk.com/product/slimmelezer-plus/).
  Geht in Österreich aber wohl nur im Netz Burgenland.
* Die Wiener Netze haben nur eine Infrarot-Kundenschnittstelle (hier im Foto hervorgehoben).
  Die müsste man dann mit einem [Optokopf](https://shop.weidmann-elektronik.de/index.php?page=product&info=24) auslesen, was man mit [smartmeter-reader](https://github.com/aburgr/smartmeter-reader) machen kann.


<!-- .slide: data-background-image="images/e450-impuls.jpg" data-background-size="contain" -->
### Pulszähler <!-- .element class="hidden" -->

<!-- Note -->
Eine weitere Option ist ein Pulszähler.

* Der Zähler gibt an einer LED (hier hervorgehoben) einen Puls pro verbrauchter Wh ab.
* Den kann man mit einer einfachen Photodiode abgreifen.
  Dafür gibt es auch fertige Lösungen, zum Beispiel mit [ESPHome](https://esphome.io/cookbook/power_meter.html) oder [OpenEnergyMonitor](https://docs.openenergymonitor.org/).


<!-- .slide: data-background-image="images/smartmeter-web.png" data-background-size="contain" -->
### Cloud <!-- .element class="hidden" -->

<!-- Note -->
Oder man macht es über die Cloud.
Das klappt natürlich nur, wenn der Versorger irgendein API zur Verfügung stellt, das man abgreifen kann.
Und dann braucht man dafür eine Home Assistant-Integration.

Von meinem Energieversorger (Wiener Netze) gibt es glücklicherweise beides:

* Smartmeter Web.
* Home Assistant-Integration [wnsm](https://github.com/DarwinsBuddy/WienerNetzeSmartmeter).

Screenshot: <https://smartmeter-web.wienernetze.at/>


<!-- .slide: data-background-image="images/energy-dashboard-202304.png" data-background-size="contain" -->
### Stromverbrauch April 2023 <!-- .element class="hidden" -->

<!-- Note -->
So sah der tageweise Stromverbrauch im April 2023 aus.
Noch ist da alles blau, so zeigt das Home Assistant Energy Dashboard nämlich Strom aus dem Netz an.

Gut zu erkennen: Heiztage (bis zu 50 kWh) und heizfreie Tage (15 kWh).


## Einzelne Geräte

<!-- Note -->
Wir wissen also, wieviel Strom wir komplett verbrauchen. Aber wie verteilt sich der?

Was jetzt kommt, sind ein paar konkrete Erwähnungen einzelner Produkte.
Das soll aber keine Werbung sein; man hat da ganz viele Möglichkeiten.

Wer sich hier für offene Firmware interessiert, der sollte sich Tasmota ansehen; unter <https://www.tasmota.info/hardware/> gibt es hier eine schöne Übersicht unterstützter Hardware.


### Smart Plugs

<!-- Note -->
Eine Möglichkeit das zu machen sind Smart Plugs, wie zum Beispiel ...


<!-- .slide: data-background-image="images/shelly-plug-s.png" data-background-size="contain" -->
#### Shelly Plug S <!-- .element class="hidden" -->

<!-- Note -->
* [Shelly Plug S](https://geizhals.at/shelly-wifi-smart-plug-s-v31046.html), bis 10A/2300W

oder auch ... 

Screenshot: <https://kb.shelly.cloud/knowledge-base/shelly-plug-s>


<!-- .slide: data-background-image="images/nous-a1t.png" data-background-size="contain" -->
#### Cloud <!-- .element class="hidden" -->

<!-- Note -->
* [Nous A1T](https://mediarath.de/en/products/4x-nous-a1t-16a-3680w-verbrauchsmessung-wifi-tasmota-optional-calibrated), bis 16A/3680W

(Tasmota vorgeflasht, nicht verwechseln mit Nous A1, die lässt sich *nicht* flashen!)

Geeignet für Waschmaschine, Trockner, Kühl-/Gefrierschrank, Geschirrspüler, Mikrowelle, evtl. auch Backofen (wenn's thermisch kein Problem ist).

Normalerweise nicht nur Messgerät, sondern auch Smart Switch (ein/ausschaltbar über API).

Screenshot: <https://nous.technology/product/a1t.html>


<!-- .slide: data-background-image="images/shelly-plus-1pm.png" data-background-size="contain" -->
### Smart Sockets <!-- .element class="hidden" -->

<!-- Note -->
Nächste Möglichkeit: Einbau eines Schalt/Messgeräts in eine Unterputz-Steckdose.

zB: [Shelly Plus 1PM](https://www.shelly.com/de-at/products/product-overview/shelly-plus-1-pm-2-pack/shelly-plus-1-pm), gibt aber jede Menge Möglichkeiten, viele mit Tasmota.

Im allgemeinen gleiche Eignung wie Smart Plugs, aber mehr Aufwand, da man die Steckdose einmal umrüsten muss.
(Ist aber eine Arbeit, die man ohne weiteres selbst machen könnte.)

Screenshot: https://www.shelly.com/de-at/products/product-overview/shelly-plus-1-pm-2-pack/shelly-plus-1-pm


<!-- .slide: data-background-image="images/shelly-pro-3em.png" data-background-size="contain" -->
### Durchsteckwandler-Zähler <!-- .element class="hidden" -->

<!-- Note -->
Nächste Eskalationsstufe: Strommessgeräte mit Durchsteckwandlern.

zB:

* [Shelly 3EM](https://www.shelly.com/de-at/products/product-overview/shelly-3em-1)
* [Shelly Pro 3EM - 400A](https://www.shelly.com/de-at/products/product-overview/shelly-pro-3-em-120-a-1/shelly-pro-3-em-400-a)

Auch geeignet für 400V-Geräte wie Herd oder Wärmepumpe.
Wird eingebaut in den Zähler- oder Anschlusskasten, ist damit eher ein Fall für den Elektriker.

Hat normalerweise *keine* Schaltmöglichkeit, ist also ein reines Messgerät.
(Wäre auch wenig sinnvoll: wenn ich mal meinen Herd oder meine Wärmepumpe ausschalten will, dann will ich da eher einen Schalter physisch betätigen.)

Screenshot: https://www.shelly.com/de-at/products/product-overview/shelly-pro-3-em-120-a-1/shelly-pro-3-em-400-a


<!-- .slide: data-background-image="images/siemens-5sl.png" data-background-size="contain" -->
### Leistungsschutzschalter mit Strommessung <!-- .element class="hidden" -->

<!-- Note -->
Die High-End-Option wären dann Sicherungsautomaten mit Strommessung.

zB: [Siemens 5SL](https://mall.industry.siemens.com/mall/de/WW/Catalog/Product/5SL6016-6MC)

Eher High-End Option.
Definitiv ein Auftrag für den Elektriker.

Screenshot: <https://mall.industry.siemens.com/mall/de/WW/Catalog/Product/5SL6016-6MC> 


## Was findet man raus?

<!-- Note -->
Mit den ganz gewöhnlichen Shelly-Smartplugs kann man einige interessante Dinge über das Verhalten einzelner Geräte rausfinden.


<!-- .slide: data-background-image="images/waschmaschine.png" data-background-size="contain" -->
### Waschmaschine <!-- .element class="hidden" -->

<!-- Note -->
* Waschmaschine: 2,1kW für 15 Minuten, dann Waschgang mit unter 100W, zum Schluss nochmal Schleudern bei 200W.
* Ziemlich egal wieviel Wäsche drin ist, weil die Heizenergie fürs Wasser immer gleich ist.


<!-- .slide: data-background-image="images/trockner.png" data-background-size="contain" -->
### Wäschetrockner <!-- .element class="hidden" -->

<!-- Note -->
* Ein Wärmepumpen-Wäschetrockner braucht viel weniger Leistung (800W, andere auch 600W), aber dafür durchgängig.
* Andererseits: wenn da weniger Wäsche drin ist, ist die Laufzeit auch kürzer.


<!-- .slide: data-background-image="images/geschirrspueler.png" data-background-size="contain" -->
### Geschirrspüler <!-- .element class="hidden" -->

<!-- Note -->
* Geschirrspüler: 2,3kW für 10 Minuten, dann Waschgang mit weit unter 100W, zum Schluss Trocknen mit 2,2kW.

Warum interessiert uns das? Das wird später nochmal interessant, wenn wir uns mit der PV-Anlage und dem Stromspeicher auseinandersetzen.
