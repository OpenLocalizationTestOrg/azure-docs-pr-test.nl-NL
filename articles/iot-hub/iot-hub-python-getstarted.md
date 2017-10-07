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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="a81d5-104">Verbinding maken met uw gesimuleerde apparaat tooyour iothub met behulp van Python</span><span class="sxs-lookup"><span data-stu-id="a81d5-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="a81d5-105">Aan het einde van de Hallo van deze zelfstudie hebt u twee Python-apps:</span><span class="sxs-lookup"><span data-stu-id="a81d5-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="a81d5-106">**CreateDeviceIdentity.py**, die een apparaat-id maakt en gekoppelde beveiliging sleutel tooconnect app op uw gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="a81d5-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="a81d5-107">**SimulatedDevice.py**die tooyour IoT-hub maakt verbinding met apparaat-id Hallo eerder hebt gemaakt en periodiek verzendt een bericht met Hallo MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="a81d5-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="a81d5-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="a81d5-109">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="a81d5-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a81d5-110">[Python 2.x of 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="a81d5-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="a81d5-111">Zorg ervoor toouse Hallo 32-bits of 64-bits installatie zoals vereist door uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="a81d5-112">Wanneer u wordt gevraagd tijdens de installatie van Hallo, moet u ervoor tooadd Python tooyour platform-specifieke omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="a81d5-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="a81d5-113">Als u Python gebruikt 2.x, moet u mogelijk te[installeren of upgraden *pip*, hello Python pakket-beheersysteem][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="a81d5-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="a81d5-114">Als u van het Windows-besturingssysteem, klikt u vervolgens gebruikmaakt [herdistribueerbaar pakket Visual C++] [ lnk-visual-c-redist] tooallow Hallo gebruik van native DLLs van Python.</span><span class="sxs-lookup"><span data-stu-id="a81d5-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="a81d5-115">[Node.js 4.0 of hoger][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="a81d5-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="a81d5-116">Zorg ervoor toouse Hallo 32-bits of 64-bits installatie zoals vereist door uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="a81d5-117">Dit is nodig tooinstall hello [IoT Hub Explorer hulpprogramma][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="a81d5-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="a81d5-118">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a81d5-118">An active Azure account.</span></span> <span data-ttu-id="a81d5-119">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="a81d5-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="a81d5-120">Hallo *pip* pakketten voor `azure-iothub-service-client` en `azure-iothub-device-client` zijn momenteel alleen beschikbaar voor Windows-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="a81d5-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="a81d5-121">Raadpleeg voor Linux/Mac OS toohello Linux- en Mac OS-specifieke secties op Hallo [uw ontwikkelingsomgeving voorbereiden voor Python] [ lnk-python-devbox] plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="a81d5-122">U hebt nu uw IoT-hub gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-122">You have now created your IoT hub.</span></span> <span data-ttu-id="a81d5-123">Hallo IoT Hub-hostnaam en verbindingsreeks IoT Hub Hallo in Hallo rest van deze handleiding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a81d5-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="a81d5-124">U kunt ook gemakkelijk maken uw IoT-hub op een opdrachtregel met Hallo Python of Node.js op basis van Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a81d5-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="a81d5-125">Hallo artikel [maken van een iothub met hello Azure CLI 2.0] [ lnk-azure-cli-hub] ziet u dus snelle stappen toodo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a81d5-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="a81d5-126">Een apparaat-id maken</span><span class="sxs-lookup"><span data-stu-id="a81d5-126">Create a device identity</span></span>
<span data-ttu-id="a81d5-127">Deze sectie vindt Hallo stappen toocreate een consoletoepassing Python, die een apparaat-id in Hallo identiteitenregister van uw iothub maakt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="a81d5-128">Een apparaat kan alleen verbinding maken met tooIoT Hub als er een vermelding in het identiteitenregister Hallo.</span><span class="sxs-lookup"><span data-stu-id="a81d5-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="a81d5-129">Zie voor meer informatie, Hallo **Identiteitsregister** sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="a81d5-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="a81d5-130">Wanneer u deze consoletoepassing uitvoert, wordt een unieke apparaat-ID gegenereerd en sleutel waarmee het apparaat tooidentify zelf kunt wanneer het apparaat-naar-cloud verzendt berichten tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a81d5-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="a81d5-131">Open een opdrachtprompt en installeer Hallo **Azure IoT Hub Service SDK voor Python**.</span><span class="sxs-lookup"><span data-stu-id="a81d5-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="a81d5-132">Hallo-opdrachtprompt sluiten nadat u Hallo SDK installeert.</span><span class="sxs-lookup"><span data-stu-id="a81d5-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="a81d5-133">Maak een Python-bestand genaamd **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="a81d5-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="a81d5-134">Openen in [een Python-editor/IDE van uw keuze][lnk-python-ide-list], bijvoorbeeld Hallo standaard [inactief][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="a81d5-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="a81d5-135">Hallo volgende codemodules tooimport Hallo vereist uit Hallo service SDK toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a81d5-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="a81d5-136">Toevoegen van Hallo code te volgen en vervangt Hallo tijdelijke aanduiding voor `[IoTHub Connection String]` met Hallo-verbindingsreeks voor Hallo iothub die u hebt gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a81d5-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="a81d5-137">U kunt elke willekeurige naam gebruiken als Hallo `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="a81d5-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="a81d5-138">Voeg Hallo volgende functie tooprint aantal Hallo apparaatgegevens.</span><span class="sxs-lookup"><span data-stu-id="a81d5-138">Add hello following function tooprint some of hello device information.</span></span>

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
3. <span data-ttu-id="a81d5-139">Hallo volgende functie toocreate Hallo apparaat id voor gebruik met Hallo register Manager toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

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
4. <span data-ttu-id="a81d5-140">Ten slotte de belangrijkste functie Hallo bijvoegen en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="a81d5-140">Finally, add hello main function as follows and save hello file.</span></span>

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
5. <span data-ttu-id="a81d5-141">Voer op de opdrachtprompt Hallo Hallo **CreateDeviceIdentity.py** als volgt:</span><span class="sxs-lookup"><span data-stu-id="a81d5-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="a81d5-142">U ziet Hallo gesimuleerd apparaat ophalen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="a81d5-143">Noteer Hallo **deviceId** en Hallo **primaryKey** van dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="a81d5-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="a81d5-144">U moet deze waarden later bij het maken van een toepassing die tooIoT Hub als apparaat verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![Apparaat maken voltooid][1]

> [!NOTE]
> <span data-ttu-id="a81d5-146">Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a81d5-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="a81d5-147">Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a81d5-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="a81d5-148">Als uw toepassing toostore andere apparaatspecifieke metagegevens moet, moet deze een toepassingsspecifieke opslagmethode gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a81d5-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="a81d5-149">Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="a81d5-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a81d5-150">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="a81d5-150">Create a simulated device app</span></span>
<span data-ttu-id="a81d5-151">Deze sectie vindt Hallo stappen toocreate een consoletoepassing Python, die een apparaat simuleert en apparaat-naar-cloudberichten tooyour iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="a81d5-152">Open een nieuw opdrachtpromptvenster en als volgt hello Azure IoT Hub apparaat-SDK voor Python installeren.</span><span class="sxs-lookup"><span data-stu-id="a81d5-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="a81d5-153">Sluit de opdrachtprompt Hallo na de installatie van de Hallo.</span><span class="sxs-lookup"><span data-stu-id="a81d5-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="a81d5-154">Maak een bestand genaamd **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="a81d5-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="a81d5-155">Open het bestand in een Python-editor/IDE naar keuze, bijvoorbeeld IDLE.</span><span class="sxs-lookup"><span data-stu-id="a81d5-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="a81d5-156">Hallo volgende codemodules tooimport Hallo vereist uit Hallo apparaat-SDK toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="a81d5-157">Hallo-volgende code en vervang Hallo tijdelijke aanduiding voor toevoegen `[IoTHub Device Connection String]` met Hallo-verbindingsreeks voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="a81d5-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="a81d5-158">verbindingsreeks Hallo-apparaat bevindt zich doorgaans in Hallo-indeling van `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="a81d5-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="a81d5-159">Gebruik Hallo **deviceId** en **primaryKey** Hallo apparaat dat u hebt gemaakt in de vorige sectie tooreplace-Hallo Hallo `<deviceId>` en `<primaryKey>` respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="a81d5-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="a81d5-160">Vervang `<hostName>` door de hostnaam van uw IoT Hub, meestal ingedeeld als `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="a81d5-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

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
5. <span data-ttu-id="a81d5-161">Hallo na code toodefine een bevestiging verzenden retouraanroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-161">Add hello following code toodefine a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="a81d5-162">Hallo na code tooinitialize Hallo device-client toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="a81d5-163">Hallo volgende tooformat werken en een bericht verzenden vanuit uw gesimuleerde apparaat tooyour IoT-hub toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

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
8. <span data-ttu-id="a81d5-164">Ten slotte de belangrijkste functie Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="a81d5-165">Opslaan en sluiten Hallo **SimulatedDevice.py** bestand.</span><span class="sxs-lookup"><span data-stu-id="a81d5-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="a81d5-166">U bent nu klaar toorun deze app.</span><span class="sxs-lookup"><span data-stu-id="a81d5-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="a81d5-167">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a81d5-168">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="a81d5-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="a81d5-169">Berichten ontvangen van uw gesimuleerde apparaat</span><span class="sxs-lookup"><span data-stu-id="a81d5-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="a81d5-170">tooreceive telemetrieberichten vanaf uw apparaat, moet u toouse een [Event Hubs][lnk-event-hubs-overview]-compatibel eindpunt die worden weergegeven door Hallo IoT-Hub Hallo apparaat-naar-cloud-berichten kan lezen.</span><span class="sxs-lookup"><span data-stu-id="a81d5-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="a81d5-171">Lees Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie voor meer informatie over hoe tooprocess van van Event Hubs voor uw IoT-hub Event Hub-compatibele eindpunt berichten.</span><span class="sxs-lookup"><span data-stu-id="a81d5-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="a81d5-172">Event Hubs biedt geen ondersteuning voor telemetrie in Python nog, zodat u kunt maken een [Node.js](iot-hub-node-node-getstarted.md#D2C_node) of een [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) op basis van Event Hubs console app tooread hello apparaat-naar-cloud-berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a81d5-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="a81d5-173">Deze zelfstudie laat zien hoe u kunt Hallo [IoT Hub Explorer hulpprogramma] [ lnk-iot-hub-explorer] tooread deze apparaatberichten.</span><span class="sxs-lookup"><span data-stu-id="a81d5-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="a81d5-174">Open een opdrachtprompt en Hallo IoT Hub Explorer installeren.</span><span class="sxs-lookup"><span data-stu-id="a81d5-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="a81d5-175">Hallo volgende opdracht op Hallo opdrachtprompt uitvoert, toobegin bewaking apparaat-naar-cloud-berichten van uw apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="a81d5-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="a81d5-176">Gebruik van uw IoT-hub-verbindingsreeks in Hallo tijdelijke aanduiding voor na `--login`.</span><span class="sxs-lookup"><span data-stu-id="a81d5-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="a81d5-177">Open een nieuw opdrachtprompt en navigeer toohello map waarin zich Hallo **SimulatedDevice.py** bestand.</span><span class="sxs-lookup"><span data-stu-id="a81d5-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="a81d5-178">Voer Hallo **SimulatedDevice.py** bestand, dat periodiek telemetrie gegevens tooyour iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="a81d5-179">Apparaat-berichten op Hallo opdrachtprompt Hallo IoT Hub Explorer uitvoeren vanaf de vorige sectie Hallo Hallo zien.</span><span class="sxs-lookup"><span data-stu-id="a81d5-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Apparaat-naar-cloud-berichten met Python][2]

## <a name="next-steps"></a><span data-ttu-id="a81d5-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a81d5-181">Next steps</span></span>
<span data-ttu-id="a81d5-182">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="a81d5-183">U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app toosend apparaat-naar-cloudberichten toohello iothub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a81d5-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="a81d5-184">U waargenomen Hallo-berichten dat is ontvangen door de IoT-hub met behulp van Hallo IoT Hub Explorer hulpprogramma Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a81d5-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="a81d5-185">tooexplore hello Python SDK voor het gebruik van Azure IoT Hub in de diepte, gaat u naar [deze Git Hub-opslagplaats][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="a81d5-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="a81d5-186">tooreview hello berichtenmogelijkheden Hallo Azure IoT Hub Service SDK voor Python, die u kunt downloaden en uitvoeren [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="a81d5-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="a81d5-187">Voor apparaat side simulatie met hello Azure IoT Hub apparaat-SDK voor Python, u kunt downloaden en uitvoeren van Hallo [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="a81d5-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="a81d5-188">toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:</span><span class="sxs-lookup"><span data-stu-id="a81d5-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="a81d5-189">[Verbinding maken met uw apparaat][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="a81d5-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="a81d5-190">[Aan de slag met apparaatbeheer][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="a81d5-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="a81d5-191">[Aan de slag met Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="a81d5-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="a81d5-192">toolearn hoe tooextend uw IoT-oplossing en proces apparaat-naar-cloud-berichten op grote schaal, zien Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a81d5-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
