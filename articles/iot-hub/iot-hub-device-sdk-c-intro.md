---
title: aaaThe Azure IoT-device SDK voor C | Microsoft Docs
description: Aan de slag met hello Azure IoT-device SDK voor C en meer informatie over hoe toocreate apps op apparaten die communiceren met een IoT-hub.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>Azure IoT-apparaat SDK voor C

Hallo **Azure IoT-device SDK** is een set van bibliotheken ontworpen toosimplify Hallo proces voor het verzenden van berichten tooand die berichten ontvangt van Hallo **Azure IoT Hub** service. Er zijn verschillende variaties Hallo SDK, elke die gericht is op een specifiek platform, maar dit artikel wordt beschreven Hallo **Azure IoT-device SDK voor C**.

Hello Azure IoT-device SDK voor C is geschreven in C ANSI (C99) toomaximize draagbaarheid. Deze functie stelt Hallo bibliotheken geschikt toooperate op meerdere platforms en apparaten, vooral wanneer het minimaliseren van schijf- en geheugengebruik is een prioriteit.

Er zijn een breed scala aan op welke Hallo SDK is getest platforms (Zie Hallo [Azure gecertificeerd voor IoT-apparaat catalogus](https://catalog.azureiotsuite.com/) voor meer informatie). Hoewel dit artikel scenario's van voorbeeldcode uitgevoerd op Windows-platform hello bevat, is Hallo-code die wordt beschreven in dit artikel is identiek voor Hallo bereik van de ondersteunde platforms.

In dit artikel vindt u toohello architectuur van hello Azure IoT-device SDK voor C. Dit laat zien hoe tooinitialize Hallo apparaatbibliotheek gegevens tooIoT Hub te verzenden en berichten ontvangen. Hallo-informatie in dit artikel moet voldoende tooget gestart met behulp van Hallo SDK, maar bevat ook aanwijzers tooadditional informatie over Hallo-bibliotheken.

## <a name="sdk-architecture"></a>SDK-architectuur

U vindt Hallo [ **Azure IoT-device SDK voor C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub-opslagplaats en de weergave details van Hallo API in Hallo [C-API-referentiemateriaal](https://azure.github.io/azure-iot-sdk-c/index.html).

meest recente versie van bibliotheken Hallo Hallo vindt u in Hallo **master** branche van Hallo opslagplaats:

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* Hallo core Hallo SDK wordt Hallo **iothub\_client** map waarin het Hallo-implementatie van Hallo API laag in Hallo SDK: Hallo **IoTHubClient** bibliotheek. Hallo **IoTHubClient** bibliotheek bevat API's implementeren onbewerkte messaging voor berichten tooIoT Hub verzenden en ontvangen van berichten uit IoT Hub. Wanneer u deze bibliotheek, bent u verantwoordelijk voor het implementeren van bericht serialisatie, maar andere details voor de communicatie met IoT Hub worden afgehandeld.
* Hallo **serialisatiefunctie** map hulpfuncties en voorbeelden waarin u kunt hoe gegevens zien voor het verzenden van Iothub met behulp van tooAzure tooserialize Hallo-clientbibliotheek bevat. Hallo-gebruik van Hallo serialisatiefunctie is niet verplicht en uw gemak is opgegeven. Hallo toouse **serialisatiefunctie** bibliotheek, definieert u een model waarmee hello gegevens toosend tooIoT Hub en Hallo-berichten tooreceive hieruit verwacht. Zodra het Hallo-model is gedefinieerd, Hallo SDK biedt u een API-gebied waarmee u tooeasily werk met apparaat-naar-cloud en cloud-naar-apparaatberichten zonder dat u Hallo serialisatie details. Hallo-bibliotheek is afhankelijk van andere open-source bibliotheken die implementeren met behulp van protocollen zoals MQTT en AMQP transport.
* Hallo **IoTHubClient** bibliotheek, is afhankelijk van andere open-source bibliotheken:
  * Hallo [Azure C gedeeld hulpprogramma](https://github.com/Azure/azure-c-shared-utility) bibliotheek, waardoor algemene functionaliteit voor basistaken (zoals tekenreeksen, bewerkingen en i/o) over diverse Azure-gerelateerde C SDK's nodig.
  * Hallo [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) bibliotheek die een client-side '-implementatie van AMQP die zijn geoptimaliseerd voor resource beperkte apparaten.
  * Hallo [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) bibliotheek is een algemene bibliotheek implementatie Hallo MQTT-protocol en geoptimaliseerd voor resource beperkte apparaten.

Gebruik van deze bibliotheken is eenvoudiger toounderstand door te kijken voorbeeldcode. Hallo uit te voeren doorlopen diverse Hallo voorbeeldtoepassingen die zijn opgenomen in Hallo SDK. In dit scenario geeft u een goede voor Hallo kunt u verschillende mogelijkheden van Hallo architectuur lagen van Hallo SDK en een inleiding toohow Hallo-API's werken.

## <a name="before-you-run-hello-samples"></a>Voordat u voorbeelden van Hallo uitvoeren

Voordat u Hallo voorbeelden in hello Azure IoT-device SDK voor C uitvoeren kunt, moet u [geen exemplaar maken van Hallo service IoT Hub](iot-hub-create-through-portal.md) in uw Azure-abonnement. Voltooi Hallo taken te volgen:

* Uw ontwikkelomgeving voorbereiden
* Apparaat-referenties ophalen.

### <a name="prepare-your-development-environment"></a>Uw ontwikkelomgeving voorbereiden

Pakketten zijn beschikbaar voor algemene platforms (zoals NuGet voor Windows of apt_get voor Debian en Ubuntu) en Hallo voorbeelden gebruiken deze pakketten indien beschikbaar. In sommige gevallen moet u toocompile Hallo SDK voor of op uw apparaat. Als u toocompile Hallo SDK moet, Zie [uw ontwikkelingsomgeving voorbereiden](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in Hallo GitHub-opslagplaats.

tooobtain hello toepassing voorbeeldcode, download een exemplaar van Hallo SDK vanuit GitHub. Uw exemplaar van Hallo bron ophalen van Hallo **master** vertakking van Hallo [GitHub-opslagplaats](https://github.com/Azure/azure-iot-sdk-c).


### <a name="obtain-hello-device-credentials"></a>Hallo apparaat referenties ophalen

Nu dat u de voorbeeldcode Hallo hebt, is de volgende dingen toodo hello tooget een set referenties apparaat. Voor een apparaat toobe kunnen tooaccess een IoT-hub, moet u eerst Hallo apparaat toohello id-register IoT Hub toevoegen. Als u uw apparaat toevoegt, krijgt u een set referenties voor apparaten die u nodig hebt voor Hallo apparaat toobe kunnen tooconnect toohello iothub. Hallo-voorbeeldtoepassingen die is beschreven in de volgende sectie Hallo verwachten deze referenties in Hallo vorm van een **apparaat verbindingsreeks**.

Er zijn verschillende open-source hulpprogramma's voor toohelp beheren van uw IoT-hub.

* Een Windows-toepassing aangeroepen [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).
* Een node.js platformoverschrijdende CLI-hulpprogramma aangeroepen [iothub explorer](https://github.com/azure/iothub-explorer).

Deze zelfstudie wordt een grafische Hallo *apparaat explorer* hulpprogramma. U kunt ook Hallo *iothub explorer* hulpprogramma als u liever toouse een CLI-hulpprogramma.

Hallo apparaat explorer hulpprogramma gebruikt hello Azure IoT service bibliotheken tooperform diverse functies op IoT Hub, inclusief het toevoegen van apparaten. Als u Hallo apparaat explorer hulpprogramma tooadd een apparaat gebruikt, krijgt u een verbindingsreeks voor uw apparaat. U moet deze verbinding tekenreeks toorun Hallo voorbeeldtoepassingen.

Als u niet bekend met Hallo apparaat explorer hulpprogramma bent, Hallo na procedure beschrijft hoe toouse het tooadd een apparaat en een apparaat-verbindingsreeks ophalen.

hulpprogramma voor tooinstall Hallo apparaat explorer, Zie [hoe toouse apparaat Explorer Hallo voor IoT Hub-apparaten](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).

Wanneer u Hallo-programma uitvoert, ziet u deze interface:

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

Voer uw **IoT Hub-verbindingsreeks** in Hallo eerst veld en klikt u op **Update**. Deze stap Hallo hulpprogramma zodanig geconfigureerd dat met IoT Hub communiceren kan.

Wanneer Hallo IoT Hub-verbindingsreeks is geconfigureerd, klikt u op Hallo **Management** tabblad:

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

Dit tabblad is waar het beheer van Hallo-apparaten die zijn geregistreerd in uw IoT-hub.

U maakt een apparaat door te klikken op Hallo **maken** knop. Er wordt een dialoogvenster weergegeven met een reeks vooraf ingestelde sleutels (primair en secundair). Voer een **apparaat-ID** en klik vervolgens op **maken**.

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

Wanneer het Hallo-apparaat is gemaakt, weergeven Hallo apparaten updates met alle Hallo ingeschreven apparaten, met inbegrip van Hallo die u zojuist hebt gemaakt. Als u met de rechtermuisknop op het nieuwe apparaat, ziet u dit menu:

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

Als u ervoor kiest **Kopieer de verbindingsreeks voor geselecteerde apparaat**, Hallo apparaat-verbindingsreeks is gekopieerde toohello Klembord. Houd een kopie van de verbindingsreeks Hallo-apparaat. U moet bij het uitvoeren van de voorbeeldtoepassingen Hallo beschreven in Hallo uit te voeren.

Wanneer u Hallo bovenstaande stappen hebt voltooid, bent u klaar toostart waarop bepaalde code wordt uitgevoerd. Beide voorbeelden hebben een constante Hallo Hallo belangrijkste bron-bestand waarmee u een verbindingsreeks tooenter bovenaan in. Bijvoorbeeld Hallo bijbehorende regel van Hallo **iothub\_client\_voorbeeld\_mqtt** toepassing wordt weergegeven als volgt.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Hallo IoTHubClient library gebruiken

Binnen Hallo **iothub\_client** map in Hallo [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) -opslagplaats, er is een **voorbeelden** map waarin een toepassing met de naam **iothub\_client\_voorbeeld\_mqtt**.

versie van Windows Hello Hallo **iothub\_client\_voorbeeld\_mqtt** toepassing bevat Hallo Visual Studio-oplossing te volgen:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> Als u dit project in Visual Studio 2017 openen, Hallo prompts tooretarget Hallo project toohello meest recente versie accepteren.

Deze oplossing bevat een project. Er zijn vier NuGet-pakketten in deze oplossing is geïnstalleerd:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

Moet u altijd Hallo **Microsoft.Azure.C.SharedUtility** wanneer u met Hallo SDK werkt-pakket. Dit voorbeeld Hallo MQTT protocol gebruikt, moet u daarom Hallo opnemen **Microsoft.Azure.umqtt** en **Microsoft.Azure.IoTHub.MqttTransport** pakketten (Er zijn equivalent pakketten voor AMQP en HTTP ). Omdat Hallo-voorbeeld Hallo gebruikt **IoTHubClient** bibliotheek, moet u ook Hallo **Microsoft.Azure.IoTHub.IoTHubClient** -pakket in uw oplossing.

U vindt Hallo-implementatie voor de voorbeeldtoepassing Hallo in Hallo **iothub\_client\_voorbeeld\_mqtt.c** bronbestand.

Hallo volgende stappen wordt gebruikt in dit voorbeeld toepassing toowalk u via wat is vereist toouse hello **IoTHubClient** bibliotheek.

### <a name="initialize-hello-library"></a>Hallo-bibliotheek initialiseren

> [!NOTE]
> Voordat u begint te werken met Hallo-bibliotheken, moet u mogelijk tooperform initialisaties platform-specifieke. Als u van plan toouse AMQP Linux bent moet u bijvoorbeeld Hallo OpenSSL bibliotheek initialiseren. voorbeelden in Hallo Hallo [GitHub-opslagplaats](https://github.com/Azure/azure-iot-sdk-c) Hallo hulpprogrammafunctie aanroepen **platform\_init** wanneer Hallo van client wordt gestart en roep Hallo **platform\_deinit**  functie voordat u afsluit. Deze functies zijn gedefinieerd in Hallo platform.h header-bestand. Hallo definities van deze functies voor uw doelplatform in Hallo onderzoeken [opslagplaats](https://github.com/Azure/azure-iot-sdk-c) toodetermine noodzaak tooinclude van de platform-specifieke initialisatiecode in de client.

werkt met bibliotheken hello, toostart toewijzen eerst een client-ingang van IoT Hub:

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

U doorgeven een kopie van de verbindingsreeks voor Hallo apparaat die u hebt verkregen via Hallo apparaat explorer hulpprogramma toothis functie. U ook opgeven Hallo communicatie protocol toouse. In dit voorbeeld wordt MQTT maar AMQP en HTTP zijn ook opties.

Wanneer u hebt een geldige **IOTHUB\_CLIENT\_verwerken**, u kunt beginnen met het aanroepen van Hallo-API's toosend en tooand berichten uit IoT Hub ontvangt.

### <a name="send-messages"></a>Berichten verzenden

Hallo-voorbeeldtoepassing stelt u een lus toosend berichten tooyour IoT-hub. Hallo codefragment te volgen:

- Hiermee maakt u een bericht.
- Voegt een eigenschap toohello-bericht.
- Verzendt een bericht.

Maak eerst een bericht weergegeven:

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

Telkens wanneer u een bericht verzendt, Geef een verwijzing tooa callback-functie die wordt aangeroepen wanneer het Hallo-gegevens worden verzonden. In dit voorbeeld Hallo callback-functie is aangeroepen **SendConfirmationCallback**. Hallo volgende fragment toont deze callback-functie:

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Houd er rekening mee Hallo aanroep toohello **IoTHubMessage\_vernietigen** werkt wanneer u met het Hallo-bericht bent klaar. Deze functie wordt vrijgemaakt Hallo-resources toegewezen tijdens het maken van het Hallo-bericht.

### <a name="receive-messages"></a>Berichten ontvangen

Het bericht is een asynchrone bewerking. Eerst registreren Hallo callback tooinvoke wanneer Hallo apparaat een bericht weergegeven ontvangt:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

de laatste parameter Hallo is een aanwijzer void toowhatever die u wilt. In Hallo voorbeeld is een aanwijzer tooan geheel getal, maar het mogelijk een wijzer tooa complexere gegevensstructuur. Deze parameter kunt Hallo callback functie toooperate op gedeelde staat met Hallo aanroeper van deze functie.

Wanneer het Hallo-apparaat een bericht ontvangt, is hello geregistreerde callback-functie aangeroepen. Deze functie voor retouraanroepen opgehaald:

* Hallo-bericht-id en correlatie-id van het Hallo-bericht.
* Hallo-berichtinhoud.
* Alle aangepaste eigenschappen van het Hallo-bericht.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Gebruik Hallo **IoTHubMessage\_GetByteArray** functie tooretrieve Hallo-bericht, die in dit voorbeeld een tekenreeks is.

### <a name="uninitialize-hello-library"></a>Initialisatie Hallo-bibliotheek

Wanneer u klaar bent met gebeurtenissen verzenden en ontvangen van berichten, kunt u Hallo IoT bibliotheek initialisatie. toodo uitgeven dus Hallo functieaanroep te volgen:

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Deze aanroep Hallo-resources eerder toegewezen door Hallo vrijgemaakt **IoTHubClient\_CreateFromConnectionString** functie.

Zoals u ziet het is gemakkelijk toosend en berichten ontvangen met Hallo **IoTHubClient** bibliotheek. Hallo-bibliotheek verwerkt Hallo details voor de communicatie met IoT Hub, met inbegrip van welke toouse protocol (dit is vanuit het perspectief van de Hallo Hallo Developer wordt een eenvoudige configuratieoptie).

Hallo **IoTHubClient** bibliotheek biedt ook nauwkeurige controle over hoe tooserialize Hallo gegevens uw apparaat tooIoT Hub verzendt. In sommige gevallen is dit niveau van controle een voordeel, maar is de details van een implementatie die u niet toobe betrokken wilt bij. Als dit Hallo geval is, kunt u met behulp van Hallo **serialisatiefunctie** bibliotheek die wordt beschreven in de volgende sectie Hallo.

## <a name="use-hello-serializer-library"></a>Hallo serialisatiefunctie bibliotheek gebruiken

Conceptueel Hallo **serialisatiefunctie** bibliotheek bevindt zich bovenaan Hallo **IoTHubClient** bibliotheek in Hallo SDK. Hierbij Hallo **IoTHubClient** -bibliotheek voor communicatie met IoT Hub, maar de onderliggende hello modellering mogelijkheden die Hallo last van omgaan met bericht serialisatie van de ontwikkelaar Hallo verwijderen toevoegt. Hoe deze bibliotheek werkt best wordt geïllustreerd door een voorbeeld.

Hallo binnen **serialisatiefunctie** map in Hallo [azure-iot-sdk-c-opslagplaats](https://github.com/Azure/azure-iot-sdk-c), is een **voorbeelden** map waarin een toepassing met de naam **simplesample \_mqtt**. Hallo Windows-versie van dit voorbeeld bevat Hallo Visual Studio-oplossing te volgen:

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> Als u dit project in Visual Studio 2017 openen, Hallo prompts tooretarget Hallo project toohello meest recente versie accepteren.

Net als bij het vorige voorbeeld hello, bevat deze een enkele NuGet-pakketten:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

U hebt gezien de meeste van deze pakketten in de vorige steekproef hello, maar **Microsoft.Azure.IoTHub.Serializer** is er nieuw. Dit pakket is vereist wanneer u Hallo **serialisatiefunctie** bibliotheek.

U vindt implementatie van de voorbeeldtoepassing Hallo Hallo in Hallo **simplesample\_mqtt.c** bestand.

Hallo volgende secties helpt u stapsgewijs door Hallo sleutel delen van dit voorbeeld.

### <a name="initialize-hello-library"></a>Hallo-bibliotheek initialiseren

werken met Hallo toostart **serialisatiefunctie** bibliotheek aanroep Hallo initialisatie API's:

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

Hallo aanroep toohello **serialisatiefunctie\_init** functie is een eenmalige aanroep en initialiseert Hallo onderliggende bibliotheek. Roep vervolgens Hallo **IoTHubClient\_LLE\_CreateFromConnectionString** functie, die is dezelfde API zoals in Hallo Hallo **IoTHubClient** voorbeeld. Deze aanroep Hiermee stelt u de verbindingsreeks van uw apparaat (deze aanroep is ook waarin u Hallo protocol kiezen gewenste toouse). Dit voorbeeld MQTT als Hallo transport gebruikt, maar kan AMQP of HTTP gebruiken.

Tenslotte roept Hallo **maken\_MODEL\_exemplaar** functie. **WeatherStation** is Hallo-naamruimte van Hallo model en **ContosoAnemometer** Hallo-naam van het Hallo-model. Zodra Hallo model exemplaar is gemaakt, kunt u deze toostart verzenden en ontvangen van berichten. Het is echter belangrijk toounderstand welk model is.

### <a name="define-hello-model"></a>Hallo model definiëren

Een model in Hallo **serialisatiefunctie** bibliotheek definieert Hallo-berichten dat uw apparaat tooIoT Hub en Hallo-berichten verzenden kunt, zogenaamde *acties* in Hallo modelleertaal op het kan ontvangen. U definieert een model met behulp van een set van C macro's zoals Hallo in **simplesample\_mqtt** voorbeeldtoepassing:

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Hallo **BEGINT\_NAAMRUIMTE** en **END\_NAAMRUIMTE** macro's beide Hallo-naamruimte van Hallo model als een argument nemen. Verwacht wordt dat is alles tussen deze macro's Hallo definitie van uw model of modellen en Hallo-gegevensstructuren die Hallo modellen gebruiken.

In dit voorbeeld is een enkelvoudig model aangeroepen **ContosoAnemometer**. Dit model definieert twee soorten gegevens kan uw apparaat tooIoT Hub verzenden: **DeviceId** en **windsnelheid**. Definieert ook drie acties (berichten) die het apparaat kan ontvangen: **TurnFanOn**, **TurnFanOff**, en **SetAirResistance**. Elk gegevenselement in de heeft een type en elke actie heeft een naam (en desgewenst een set parameters).

Hallo-gegevens en acties die zijn gedefinieerd in Hallo model definiëren een API-gebied dat u gebruik kunt toosend berichten tooIoT Hub en toomessages verzonden toohello apparaat reageren. Door een voorbeeld van het gebruik van dit model best begrijpen.

### <a name="send-messages"></a>Berichten verzenden

Hallo model definieert Hallo gegevens u tooIoT Hub kunt verzenden. In dit voorbeeld dit betekent dat een Hallo twee gegevensitems die zijn gedefinieerd met behulp van Hallo **WITH_DATA** macro. Er zijn verschillende stappen vereist toosend **DeviceId** en **windsnelheid** waarden tooan IoT-hub. Hallo is eerst tooset Hallo gegevens die u wilt dat toosend:

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

Hallo model dat u eerder hebt gedefinieerd kunt u tooset Hallo waarden door leden van een **struct**. Vervolgens serialiseren gewenste toosend Hallo-bericht:

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

Deze code serialiseert Hallo apparaat-naar-cloud tooa buffer (waarnaar wordt verwezen door **bestemming**). Hallo code roept vervolgens Hallo **sendMessage** toosend Hallo-bericht tooIoT Hub werken:

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


tweede toolast-parameter van Hallo **IoTHubClient\_LLE\_SendEventAsync** is een verwijzing tooa callback-functie die wordt aangeroepen wanneer het Hallo-gegevens is verzonden. Hier volgt Hallo callback-functie in Hallo-voorbeeld:

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

de tweede parameter Hallo is een aanwijzer toouser context; Hallo dezelfde aanwijzer te doorgegeven**IoTHubClient\_LLE\_SendEventAsync**. In dit geval Hallo-context is een eenvoudige Prestatiemeter gebruiken, maar dit alles kan zijn.

Dit is alles wat er is toosending apparaat-naar-cloud-berichten. Hallo alleen wat toocover links, is hoe tooreceive berichten.

### <a name="receive-messages"></a>Berichten ontvangen

Ontvangen van een bericht werkt op dezelfde manier toohello werkwijze berichten in Hallo **IoTHubClient** bibliotheek. U registreert eerst een callback-functie van het bericht:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

U schrijft vervolgens Hallo callbackfunctie die wordt aangeroepen wanneer een bericht wordt ontvangen:

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

Deze code is standaardtekst--deze heeft dezelfde Hallo voor een oplossing. Deze functie het Hallo-bericht ontvangt, en zorgt voor routering toohello juiste functie via Hallo aanroep te**EXECUTE\_opdracht**. aangeroepen Hallo-functie is op dit moment hangt af van het Hallo-definitie van Hallo-acties in uw model.

Wanneer u een actie in het model definiëren, bent u klaar vereist tooimplement een functie die wordt aangeroepen wanneer het apparaat het bijbehorende Hallo-bericht ontvangt. Bijvoorbeeld, als het model is gedefinieerd met deze actie:

```c
WITH_ACTION(SetAirResistance, int, Position)
```

Een functie met deze handtekening definiëren:

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Houd er rekening mee hoe Hallo-naam van de functie Hallo overeenkomt met Hallo-naam van Hallo actie in Hallo model en dat Hallo parameters van functie Hallo Hallo parameters opgegeven voor de Hallo actie. de eerste parameter Hallo is altijd vereist en een exemplaar van de wijzer toohello van uw model bevat.

Wanneer Hallo apparaat een bericht dat overeenkomt met deze handtekening ontvangt, wordt de overeenkomende functie Hallo genoemd. Daarom in combinatie met tooinclude Hallo standaardtekst code uit **IoTHubMessage**, ontvangen van berichten is slechts een kwestie van het definiëren van een eenvoudige functie voor elke actie in het model is gedefinieerd.

### <a name="uninitialize-hello-library"></a>Initialisatie Hallo-bibliotheek

Wanneer u klaar bent met gegevens verzenden en ontvangen van berichten, kunt u Hallo IoT bibliotheek initialisatie:

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

Elk van deze drie functies wordt uitgelijnd met Hallo drie initialisatie van de functies die eerder zijn beschreven. Het aanroepen van deze API's zorgt ervoor dat u eerder toegewezen resources vrij.

## <a name="next-steps"></a>Volgende stappen

In dit artikel gedekt Hallo grondbeginselen van het gebruik van Hallo-bibliotheken in Hallo **Azure IoT-device SDK voor C**. Dit u geleverd met voldoende informatie toounderstand wat opgenomen in Hallo SDK, de architectuur en hoe het werken met Hallo Windows voorbeelden van tooget wordt gestart. het volgende artikel Hallo Hallo beschrijving van Hallo SDK blijft door waarin wordt uitgelegd [meer over Hallo IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).

toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo [Azure IoT SDK's][lnk-sdks].

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
