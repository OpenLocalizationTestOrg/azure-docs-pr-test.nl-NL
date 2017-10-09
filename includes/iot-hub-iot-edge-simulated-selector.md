> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

In dit scenario Hallo [gesimuleerde apparaat Cloud uploaden voorbeeld] laat u zien hoe toouse [Azure IoT rand] [ lnk-sdk] toosend tooIoT Hub van gesimuleerde telemetrie voor apparaat-naar-cloud apparaten.

Dit overzicht omvat:

* **Architectuur**: architecturale informatie over Hallo [gesimuleerde apparaat Cloud uploaden voorbeeld].
* **Bouwen en uitvoeren van**: Hallo stappen vereist toobuild en Voer Hallo-voorbeeld.

## <a name="architecture"></a>Architectuur

Hallo [gesimuleerde apparaat Cloud uploaden voorbeeld] ziet u hoe een gateway die u telemetrie van verzendt toocreate gesimuleerde apparaten tooan IoT-hub. Een apparaat mogelijk niet kunnen tooconnect rechtstreeks tooIoT Hub omdat Hallo apparaat:

* Gebruikt geen een communicatieprotocol begrepen door de IoT Hub.
* Is niet genoeg smart tooremember Hallo identiteit toegewezen tooit door de IoT Hub.

Een IoT-Edge-gateway kan deze problemen in Hallo volgende manieren oplossen:

* Hallo gateway Hallo protocol dat wordt gebruikt door Hallo apparaat begrijpt, ontvangt telemetrie voor apparaat-naar-cloud van Hallo-apparaat en stuurt deze berichten tooIoT Hub met behulp van een protocol begrepen door de Hallo iothub.

* Hallo gateway IoT Hub identiteiten toodevices toegewezen en fungeert als een proxy wanneer een apparaat berichten tooIoT Hub verzendt.

Hallo volgende diagram ziet u Hallo hoofdonderdelen van Hallo voorbeeld, met inbegrip van IoT rand modules Hallo:

![][1]

Hallo-modules niet doorgegeven berichten rechtstreeks tooeach andere. Hallo-modules publiceren berichten interne broker tooan die Hallo berichten toohello biedt andere modules met behulp van een mechanisme voor het abonnement. Zie voor meer informatie [aan de slag met Azure IoT rand][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Module voor het protocolopname

Deze module is een startpunt voor de ontvangst van gegevens van apparaten, via de gateway hello en in de cloud Hallo Hallo. In de module Hallo Hallo voorbeeld:

1. Gesimuleerde temperatuur gegevens maakt. Als u fysieke apparaten gebruikt, leest Hallo module de gegevens van deze fysieke apparaten.
1. Hiermee maakt u een bericht.
1. Hallo gesimuleerde temperatuur gegevens in inhoud van het bericht Hallo geplaatst.
1. Voegt een eigenschap met een valse toohello bericht dat MAC-adres toe.
1. Hallo-bericht beschikbaar toohello volgende module maakt in de keten Hallo.

Hallo module met de naam **Protocol X opname** in Hallo vorige diagram heet **gesimuleerd apparaat** in Hallo broncode.

### <a name="mac-lt-gt-iot-hub-id-module"></a>Module MAC &lt;-&gt; IoT Hub-id

Deze module wordt gescand voor berichten met een Mac-adres-eigenschap. In voorbeeld Hallo toegevoegd Hallo protocol opname module Hallo MAC-adres-eigenschap. Als Hallo module vindt een dergelijke eigenschap, wordt een andere eigenschap met een IoT Hub apparaat sleutel toohello bericht toegevoegd. Hallo module maakt vervolgens Hallo-bericht beschikbaar toohello volgende module in de keten Hallo.

Hallo developer stelt u een toewijzing tussen MAC-adressen en IoT Hub identiteiten tooassociate Hallo gesimuleerde apparaten met IoT Hub apparaat-id's. Hallo-ontwikkelaar wordt Hallo toewijzing handmatig toegevoegd als onderdeel van de moduleconfiguratie Hallo.

> [!NOTE]
> In dit voorbeeld wordt een MAC-adres gebruikt als een unieke apparaat-id en wordt deze gekoppeld aan de id van een IoT Hub-apparaat. U kunt echter uw eigen module schrijven die een andere unieke id gebruikt. Bijvoorbeeld, uw apparaten mogelijk zijn unieke serienummers of Hallo telemetrische gegevens kan bevatten de naam van een unieke embedded-apparaat.

### <a name="iot-hub-communication-module"></a>Module voor IoT Hub-communicatie

Deze module wordt berichten met een IoT Hub apparaat-sleuteleigenschap die is toegewezen door de vorige module Hallo. Hallo module verzendt de inhoud tooIoT Hub met behulp van HTTP-protocol Hallo het Hallo-bericht. HTTP is een Hallo drie protocollen begrepen door de IoT Hub.

Deze module wordt in plaats van een verbinding voor elk gesimuleerd apparaat te openen, één HTTP-verbinding geopend uit Hallo gateway toohello iothub. Hallo module multiplexes vervolgens verbindingen van alle Hallo gesimuleerde apparaten via deze verbinding. Deze aanpak kunt een enkele gateway tooconnect veel meer apparaten.

## <a name="before-you-get-started"></a>Voordat u aan de slag gaat

Voordat u begint, moet u het volgende doen:

* [Een iothub maken] [ lnk-create-hub] in uw Azure-abonnement, moet u het Hallo-naam van uw hub toocomplete in dit scenario. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* Voeg twee apparaten tooyour IoT-hub en noteer de id's en apparaten sleutels. Kunt u Hallo [apparaat explorer] [ lnk-device-explorer] of [iothub explorer] [ lnk-iothub-explorer] tooadd uw apparaten toohello IoT-hub u hebt gemaakt in Hallo hulpprogramma vorige stap en de sleutels op te halen.

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