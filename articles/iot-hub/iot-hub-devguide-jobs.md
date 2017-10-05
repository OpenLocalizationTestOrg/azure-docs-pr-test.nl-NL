---
title: Azure IoT Hub taken begrijpen | Microsoft Docs
description: Handleiding voor ontwikkelaars - plannen van taken uit te voeren op meerdere apparaten verbonden met uw IoT-hub. Taken kunnen bijwerken labels en gewenste eigenschappen en methoden niet aanroepen direct voor meerdere apparaten.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Taken op meerdere apparaten plannen
## <a name="overview"></a>Overzicht
Zoals beschreven door de vorige artikelen, maakt Azure IoT Hub een aantal bouwstenen ([twin apparaateigenschappen en tags] [ lnk-twin-devguide] en [methoden directe] [ lnk-dev-methods]).  Back-end-apps inschakelen normaal gesproken apparaatbeheerders en operators om te werken en te communiceren met IoT-apparaten bulksgewijs en op een gepland tijdstip.  Taken bevatten de uitvoering van twin apparaatupdates en rechtstreekse methoden op basis van een verzameling apparaten op een tijdstip planning.  Een operator gebruikt bijvoorbeeld een back-end-app die u wilt starten en bijhouden van een taak opnieuw opstarten van een reeks apparaten bij het bouwen van 43 en floor 3 tegelijk die niet aan de bewerkingen van het gebouw verstoren.

### <a name="when-to-use"></a>Wanneer gebruikt u dit?
Overweeg het gebruik van taken wanneer: een oplossing voor back-endnetwerk moet plannen en de voortgang volgen van de volgende activiteiten in een set van apparaat:

* Gewenste eigenschappen bijwerken
* Labels bijwerken
* Directe methoden aanroepen

## <a name="job-lifecycle"></a>De levenscyclus van taak
Taken worden gestart door de back-end van de oplossing en beheerd door de IoT Hub.  U kunt een taak via een URI service gerichte starten (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) en de query voor de voortgang van een taak wordt uitgevoerd via een URI service gerichte (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Zodra een taak wordt gestart, kan een query uitvoert voor taken de back-end-app vernieuwen van de status van actieve taken.

> [!NOTE]
> Wanneer u een taak gestart, namen en waarden mogen alleen US-ASCII-afdrukbare alfanumerieke behalve aanwezig in de volgende set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>De onderwerpen waarnaar wordt verwezen:
De volgende onderwerpen met naslaginformatie bieden u meer informatie over het gebruik van taken.

## <a name="jobs-to-execute-direct-methods"></a>Taken direct methoden uit te voeren
Hieronder ziet u de details van de HTTP 1.1-aanvraag voor het uitvoeren van een [directe methode] [ lnk-dev-methods] in een set van apparaten met behulp van een taak:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
De queryvoorwaarde kan ook worden voor één apparaat-Id of een lijst van apparaat-id's, zoals hieronder wordt weergegeven

**Voorbeelden**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[IoT Hub-querytaal] [ lnk-query] worden querytaal IoT-Hub in meer detail behandeld.

## <a name="jobs-to-update-device-twin-properties"></a>Taken bijwerken twin apparaateigenschappen
Hieronder ziet u de details van het HTTP 1.1-aanvraag voor het bijwerken van twin apparaateigenschappen met behulp van een taak:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>Een query uitvoert voor de voortgang van taken
Hieronder ziet u de details van het HTTP 1.1-aanvraag voor [opvragen van taken][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

De continuationToken wordt geleverd door het antwoord.  

## <a name="jobs-properties"></a>Eigenschappen van taken
Hier volgt een lijst met eigenschappen en bijbehorende beschrijvingen, die kunnen worden gebruikt voor het uitvoeren van query's voor taken of taak resultaten.

| Eigenschap | Beschrijving |
| --- | --- |
| **jobId** |Aanvraag-ID opgegeven voor de taak. |
| **startTime** |Toepassing opgegeven begintijd (ISO 8601-) voor de taak. |
| **Eindtijd** |IoT Hub opgegeven datum (ISO 8601-) voor wanneer de taak is voltooid. Geldig nadat de taak de status 'voltooid' bereikt. |
| **type** |Typen taken: |
| **scheduledUpdateTwin**: een taak die wordt gebruikt voor het bijwerken van een reeks gewenste eigenschappen of labels. | |
| **scheduledDeviceMethod**: een taak gebruikt de methode van een apparaat op een reeks horende apparaten aan te roepen. | |
| **status** |Huidige status van de taak. Mogelijke waarden voor de status van: |
| **in behandeling** : gepland en wacht om te worden opgenomen door de taak service. | |
| **geplande** : gepland voor een tijd in de toekomst. | |
| **met** : momenteel actieve taken. | |
| **geannuleerd** : taak is geannuleerd. | |
| **kan geen** : taak is mislukt. | |
| **voltooid** : taak is voltooid. | |
| **deviceJobStatistics** |Statistieken over van de taak kan worden uitgevoerd. |

**deviceJobStatistics** eigenschappen.

| Eigenschap | Beschrijving |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Het aantal apparaten in de taak. |
| **deviceJobStatistics.failedCount** |Het aantal apparaten waarop de taak is mislukt. |
| **deviceJobStatistics.succeededCount** |Het aantal apparaten waarop de taak is voltooid. |
| **deviceJobStatistics.runningCount** |Het aantal apparaten dat de taak die momenteel worden uitgevoerd. |
| **deviceJobStatistics.pendingCount** |Het aantal apparaten dat in behandeling zijn de taak uit te voeren. |

### <a name="additional-reference-material"></a>Aanvullende referentiemateriaal
Er zijn andere onderwerpen waarnaar wordt verwezen in de IoT Hub developer guide:

* [IoT-hubeindpunten] [ lnk-endpoints] beschrijft de verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.
* [Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijving van de quota die betrekking hebben op de IoT Hub-service en het gedrag bandbreedteregeling kunt verwachten wanneer u de service gebruiken.
* [Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] geeft een lijst van de taal van de verschillende SDK's u een gebruiken bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub.
* [IoT Hub-querytaal voor apparaat horende, taken en berichtroutering] [ lnk-query] beschrijft de IoT Hub-querytaal kunt u gegevens ophalen uit IoT Hub over uw apparaat horende en taken.
* [Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor het MQTT-protocol.

## <a name="next-steps"></a>Volgende stappen
Als u wilt uitproberen enkele concepten die in dit artikel wordt beschreven, kunt u mogelijk geïnteresseerd in de volgende IoT Hub-zelfstudie:

* [Planning en broadcast-taken][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
