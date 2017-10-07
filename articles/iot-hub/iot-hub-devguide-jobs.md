---
title: taken voor aaaUnderstand Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - taken toorun op meerdere apparaten plannen tooyour IoT-hub verbonden. Taken kunnen bijwerken labels en gewenste eigenschappen en methoden niet aanroepen direct voor meerdere apparaten.
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
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Taken op meerdere apparaten plannen
## <a name="overview"></a>Overzicht
Zoals beschreven door de vorige artikelen, maakt Azure IoT Hub een aantal bouwstenen ([twin apparaateigenschappen en tags] [ lnk-twin-devguide] en [methoden directe] [ lnk-dev-methods]).  Normaal gesproken back-end-apps inschakelen apparaat beheerders en operators tooupdate en communiceren met IoT-apparaten bulksgewijs en op een gepland tijdstip.  Taken inkapselen Hallo uitvoering van twin apparaatupdates en rechtstreekse methoden op basis van een verzameling apparaten op een tijdstip planning.  Een operator zou bijvoorbeeld een back-end-app die u wilt starten en bijhouden van een taak tooreboot een reeks apparaten bij het bouwen van 43 en floor 3 op een tijdstip dat verstoren toohello bewerkingen van Hallo gebouw niet zou gebruiken.

### <a name="when-toouse"></a>Wanneer toouse
Overweeg het gebruik van taken wanneer: van Hallo activiteiten in een set van apparaat na de voortgang van een oplossing voor back-end behoeften tooschedule en bijhouden:

* Gewenste eigenschappen bijwerken
* Labels bijwerken
* Directe methoden aanroepen

## <a name="job-lifecycle"></a>De levenscyclus van taak
Taken worden gestart door Hallo back-end oplossing en beheerd door de IoT Hub.  U kunt een taak via een URI service gerichte starten (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) en de query voor de voortgang van een taak wordt uitgevoerd via een URI service gerichte (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Zodra een taak wordt gestart, kunt een query uitvoert voor taken Hallo back-endserver voor apps toorefresh Hallo status van actieve taken.

> [!NOTE]
> Wanneer u een taak gestart, namen en waarden mogen alleen US-ASCII-afdrukbare alfanumerieke behalve aanwezig in de volgende set Hallo: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>De onderwerpen waarnaar wordt verwezen:
Hallo volgende verwijzing onderwerpen bieden u meer informatie over het gebruik van taken.

## <a name="jobs-tooexecute-direct-methods"></a>Taken tooexecute rechtstreekse methoden
Hallo volgt Hallo HTTP 1.1-gegevens voor de aanvraag voor het uitvoeren van een [directe methode] [ lnk-dev-methods] in een set van apparaten met behulp van een taak:

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
Hallo queryvoorwaarde kan ook worden voor één apparaat-Id of een lijst van apparaat-id's zoals hieronder wordt weergegeven

**Voorbeelden**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[IoT Hub-querytaal] [ lnk-query] worden querytaal IoT-Hub in meer detail behandeld.

## <a name="jobs-tooupdate-device-twin-properties"></a>Taken tooupdate apparaateigenschappen twin
Hallo volgende is Hallo HTTP 1.1-aanvraagdetails voor het bijwerken van twin apparaateigenschappen met behulp van een taak:

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
Hallo volgt Hallo details voor HTTP 1.1-aanvraag voor [opvragen van taken][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

Hallo continuationToken wordt geleverd door het Hallo-antwoord.  

## <a name="jobs-properties"></a>Eigenschappen van taken
Hallo Hieronder volgt een lijst met eigenschappen en bijbehorende beschrijvingen, die kunnen worden gebruikt voor het uitvoeren van query's voor taken of taak resultaten.

| Eigenschap | Beschrijving |
| --- | --- |
| **jobId** |Aanvraag-ID opgegeven voor Hallo-taak. |
| **startTime** |Toepassing opgegeven begintijd (ISO 8601-) voor Hallo-taak. |
| **Eindtijd** |IoT Hub opgegeven datum (ISO 8601-) als Hallo-taak is voltooid. Geldig nadat de taak Hallo Hallo 'voltooid' status bereikt. |
| **type** |Typen taken: |
| **scheduledUpdateTwin**: een taak gebruikt tooupdate een reeks gewenste eigenschappen of labels. | |
| **scheduledDeviceMethod**: een taak gebruikt tooinvoke een methode van het apparaat van een reeks horende apparaten. | |
| **status** |Huidige status van het Hallo-taak. Mogelijke waarden voor de status van: |
| **in behandeling** : gepland en wachten toobe die zijn opgepikt door Hallo taak service. | |
| **geplande** : gepland voor een tijd in toekomstige Hallo. | |
| **met** : momenteel actieve taken. | |
| **geannuleerd** : taak is geannuleerd. | |
| **kan geen** : taak is mislukt. | |
| **voltooid** : taak is voltooid. | |
| **deviceJobStatistics** |Statistieken over Hallo taakuitvoering. |

**deviceJobStatistics** eigenschappen.

| Eigenschap | Beschrijving |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Het aantal apparaten in het Hallo-taak. |
| **deviceJobStatistics.failedCount** |Het aantal apparaten waarop Hallo-taak is mislukt. |
| **deviceJobStatistics.succeededCount** |Het aantal apparaten waarbij Hallo-taak is voltooid. |
| **deviceJobStatistics.runningCount** |Het aantal apparaten dat Hallo taak momenteel worden uitgevoerd. |
| **deviceJobStatistics.pendingCount** |Het aantal apparaten met wachtende toorun Hallo taak. |

### <a name="additional-reference-material"></a>Aanvullende referentiemateriaal
Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:

* [IoT-hubeindpunten] [ lnk-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.
* [Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijft Hallo quota's die van toepassing toohello service IoT Hub en bandbreedteregeling gedrag tooexpect Hallo wanneer u Hallo-service gebruiken.
* [Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] lijsten Hallo verschillende taal SDK's u een gebruiken bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub.
* [IoT Hub-querytaal voor apparaat horende, taken en berichtroutering] [ lnk-query] Hallo querytaal IoT-Hub kunt u informatie van de tooretrieve uit IoT Hub over uw apparaat horende en taken worden beschreven.
* [Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor Hallo MQTT protocol.

## <a name="next-steps"></a>Volgende stappen
Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub-zelfstudie:

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
