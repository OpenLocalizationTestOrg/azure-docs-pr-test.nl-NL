---
title: aaaGet de slag met Azure IoT Hub (Python) | Microsoft Docs
description: Meer informatie over hoe toosend apparaat-naar-cloud tooAzure IoT Hub met IoT SDK's voor Python berichten. Gesimuleerde apparaat en service-apps tooregister uw apparaat maken en berichten uit iothub berichten verzenden.
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Verbinding maken met uw gesimuleerde apparaat tooyour iothub met behulp van Python
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u twee Python-apps:

* **CreateDeviceIdentity.py**, die een apparaat-id maakt en gekoppelde beveiliging sleutel tooconnect app op uw gesimuleerde apparaat.
* **SimulatedDevice.py**die tooyour IoT-hub maakt verbinding met apparaat-id Hallo eerder hebt gemaakt en periodiek verzendt een bericht met Hallo MQTT-protocol.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.
> 
> 

toocomplete in deze zelfstudie, moet u hello te volgen:

* [Python 2.x of 3.x][lnk-python-download]. Zorg ervoor toouse Hallo 32-bits of 64-bits installatie zoals vereist door uw instellingen. Wanneer u wordt gevraagd tijdens de installatie van Hallo, moet u ervoor tooadd Python tooyour platform-specifieke omgevingsvariabele. Als u Python gebruikt 2.x, moet u mogelijk te[installeren of upgraden *pip*, hello Python pakket-beheersysteem][lnk-install-pip].
* Als u van het Windows-besturingssysteem, klikt u vervolgens gebruikmaakt [herdistribueerbaar pakket Visual C++] [ lnk-visual-c-redist] tooallow Hallo gebruik van native DLLs van Python.
* [Node.js 4.0 of hoger][lnk-node-download]. Zorg ervoor toouse Hallo 32-bits of 64-bits installatie zoals vereist door uw instellingen. Dit is nodig tooinstall hello [IoT Hub Explorer hulpprogramma][lnk-iot-hub-explorer].
* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.

> [!NOTE]
> Hallo *pip* pakketten voor `azure-iothub-service-client` en `azure-iothub-device-client` zijn momenteel alleen beschikbaar voor Windows-besturingssysteem. Raadpleeg voor Linux/Mac OS toohello Linux- en Mac OS-specifieke secties op Hallo [uw ontwikkelingsomgeving voorbereiden voor Python] [ lnk-python-devbox] plaatsen.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

U hebt nu uw IoT-hub gemaakt. Hallo IoT Hub-hostnaam en verbindingsreeks IoT Hub Hallo in Hallo rest van deze handleiding gebruiken.

> [!NOTE]
> U kunt ook gemakkelijk maken uw IoT-hub op een opdrachtregel met Hallo Python of Node.js op basis van Azure CLI. Hallo artikel [maken van een iothub met hello Azure CLI 2.0] [ lnk-azure-cli-hub] ziet u dus snelle stappen toodo Hallo. 
> 

## <a name="create-a-device-identity"></a>Een apparaat-id maken
Deze sectie vindt Hallo stappen toocreate een consoletoepassing Python, die een apparaat-id in Hallo identiteitenregister van uw iothub maakt. Een apparaat kan alleen verbinding maken met tooIoT Hub als er een vermelding in het identiteitenregister Hallo. Zie voor meer informatie, Hallo **Identiteitsregister** sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity]. Wanneer u deze consoletoepassing uitvoert, wordt een unieke apparaat-ID gegenereerd en sleutel waarmee het apparaat tooidentify zelf kunt wanneer het apparaat-naar-cloud verzendt berichten tooIoT Hub.

1. Open een opdrachtprompt en installeer Hallo **Azure IoT Hub Service SDK voor Python**. Hallo-opdrachtprompt sluiten nadat u Hallo SDK installeert.

    ```
    pip install azure-iothub-service-client
    ```

2. Maak een Python-bestand genaamd **CreateDeviceIdentity.py**. Openen in [een Python-editor/IDE van uw keuze][lnk-python-ide-list], bijvoorbeeld Hallo standaard [inactief][lnk-idle].

3. Hallo volgende codemodules tooimport Hallo vereist uit Hallo service SDK toevoegen:

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Toevoegen van Hallo code te volgen en vervangt Hallo tijdelijke aanduiding voor `[IoTHub Connection String]` met Hallo-verbindingsreeks voor Hallo iothub die u hebt gemaakt in de vorige sectie Hallo. U kunt elke willekeurige naam gebruiken als Hallo `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Voeg Hallo volgende functie tooprint aantal Hallo apparaatgegevens.

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. Hallo volgende functie toocreate Hallo apparaat id voor gebruik met Hallo register Manager toevoegen. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. Ten slotte de belangrijkste functie Hallo bijvoegen en sla Hallo-bestand.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. Voer op de opdrachtprompt Hallo Hallo **CreateDeviceIdentity.py** als volgt:

    ```python
    python CreateDeviceIdentity.py
    ```
6. U ziet Hallo gesimuleerd apparaat ophalen gemaakt. Noteer Hallo **deviceId** en Hallo **primaryKey** van dit apparaat. U moet deze waarden later bij het maken van een toepassing die tooIoT Hub als apparaat verbinding maakt.

    ![Apparaat maken voltooid][1]

> [!NOTE]
> Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub. Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld. Als uw toepassing toostore andere apparaatspecifieke metagegevens moet, moet deze een toepassingsspecifieke opslagmethode gebruiken. Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
Deze sectie vindt Hallo stappen toocreate een consoletoepassing Python, die een apparaat simuleert en apparaat-naar-cloudberichten tooyour iothub verzendt.

1. Open een nieuw opdrachtpromptvenster en als volgt hello Azure IoT Hub apparaat-SDK voor Python installeren. Sluit de opdrachtprompt Hallo na de installatie van de Hallo.

    ```
    pip install azure-iothub-device-client
    ```
2. Maak een bestand genaamd **SimulatedDevice.py**. Open het bestand in een Python-editor/IDE naar keuze, bijvoorbeeld IDLE.

3. Hallo volgende codemodules tooimport Hallo vereist uit Hallo apparaat-SDK toevoegen.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Hallo-volgende code en vervang Hallo tijdelijke aanduiding voor toevoegen `[IoTHub Device Connection String]` met Hallo-verbindingsreeks voor uw apparaat. verbindingsreeks Hallo-apparaat bevindt zich doorgaans in Hallo-indeling van `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Gebruik Hallo **deviceId** en **primaryKey** Hallo apparaat dat u hebt gemaakt in de vorige sectie tooreplace-Hallo Hallo `<deviceId>` en `<primaryKey>` respectievelijk. Vervang `<hostName>` door de hostnaam van uw IoT Hub, meestal ingedeeld als `<IoT hub name>.azure-devices.net`.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. Hallo na code toodefine een bevestiging verzenden retouraanroep toevoegen. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. Hallo na code tooinitialize Hallo device-client toevoegen.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Hallo volgende tooformat werken en een bericht verzenden vanuit uw gesimuleerde apparaat tooyour IoT-hub toevoegen.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. Ten slotte de belangrijkste functie Hallo toevoegen. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Opslaan en sluiten Hallo **SimulatedDevice.py** bestand. U bent nu klaar toorun deze app.

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Berichten ontvangen van uw gesimuleerde apparaat
tooreceive telemetrieberichten vanaf uw apparaat, moet u toouse een [Event Hubs][lnk-event-hubs-overview]-compatibel eindpunt die worden weergegeven door Hallo IoT-Hub Hallo apparaat-naar-cloud-berichten kan lezen. Lees Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie voor meer informatie over hoe tooprocess van van Event Hubs voor uw IoT-hub Event Hub-compatibele eindpunt berichten. Event Hubs biedt geen ondersteuning voor telemetrie in Python nog, zodat u kunt maken een [Node.js](iot-hub-node-node-getstarted.md#D2C_node) of een [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) op basis van Event Hubs console app tooread hello apparaat-naar-cloud-berichten uit IoT Hub. Deze zelfstudie laat zien hoe u kunt Hallo [IoT Hub Explorer hulpprogramma] [ lnk-iot-hub-explorer] tooread deze apparaatberichten.

1. Open een opdrachtprompt en Hallo IoT Hub Explorer installeren. 

    ```
    npm install -g iothub-explorer
    ```

2. Hallo volgende opdracht op Hallo opdrachtprompt uitvoert, toobegin bewaking apparaat-naar-cloud-berichten van uw apparaat Hallo. Gebruik van uw IoT-hub-verbindingsreeks in Hallo tijdelijke aanduiding voor na `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Open een nieuw opdrachtprompt en navigeer toohello map waarin zich Hallo **SimulatedDevice.py** bestand.

4. Voer Hallo **SimulatedDevice.py** bestand, dat periodiek telemetrie gegevens tooyour iothub verzendt. 
   
    ```
    python SimulatedDevice.py
    ```
5. Apparaat-berichten op Hallo opdrachtprompt Hallo IoT Hub Explorer uitvoeren vanaf de vorige sectie Hallo Hallo zien. 

    ![Apparaat-naar-cloud-berichten met Python][2]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app toosend apparaat-naar-cloudberichten toohello iothub gebruikt. U waargenomen Hallo-berichten dat is ontvangen door de IoT-hub met behulp van Hallo IoT Hub Explorer hulpprogramma Hallo Hallo. 

tooexplore hello Python SDK voor het gebruik van Azure IoT Hub in de diepte, gaat u naar [deze Git Hub-opslagplaats][lnk-python-github]. tooreview hello berichtenmogelijkheden Hallo Azure IoT Hub Service SDK voor Python, die u kunt downloaden en uitvoeren [iothub_messaging_sample.py][lnk-messaging-sample]. Voor apparaat side simulatie met hello Azure IoT Hub apparaat-SDK voor Python, u kunt downloaden en uitvoeren van Hallo [iothub_client_sample.py][lnk-client-sample].

toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:

* [Verbinding maken met uw apparaat][lnk-connect-device]
* [Aan de slag met apparaatbeheer][lnk-device-management]
* [Aan de slag met Azure IoT Edge][lnk-iot-edge]

toolearn hoe tooextend uw IoT-oplossing en proces apparaat-naar-cloud-berichten op grote schaal, zien Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
