---
title: aaaUse metrische gegevens toomonitor Azure IoT Hub | Microsoft Docs
description: Toouse Azure IoT Hub metrische gegevens tooassess en monitor Hallo hoe algemene status van uw IoT-hubs.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>Inzicht in IoT Hub metrische gegevens
IoT Hub metrische gegevens kunt u betere gegevens over Hallo toestand van hello Azure IoT-resources in uw Azure-abonnement. IoT Hub metrische gegevens inschakelen u tooassess algemene status van Hallo service IoT Hub en Hallo apparaten Hallo verbonden tooit. Gebruikersgerichte statistieken zijn belangrijk omdat ze u zien wat er gebeurt met uw IoT hub help hoofdoorzaak problemen met en helpen zonder toocontact ondersteuning van Azure.

Metrische gegevens zijn standaard ingeschakeld. U kunt IoT Hub metrische gegevens van hello Azure-portal bekijken.

## <a name="how-tooview-iot-hub-metrics"></a>Hoe tooview IoT Hub metrische gegevens
1. Een iothub maken. U vindt instructies over het toocreate een IoT-hub in Hallo [aan de slag] [ lnk-get-started] handleiding.
2. Open Hallo-blade van uw IoT-hub. Van daaruit, klikt u op **metrische gegevens**.
   
    ![][1]
3. U kunt Hallo metrische gegevens blade Hallo metrische gegevens weergeven voor uw iothub en aangepaste weergaven van de metrische gegevens maken. U kunt toosend uw metrische gegevens tooan Event Hubs-eindpunt of een Azure Storage-account door te klikken op **diagnostische instellingen**.
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>IoT Hub metrische gegevens en hoe toouse ze
IoT Hub biedt verschillende metrische gegevens toogive u een overzicht van de status van uw hub en Hallo Hallo totale aantal verbonden apparaten. U kunt gegevens uit meerdere metrische gegevens toopaint een grotere afbeelding van Hallo status van de IoT-hub Hallo combineren. Hallo volgende tabel beschrijft Hallo metrische gegevens elke IoT-hub houdt en hoe elke metriek is gekoppeld toohello algehele status van Hallo IoT-hub.

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Telemetrie-bericht verzenden pogingen|Count|Totaal|Aantal pogingen tot toobe voor telemetrie voor apparaat-naar-cloud-berichten verzonden tooyour IoT-hub|
|d2c.telemetry.ingress.Success|Telemetrieberichten|Count|Totaal|Aantal voor apparaat-naar-cloud-telemetrieberichten verzonden tooyour IoT-hub|
|c2d.Commands.egress.complete.Success|Opdrachten voltooid|Count|Totaal|Aantal opdrachten voor cloud-naar-apparaat is voltooid door Hallo-apparaat|
|c2d.Commands.egress.Abandon.Success|Opdrachten afgebroken|Count|Totaal|Aantal afgebroken door Hallo apparaat opdrachten voor cloud-naar-apparaat|
|c2d.Commands.egress.Reject.Success|Opdrachten geweigerd|Count|Totaal|Aantal opdrachten voor cloud-naar-apparaat geweigerd door het Hallo-apparaat|
|devices.totalDevices|Totaal aantal apparaten|Count|Totaal|Aantal apparaten geregistreerd tooyour IoT-hub|
|devices.connectedDevices.allProtocol|Verbonden apparaten|Count|Totaal|Het aantal apparaten zijn verbonden tooyour IoT-hub|
|d2c.telemetry.egress.Success|Telemetrieberichten geleverd|Count|Totaal|Aantal keren dat berichten zijn geschreven tooendpoints (totaal)|
|d2c.telemetry.egress.Dropped|Verwijderde berichten|Count|Totaal|Aantal berichten is verwijderd omdat ze komt niet overeen met alle routes en terugval Hallo-route is uitgeschakeld|
|d2c.telemetry.egress.orphaned|Zwevende berichten|Count|Totaal|het aantal berichten die niet voldoen aan alle routes inclusief terugval route Hallo Hallo|
|d2c.telemetry.egress.Invalid|Ongeldige-berichten|Count|Totaal|Hallo aantal berichten niet verzonden vanwege tooincompatibility met Hallo-eindpunt|
|d2c.telemetry.egress.fallback|Berichten die overeenkomt met alternatieve voorwaarde|Count|Totaal|Aantal berichten dat is geschreven toohello terugval eindpunt|
|d2c.endpoints.egress.eventHubs|Berichten bezorgd tooEvent hubeindpunten|Count|Totaal|Aantal keren dat berichten is geschreven tooEvent-hubeindpunten zijn|
|d2c.endpoints.Latency.eventHubs|Bericht latentie voor Event Hub-eindpunten|milliseconden|Gemiddelde|Hallo gemiddelde latentie tussen bericht inkomend toohello iothub en inkomend bericht in een Event Hub-eindpunt, in milliseconden|
|d2c.endpoints.egress.serviceBusQueues|Berichten bezorgd tooService Bus-wachtrij-eindpunten|Count|Totaal|Aantal keren dat berichten is geschreven tooService Bus-wachtrij eindpunten zijn|
|d2c.endpoints.Latency.serviceBusQueues|Bericht latentie voor Service Bus-wachtrij-eindpunten|milliseconden|Gemiddelde|Hallo gemiddelde latentie tussen bericht inkomend toohello iothub en inkomend bericht in een Service Bus-wachtrij eindpunt, in milliseconden|
|d2c.endpoints.egress.serviceBusTopics|Berichten bezorgd tooService Bus-onderwerp eindpunten|Count|Totaal|Aantal keren dat berichten is geschreven tooService Bus-onderwerp eindpunten zijn|
|d2c.endpoints.Latency.serviceBusTopics|Bericht latentie voor Service Bus-onderwerp eindpunten|milliseconden|Gemiddelde|Hallo gemiddelde latentie tussen bericht inkomend toohello iothub en inkomend bericht in een eindpunt Service Bus-onderwerp in milliseconden|
|d2c.endpoints.egress.builtIn.events|Berichten bezorgd toohello ingebouwd eindpunt (berichten/gebeurtenissen)|Count|Totaal|Aantal keren dat berichten met succes geschreven toohello ingebouwd eindpunt (berichten/gebeurtenissen zijn)|
|d2c.endpoints.Latency.builtIn.events|Bericht latentie voor Hallo ingebouwd eindpunt (berichten/gebeurtenissen)|milliseconden|Gemiddelde|Hallo gemiddelde latentie tussen bericht inkomend toohello iothub en inkomend bericht in Hallo ingebouwd eindpunt (berichten/gebeurtenissen), in milliseconden |
|d2c.Twin.Read.Success|Geslaagde twin leesbewerkingen van apparaten|Count|Totaal|Hallo-telling van alle geslaagde apparaat geïnitieerde twin leest.|
|d2c.Twin.Read.failure|Twin leesbewerkingen van apparaten is mislukt|Count|Totaal|Hallo-telling van alle apparaat geïnitieerde twin leesbewerkingen mislukt.|
|d2c.Twin.Read.Size|De grootte van de antwoorden twin leesbewerkingen van apparaten|Bytes|Gemiddelde|Hallo gemiddelde, min en max van alle geslaagde apparaat geïnitieerde twin leest.|
|d2c.Twin.update.Success|Geslaagde twin updates van apparaten|Count|Totaal|Hallo-telling van alle geslaagde apparaat geïnitieerde twin updates.|
|d2c.Twin.update.failure|Twin updates van apparaten is mislukt|Count|Totaal|Hallo-telling van alle apparaat geïnitieerde twin updates mislukt.|
|d2c.Twin.update.Size|Grootte van de updates twin van apparaten|Bytes|Gemiddelde|gemiddelde Hello, minimale en maximale grootte van alle geslaagde apparaat geïnitieerde twin updates.|
|c2d.Methods.Success|Geslaagde directe methode aanroepen|Count|Totaal|Hallo-telling van alle geslaagde directe methodeaanroepen.|
|c2d.Methods.failure|Directe methode aanroepen is mislukt|Count|Totaal|Hallo-telling van alle directe methodeaanroepen mislukt.|
|c2d.Methods.requestSize|Aanvraaggrootte van directe methode aanroepen|Bytes|Gemiddelde|Hallo gemiddelde, min en max van alle geslaagde aanvragen voor directe methode.|
|c2d.Methods.responseSize|Reactiegrootte van directe methode aanroepen|Bytes|Gemiddelde|Hallo gemiddelde, min en max van alle geslaagde directe methode antwoorden.|
|c2d.Twin.Read.Success|Geslaagde twin leest uit back-end|Count|Totaal|Hallo-telling van alle geslaagde back-end-geïnitieerde twin leest.|
|c2d.Twin.Read.failure|Mislukte twin leest uit back-end|Count|Totaal|Hallo-telling van alle back-end-geïnitieerde twin leesbewerkingen mislukt.|
|c2d.Twin.Read.Size|De grootte van de antwoorden twin leesbewerkingen van back-end|Bytes|Gemiddelde|Hallo gemiddelde, min en max van alle geslaagde back-end-geïnitieerde twin leest.|
|c2d.Twin.update.Success|Geslaagde twin updates van de back-end|Count|Totaal|Hallo-telling van alle geslaagde back-end-geïnitieerde twin updates.|
|c2d.Twin.update.failure|Mislukte twin updates van de back-end|Count|Totaal|Hallo-telling van alle back-end-geïnitieerde twin updates mislukt.|
|c2d.Twin.update.Size|Grootte van twin updates van de back-end|Bytes|Gemiddelde|gemiddelde Hello, minimale en maximale grootte van alle geslaagde back-end-geïnitieerde twin updates.|
|twinQueries.success|Geslaagde twin query 's|Count|Totaal|Hallo-telling van alle geslaagde twin query's.|
|twinQueries.failure|Mislukte twin query 's|Count|Totaal|Hallo-telling van alle mislukte twin query's.|
|twinQueries.resultSize|Grootte van query's Twin|Bytes|Gemiddelde|Hallo gemiddelde, min en max van Hallo resultaat grootte van alle geslaagde twin query's.|
|jobs.createTwinUpdateJob.success|Geslaagde bewerkingen voor het maken van twin taken bijwerken|Count|Totaal|Hallo-telling van alle geslaagde twin update taken worden gemaakt.|
|jobs.createTwinUpdateJob.failure|Mislukte bewerkingen voor het maken van twin taken bijwerken|Count|Totaal|Hallo-telling van alle mislukte twin update taken worden gemaakt.|
|jobs.createDirectMethodJob.success|Geslaagde bewerkingen voor het maken van de methode aanroepen van taken|Count|Totaal|Hallo-telling van alle geslaagde directe methode aanroepen taken worden gemaakt.|
|jobs.createDirectMethodJob.failure|Mislukte bewerkingen voor het maken van de methode aanroepen van taken|Count|Totaal|Hallo-telling van alle maken van taken voor directe methode-aanroep is mislukt.|
|jobs.listJobs.success|Geslaagde aanroepen toolist taken|Count|Totaal|Hallo-telling van alle geslaagde aanroepen toolist taken.|
|jobs.listJobs.failure|Mislukte aanroepen toolist taken|Count|Totaal|Hallo-telling van alle mislukte aanroepen toolist taken.|
|jobs.cancelJob.success|Geslaagde taakannuleringen|Count|Totaal|Hallo-telling van alle geslaagde roept toocancel een taak.|
|jobs.cancelJob.failure|Mislukte taakannuleringen|Count|Totaal|Hallo-telling van alle mislukte aanroepen toocancel een taak.|
|jobs.queryJobs.success|Taak query 's|Count|Totaal|Hallo-telling van alle geslaagde aanroepen tooquery taken.|
|jobs.queryJobs.failure|Taak voert een query is mislukt|Count|Totaal|Hallo-telling van alle mislukte aanroepen tooquery taken.|
|jobs.completed|Voltooide taken|Count|Totaal|Hallo-telling van alle voltooide taken.|
|jobs.failed|Mislukte taken|Count|Totaal|Hallo-telling van alle mislukte taken.|

## <a name="next-steps"></a>Volgende stappen
Nu u een overzicht van IoT Hub metrische gegevens hebt gezien, volgt u deze koppeling toolearn meer over het beheren van Azure IoT Hub:

* [Bewerkingen controleren][lnk-monitor]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
