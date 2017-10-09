> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

Azure IoT Hub is een volledig beheerde service waarmee betrouwbare en veilige tweerichtingscommunicatie tussen miljoenen apparaten en een oplossing voor back-end. Vorige zelfstudies ([aan de slag met IoT Hub] en [Cloud naar apparaat verzenden met IoT Hub]) illustreren Hallo apparaat-naar-cloud- en cloud-naar-apparaat messaging basisfunctionaliteit van IoT-Hub. IoT Hub biedt u eveneens de mogelijkheid tooinvoke niet duurzame methoden op apparaten uit de cloud Hallo Hallo. Directe methoden vertegenwoordigen een request-reply interactie met een apparaat vergelijkbare tooan HTTP aanroepen in dat ze slagen of mislukken onmiddellijk (na een door de gebruiker opgegeven time) toolet Hallo gebruiker Hallo status van Hallo oproep kennen. [Een directe methode aangeroepen voor een apparaat] [ lnk-devguide-methods] worden direct methoden in meer detail beschreven en biedt hulp bij wanneer toouse directe methoden in plaats van cloud naar apparaat-berichten of gewenste eigenschappen.

In deze handleiding ontdekt u hoe u:

* Gebruik Hallo toocreate met Azure portal een IoT-hub en een apparaat-id maakt in uw IoT-hub.
* Een gesimuleerd apparaat-app met een directe methode die kan worden aangeroepen door Hallo cloud maken.
* Een consoletoepassing maken die een directe methode wordt aangeroepen in Hallo gesimuleerde apparaattoepassing via uw IoT-hub.

> [!NOTE]
> Op dit moment rechtstreekse methoden worden alleen ondersteund op apparaten die verbinding maken met behulp van tooIoT Hub Hallo MQTT-protocol. Raadpleeg toohello [MQTT ondersteuning] [ lnk-devguide-mqtt] artikel voor instructies over het tooconvert bestaande apparaat app toouse MQTT.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[Cloud naar apparaat verzenden met IoT Hub]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[aan de slag met IoT Hub]: ../articles/iot-hub/iot-hub-node-node-getstarted.md