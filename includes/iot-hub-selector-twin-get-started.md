> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

Apparaatdubbels zijn JSON-documenten waarin statusinformatie van een apparaat (metagegevens, configuraties en voorwaarden) zijn opgeslagen. IoT Hub persistente een apparaat twin voor elk apparaat dat tooit verbindt.

Apparaat horende te gebruiken:

* Opslaan van metagegevens van apparaten uit de back-end van uw oplossing.
* Huidige statusinformatie zoals de beschikbare mogelijkheden en voorwaarden (bijvoorbeeld Hallo connectiviteit methode die wordt gebruikt) van uw app apparaat rapporteren.
* Hallo-status van langlopende werkstromen (zoals updates, firmware en configuratie) tussen een apparaat-app en een back-endserver voor apps worden gesynchroniseerd.
* De metagegevens van apparaten, de configuratie of de status opvragen.

> [!NOTE]
> Apparaat horende zijn ontworpen voor synchronisatie en voor het uitvoeren van query's apparaatconfiguraties en voorwaarden. Meer informatie over op wanneer toouse apparaat horende vindt u in [apparaat horende begrijpen][lnk-twins].

Apparaat horende worden opgeslagen in een IoT-hub en bevatten:

* *labels*, de metagegevens van de apparaten is alleen toegankelijk zijn voor Hallo back-end oplossing;
* *Eigenschappen gewenst*, JSON-objecten die kunnen worden gewijzigd door Hallo oplossing back-end en opslagtijd met Hallo apparaattoepassing; en
* *Eigenschappen gerapporteerd*, JSON-objecten kunnen worden gewijzigd door Hallo apparaattoepassing en gelezen door Hallo back-end oplossing. Labels en eigenschappen kunnen geen matrices bevatten, maar objecten kunnen worden genest.

![][img-twin]

Hallo back-end oplossing kan bovendien apparaat horende op basis van alle Hallo boven gegevens opvragen.
Raadpleeg te[horende apparaten begrijpen] [ lnk-twins] voor meer informatie over apparaat horende en toohello [IoT Hub-querytaal] [ lnk-query] verwijzing query's.

> [!NOTE]
> Op dit moment horende apparaten zijn alleen toegankelijk vanaf apparaten die verbinding tooIoT Hub maken met Hallo MQTT-protocol. Raadpleeg toohello [MQTT ondersteuning] [ lnk-devguide-mqtt] artikel voor instructies over het tooconvert bestaande apparaat app toouse MQTT.

In deze handleiding ontdekt u hoe u:

* Maakt een back-end-app die wordt toegevoegd *labels* tooa apparaat twin en een gesimuleerde apparaattoepassing die rapporteert de connectiviteit van de channel-als een *gerapporteerd eigenschap* op Hallo apparaat twin.
* Query uitvoeren op apparaten van uw back-end-app met behulp van filters op Hallo-labels en eigenschappen eerder hebt gemaakt.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md