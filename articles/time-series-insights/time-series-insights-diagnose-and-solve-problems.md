---
title: aaaDiagnose en problemen oplossen | Microsoft Docs
description: Deze zelfstudie bevat informatie over hoe toodiagnose en oplossen van problemen in uw omgeving Time Series Insights
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Diagnosticeren en oplossen van problemen in uw omgeving Time Series Insights

## <a name="i-dont-see-my-data"></a>Ik weergegeven mijn gegevens niet
Hier volgen enkele redenen waarom u niet uw gegevens in uw omgeving in Hallo ziet [Azure Time Series Insights-portal](https://insights.timeseries.azure.com).

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>De gebeurtenisbron bevat geen gegevens in JSON-indeling
Inzicht van Azure Time Series ondersteunt vandaag JSON-gegevens. Zie voor voorbeelden van de JSON, [JSON ondersteund vormen](time-series-insights-send-events.md#supported-json-shapes).

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>Bij de registratie van uw gebeurtenisbron opgeven u Hallo-sleutel die bevoegd zijn Hallo vereist niet
* Voor een IoT-hub, moet u tooprovide Hallo sleutel waarvoor **service verbinding** machtiging.

   ![IoT hub service connect machtiging](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Zoals wordt weergegeven in de voorgaande afbeelding, Hallo ofwel Hallo beleid **iothubowner** en **service** zou werken, omdat beide **service verbinding** machtiging.
* Voor een event hub, moet u tooprovide Hallo sleutel waarvoor **luisteren** machtiging.

   ![Event hub listen machtiging](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Zoals wordt weergegeven in de voorgaande afbeelding, Hallo ofwel Hallo beleid **lezen** en **beheren** zou werken, omdat beide **luisteren** machtiging.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>Hallo opgegeven consumergroep is niet exclusief tooTime reeks Insights
Voor een IoT-hub of een event hub, tijdens de registratie moet u toospecify hello consumergroep die moet worden gebruikt voor het lezen van uw gegevens. Deze consumergroep moet niet worden gedeeld. Als deze wordt gedeeld, Hallo onderliggende event hub automatisch wordt verbroken een Hallo lezers willekeurig.

## <a name="i-see-my-data-but-theres-a-lag"></a>Ik mijn gegevens worden weergegeven, maar er is een vertraging
Hier volgen de redenen waarom u gegevens gedeeltelijk in uw omgeving in Hallo ziet mogelijk [Time Series Insights-portal](https://insights.timeseries.azure.com).

### <a name="your-environment-is-getting-throttled"></a>Uw omgeving worden beperkt door ophalen
Hallo limiet beperking wordt afgedwongen op basis van de SKU-type en de capaciteit Hallo-omgeving. Alle bronnen van gebeurtenissen in de omgeving Hallo delen deze capaciteit. Als de gebeurtenisbron Hallo voor uw IoT-hub of event hub gegevens buiten de limieten voor Hallo afgedwongen pusht, ziet u bandbreedtebeperking en een vertraging.

Hallo volgende diagram ziet u een tijd reeks Insights-omgeving die een SKU S1 en een capaciteit van 3 heeft. Kan het 3 miljoen ingangsgebeurtenissen per dag.

![Huidige omgeving SKU-capaciteit](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Wordt ervan uitgegaan dat deze omgeving berichten van een event hub met Hallo inkomend tarief wordt weergegeven in het volgende diagram Hallo is opnemen:

![Voorbeeld inkomend frequentie voor een event hub](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Zoals u in het diagram hello, is Hallo dagelijkse inkomend snelheid ~ 67,000 berichten. Deze snelheid vertaalt ongeveer too46 berichten elke minuut. Als elk gebeurtenisbericht hub platte tooa één keer reeks Insights gebeurtenis is, ziet deze omgeving geen beperking. Als elk gebeurtenisbericht hub platte too100 Time Series Insights-gebeurtenissen, moeten klikt u vervolgens 4,600 gebeurtenissen worden ingenomen elke minuut. Een S1 SKU-omgeving met een capaciteit van 3 kunnen alleen 2 100 ingangsgebeurtenissen elke minuut (1 miljoen gebeurtenissen per dag = 700 gebeurtenissen per minuut bij 3 eenheden = 2 100 gebeurtenissen per minuut). Daarom ziet u een vertraging vanwege toothrottling. 

Zie voor een grondige kennis van de logica plat werking [JSON ondersteund vormen](time-series-insights-send-events.md#supported-json-shapes).

#### <a name="recommended-steps"></a>Aanbevolen stappen
toofix hello lag toename Hallo SKU-capaciteit van uw omgeving. Zie voor meer informatie [hoe tooscale uw omgeving Time Series Insights](time-series-insights-how-to-scale-your-environment.md).

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>U historische gegevens worden gepusht en veroorzaakt door trage inkomend
Als u een bestaande gebeurtenisbron verbindt, is het waarschijnlijk dat uw IoT-hub of event hub al gegevens daarin. Hallo-omgeving wordt dus gestart binnenhalen van gegevens vanaf Hallo Hallo gebeurtenisbron bericht bewaarperiode. 

Dit gedrag is de standaardinstelling Hallo en kan niet worden overschreven. U kunt benaderen bandbreedtebeperking en duurt het even toocatch up voor het opnemen van historische gegevens.

#### <a name="recommended-steps"></a>Aanbevolen stappen
toofix hello lag nemen Hallo stappen te volgen:
1. Toename Hallo SKU-capaciteit toohello maximaal toegestane waarde (10 in dit geval). Nadat het Hallo-capaciteit wordt verhoogd, Hallo inkomend begint afvangen veel sneller. U kunt visualiseren hoe snel u bent bouwen via Hallo beschikbaarheid grafiek in Hallo [Time Series Insights-portal](https://insights.timeseries.azure.com). Worden in rekening gebracht voor Hallo grotere capaciteit.
2. Na het Hallo lag wordt bijgewerkt, Hallo SKU capaciteit back tooyour normale inkomend snelheid.

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>Mijn gebeurtenisbron *tijdstempel eigenschapsnaam* instelling werkt niet
Overeenstemming Hallo naam en waarde volgens de regels voor toohello:
* naam van de eigenschap Hallo tijdstempel is _hoofdlettergevoelig_.
* Hallo timestamp-eigenschapswaarde die afkomstig is van de gebeurtenisbron, als een JSON-tekenreeks moet Hallo indeling _jjjj-MM-ddTUU. FFFFFFFK_. Een voorbeeld van een dergelijke tekenreeks is ' 2008-04-12T12:53Z '.
