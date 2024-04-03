# Automation mit Home Assistant

<!-- Note -->
Home Assistant ist eine Open-Source-Software zur Heimautomatisierung und Energieoptimierung.
Sie steht unter der Apache Software License und besteht aus einer Python-Codebase mit vielen (sehr vielen!) Integrationsmodulen für verschiedenste Dinge im und ums Haus.

Über das Home Assistant Energy Dashboard hab ich ja schon einiges gesagt, jetzt mag ich noch ein bisschen was zu den Integrationen sagen, die wir so verwenden.


<!-- .slide: data-background-image="images/heat-pump-dashboard.png" data-background-size="contain" -->
## Wärmepumpe <!-- .element class="hidden" -->

<!-- Note -->
Da ist einerseits mal die Integration der Wärmepumpe.

Praktischerweise unterstützt die [Modbus TCP](https://en.wikipedia.org/wiki/Modbus#Modbus_TCP) (allerdings muss man da lieb bitten, damit man diese Funktionalität auch aktiviert bekommt).

Wenn das mal aktiviert ist, dann ist die Home Assistant-Integration fast trivial ...


<!-- .slide: data-background-image="images/ha-modbus.png" data-background-size="contain" -->
## Modbus <!-- .element class="hidden" -->

<!-- Note -->
... denn dafür gibt es eine fertige Modbus-Integration.

Bei der Einbindung des Wechselrichters wird es schon etwas komplexer:


<!-- .slide: data-background-image="images/ha-growatt.png" data-background-size="contain" -->
## Growatt <!-- .element class="hidden" -->

<!-- Note -->
Integration `growatt_server`

Damit habe ich angefangen:

* Liefert alle möglichen Daten zum Wechselrichter und zum Stromspeicher. Über 30 Einzelwerte.
* Greift ein Cloud-basiertes Service meines Wechselrichter-Herstellers über ein Web-API ab.
* War nicht ganz so toll, weil API immer mal wieder instabil oder auch über Stunden oder Tage unerreichbar ist.
* War auch irgendwie ein bisschen doof: Daten gehen vom Wechselrichter um die Welt auf irgendeinen Server, und werden von dort von einem Raspberry Pi ausgewertet, der keine 10m vom Wechselrichter entfernt steht.
* Da musste also eine Alternative her:

Screenshot: <https://www.home-assistant.io/integrations/growatt_server/>


<!-- .slide: data-background-image="images/growatt-shine-wifi-s.png" data-background-size="contain" --> 
### Growatt Shine WiFi-S <!-- .element class="hidden" -->

<!-- Note -->
Das ist der Wifi-Stick ("Datenlogger") des Wechselrichters.
Der verarbeitet Daten, die vom Wechselrichter über Modbus/USB abgefragt werden, und lädt sie dann zum Cloud-API hoch.
Das ist aber ein ESP32-Ding, und damit kann man da auch alternative Firmware drauf kriegen.

Screenshot: https://growatt.tech/de/product/growatt-shine-wifi-s/


<!-- .slide: data-background-image="images/github-growatt-shine.png" data-background-size="contain" --> 
### Growatt Shine WiFi-S Firmware <!-- .element class="hidden" -->

<!-- Note -->
Damit ergibt sich die

* mögliche Alternative  1: [open source aftermarket Firmware für den Datenlogger](https://github.com/otti/Growatt_ShineWiFi-S/) (ESP32)

Von da gehen die aktuellen Zustandsdaten dann [direkt via MQTT in Home Assistant](https://github.com/otti/Growatt_ShineWiFi-S/blob/master/Doc/MQTT.md).

Screenshot: <https://github.com/otti/Growatt_ShineWiFi-S/>


<!-- .slide: data-background-image="images/grott.png" data-background-size="contain" -->
### Grott <!-- .element class="hidden" -->

<!-- Note -->
* Mögliche Alternative 2: [Grott](https://github.com/johanmeijer/grott), das ist mehr oder weniger ein Growatt-API-Proxy.
* Shine Wifi liefert Daten an Grott, Grott schickt sie dann sowohl an Home Assistant als auch (optional) an den Growatt-Server weiter.

Screenshot: <https://github.com/johanmeijer/grott/wiki/Rerouting-Growatt-Wifi-TCPIP-data-via-your-Grott-Server>


<!-- .slide: data-background-image="images/github-homeassistant-grott.png" data-background-size="contain" -->
### Home Assistant Grott <!-- .element class="hidden" -->

<!-- Note -->
* Dafür gibt's zwischenzeitlich auch schon eine fertige Home Assistant-Integration, und damit läuft das alles ganz großartig.
* Im Augenblick fahre ich Grott noch im Proxy-Modus, also Datenlogger zu Grott und von dort zu HomeAssistant (via MQTT) *und* in die Cloud, aber irgendwann werde ich den Cloud-Upload wohl ausschalten.

Screenshot: <https://github.com/muppet3000/homeassistant-grott>


<!-- .slide: data-background-image="images/ha-forecastsolar.png" data-background-size="contain" -->
## Forecast.Solar <!-- .element class="hidden" -->

<!-- Note -->
Integration `forecast_solar`

* Bezieht die Position, Richtung, und Dachneigung der Solarmodule sowie die Wettervorhersage in eine Schätzung der vermutlichen PV-Leistung im Tagesverlauf ein.
* Geht auch ins Energy Dashboard ein.

Screenshot: <https://www.home-assistant.io/integrations/forecast_solar/>


<!-- .slide: data-background-image="images/ha-shelly.png" data-background-size="contain" -->
## Shelly <!-- .element class="hidden" -->

<!-- Note -->
Integration `shelly`

* Liefert Verbrauchsdaten ins Energy Dashboard.
* Ist außerdem für Automation als Schalter ansteuerbar.
* Home Assistant-Integration macht auch Firmware-Updates.

Screenshot: <https://www.home-assistant.io/integrations/shelly/>


<!-- .slide: data-background-image="images/github-wnsm.png" data-background-size="contain" -->
## WienerNetzeSmartMeter <!-- .element class="hidden" -->

<!-- Note -->
Integration `wnsm`

* Liefert Verbrauchsdaten ins Energy Dashboard.
* Ist damit auch ein Vergleichswert zur Einspeisemenge, die der Wechselrichter meldet.

Screenshot: <https://github.com/DarwinsBuddy/WienerNetzeSmartmeter>


## Home Assistant Automation, Anwendungsbeispiel <!-- .element class="hidden" -->

"Schalte den Geschirrspüler und die Waschmaschine ein, sobald wir ausreichend Solarstrom produzieren.

Aber nicht beide Geräte gleichzeitig!"

<!-- Note -->
All das zusammen kann man jetzt für alle möglichen Automationslösungen verwenden.

Davon greife ich jetzt einfach mal eine zufällig heraus:

* Wir wissen, dass wir gern Strom im Moment der Produktion verbrauchen wollen.
* Eine PV-Leistung von 2,3kW erzielen wir normalerweise irgendwann am frühen bis mittleren Vormittag.
* Damit können wir, wie wir wissen, die Spitze der Waschmaschinen- und Geschirrspüler-Leistungsaufnahme abdecken.
* Und wir wissen, dass diese Spitze für höchstens 10-15 Minuten erreicht wird.

Also: wir können diese beiden Geräte einfach gestaffelt einschalten, sobald diese PV-Produktionsleistung erreicht ist. 


<!-- .slide: data-background-image="images/ha-trigger-on-pv.png" data-background-size="contain" -->
## Home Assistant Automation, Anwendungsbeispiel (Code) <!-- .element class="hidden" -->

<!-- Note -->
So sieht das im Home Assistant-UI aus, und das ist die so erzeugte YAML-Konfiguration:

```yaml
alias: Turn on dishwasher
description: Turn on dishwasher when solar production is above threshold
trigger:
  - platform: numeric_state
    entity_id: sensor.actual_power_production_now_aggregate
    above: 2300
condition:
  - condition: state
    entity_id: switch.shellyplug_s_88888888888f
    state: "off"
action:
  - delay: 00:{{ range(1, 16)|random }}:00
  - type: turn_on
    device_id: 7fb1d95e1a79476da85b359860b3a4b8
    entity_id: switch.shellyplug_s_88888888888f
    domain: switch
mode: single
```
