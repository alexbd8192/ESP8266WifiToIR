But:
Créer une manette IR controllé via Wifi à partir de Home Assistant.

Materiel:
- ESP8266 (Parait que ESP32 est mieux car le clock serait plsu précis..)
- Fil micro USB
- Transfo USB 1A
- Transistor (J'ai utilise un 2N3904 mais dautres peuvent faire l'affaire)
- IR Emitter (de Control4 dans mon cas...)

Protection du circuit:
- Puisque le transistor peux laisser passer un courant de 200ma, jai ajouté une diode de 27ohm pour le limiter a 59ma en supposant que la led consomme environ 1.7v afin de protéger le circuit. Cette LED en partculier blink rouge en plus de IR donc j'ai choisis une valeur de 1.7v, ce qui est plus haut que le 1.2v du spectre infrarouge seulement
Plus la valeur de resistance est haute, moin le IR capte loins.
Je me suis fié sur un post reddit pour déterminer la bonne valeur:

	They typically have something like 10-50 ohms in series with one or two parallel LEDs and a driver transistor or MOSFET.

	Assuming a 2.5-3V battery voltage (2 AA or AAA) and a 1.2V LED voltage that's maybe 20 to 200mA.

	I had a remote that I extended the range on (for a bedroom remote where the IR light had to bounce to get to the set-top box at the back of the lift), and I 	     did it by replacing the LED with a more efficient type rather than by jacking up the LED current.

	https://electronics.stackexchange.com/questions/432396/how-much-current-is-usually-used-with-ir-transmitting-leds-in-remote-controls
	
La résistance à été ajouté entre le l'émetteur du transistor et le ground.
Calculateur de résistance: https://www.digikey.ca/en/resources/conversion-calculators/conversion-calculator-led-series-resistor
Quelquechose pour apprendre les codes IR, dans mon cas j<ai utilisé un processeur Control4 mais possible de le faire avec un ESP8266 et un IR receiver.

Inspiré de ce projet:
https://www.instructables.com/Universal-Remote-Using-ESP8266Wifi-Controlled/

Logiciel:
- Esphome (soit docker ou dans les addons HA)
- Home Assistant
- Logiciel pour convertir les signaux IR (au besoin):
- http://www.harctoolbox.org/downloads/index.html#Current+software

Si besoin d'ajuster le format des signaux IR dans ESPhome:
https://esphome.io/components/remote_transmitter.html

Remarque:
attention de mettre le bon domaine local pour que esphome retrouve le module sur le réseau, dans mon cas local.lan

Une fois ajouté a Home Assistant, il faut ajouter le module et la clef d'encryption.
Une fois cela fait, HA détecte tout les changement automatiquement.
