---
title: leidraad voor aaaPredictive onderhoud | Microsoft Docs
description: Een overzicht van hello Azure IoT voor voorspeld onderhoud vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>Leidraad voor vooraf geconfigureerde oplossing voor voorspeld onderhoud

Hallo voorspeld onderhoud vooraf geconfigureerde oplossing is een end-to-end-oplossing voor een bedrijfsscenario die voorspelt waarop een fout waarschijnlijk toooccur wordt Hallo-punt. U kunt deze vooraf geconfigureerde oplossing proactief gebruiken voor activiteiten zoals het optimaliseren van onderhoud. Hallo oplossing combineert belangrijke Azure IoT Suite-services, zoals IoT Hub, Stream analytics, en een [Azure Machine Learning] [ lnk-machine-learning] werkruimte. Deze werkruimte bevat een model, op basis van een verzameling openbare voorbeeldgegevens, toopredict Hallo resterende levensduur (resterende Levensduur) van een vliegtuigmotor. Hallo-oplossing implementeert Hallo IoT-bedrijfsscenario als een beginpunt voor u tooplan volledig en implementeren van een oplossing die voldoet aan uw eigen specifieke zakelijke vereisten.

## <a name="logical-architecture"></a>Logische architectuur

Hallo volgende diagram geeft een overzicht van de logische onderdelen van de Hallo van Hallo vooraf geconfigureerde oplossing:

![][img-architecture]

Hallo blauwe items zijn Azure-services ingericht in Hallo regio waar u Hallo vooraf geconfigureerde oplossing hebt geïmplementeerd. Hallo-lijst met regio's waarin u Hallo vooraf geconfigureerde oplossing kunt implementeren op Hallo geeft [inrichting pagina][lnk-azureiotsuite].

Hallo groene item is een gesimuleerd apparaat dat een vliegtuigmotor vertegenwoordigt. U kunt meer informatie over deze gesimuleerde apparaten in de volgende sectie Hallo.

Hallo grijze items vertegenwoordigen onderdelen die worden geïmplementeerd *Apparaatbeheer* mogelijkheden. de huidige release Hallo van Hallo voorspeld onderhoud vooraf geconfigureerde oplossing deze resources niet ingericht. toolearn meer informatie over Apparaatbeheer, raadpleegt u toohello [vooraf geconfigureerde oplossing voor externe controle][lnk-remote-monitoring].

## <a name="simulated-devices"></a>Gesimuleerde apparaten

In Hallo vooraf geconfigureerde oplossing voor een gesimuleerd apparaat een vliegtuigmotor vertegenwoordigt. Hallo-oplossing is ingericht met twee motoren die één vliegtuig tooa toewijzen. Elke motor verzendt vier typen telemetrie: Sensor 9, Sensor 11 Sensor 14 en Sensor 15 bieden Hallo gegevens die nodig zijn voor Hallo Machine Learning-model toocalculate Hallo resterende Levensduur voor Hallo-engine. Elk gesimuleerd apparaat verzendt Hallo telemetrie berichten tooIoT Hub te volgen:

*Aantal maal gebruikt*. Een cyclus vertegenwoordigt een voltooide vlucht met een duur van tussen de twee en de tien uur. Telemetriegegevens worden tijdens de vlucht hello, elk half uur worden vastgelegd.

*Telemetrie*. Er zijn vier sensoren die motorkenmerken vertegenwoordigen. Hallo sensoren gelabeld algemeen Sensor 9, Sensor 11 Sensor 14 en Sensor 15. Deze vier sensoren vertegenwoordigen telemetrie voldoende tooobtain bruikbare resultaten uit Hallo resterende Levensduur model. Hallo-model in Hallo vooraf geconfigureerde oplossing gebruikt wordt gemaakt van een openbare gegevensset die echte motorsensorgegevens bevat. Zie voor meer informatie over hoe Hallo model is gemaakt vanaf de oorspronkelijke gegevensset Hallo Hallo [Cortana Intelligence Gallery Predictive Maintenance sjabloon][lnk-cortana-analytics].

Hallo gesimuleerde apparaten kunnen verwerken Hallo opdrachten verzonden uit Hallo iothub in Hallo oplossing te volgen:

| Opdracht | Beschrijving |
| --- | --- |
| StartTelemetry |Besturingselementen Hallo status van Hallo simulatie.<br/>Start Hallo apparaat verzenden van telemetrie |
| StopTelemetry |Besturingselementen Hallo status van Hallo simulatie.<br/>Stopt Hallo apparaat verzenden van telemetrie |

IoT Hub biedt een bevestiging van apparaatopdrachten.

## <a name="azure-stream-analytics-job"></a>Azure Stream Analytics-job

**Job: Telemetrie** is van invloed op Hallo binnenkomende apparaat telemetriestroom met behulp van twee instructies:

* Hallo eerst selecteert alle telemetrie van Hallo apparaten en verzendt deze gegevens tooblob opslag. Hier wordt het weergegeven in Hallo web-app.
* Hallo tweede berekent gemiddelde sensorwaarden gedurende een sliding window van twee minuten en verzendt deze gegevens via Hallo Event hub tooan **gebeurtenisprocessor**.

## <a name="event-processor"></a>Gebeurtenisprocessor
Hallo **gebeurtenisprocessorhost** in een Azure-Web-taak wordt uitgevoerd. Hallo **gebeurtenisprocessor** Hallo gemiddelde sensorwaarden duurt voordat een voltooide cyclus. Deze stuurt vervolgens deze waarden tooan API die het getrainde model toocalculate Hallo resterende Levensduur van een motor beschrijft. Hallo API wordt blootgelegd door een Machine Learning-werkruimte die als onderdeel van Hallo-oplossing is ingericht.

## <a name="machine-learning"></a>Machine Learning
Hallo Machine Learning-component gebruikt een model dat is afgeleid van gegevens van echte vliegtuigmotoren verzameld. U kunt navigeren toohello Machine Learning-werkruimte van de tegel Hallo op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] pagina voor de ingerichte oplossing. Hallo tegel is beschikbaar als Hallo oplossing in Hallo **gereed** status.


## <a name="next-steps"></a>Volgende stappen
Nu u Hallo belangrijke onderdelen van Hallo voorspeld onderhoud vooraf geconfigureerde oplossing hebt gezien, kunt u toocustomize deze. Zie [Guidance on Customizing Preconfigured Solutions][lnk-customize] (Handleiding voor het aanpassen van vooraf geconfigureerde oplossingen).

U kunt ook verkennen van Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:

* [Veelgestelde vragen over IoT Suite][lnk-faq]
* [Beveiliging van de IoT van Hallo gemalen][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/