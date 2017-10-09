---
title: ID-register van aaaUnderstand Hallo Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - beschrijving van Hallo id-register IoT Hub en hoe toouse het toomanage uw apparaten. Bevat informatie over Hallo importeren en exporteren van apparaat-id's in bulk.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>Hallo identiteitenregister van uw IoT-hub begrijpen

Elke iothub heeft een register-id's die worden opgeslagen informatie over Hallo apparaten tooconnect toohello iothub toegestaan. Voordat een apparaat verbinding tooan IoT-hub maken kunt, moet er een vermelding voor het apparaat in de id-register Hallo iothub. Een apparaat moet ook worden geverifieerd bij Hallo op basis van de referenties die zijn opgeslagen in het identiteitenregister Hallo IoT-hub.

Hallo apparaat-ID is opgeslagen in het identiteitenregister Hallo is hoofdlettergevoelig.

Hallo id-register is op een hoog niveau een REST-compatibele verzameling apparaatbronnen identiteit. Wanneer u een vermelding in het identiteitenregister Hallo toevoegt, maakt de IoT Hub een set resources zoals Hallo wachtrij met onderweg cloud-naar-apparaat-berichten per apparaat.

### <a name="when-toouse"></a>Wanneer toouse

Hallo identiteitsregister gebruiken als u wilt:

* Inrichten van apparaten die verbinding maken met tooyour IoT-hub.
* Per apparaat toegang tooyour van de hub apparaat gerichte eindpunten beheren.

> [!NOTE]
> Hallo identiteitsregister bevat geen toepassingsspecifieke metagegevens.

## <a name="identity-registry-operations"></a>Registerbewerkingen voor identiteit

Hallo id-register IoT Hub beschrijft Hallo volgende bewerkingen:

* Apparaat-id maken
* Apparaat-ID bijwerken
* Apparaat-id door-ID ophalen
* Verwijderen van apparaat-id
* Lijst van too1000 identiteiten
* Exporteren van alle identiteiten tooAzure blob-opslag
* Identiteiten importeren uit Azure blob-opslag

Alle deze bewerkingen kunt optimistische gelijktijdigheid van taken, zoals opgegeven in [RFC7232][lnk-rfc7232].

> [!IMPORTANT]
> Hallo alleen manier tooretrieve alle identiteiten in het identiteitenregister een IoT-hub is toouse hello [exporteren] [ lnk-export] functionaliteit.

Een id-register van IoT-Hub:

* Bevat geen metagegevens voor de toepassing.
* Zoals een woordenboek kan toegankelijk via Hallo **deviceId** als Hallo-sleutel.
* Ondersteunt geen expressieve query's.

Een IoT-oplossing heeft doorgaans een afzonderlijk archief oplossings-specifieke die toepassingsspecifieke metagegevens bevat. Bijvoorbeeld: hello oplossings-specifieke opslaan in een oplossing voor smart gebouw legt Hallo ruimte waarin een temperatuursensor wordt geïmplementeerd.

> [!IMPORTANT]
> Hallo identiteitsregister alleen gebruiken voor het beheer van apparaten en inrichten van operations. Hoge doorvoersnelheid operations tijdens runtime moeten niet afhankelijk is van het uitvoeren van bewerkingen in het identiteitenregister Hallo. De verbindingsstatus Hallo van een apparaat controleren voordat een opdracht verzonden is bijvoorbeeld niet een ondersteunde patroon. Zorg ervoor dat toocheck hello [tarieven beperking] [ lnk-quotas] voor Hallo id-register en Hallo [apparaat heartbeat] [ lnk-guidance-heartbeat] patroon.

## <a name="disable-devices"></a>Apparaten uitschakelen

U kunt apparaten uitschakelen door het bijwerken van Hallo **status** eigenschap van een identiteit in het identiteitenregister Hallo. Normaal gesproken gebruikt u deze eigenschap in twee scenario's:

* Tijdens een inrichtingsproces orchestration. Zie voor meer informatie [apparaten inrichten][lnk-guidance-provisioning].
* Als u om welke reden overwegen een apparaat is geknoeid of niet-geautoriseerde is geworden.

## <a name="import-and-export-device-identities"></a>Importeren en exporteren van apparaat-id 's

U kunt apparaat-id's in bulk exporteren uit het register van de identiteit van een IoT-hub, met behulp van asynchrone bewerkingen op Hallo [IoT Hub resource provider-eindpunt][lnk-endpoints]. Uitvoer zijn langlopende taken die gebruikmaken van een klant opgegeven blob-container toosave apparaat identiteitsgegevens lezen uit Hallo id-register.

U kunt de apparaat-id's in de id-register bulksgewijs tooan iothub van importeren met behulp van asynchrone bewerkingen op Hallo [IoT Hub resource provider-eindpunt][lnk-endpoints]. Invoer zijn langlopende taken die gegevens gebruiken voor een klant opgegeven blob-container toowrite apparaat identiteitsgegevens in het identiteitsregister Hallo.

* Zie voor gedetailleerde informatie over Hallo importeren en exporteren API's, [resourceprovider IoT Hub REST-API's][lnk-resource-provider-apis].
* toolearn meer informatie over het uitvoeren importeren en exporteren van taken, Zie [bulksgewijs beheer van IoT Hub apparaat-id's][lnk-bulk-identity].

## <a name="device-provisioning"></a>Mobiele apparaten inrichten

Hallo apparaatgegevens die een bepaalde IoT-oplossing zijn opgeslagen, is afhankelijk van Hallo specifieke vereisten van deze oplossing. Maar ten minste een oplossing moet opslaan, apparaat-id's en verificatiesleutels. Azure IoT Hub bevat een identity-registry die waarden voor elk apparaat zoals-id's en verificatiesleutels statuscodes kunt opslaan. Een oplossing kunt andere Azure-services zoals tabelopslag, blob-opslag of Cosmos DB toostore geen apparaatgegevens meer gebruiken.

*Mobiele apparaten inrichten* Hallo-proces voor het toevoegen van Hallo initiële gegevensarchieven toohello in uw oplossing is. een nieuwe apparaat tooconnect tooyour hub tooenable, moet u een apparaat-ID en sleutels toohello id-register IoT Hub toevoegen. Als onderdeel van Hallo inrichtingsproces, moet u mogelijk tooinitialize apparaatspecifieke gegevens in andere archieven oplossing.

## <a name="device-heartbeat"></a>Apparaat heartbeat

Hallo id-register IoT Hub bevat een veld met de naam **connectionState**. Gebruik alleen Hallo **connectionState** veld tijdens de ontwikkeling en foutopsporing. IoT-oplossingen moeten geen query uitvoeren op Hallo veld tijdens runtime. Bijvoorbeeld geen Hallo query **connectionState** veld toocheck als een apparaat is verbonden alvorens u een bericht cloud-naar-apparaat of een SMS-bericht verzenden.

Als uw IoT-oplossing tooknow moet als een apparaat is verbonden, moet u Hallo implementeren *heartbeat patroon*.

In Hallo heartbeat patroon verzendt Hallo apparaat apparaat-naar-cloudberichten ten minste één keer voor elke vaste hoeveelheid tijd (bijvoorbeeld ten minste één keer per uur). Dus zelfs als een apparaat geen eventuele toosend gegevens, deze nog steeds een leeg apparaat-naar-cloud bericht verzenden (meestal met een eigenschap die deze als een heartbeat identificeert) Hallo-service-zijde onderhoudt Hallo oplossing een kaart met de laatste heartbeat Hallo ontvangen voor elk apparaat. Als het Hallo-oplossing niet binnen de tijd van apparaat Hallo Hallo verwacht heartbeat-bericht ontvangt, wordt ervan uitgegaan dat er een probleem met Hallo-apparaat is.

Een complexere implementatie kan Hallo informatie bevatten van [operations bewaking] [ lnk-devguide-opmon] tooidentify-apparaten die u probeert tooconnect of communiceren, maar mislukken. Wanneer u Hallo heartbeat patroon implementeert, zorg ervoor dat toocheck [IoT Hub quota en vertragingen][lnk-quotas].

> [!NOTE]
> Als u een IoT-oplossing maakt gebruik van Hallo verbinding status uitsluitend toodetermine of toosend-cloud-naar-apparaat-berichten en berichten worden niet broadcast toolarge sets van apparaten, kunt u een eenvoudigere Hallo *korte verlooptijd* patroon. Dit patroon realiseert Hallo hetzelfde resultaat als een apparaat verbinding status register via Hallo heartbeat patroon, terwijl het efficiënter wordt onderhouden. Als u een bericht bevestigingen aanvraagt, IoT-Hub u kunt een melding over welke apparaten kunnen tooreceive berichten zijn en welke niet.

## <a name="device-lifecycle-notifications"></a>Meldingen over de levenscyclus van apparaat

IoT Hub kan uw IoT-oplossing melden wanneer een apparaat-id wordt gemaakt of verwijderd door het verzenden van meldingen over de levenscyclus van apparaat. toodo, uw IoT-oplossing moet een route toocreate en tooset Hallo gegevensbron gelijk te*DeviceLifecycleEvents*. Standaard geen lifecycle meldingen worden verzonden, dat wil zeggen, geen dergelijke routes vooraf bestaan. melding het Hallo-bericht bevat eigenschappen en hoofdtekst.

Eigenschappen: Eigenschappen bericht worden voorafgegaan door Hallo `'$'` symbool.

| Naam | Waarde |
| --- | --- |
$content-type | application/json |
$iothub-enqueuedtime |  Tijd waarop het Hallo-bericht is verzonden |
$iothub-bericht-bron | deviceLifecycleEvents |
$content-codering | UTF-8 |
opType | **createDeviceIdentity** of **deleteDeviceIdentity** |
hubName | Naam van de IoT-Hub |
deviceId | Hallo-apparaat-ID |
operationTimestamp | ISO8601 tijdstempel van bewerking |
bericht-iothub-schema | deviceLifecycleNotification |

Hoofdtekst: In deze sectie is in JSON-indeling en Hallo twin Hallo gemaakt van apparaat-id vertegenwoordigt. Bijvoorbeeld:

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a>De onderwerpen waarnaar wordt verwezen:

Hallo bieden volgende naslagonderwerpen u meer informatie over het Hallo-id-register.

## <a name="device-identity-properties"></a>Identiteitseigenschappen van apparaat

Apparaat-id's worden weergegeven als JSON-documenten met Hallo volgende eigenschappen:

| Eigenschap | Opties | Beschrijving |
| --- | --- | --- |
| deviceId |vereist alleen-lezen op updates |Een hoofdlettergevoelige tekenreeks (omhoog too128 tekens lang) van ASCII-7-bits alfanumerieke tekens + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| generationId |vereist alleen-lezen |Een IoT hub is gegenereerd, hoofdlettergevoelig tekenreeks up too128 tekens bevatten. Deze waarde is gebruikte toodistinguish apparaten met Hallo dezelfde **deviceId**wanneer ze zijn verwijderd en opnieuw gemaakt. |
| ETag |vereist alleen-lezen |Een tekenreeks voor een zwakke ETag Hallo apparaat-id, conform [RFC7232][lnk-rfc7232]. |
| auth |Optioneel |Een samengestelde-object met de informatie en beveiliging materiaal verificatie. |
| auth.symkey |Optioneel |Een samengestelde-object met een primaire en secundaire sleutel, opgeslagen in base64-indeling. |
| status |Vereist |Een indicator toegang. Kan **ingeschakeld** of **uitgeschakelde**. Als **ingeschakeld**, Hallo apparaat tooconnect is toegestaan. Als **uitgeschakelde**, dit apparaat geen toegang tot een willekeurig eindpunt apparaat gerichte. |
| statusReason |Optioneel |Een 128 tekens lang tekenreeks winkels Hallo daarom voor Hallo identiteit Apparaatstatus. Alle UTF-8 tekens zijn toegestaan. |
| statusUpdateTime |alleen-lezen |Een tijdelijke aanduiding Hallo datum en tijd van laatste statusupdate hello wordt weergegeven. |
| connectionState |alleen-lezen |Een veld dat aangeeft verbindingsstatus: beide **verbonden** of **verbroken**. Dit veld vertegenwoordigt Hallo Iothub-weergave van de verbindingsstatus Hallo-apparaat. **Belangrijke**: dit veld mag alleen worden gebruikt voor ontwikkeling/foutopsporing doeleinden. Hallo verbindingsstatus wordt alleen voor apparaten met behulp van protocollen MQTT of AMQP zijn bijgewerkt. Bovendien is het gebaseerd op protocolniveau pings (MQTT pings of AMQP pings) en er een maximale vertraging van slechts 5 minuten. Daarom kunnen er valse positieven, zoals apparaten gerapporteerd als verbonden, maar die niet zijn verbonden. |
| connectionStateUpdatedTime |alleen-lezen |Hallo datum en de status van laatste tijd Hallo verbinding met een tijdelijke indicator is bijgewerkt. |
| lastActivityTime |alleen-lezen |Een tijdelijke aanduiding met Hallo datum en de laatste tijd Hallo apparaat is verbonden, ontvangen of een bericht verzonden. |

> [!NOTE]
> Verbindingsstatus kan alleen Hallo IoT Hub-weergave van Hallo status van Hallo verbinding vertegenwoordigen. Hiermee wordt de status toothis mag worden uitgesteld, afhankelijk van de netwerkomstandigheden en configuraties.

## <a name="additional-reference-material"></a>Aanvullende referentiemateriaal

Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:

* [IoT-hubeindpunten] [ lnk-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.
* [Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijft Hallo quota's en beperking gedrag die van toepassing zijn toohello service IoT Hub.
* [Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] lijsten Hallo verschillende taal kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub SDK's.
* [IoT Hub-querytaal] [ lnk-query] Hallo querytaal tooretrieve informatie uit IoT Hub over uw apparaat horende taken kunt u hierin wordt beschreven.
* [Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor Hallo MQTT protocol.

## <a name="next-steps"></a>Volgende stappen

Nu hebt u geleerd hoe identiteitsregister van toouse Hallo Iothub, hebt u mogelijk geïnteresseerd in de volgende onderwerpen voor IoT Hub developer guide Hallo:

* [Beheer toegang tooIoT Hub][lnk-devguide-security]
* [Gebruik Apparaatstatus horende toosynchronize en configuraties][lnk-devguide-device-twins]
* [Een directe methode aangeroepen voor een apparaat][lnk-devguide-directmethods]
* [Taken plannen op meerdere apparaten][lnk-devguide-jobs]

Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub-zelfstudie:

* [Aan de slag met Azure IoT Hub][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
