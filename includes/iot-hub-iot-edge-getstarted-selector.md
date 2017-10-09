> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

Dit artikel bevat een gedetailleerd overzicht van Hallo [Hallo wereld voorbeeldcode] [ lnk-helloworld-sample] tooillustrate Hallo fundamentele onderdelen van Hallo [Azure IoT rand] [ lnk-iot-edge] architectuur. Hallo voorbeeld maakt gebruik van hello Azure IoT rand toobuild een eenvoudige gateway die u een "Hallo wereld" tooa berichtbestand elke vijf seconden registreert.

Dit overzicht omvat:

* **Hallo wereld voorbeeldarchitectuur**: hierin wordt beschreven hoe [Azure IoT rand architectuur concepten] [ lnk-edge-concepts] toohello Hallo wereld-voorbeeld en hoe Hallo-onderdelen in elkaar passen toepassen.
* **Hoe toobuild voorbeeld Hallo**: Hallo stappen vereist toobuild Hallo voorbeeld.
* **Hoe toorun voorbeeld Hallo**: Hallo stappen vereist toorun Hallo voorbeeld. 
* **Typische uitvoer**: een voorbeeld van Hallo tooexpect uitvoer wanneer u Hallo voorbeeld uitvoert.
* **Codefragmenten**: een verzameling van code codefragmenten tooshow hoe Hallo Hallo wereld-voorbeeld implementeert sleutel rand IoT gateway-onderdelen.


## <a name="hello-world-sample-architecture"></a>Architectuur van het 'Hallo wereld'-voorbeeld
Hallo Hallo wereld-voorbeeld illustreert Hallo concepten beschreven in de vorige sectie Hallo. Hallo Hallo wereld-voorbeeld implementeert een IoT-Edge-gateway met een pijplijn die bestaat uit twee IoT Edge-modules:

* Hallo *Hallo wereld* module elke vijf seconden een bericht wordt gemaakt en wordt doorgegeven toohello berichtenlogboek module.
* Hallo *berichtenlogboek* module schrijfbewerkingen Hallo-berichten ontvangen tooa-bestand.

![Architectuur van 'Hallo wereld'-voorbeeld gebouwd met Azure IoT Edge][4]

Zoals beschreven in de vorige sectie hello, Hallo Hallo wereld module niet geeft-berichten rechtstreeks toohello berichtenlogboek module elke vijf seconden. Het publiceert in plaats daarvan elke vijf seconden een bericht toohello broker.

Hallo berichtenlogboek module Hallo-bericht ontvangt van Hallo broker en fungeert daarvan Hallo inhoud van Hallo-bericht tooa bestand schrijven.

Hallo berichtenlogboek module alleen berichten van Hallo broker verbruikt, nieuwe berichten toohello broker nooit wordt gepubliceerd.

![Hoe Hallo broker routeert berichten tussen de modules in Azure IoT rand][5]

Hallo bovenstaande afbeelding ziet u Hallo-architectuur van Hallo Hallo wereld-voorbeeld en relatieve paden Hallo toohello bronbestanden die andere gedeelten van Hallo voorbeeld in Hallo implementeren [opslagplaats][lnk-iot-edge]. Verken Hallo code in uw eigen of Hallo codefragmenten hieronder als richtlijn gebruiken.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md