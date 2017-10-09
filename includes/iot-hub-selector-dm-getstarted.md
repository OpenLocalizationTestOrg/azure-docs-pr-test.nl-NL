> [!div class="op_single_selector"]
> * [Apparaat: Node.js-Service: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Apparaat: Node.js-Service: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Apparaat: Java-Service: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Back-end apps kunnen gebruiken Azure IoT Hub primitieven, zoals [apparaat twin] [ lnk-devtwin] en [methoden directe][lnk-c2dmethod], tooremotely starten en te controleren Device management acties op apparaten. Deze zelfstudie leert u hoe een back-end-app en een apparaat-app kunnen samenwerken tooinitiate en controleren van externe apparaten opnieuw worden opgestart met IoT Hub.

Een directe methode tooinitiate apparaatacties (zoals het opnieuw opstarten, Fabrieksinstellingen terugzetten en firmware-update) van een back-end-app in de cloud Hallo gebruiken. Hallo-apparaat is verantwoordelijk voor:

* Verwerking Hallo methode aanvraag die uit IoT Hub zijn verzonden.
* Hallo overeenkomstige apparaatspecifieke actie op Hallo-apparaat wordt gestart.
* Van statusupdates via bieden *gerapporteerd eigenschappen* tooIoT Hub.

U kunt een back-endserver voor apps in Hallo cloud toorun apparaat twin query's tooreport op Hallo voortgang van de acties voor uw apparaat.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
