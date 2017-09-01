> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

Dit overzicht van de [gesimuleerde apparaat Cloud uploaden voorbeeld] leest u hoe u [Azure IoT rand] [ lnk-sdk] IoT Hub apparaat-naar-cloud telemetrie verzenden van de gesimuleerde apparaten .

Dit overzicht omvat:

* **Architectuur**: architecturale informatie over de [gesimuleerde apparaat Cloud uploaden voorbeeld].
* **Ontwikkeling en uitvoering**: de stappen die nodig zijn om het voorbeeld te bouwen en uit te voeren.

## <a name="architecture"></a>Architectuur

De [gesimuleerde apparaat Cloud uploaden voorbeeld] laat zien hoe u een gateway die telemetrie van de gesimuleerde apparaten naar een iothub verzendt maken. Een apparaat mogelijk niet rechtstreeks verbinding maken met IoT Hub omdat het apparaat:

* Gebruikt geen een communicatieprotocol begrepen door de IoT Hub.
* Is geen smartcard te onthouden van de identiteit die is toegewezen door de IoT Hub.

Een IoT-Edge-gateway kan deze problemen op de volgende manieren oplossen:

* De gateway begrijpt het protocol dat wordt gebruikt door het apparaat ontvangt telemetrie voor apparaat-naar-cloud van het apparaat en stuurt deze berichten naar IoT Hub met behulp van een protocol begrepen door de IoT-hub.

* De gateway IoT Hub identiteiten wordt toegewezen aan apparaten en fungeert als een proxy wanneer een apparaat berichten naar IoT Hub verzendt.

Het volgende diagram toont de belangrijkste onderdelen van het voorbeeld, met inbegrip van de rand van de IoT-modules:

![][1]

De modules geven geen berichten rechtstreeks aan elkaar door. De modules publiceren berichten naar een interne broker, die zorgt voor de berichten op de andere modules met behulp van een mechanisme voor het abonnement. Zie voor meer informatie [aan de slag met Azure IoT rand][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Module voor het protocolopname

Dit is het startpunt voor de ontvangst van gegevens van apparaten, via de gateway en naar de cloud. In het voorbeeld wordt de module:

1. Gesimuleerde temperatuur gegevens maakt. Als u fysieke apparaten, leest de module gegevens van deze fysieke apparaten.
1. Hiermee maakt u een bericht.
1. De gesimuleerde temperatuur-gegevens in de inhoud van het bericht geplaatst.
1. Hiermee voegt u een eigenschap met een valse MAC-adres toe aan het bericht.
1. Maakt het bericht beschikbaar voor de volgende module in de keten.

De module wordt aangeroepen **Protocol X opname** in het vorige diagram heet **gesimuleerd apparaat** in de broncode.

### <a name="mac-lt-gt-iot-hub-id-module"></a>Module MAC &lt;-&gt; IoT Hub-id

Deze module wordt gescand voor berichten met een Mac-adres-eigenschap. In het voorbeeld wordt de module protocol opname toegevoegd de MAC-adres-eigenschap. Als de module vindt een dergelijke eigenschap, deze wordt toegevoegd een andere eigenschap met de sleutel van een IoT Hub-apparaat aan het bericht. De module wordt het bericht naar de volgende module beschikbaar in de keten.

De ontwikkelaar stelt een toewijzing tussen MAC-adressen en IoT Hub identiteiten in de gesimuleerde apparaten koppelen met IoT Hub apparaat-id's. De ontwikkelaar wordt de toewijzing handmatig toegevoegd als onderdeel van de moduleconfiguratie.

> [!NOTE]
> In dit voorbeeld wordt een MAC-adres gebruikt als een unieke apparaat-id en wordt deze gekoppeld aan de id van een IoT Hub-apparaat. U kunt echter uw eigen module schrijven die een andere unieke id gebruikt. Bijvoorbeeld, uw apparaten mogelijk zijn unieke serienummers of de telemetriegegevens kan de naam van een unieke embedded-apparaat bevatten.

### <a name="iot-hub-communication-module"></a>Module voor IoT Hub-communicatie

Deze module wordt berichten met een IoT Hub apparaat-sleuteleigenschap die is toegewezen door de vorige module. De module verzendt inhoud van het bericht naar IoT Hub met de HTTP-protocol. HTTP is een van de drie protocollen die door IoT Hub wordt begrepen.

Deze module wordt in plaats van een verbinding voor elk gesimuleerd apparaat te openen, één HTTP-verbinding geopend van de gateway met de iothub. De module multiplexes vervolgens verbindingen van de gesimuleerde apparaten via deze verbinding. Deze aanpak kunt één gateway om veel meer apparaten te verbinden.

## <a name="before-you-get-started"></a>Voordat u aan de slag gaat

Voordat u begint, moet u het volgende doen:

* [Een iothub maken] [ lnk-create-hub] in uw Azure-abonnement, moet u de naam van uw hub voor dit scenario. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* Twee apparaten toevoegen aan uw IoT-hub en noteer de id's en apparaten sleutels. U kunt de [apparaat explorer] [ lnk-device-explorer] of [iothub explorer] [ lnk-iothub-explorer] hulpprogramma uw apparaten toevoegen aan de IoT-hub die u in de vorige stap hebt gemaakt en de sleutels worden opgehaald.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[gesimuleerde apparaat Cloud uploaden voorbeeld]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md