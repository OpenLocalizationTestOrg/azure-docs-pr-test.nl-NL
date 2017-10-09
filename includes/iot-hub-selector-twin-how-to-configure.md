> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>Inleiding

In [aan de slag met IoT Hub apparaat horende][lnk-twin-tutorial], hebt u geleerd hoe tooset metagegevens voor de apparaten van uw oplossing terug eindigen met behulp van *labels*, voorwaarden apparaat vanuit een app apparaat rapporteren met behulp van *gerapporteerd eigenschappen*, en deze gegevens door middel van een SQL-achtige taal opvragen.

In deze zelfstudie leert u hoe toouse Hallo Hallo apparaat twin *gewenst eigenschappen* samen met *gerapporteerd eigenschappen*, tooremotely apparaat-apps configureren. Meer specifiek, deze zelfstudie laat zien hoe een apparaat-twin gerapporteerd en gewenste eigenschappen een configuratie met meerdere stappen van de apparaattoepassing van een inschakelen en bieden Hallo zichtbaarheid toohello back-end oplossing van Hallo status van deze bewerking op alle apparaten. U vindt meer informatie over het Hallo-rol van apparaatconfiguraties in [overzicht van Apparaatbeheer met IoT Hub][lnk-dm-overview].

Op een hoog niveau kunt apparaat horende Hallo oplossing voor back-end toospecify Hallo gewenste configuratie voor Hallo beheerde apparaten, door specifieke opdrachten te verzenden in plaats van. Dit apparaat Hallo verantwoordelijk instellen van de beste manier tooupdate Hallo configuratie ervan (zeer belangrijk in IoT-scenario's waarin specifieke apparaat voorwaarden invloed hebben op Hallo mogelijkheid tooimmediately uitvoeren door specifieke opdrachten), plaatst tijdens voortdurend reporting toohello back-end oplossing Hallo huidige status en potentiële fouten van Hallo updateproces kan controleren. Dit patroon is instrumentale toohello beheer van grote sets van apparaten, zoals Hallo oplossing voor back-end toohave volledig inzicht in de status van de configuratie van Hallo Hallo op alle apparaten kunnen.

> [!NOTE]
> In scenario's waarin apparaten worden beheerd op een nieuwe interactieve wijze (inschakelen voor een ventilator van een gebruiker beheerde app), kunt u overwegen [methoden directe][lnk-methods].
> 
> 

In deze zelfstudie update Hallo oplossing voor back-end wijzigingen Hallo telemetrie configuratie van een doelapparaat en, als gevolg van die Hallo apparaattoepassing een proces met meerdere stappen tooapply een configuratie volgt (bijvoorbeeld software-module opnieuw moet worden gestart, waarvoor deze zelfstudie simuleert met een eenvoudige vertraging).

Hallo back-end oplossing slaat Hallo configuratie in de gewenste eigenschappen in de volgende manieren Hallo Hallo apparaat twin:

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> Omdat configuraties kunnen complexe objecten, worden ze meestal toegewezen unieke id's (hashes of [GUID's][lnk-guid]) toosimplify hun vergelijkingen.
> 
> 

Hallo apparaattoepassing rapporteert de huidige configuratie gewenst Hallo eigenschap spiegelen **telemetryConfig** Hallo gerapporteerd eigenschappen:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Houd er rekening mee hoe Hallo gerapporteerd **telemetryConfig** heeft een extra eigenschap **status**, tooreport Hallo status van de update configuratieproces Hallo gebruikt.

Wanneer een nieuwe gewenste configuratie wordt ontvangen, rapporten Hallo apparaattoepassing een in behandeling configuratie door Hallo gegevens te wijzigen:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

Klik vervolgens op een later tijdstip rapporteert Hallo apparaattoepassing Hallo slagen of mislukken van deze bewerking door Hallo boven eigenschap bij te werken.
Houd er rekening mee hoe Hallo back-end oplossing kunnen op elk gewenst moment, tooquery Hallo status van de configuratieproces Hallo op alle Hallo-apparaten.

In deze handleiding ontdekt u hoe u:

* Maakt een gesimuleerd apparaat-app die configuratie-updates ontvangt van Hallo back-end oplossing en rapporten van meerdere updates als *eigenschappen gerapporteerd* op Hallo configuratie proces niet bijwerken.
* Maakt een back-end-app dat updates Hallo gewenste configuratie van een apparaat, en vervolgens query's Hallo update configuratieproces.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
