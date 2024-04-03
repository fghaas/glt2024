<!-- .slide: data-timing="1" --> 
# Fragen <!-- .element class="hidden" -->

* * *

<!-- Note -->
Es folgen Backup-Slides für zu erwartende Fragen.


<!-- .slide: data-timing="1" --> 
## Tarife <!-- .element class="hidden" -->
Wie sieht das mit dem Einspeisetarif aus?

Ist das nicht total unfair?

<!-- Note -->
In Österreich gibt es keine nationale Saldierungsregelung ("Einspeisen dreht Stromzähler zurück") wie in den Niederlanden, es ist also nicht garantiert, dass der Abnahme- gleich dem Einspeisepreis ist.

In Wien allerdings passt Wien Energie *beide* Preise zweimal jährlich an.

Wir haben ab Ende August um €0,29/kWh eingespeist, als der Abnahmestrompreis noch bei €0,28/kWh lag.
Mittlerweile stehen wir bei €0,14/kWh und €0,13/kWh.

Das kann aber in anderen Bundesländern und bei anderen Anbietern anders sein.


<!-- .slide: data-timing="1" --> 
## Monoblock <!-- .element class="hidden" -->
Warum eine Monoblock-Wärmepumpe?

Sind die nicht laut und ineffizient?

<!-- Note -->
Geräusch: dass Monoblock-Wärmepumpen sehr laut sind, ist so allgemein nicht zu sagen.
Unsere hat 38 dB(A) in 1m Abstand, das entspricht etwa Blätterrauschen im Baum — und bei uns steht tatsächlich ein Laubbaum neben der Wärmepumpe, der sie bei leichtem Wind schon übertönt.
Auch Regengeräusch ist lauter als die Wärmepumpe.

Das Geräusch ist auch sehr gleichmäßig und niedrigfrequent (etwa so wie rosa Rauschen).

Effizienz: Monoblock-Wärmepumpen können (weil das gesamte Kühlmittel im Freien zirkuliert) brennbare Kühlmittel verwenden, die — nach Aussage unseres Installateurs — effizienter sind als die nicht-brennbaren, die in Split-Geräten eingesetzt werden dürfen.


<!-- .slide: data-timing="1" --> 
## Radiatoren <!-- .element class="hidden" -->

Was habt ihr mit den Radiatoren gemacht?

<!-- Note -->
Die sind geblieben.
Wiederum nach Aussage unseres Installateurs braucht es lediglich einen Temperaturhub von 5K, um einen Heizeffekt zu erzielen.

Also: hat ein Raum 19°C und will ich ihn auf 20°C erwärmen, dann brauche ich dafür eine Oberflächentemperatur von 25°C am Radiator.
Alles was darüber liegt, macht die Erwärmung nur schneller.

Also: mit derselben Vorlauftemperatur von ca. 33°C (ohne Nachtabsenkung) in Fußboden- und Radiatorenheizung, kein Problem.


<!-- .slide: data-timing="1" --> 
## Kühlung <!-- .element class="hidden" -->

Wärmepumpenheizung als Kühlung?

Wie funktioniert das?

<!-- Note -->
Einfach mit Wasser mit ca. 18°C in Fußbodenheizung und Radiatoren.
Sehr praktisch, weil man braucht die Kühlung fast nur an Tagen, wo es auch sonnig ist — und dann ist Strom im Überfluss aus der PV-Anlage da.


<!-- .slide: data-timing="1" --> 
## Förderungen <!-- .element class="hidden" -->

Was ist mit Genehmigungen, Anzeigen, Förderungen?

<!-- Note -->
* Genehmigung: in Niederösterreich ist eine PV-Anlage *auf* dem *eigenen* Haus nicht genehmigungspflichtig, außer das Haus befindet sich in einer Ortsbild-Schutzzone.
  Das ist aber von Bundesland zu Bundesland verschieden.
* Anzeigen: eine Fertigstellungsanzeige ist in NÖ ebenfalls nicht behördlich erforderlich, allerdings braucht sie der Netzbetreiber für den Netznutzungs- und Energieliefervertrag, und die Förderinstitutionen.
* Förderungen: sind kompliziert!


<!-- .slide: data-timing="1" -->
## Home Assistant <!-- .element class="hidden" -->

Wie betreibst du Home Assistant?

<!-- Note -->
Genau so wie auch Nextcloud, Grocy, und anderes Container-Zeug.

* Raspberry Pi 4 mit Ubuntu Jammy
* Rootless Podman mit `podman-compose`
* Offizielles [Docker-Image  für Home Assistant](https://hub.docker.com/r/homeassistant/home-assistant)
* `loginctl --enable-linger homeassistant`
* `systemctl --user start podman-compose`


<!-- .slide: data-timing="1" -->
## Home Assistant docker-compose.yaml <!-- .element class="hidden" -->

```yaml
version: 3
services:
  homeassistant:
    container_name: homeassistant
    image: "ghcr.io/home-assistant/home-assistant:2024.3.1"
    volumes:
      - /home/homeassistant/.config/homeassistant:/config
      - /etc/localtime:/etc/localtime:ro
      - /run/dbus:/run/dbus:ro
    ports:
      - "8123:8123"
    restart: always
    environment : {}
```


<!-- .slide: data-timing="1" -->
## Home Assistant systemd unit <!-- .element class="hidden" -->

```ini
[Unit]
Description=Podman via podman-compose
Wants=network-online.target
After=network-online.target
RequiresMountsFor=%t/containers

[Service]
Environment=PODMAN_SYSTEMD_UNIT=%n
Environment=PODMAN_USERNS=keep-id
Restart=always
TimeoutStartSec=60
TimeoutStopSec=60
ExecStart=/usr/bin/podman-compose up --remove-orphans
ExecStop=/usr/bin/podman-compose stop
Type=simple
WorkingDirectory=%h

[Install]
WantedBy=default.target
```

<https://xahteiwi.eu/resources/hints-and-kinks/rootless-podman-docker-compose/>
