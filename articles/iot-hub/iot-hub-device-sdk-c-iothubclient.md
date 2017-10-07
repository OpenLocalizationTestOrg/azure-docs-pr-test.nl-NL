---
title: aaaAzure IoT-apparaat SDK voor C - IoTHubClient | Microsoft Docs
description: Hoe toouse hello IoTHubClient bibliotheek op Hallo van het apparaat van Azure IoT SDK voor C toocreate apparaat-apps die communiceren met een IoT-hub.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>Azure IoT-apparaat SDK voor C: meer informatie over IoTHubClient
Hallo [eerst artikel](iot-hub-device-sdk-c-intro.md) in deze reeks geïntroduceerd Hallo **Azure IoT-device SDK voor C**. Dit artikel worden beschreven dat er twee architectuur lagen SDK zijn. Hallo base is Hallo **IoTHubClient** bibliotheek die rechtstreeks communicatie met IoT Hub beheert. Er is ook Hallo **serialisatiefunctie** bibliotheek die op deze tooprovide serialisatie-services voortbouwt. In dit artikel bieden we extra details op Hallo **IoTHubClient** bibliotheek.

Hallo vorige artikel wordt beschreven hoe toouse hello **IoTHubClient** bibliotheek toosend gebeurtenissen tooIoT Hub en ontvangen van berichten. In dit artikel wordt uitgebreid die discussie waarin wordt uitgelegd hoe toomore nauwkeurig beheren *wanneer* verzenden en ontvangen van gegevens, introductie van toohello **lager niveau API's**. Ook wordt uitgelegd hoe tooattach eigenschappen tooevents (en berichten ophalen) met Hallo eigenschap afhandeling van functies in Hallo **IoTHubClient** bibliotheek. Ten slotte, bieden we extra uitleg van de verschillende manieren toohandle berichten uit IoT Hub is ontvangen.

Hallo artikel tot slot die betrekking hebben op een aantal verschillende onderwerpen, waaronder informatie over referenties voor apparaat en hoe toochange gedrag van Hallo Hallo **IoTHubClient** via configuratieopties.

We gebruiken Hallo **IoTHubClient** SDK tooexplain voorbeelden in deze onderwerpen. Als u toofollow langs wilt, raadpleegt u Hallo **iothub\_client\_voorbeeld\_http** en **iothub\_client\_voorbeeld\_amqp** toepassingen die zijn opgenomen in hello Azure IoT-device SDK voor C. alles dat wordt beschreven in Hallo uit te voeren in deze voorbeelden wordt gedemonstreerd.

U vindt Hallo [ **Azure IoT-device SDK voor C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub-opslagplaats en de weergave details van Hallo API in Hallo [C-API-referentiemateriaal](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Hallo lager niveau API's
Hallo vorige artikel beschreven Hallo de werking van Hallo **IotHubClient** binnen de context Hallo Hallo **iothub\_client\_voorbeeld\_amqp** de toepassing. Bijvoorbeeld, het uitgelegd hoe tooinitialize Hallo tapewisselaar met deze code.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Ook wordt beschreven hoe toosend gebeurtenissen gebruik van deze aanroep van functie.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

Hallo artikel wordt ook beschreven hoe tooreceive berichten via het registreren van een callback-functie.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

hebt u Hallo artikel ook geleerd hoe toofree resources met behulp van zoals Hallo volgende code.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

Er zijn echter aanvullende functies tooeach van deze API's:

* IoTHubClient\_LLE\_CreateFromConnectionString
* IoTHubClient\_LLE\_SendEventAsync
* IoTHubClient\_LLE\_SetMessageCallback
* IoTHubClient\_LLE\_vernietigen

Deze functies alle opnemen 'LLE' in hello API-naam. Hallo-parameters van elk van deze functies zijn dan die identiek tootheir niet LLE collega's. Hallo-gedrag van deze functies verschilt echter op één belangrijk.

Als u aanroept **IoTHubClient\_CreateFromConnectionString**, nieuwe thread die wordt uitgevoerd op de achtergrond Hallo Hallo onderliggende bibliotheken maken. Deze thread gebeurtenissen verzendt en ontvangt berichten uit IoT Hub. Er is geen dergelijke thread wordt gemaakt bij het werken met Hallo 'LLE' API's. Hallo maken van de achtergrondthread Hallo is een gemak toohello ontwikkelaar. U hebt geen tooworry over expliciet gebeurtenissen verzenden en ontvangen van berichten uit IoT Hub--gebeurt automatisch op Hallo achtergrond. Daarentegen Hallo 'LLE' API's bieden u een expliciete controle over de communicatie met IoT Hub, als u deze nodig hebt.

toounderstand deze beter we bekijken een voorbeeld:

Als u aanroept **IoTHubClient\_SendEventAsync**, wat u daadwerkelijk doet Hallo gebeurtenis is als in een buffer. Hallo achtergrondthread gemaakt bij het aanroepen van **IoTHubClient\_CreateFromConnectionString** voortdurend deze buffer bewaakt en worden alle gegevens verzonden dat deze tooIoT Hub bevat. Dit gebeurt op de achtergrond op Hallo Hallo dezelfde tijd die Hallo hoofdthread is bezig met andere taken.

Op dezelfde manier als het registreren van een callback-functie voor berichten met **IoTHubClient\_SetMessageCallback**, bent u Hallo SDK toohave Hallo achtergrond instructie thread Hallo callback-functie aanroepen wanneer een bericht ontvangen, onafhankelijk van Hallo hoofdthread.

Hallo 'LLE' API's niet een achtergrond-thread niet maken. In plaats daarvan een nieuwe API moet worden aangeroepen tooexplicitly verzenden en ontvangen van gegevens uit IoT Hub. Dit wordt geïllustreerd in Hallo voorbeeld te volgen.

Hallo **iothub\_client\_voorbeeld\_http** toepassing die opgenomen in de SDK demonstreert Hallo Hallo lager niveau API's. In dit voorbeeld sturen we gebeurtenissen tooIoT Hub met code zoals Hallo volgende:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Hallo eerste drie regels maken het Hallo-bericht en de laatste regel Hallo verzendt Hallo-gebeurtenis. Echter, zoals eerder vermeld, 'verzenden' hello gebeurtenis betekent dat gegevens Hallo gewoon wordt geplaatst in een buffer. Niets op Hallo netwerk wordt verzonden wanneer we noemen **IoTHubClient\_LLE\_SendEventAsync**. U moet aanroepen in volgorde tooactually inkomende hello gegevens tooIoT Hub **IoTHubClient\_LLE\_DoWork**, zoals in dit voorbeeld:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Deze code (van Hallo **iothub\_client\_voorbeeld\_http** toepassing) herhaaldelijk roept **IoTHubClient\_LLE\_DoWork** . Elke keer **IoTHubClient\_LLE\_DoWork** is aangeroepen, het sommige gebeurtenissen van Hallo buffer tooIoT Hub verzendt en het ophalen van een bericht in de wachtrij toohello apparaat worden verzonden. het laatste geval Hallo betekent dat als we een callback-functie voor berichten, geregistreerd en vervolgens het Hallo-callback is aangeroepen (ervan uitgaande dat alle berichten worden in de wachtrij geplaatst). Hebben zou we een callbackfunctie met code zoals Hallo volgende geregistreerd:

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

Hallo reden die **IoTHubClient\_LLE\_DoWork** heet vaak in een lus is dat elke keer dat deze wordt aangeroepen, verzendt *sommige* buffer opgeslagen gebeurtenissen tooIoT Hub en haalt *naast Hallo* bericht dat in de wachtrij geplaatst voor Hallo-apparaat. Elke aanroep wordt niet gegarandeerd toosend buffer opgeslagen gebeurtenissen of in de wachtrij tooretrieve alle berichten. Als u wilt dat toosend alle gebeurtenissen in Hallo buffer en ga vervolgens door op met de andere verwerking kunt u deze lus vervangen met code zoals Hallo volgende:

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Deze code roept **IoTHubClient\_LLE\_DoWork** totdat alle gebeurtenissen in de buffer Hallo tooIoT Hub zijn verzonden. Houd er rekening mee dat dit ook impliceert niet alle berichten in de wachtrij is ontvangen. Deel van Hallo reden hiervoor is dat als deterministische een actie controleren of er 'alle' berichten niet. Wat gebeurt er als u 'alle' Hallo-berichten ophalen, maar wordt nog een toohello apparaat verzonden onmiddellijk na? Er is een betere manier toodeal met die met een geprogrammeerde time-out. Hallo-bericht callback-functie kan bijvoorbeeld een timer ingesteld telkens wanneer deze wordt aangeroepen. Vervolgens kunt u bedrijfslogica toocontinue verwerken als u bijvoorbeeld geen berichten ontvangen in Hallo laatste *X* seconden.

Wanneer u bent klaar ingressing gebeurtenissen en ontvangen van berichten, ervoor toocall Hallo bijbehorende functie tooclean resources worden.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

In feite is er slechts één set API's toosend en ontvangen van gegevens met een achtergrond-thread en een andere set API's die hetzelfde zonder Hallo achtergrondthread Hallo. Veel van ontwikkelaars mogelijk liever Hallo niet - LLE API's, maar hello API's van lager niveau zijn nuttig wanneer Hallo developer wil expliciete controle over Netwerkoverdrachten. Bijvoorbeeld: op sommige apparaten verzamelen van gegevens gedurende een bepaalde tijd alleen ingangsgebeurtenissen tussenpozen (bijvoorbeeld één keer een uur of één keer per dag). Hallo lager niveau API's kunt u de mogelijkheid tooexplicitly besturingselement Hallo bij het verzenden en ontvangen van gegevens uit IoT Hub. Anderen liever Hallo eenvoud gewoon die Hallo die lager niveau API's bieden. Alles op Hallo hoofdthread in plaats van sommige werk gebeurt op Hallo achtergrond gebeurt.

Het model dat u kiest, worden ervoor toobe consistent in welke API's die u gebruikt. Als u met het aanroepen van Start **IoTHubClient\_LLE\_CreateFromConnectionString**, zorg ervoor dat u alleen Hallo overeenkomt lager niveau API's voor een vervolgzelfstudie werk gebruiken:

* IoTHubClient\_LLE\_SendEventAsync
* IoTHubClient\_LLE\_SetMessageCallback
* IoTHubClient\_LLE\_vernietigen
* IoTHubClient\_LLE\_DoWork

Hallo tegengestelde is ook ingesteld op true. Als u met opstart **IoTHubClient\_CreateFromConnectionString**, en vervolgens gebruik Hallo niet - LLE API's voor alle verdere verwerking.

Zie in hello Azure IoT-apparaat SDK voor C, Hallo **iothub\_client\_voorbeeld\_http** -toepassing voor een compleet voorbeeld van Hallo lager niveau API's. Hallo **iothub\_client\_voorbeeld\_amqp** toepassing voor een voorbeeld van een volledige Hallo niet - LLE API's kan worden verwezen.

## <a name="property-handling"></a>Verwerking van de eigenschap
Tot nu toe wanneer we verzenden van gegevens hebt die worden beschreven, hebt we is verwijst toohello hoofdtekst van het Hallo-bericht. Neem bijvoorbeeld deze code:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Het volgende voorbeeld wordt een bericht tooIoT Hub met Hallo tekst "Hallo wereld". IoT Hub kan echter ook eigenschappen toobe gekoppelde tooeach bericht. Eigenschappen zijn naam/waarde-paren die aangesloten toohello bericht worden kunnen. Bijvoorbeeld, kunt we Hallo vorige code tooattach een eigenschap toohello bericht wijzigen:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Begin met het aanroepen van **IoTHubMessage\_eigenschappen** en deze Hallo-ingang van ons bericht wordt doorgegeven. Wat we terughalen is een **kaart\_verwerken** verwijzing waarmee we toostart eigenschappen toe te voegen. Hallo laatstgenoemde wordt bereikt door het aanroepen van **kaart\_AddOrUpdate**, wat een verwijzing tooa kaart duurt\_INGANG Hallo eigenschapsnaam en Hallo eigenschapswaarde. Met deze API kunnen we zoveel eigenschappen als we wilt toevoegen.

Wanneer de gebeurtenis Hallo wordt gelezen uit **Event Hubs**, Hallo ontvanger kunt opsommen Hallo eigenschappen en de bijbehorende waarden ophalen. Bijvoorbeeld in .NET dit zou worden bereikt door het openen van Hallo [eigenschappen verzameling op Hallo EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

In het vorige voorbeeld hello koppelt we eigenschappen tooan gebeurtenis dat we tooIoT Hub verzendt. Eigenschappen kunnen ook worden aangesloten toomessages ontvangen van IoT-Hub. Als we tooretrieve eigenschappen van een bericht wilt, kunnen we code zoals Hallo volgende gebruiken in onze callback-functie van het bericht:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

Hallo aanroep te**IoTHubMessage\_eigenschappen** retourneert Hallo **kaart\_verwerken** verwijzing. We geeft die verwijzen naar te**kaart\_GetInternals** tooobtain een verwijzing tooan-matrix van Hallo naam/waarde-paren (evenals een aantal Hallo-eigenschappen). Op dat moment is een kwestie van Hallo eigenschappen tooget toohello waarden die we wilt inventariseren.

U hebt geen toouse eigenschappen in uw toepassing. Echter, als u tooset moet ze op gebeurtenissen of deze worden opgehaald van berichten, hello **IoTHubClient** bibliotheek kunt u gemakkelijk.

## <a name="message-handling"></a>Afhandeling van berichten
Zoals eerder gezegd, wanneer berichten uit IoT Hub Hallo **IoTHubClient** bibliotheek antwoordt door een geregistreerde callback-functie wordt aangeroepen. Er is een retourparameter van deze functie die een extra verklaring verdient. Hier volgt een fragment van de callback-functie in Hallo Hallo **iothub\_client\_voorbeeld\_http** voorbeeldtoepassing:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Houd er rekening mee dat het retourtype Hallo **IOTHUBMESSAGE\_toestand\_resultaat** en in dit geval wordt teruggeplaatst **IOTHUBMESSAGE\_GEACCEPTEERDE**. Er zijn andere waarden die we van deze functie kunt terugkeren wijzigen hoe Hallo **IoTHubClient** bibliotheek reageert toohello bericht retouraanroep. Hier volgen Hallo-opties.

* **IOTHUBMESSAGE\_GEACCEPTEERDE** – het Hallo-bericht is verwerkt. Hallo **IoTHubClient** bibliotheek zullen niet worden aangeroepen Hallo callback-functie opnieuw met de Hallo hetzelfde bericht.
* **IOTHUBMESSAGE\_geweigerd** : het Hallo-bericht is niet verwerkt en er is geen toodo desire Hallo daarom in toekomstige. Hallo **IoTHubClient** bibliotheek moet niet worden aangeroepen Hallo callback-functie opnieuw met de Hallo hetzelfde bericht.
* **IOTHUBMESSAGE\_ABANDONED** – het Hallo-bericht is niet verwerkt, maar Hallo **IoTHubClient** bibliotheek Hallo callback-functie opnieuw met de Hallo moet aanroepen hetzelfde bericht.

Voor Hallo eerst twee retourcodes, hello **IoTHubClient** bibliotheek verzendt een bericht tooIoT Hub die aangeeft dat het Hallo-bericht moet worden verwijderd uit Hallo apparaatwachtrij en niet opnieuw worden bezorgd. Hallo netto effect is dezelfde Hallo (het Hallo-bericht is verwijderd uit Hallo apparaatwachtrij), maar Hiermee wordt aangegeven of het Hallo-bericht is goedgekeurd of geweigerd nog steeds wordt vastgelegd.  Dit verschil Recording is nuttig toosenders van het Hallo-bericht die luisteren naar feedback en weten als een apparaat heeft geaccepteerd of een bepaald bericht afgewezen.

In het laatste geval Hallo een bericht ook tooIoT Hub wordt verzonden, maar Hiermee wordt aangegeven dat het Hallo-bericht moet opnieuw worden bezorgd. Meestal zult u een bericht afbreken als u er een fout optreden tootry tooprocess Hallo bericht opnieuw. Daarentegen is weigeren van een bericht geschikt als er een onherstelbare fout optreden (of als u gewoon besluit dat u niet wilt dat het Hallo-bericht tooprocess).

In elk geval worden op de hoogte van de andere retourcodes Hallo zodat u van Hallo gewenste Hallo-gedrag kan veroorzaken **IoTHubClient** bibliotheek.

## <a name="alternate-device-credentials"></a>Alternatieve apparaat referenties
Zoals eerder vermeld, Hallo eerst te beginnen toodo bij het werken met Hallo **IoTHubClient** bibliotheek tooobtain is een **IOTHUB\_CLIENT\_verwerken** met een aanroep zoals Hallo te volgen:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Hallo argumenten te**IoTHubClient\_CreateFromConnectionString** zijn verbindingsreeks Hallo-apparaat en een parameter die aangeeft Hallo-protocol gebruiken we toocommunicate met IoT Hub. verbindingsreeks Hallo-apparaat heeft een indeling die wordt weergegeven als volgt:

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

Er zijn vier stukjes informatie in deze tekenreeks: naam van de IoT Hub, achtervoegsel IoT Hub, apparaat-ID en gedeelde toegangssleutel. U Hallo volledig gekwalificeerde domeinnaam (FQDN) van een IoT-hub verkrijgen wanneer u uw IoT hub-instantie in hello Azure-portal maakt — Hiermee krijgt u naam Hallo IoT-hub (Hallo eerste deel van Hallo Fully Qualified Domain Name) en het Hallo IoT hub achtervoegsel (Hallo rest Hallo Fully Qualified Domain Name). U krijgt Hallo apparaat-ID en de gedeelde toegangssleutel Hallo wanneer u uw apparaat met IoT Hub registreert (zoals beschreven in Hallo [vorige artikel](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** biedt u eenrichtingssessie tooinitialize Hallo-bibliotheek. Als u liever, kunt u een nieuwe **IOTHUB\_CLIENT\_verwerken** met behulp van deze afzonderlijke parameters in plaats van verbindingsreeks Hallo-apparaat. Dit wordt bereikt met de volgende code Hallo:

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

Dit kunnen worden behaald Hallo hetzelfde is als **IoTHubClient\_CreateFromConnectionString**.

Het lijkt misschien duidelijk dat u toouse wilt **IoTHubClient\_CreateFromConnectionString** in plaats van deze uitgebreidere methode van de initialisatie. Houd er rekening mee echter, wanneer u een apparaat in IoT Hub registreren wat er een apparaat-ID en de apparaatsleutel (niet een verbindingsreeks is). Hallo *apparaat explorer* SDK hulpprogramma geïntroduceerd in Hallo [vorige artikel](iot-hub-device-sdk-c-intro.md) maakt gebruik van bibliotheken in Hallo **Azure IoT service SDK** toocreate Hallo apparaat verbindingsreeks uit Hallo apparaat-ID, de sleutel voor apparaat en IoT Hub-hostnaam. Aanroepen van dus **IoTHubClient\_LLE\_maken** wellicht de voorkeur omdat u Hallo stap voor het genereren van een verbindingsreeks. Gebruik de methode is handig.

## <a name="configuration-options"></a>Configuratie-opties
Tot nu toe alles over Hallo manier Hallo beschreven **IoTHubClient** bibliotheek werkt weerspiegelt het standaardgedrag. Er zijn echter een aantal opties die u kunt de werking van Hallo bibliotheek toochange instellen. Dit wordt bereikt door het gebruik van Hallo **IoTHubClient\_LLE\_SetOption** API. Bekijk het volgende voorbeeld:

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Er zijn een aantal opties die vaak worden gebruikt:

* **SetBatching** (bool) – als **true**, en vervolgens de gegevens die worden verzonden tooIoT Hub wordt verzonden in batches. Als **false**, en vervolgens berichten afzonderlijk worden verzonden. Hallo standaardwaarde is **false**. Houd er rekening mee dat Hallo **SetBatching** optie is alleen van toepassing toohello HTTP-protocol en niet toohello MQTT of AMQP-protocol.
* **Time-out** (niet-ondertekende int): deze waarde wordt weergegeven in milliseconden. Als een HTTP-aanvraag of antwoord ontvangen duurt langer dan de opgegeven tijd, verzendt vervolgens Hallo verbinding een time-out optreedt.

Hallo optie batchverwerking is belangrijk. Standaard Hallo bibliotheek ingresses gebeurtenissen afzonderlijk (één gebeurtenis is wat u te doorgeven**IoTHubClient\_LLE\_SendEventAsync**). Als de optie batchverwerking Hallo **waar**, Hallo-bibliotheek verzamelt zoveel gebeurtenissen zoals kan het Hallo-buffer (omhoog toohello maximale berichtgrootte die IoT Hub accepteert).  Hallo gebeurtenis batch wordt verzonden tooIoT Hub in één HTTP-aanroep (Hallo afzonderlijke gebeurtenissen zijn gebundeld in een JSON-matrix). Inschakelen van batchverwerking doorgaans resulteert in grote prestatiewinst omdat u bent netwerk retourbewerkingen verminderen. Bovendien vermindert bandbreedte omdat u bij het verzenden van een set HTTP-headers met een gebeurtenis batch in plaats van een set headers voor elke afzonderlijke gebeurtenis. Tenzij u een specifieke reden toodo anders hebt, moet doorgaans u tooenable batchverwerking.

## <a name="next-steps"></a>Volgende stappen
Dit artikel wordt beschreven in detail Hallo gedrag van Hallo **IoTHubClient** bibliotheek gevonden in Hallo **Azure IoT-device SDK voor C**. Met deze informatie kunt u een goed begrip van Hallo-mogelijkheden van Hallo hebt **IoTHubClient** bibliotheek. Hallo [volgende artikel](iot-hub-device-sdk-c-serializer.md) biedt vergelijkbare detail op Hallo **serialisatiefunctie** bibliotheek.

toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo [Azure IoT SDK's][lnk-sdks].

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
