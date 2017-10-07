---
title: aaaRemote bewaking van de vooraf geconfigureerde oplossing overzicht | Microsoft Docs
description: Een beschrijving van hello Azure IoT vooraf geconfigureerde oplossing voor externe controle en de bijbehorende architectuur.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>Walkthrough over vooraf geconfigureerde oplossing voor externe controle

Hallo externe controle IoT Suite [vooraf geconfigureerde oplossing] [ lnk-preconfigured-solutions] is een implementatie van een end-to-end-bewakingsoplossing voor meerdere machines die worden uitgevoerd op externe locaties. Hallo oplossing combineert belangrijke Azure-services tooprovide een algemene implementatie van Hallo bedrijfsscenario. U kunt Hallo oplossing gebruiken als een beginpunt voor uw eigen implementatie en [aanpassen] [ lnk-customize] het toomeet uw eigen specifieke zakelijke vereisten.

In dit artikel worden enkele van de belangrijkste elementen van de Hallo van Hallo remote monitoring solution tooenable toounderstand u hoe het werkt. Deze kennis helpt u bij:

* Los problemen met het Hallo-oplossing.
* Plannen hoe toocustomize toohello oplossing toomeet uw eigen specifieke vereisten. 
* Het ontwerpen van uw eigen IoT-oplossing die gebruikmaakt van Azure-services.

## <a name="logical-architecture"></a>Logische architectuur

Hallo volgende diagram geeft een overzicht van de logische onderdelen van de Hallo van Hallo vooraf geconfigureerde oplossing:

![Logische architectuur](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>Gesimuleerde apparaten

In Hallo vooraf geconfigureerde oplossing vertegenwoordigt Hallo gesimuleerde apparaat een koelapparaat (zoals een airconditioner of faciliteit lucht verwerking eenheid). Wanneer u Hallo vooraf geconfigureerde oplossing implementeert, u ook automatisch inrichten vier gesimuleerde apparaten die worden uitgevoerd in een [Azure webtaak][lnk-webjobs]. Hallo gesimuleerde apparaten eenvoudiger voor u tooexplore Hallo gedrag van Hallo oplossing zonder Hallo nodig toodeploy fysieke apparaten. een echte fysiek apparaat toodeploy Zie Hallo [verbinding maken met uw vooraf geconfigureerde oplossing voor externe controle apparaat toohello] [ lnk-connect-rm] zelfstudie.

### <a name="device-to-cloud-messages"></a>Apparaat-naar-cloud-berichten

Elk gesimuleerd apparaat kunt verzenden Hallo-bericht typen tooIoT Hub te volgen:

| Bericht | Beschrijving |
| --- | --- |
| Opstarten |Wanneer het Hallo-apparaat wordt gestart, stuurt een **apparaatgegevens** -bericht met informatie over zichzelf toohello back-end. Deze gegevens omvatten Hallo apparaat-id en een lijst met opdrachten Hallo en methoden Hallo apparaat worden ondersteund. |
| Aanwezigheid |Een apparaat periodiek verzendt een **aanwezigheid** tooreport bericht of Hallo apparaat Hallo aanwezigheid van een sensor kunt detecteren. |
| Telemetrie |Een apparaat periodiek verzendt een **telemetrie** bericht die gesimuleerde waarden voor Hallo temperatuur en vochtigheid verzameld van Hallo apparaat rapporteert de sensoren gesimuleerd. |

> [!NOTE]
> Hallo oplossing slaat Hallo lijst met opdrachten die worden ondersteund door Hallo-apparaat in een Cosmos-DB-database en niet in Hallo apparaat twin.

### <a name="properties-and-device-twins"></a>Eigenschappen en apparaatdubbels

Hallo gesimuleerde apparaten verzenden Hallo na apparaat eigenschappen toohello [twin] [ lnk-device-twins] in Hallo IoT-hub als *eigenschappen gerapporteerd*. Hallo apparaat verzendt gerapporteerd eigenschappen bij het opstarten en in reactie tooa **Changedevicestate** opdracht of methode.

| Eigenschap | Doel |
| --- | --- |
| Config.TelemetryInterval | Frequentie (seconden) Hallo apparaat verzendt telemetrie |
| Config.TemperatureMeanValue | Geeft de gemiddelde waarde Hallo voor Hallo gesimuleerde temperatuur telemetrie |
| Device.DeviceID |-ID die is opgegeven of is toegewezen als een apparaat is gemaakt in Hallo-oplossing |
| Device.DeviceState | Is gerapporteerd door het Hallo-apparaat |
| Device.CreatedTime |Tijd Hallo apparaat is gemaakt in het Hallo-oplossing |
| Device.StartupTime |Tijd Hallo apparaat is gestart |
| Device.LastDesiredPropertyChange |Hallo-versienummer van de laatste gewenste eigenschap Hallo wijzigen |
| Device.Location.Latitude |Locatie van de breedte van Hallo-apparaat |
| Device.Location.Longitude |Locatie van de lengtegraad van Hallo-apparaat |
| System.Manufacturer |Fabrikant van apparaat |
| System.ModelNumber |Modelnummer van het Hallo-apparaat |
| System.SerialNumber |Serienummer van Hallo-apparaat |
| System.FirmwareVersion |Huidige versie van de firmware op Hallo-apparaat |
| System.Platform |Platformarchitectuur van Hallo-apparaat |
| System.Processor |Processor actieve Hallo-apparaat |
| System.InstalledRAM |Hoeveelheid RAM-geheugen op Hallo-apparaat |

Hallo simulator voorziet deze eigenschappen in de gesimuleerde apparaten van voorbeeldwaarden. Elke keer Hallo simulator een gesimuleerd apparaat, het Hallo-apparaat initialiseert rapporteert Hallo vooraf gedefinieerde metagegevens tooIoT Hub als gemelde eigenschappen. Gerapporteerde eigenschappen kunnen alleen worden bijgewerkt door Hallo-apparaat. een gerapporteerde eigenschap toochange, stelt u een gewenste eigenschap in de portal van de oplossing. Hallo verantwoordelijkheid van Hallo van het apparaat is:

1. Periodiek de gewenste eigenschappen ophalen uit Hallo iothub.
2. Werk de configuratie waarbij de eigenschapwaarde Hallo gewenst.
3. Hallo nieuwe waarde back toohello hub als een gerapporteerde eigenschap verzenden.

Vanuit het dashboard van de oplossing hello, kunt u met *gewenst eigenschappen* tooset eigenschappen op een apparaat met behulp van Hallo [apparaat twin][lnk-device-twins]. Normaal gesproken leest een apparaat een gewenste eigenschapswaarde van Hallo hub tooupdate die de interne status en het rapport Hallo weer als een eigenschap gemeld wijzigen.

> [!NOTE]
> Hallo gesimuleerd apparaatcode gebruikt alleen Hallo **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** gewenste eigenschappen tooupdate Hallo eigenschappen teruggestuurd gerapporteerd tooIoT Hub. Alle andere gewenste eigenschap wijzigingsaanvragen worden genegeerd in Hallo gesimuleerde apparaat.

### <a name="methods"></a>Methoden

Hallo gesimuleerde apparaten kunnen verwerken Hallo volgende methoden ([methoden directe][lnk-direct-methods]) aangeroepen vanuit de oplossingsportal Hallo via Hallo iothub:

| Methode | Beschrijving |
| --- | --- |
| InitiateFirmwareUpdate |Hiermee geeft u Hallo apparaat tooperform een firmware-update |
| Opnieuw opstarten |Hiermee geeft u Hallo apparaat tooreboot |
| FactoryReset |Hiermee geeft u een van de fabrieksinstellingen van Hallo apparaat tooperform |

Bepaalde methoden voor het gebruik gemelde eigenschappen tooreport op uitgevoerd. Bijvoorbeeld, Hallo **InitiateFirmwareUpdate** methode actieve Hallo update asynchroon op Hallo apparaat simuleert. Hallo-methode retourneert onmiddellijk op Hallo-apparaat, terwijl de Hallo asynchrone taak nog steeds statusupdates terug toosend toohello oplossing dashboard gebruikt gerapporteerd eigenschappen.

### <a name="commands"></a>Opdrachten

Hallo gesimuleerde apparaten kunnen verwerken Hallo opdrachten (cloud-naar-apparaat-berichten) verzonden vanaf de oplossingsportal Hallo via Hallo iothub te volgen:

| Opdracht | Beschrijving |
| --- | --- |
| PingDevice |Verzendt een *ping* toohello apparaat toocheck het actief is |
| StartTelemetry |Start Hallo apparaat verzenden van telemetrie |
| StopTelemetry |Stopt Hallo apparaat verzenden van telemetriegegevens |
| ChangeSetPointTemp |Wijzigingen Hallo set puntwaarde rond welke Hallo willekeurige gegevens worden gegenereerd |
| DiagnosticTelemetry |Triggers Hallo apparaat simulator toosend een extra telemetriewaarde (externalTemp) |
| ChangeDeviceState |Een eigenschap uitgebreide status voor Hallo apparaat wijzigingen en Hallo bericht met apparaatgegevens vanaf Hallo apparaat verzenden |

> [!NOTE]
> Zie [Cloud-to-device communications guidance][lnk-c2d-guidance] (Richtlijnen voor communicatie tussen cloud en apparaat) voor een vergelijking van deze opdrachten (berichten van cloud naar apparaat) en methoden (directe methoden).

## <a name="iot-hub"></a>IoT Hub

Hallo [IoT-hub] [ lnk-iothub] opgenomen in de cloud Hallo Hallo apparaten verzonden gegevens en maakt het beschikbaar toohello Azure Stream Analytics (ASA)-taken. Elke stream ASA-taak maakt gebruik van een afzonderlijke IoT Hub consumer groep tooread Hallo stroom van berichten van uw apparaten.

Hallo IoT-hub in Hallo oplossing ook:

- Onderhoudt een identity-registry die Hallo-id's en verificatiesleutels van alle Hallo apparaten toegestaan tooconnect toohello portal worden opgeslagen. U kunt inschakelen en uitschakelen van apparaten via Hallo id-register.
- Opdrachten verzendt tooyour apparaten namens de oplossingsportal Hallo.
- Methoden op uw apparaten aanroept namens de oplossingsportal Hallo.
- Onderhoudt apparaatdubbels voor alle geregistreerde apparaten. Een apparaat-twin slaat Hallo eigenschapswaarden gemeld door een apparaat. Een apparaat-twin slaat ook gewenste eigenschappen instellen in de oplossingsportal Hallo voor Hallo apparaat tooretrieve wanneer deze vervolgens verbinding maakt.
- Planningen taken tooset eigenschappen voor meerdere apparaten of methoden op meerdere apparaten.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

In de oplossing, voor externe controle Hallo [Azure Stream Analytics] [ lnk-asa] (ASA) verzendt de apparaat-berichten ontvangen door Hallo IoT hub tooother back-end-onderdelen voor de verwerking of opslag. Andere ASA-jobs uitvoeren specifieke functies op basis van inhoud van het Hallo-berichten Hallo.

**Taak 1: Apparaatgegevens** filtert berichten met apparaatgegevens uit Hallo binnenkomende berichtenstroom en stuurt deze tooan Event Hub-eindpunt. Een apparaat verzendt berichten met apparaatgegevens bij het opstarten en in reactie tooa **SendDeviceInfo** opdracht. Deze taak wordt gebruikgemaakt van Hallo query definitie tooidentify na **apparaatgegevens** berichten:

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

Deze taak wordt de uitvoer tooan Event Hub verzendt voor verdere verwerking.

**Taak 2: regels** evalueren de binnenkomende telemetriegegevens over temperatuur en vochtigheid aan de hand van de drempelwaarden voor elk apparaat. Drempelwaarden zijn in Hallo regeleditor die beschikbaar zijn in de oplossingsportal Hallo ingesteld. Elk koppel apparaat/waarde wordt per tijdstempel opgeslagen in een blob die met Stream Analytics wordt gelezen als **referentiegegevens**. Hallo taak vergelijkt elke niet-lege waarde tegen Hallo ingestelde drempelwaarde voor Hallo-apparaat. Als deze groter is dan Hallo ' >' voorwaarde, Hallo taak voert een **alarm** gebeurtenis die dat Hallo drempelwaarde aangeeft wordt overschreden en biedt Hallo-apparaat, waarde en timestamp-waarden. Deze taak maakt gebruik van Hallo query definitie tooidentify telemetrieberichten die moeten worden geactiveerd door een waarschuwing te volgen:

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

Hallo taak verzendt de uitvoer tooan Event Hub voor verdere verwerking en details van de opslag van elke waarschuwing tooblob opslaat uit waarbij de oplossingsportal Hallo Hallo waarschuwingsgegevens kan lezen.

**Taak 3: Telemetrie** is van invloed op Hallo binnenkomende apparaat telemetriestroom op twee manieren. Hallo verzendt eerst alle telemetrieberichten van Hallo apparaten toopersistent blob-opslag voor langdurige opslag. Hallo berekent een gemiddelde, de minimale en maximale vochtigheid gedurende een sliding window van vijf minuten en verzendt deze gegevens tooblob opslag tweede verbruik. Hallo oplossingsportal leest Hallo telemetrische gegevens uit blob storage toopopulate Hallo grafieken. Deze taak maakt gebruik van Hallo volgende querydefinitie:

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Event Hubs

Hallo **apparaatgegevens** en **regels** ASA-jobs uitvoer hun gegevens tooEvent Hubs tooreliably doorsturen op toohello **Gebeurtenisprocessor** in Hallo webtaak wordt uitgevoerd.

## <a name="azure-storage"></a>Azure-opslag

Hallo-oplossing gebruikt Azure blob storage toopersist alle Hallo ruwe en het samengevatte telemetriegegevens van Hallo apparaten in Hallo-oplossing. Hallo portal leest Hallo telemetrische gegevens uit blob storage toopopulate Hallo grafieken. toodisplay waarschuwingen, oplossingsportal Hallo Hallo gegevens leest uit blob-opslag die records wanneer telemetrie waarden overschreden Hallo drempelwaarden geconfigureerd. Hallo-oplossing gebruikt ook blob storage toorecord Hallo drempelwaarden die u in de oplossingsportal Hallo instellen.

## <a name="webjobs"></a>Webtaken

Bovendien toohosting Hallo apparaat simulatoren Hallo webtaken in Hallo oplossing ook host Hallo **Gebeurtenisprocessor** uitgevoerd in een Azure-webtaak die verantwoordelijk is voor reacties op opdrachten. Antwoord berichten tooupdate Hallo apparaat opdracht opdrachtgeschiedenis (opgeslagen in Hallo Cosmos DB database) wordt gebruikt.

## <a name="cosmos-db"></a>Cosmos DB

Hallo-oplossing gebruikt een Cosmos-DB toostore databasegegevens over Hallo apparaten verbonden toohello oplossing. Deze informatie omvat Hallo geschiedenis van opdrachten toodevices verzonden vanaf de oplossingsportal hello en methoden die worden aangeroepen vanuit de portal van de oplossing Hallo.

## <a name="solution-portal"></a>Oplossingsportal

Hallo oplossingsportal is een web-app geïmplementeerd als onderdeel van Hallo vooraf geconfigureerde oplossing. Hallo belangrijkste pagina's in de oplossingsportal Hallo zijn Hallo dashboard en de lijst met Hallo-apparaten.

### <a name="dashboard"></a>Dashboard

Deze pagina in Hallo web-app maakt gebruik van PowerBI javascript-besturingselementen (Zie [PowerBI-visuals Reports](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetriegegevens van Hallo-apparaten. Hallo-oplossing gebruikt Hallo ASA telemetrie taak toowrite Hallo telemetrie tooblob opslag van gegevens.

### <a name="device-list"></a>Lijst met apparaten

U kunt via deze pagina in de oplossingsportal Hallo:

* Nieuwe apparaten inrichten. Deze actie stelt Hallo unieke apparaat-id en verificatiesleutel Hallo genereert. Informatie over Hallo apparaat tooboth Hallo id-register IoT Hub en Hallo oplossings-specifieke Cosmos-DB-database geschreven.
* Apparaateigenschappen beheren. Deze actie omvat het weergeven van bestaande eigenschappen en het bijwerken met nieuwe eigenschappen.
* Opdrachten tooa apparaat verzenden.
* Hallo opdrachtgeschiedenis voor een apparaat weergeven.
* Apparaten in- en uitschakelen.

## <a name="next-steps"></a>Volgende stappen

Hallo bieden volgende TechNet-blogberichten meer informatie over vooraf geconfigureerde oplossing voor externe controle Hallo:

* [IoT Suite - Under Hallo schermen - externe controle](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (IoT Suite - externe controle - live- en gesimuleerde apparaten toevoegen)](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

U kunt blijven aan de slag met IoT Suite door te lezen Hallo artikelen te volgen:

* [Verbinding maken met uw apparaat toohello vooraf geconfigureerde oplossing voor externe controle][lnk-connect-rm]
* [Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
