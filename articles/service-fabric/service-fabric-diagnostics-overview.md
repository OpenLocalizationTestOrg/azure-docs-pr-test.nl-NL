---
title: aaaAzure overzicht van diagnostische gegevens en het Service Fabric Monitoring | Microsoft Docs
description: Meer informatie over controle en diagnostische gegevens voor Azure Service Fabric-clusters, toepassingen en services.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Controle en diagnostische gegevens voor Azure Service Fabric

Controle en diagnostische gegevens zijn essentieel toodeveloping, testen en implementeren van toepassingen en services in elke omgeving. Service Fabric-oplossingen werken het beste wanneer u plannen en implementeren van controle en diagnostische gegevens waarmee Zorg ervoor toepassingen dat en services werkt zoals verwacht in een lokale ontwikkelingsomgeving of in de productieomgeving.

Hallo belangrijkste doelstellingen van controle en diagnostische gegevens zijn naar:
* Detecteren en onderzoeken van problemen met hardware- en infrastructuur
* Problemen met software- en app detecteren, de service uitvaltijd beperken
* Resource gebruiks- en help station operations beslissingen begrijpen
* Toepassings-, service- en infrastructuur optimaliseren
* Zakelijke inzichten genereren en te identificeren gebieden van de gebruikerservaring


Hallo totale werkstroom van de bewaking en diagnostische gegevens bestaat uit drie stappen:

1. **Genereren van gebeurtenis**: dit bevat gebeurtenissen (Logboeken, traceringen, aangepaste gebeurtenissen) op het Hallo-infrastructuur (cluster), platform en toepassing / service niveau
2. **Gebeurtenis aggregatie**: gegenereerde gebeurtenissen moeten toobe worden verzameld en geaggregeerd voordat ze kunnen worden weergegeven
3. **Analyse**: gebeurtenissen moeten toobe gevisualiseerde en toegankelijk zijn in sommige-indeling, tooallow voor analyse en weergeven indien nodig

Meerdere producten zijn beschikbaar die betrekking op deze drie gebieden, en u gratis toochoose verschillende technologieën voor elk. Het is belangrijk toomake ervoor dat Hallo stukken werk samen toodeliver verschillende een oplossing voor de end-to-end-controle voor uw cluster.

## <a name="event-generation"></a>Genereren van gebeurtenis

Hallo eerste stap in de werkstroom controle en diagnostische gegevens Hallo is Hallo maken en het genereren van gebeurtenissen en Logboeken. Deze gebeurtenissen, logboeken en traceringen worden gegenereerd op twee niveaus: Hallo platformlaag (inclusief Hallo-cluster, Hallo machines of acties van de Service Fabric) of Hallo toepassingslaag (instrumentation toegevoegd tooapps en -services geïmplementeerd toohello cluster). Gebeurtenissen op elk niveau worden aangepast, hoewel Service Fabric een aantal instrumentation standaard biedt.

Lees meer over [platform niveau gebeurtenissen](service-fabric-diagnostics-event-generation-infra.md) en [niveau toepassingsgebeurtenissen](service-fabric-diagnostics-event-generation-app.md) toounderstand wat is opgegeven en hoe tooadd instrumentation verder.

Nadat u een beslissing op Hallo provider die u wilt dat toouse logboekregistratie, moet u ervoor dat uw logboeken worden toomake geaggregeerd en juist opgeslagen.

## <a name="event-aggregation"></a>Aggregatie van gebeurtenis

Voor het verzamelen van Logboeken Hallo en gebeurtenissen die door uw toepassingen en het cluster wordt gegenereerd, meestal aangeraden [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) (meer lijken op basis van tooagent logboekverzameling) of [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)(in-process logboekgegevens verzameld).

Verzamelen van toepassingslogboeken met behulp van Azure Diagnostics-extensie is een goede optie voor Service Fabric-services als Hallo ingesteld van logboek-bronnen en bestemmingen niet vaak wordt gewijzigd en er is een eenvoudige toewijzing tussen Hallo bronnen en hun bestemmingen. Hallo reden voor dit is het configureren van Azure Diagnostics gebeurt op Hallo Resource Manager-laag, zodat u belangrijke wijzigingen toohello configuratie Hallo cluster bijwerken vereist/opnieuw distribueren. Bovendien best gebruikt om er zeker van te zijn uw logboeken worden opgeslagen op een iets meer permanente van waar ze toegankelijk zijn voor verschillende platforms voor analyse. Dit betekent dat wordt minder efficiënt van een pijplijn terechtkomt dan gaat met de optie zoals EventFlow.

Met behulp van [EventFlow](https://github.com/Azure/diagnostics-eventflow) kunt u services toohave hun logboeken verzenden rechtstreeks tooan analyse en visualisatie platform en/of toostorage. Andere bibliotheken (ILogger, Serilog, enz.) kunnen worden gebruikt voor Hallo hetzelfde doel, maar EventFlow Hallo voordeel dat is speciaal ontworpen voor proces logboek verzameling en toosupport Service Fabric-services heeft. Dit heeft vaak toohave verschillende mogelijke voordelen:

* Eenvoudige configuratie en implementatie
    * Hallo-configuratie van verzamelen van diagnostische gegevens net is onderdeel van de serviceconfiguratie Hallo. Het is gemakkelijk tooalways Houd deze 'synchroon' Hello rest van de toepassing hello
    * De configuratie van per toepassing of per-service is eenvoudig haalbare
    * Gegevensbestemmingen via EventFlow configureren is slechts een kwestie van Hallo juiste NuGet-pakket toevoegen en het wijzigen van Hallo *eventFlowConfig.json* bestand
* Flexibiliteit
    * Hallo-toepassing kunt hello gegevens verzenden waar het toogo, moet, zolang er is een clientbibliotheek die ondersteuning biedt voor systeem voor gegevensopslag Hallo gericht. Nieuwe doelen kunnen worden toegevoegd naar wens
    * Complexe regels voor het vastleggen, filteren en samenvoegen van gegevens kunnen worden geïmplementeerd
* Toegang toointernal toepassingsgegevens en -context
    * Hallo diagnostische subsysteem uitvoering binnen Hallo toepassing/service-proces kan eenvoudig hello traceringen met contextafhankelijke informatie verbeteren

Een ding toonote is dat deze twee opties elkaar niet uitsluiten en terwijl deze mogelijk tooget dezelfde functie uitgevoerd wordt met behulp van een of andere hello, het kan ook zinvol voor u tooset van beide. In de meeste gevallen een agent combineren met process-verzameling kan ertoe leiden tooa betrouwbaarder bewaking van de werkstroom. Hello Azure Diagnostics-extensie (agent) kan worden uw gekozen pad voor platform-niveau logboeken terwijl EventFlow (in-process verzameling) kunt u gebruiken voor uw toepassing niveau Logboeken. Zodra u hebt doorberekend af wat het beste voor u werkt, is het tijd toothink over hoe u wilt dat uw gegevens toobe weergegeven en geanalyseerd.

## <a name="event-analysis"></a>Analyse van gebeurtenis

Er zijn verschillende geweldige platforms die aanwezig zijn in de markt Hallo wanneer deze toohello analyse en visualisatie van controle en diagnostische gegevens wordt. Hallo twee die wij adviseren zijn [OMS](service-fabric-diagnostics-event-analysis-oms.md) en [Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) vanwege tootheir betere integratie met Service Fabric, maar u moet ook zoeken in Hallo [elastische Stack](https://www.elastic.co/products) (met name als u een cluster uitvoert in een offline omgeving overweegt), [Splunk](https://www.splunk.com/), of een andere platform van uw voorkeur.

Hallo belangrijke punten voor elk platform dat u kiest, moet zijn scenario dat u zich met Hallo-gebruikersinterface en gegevensquery's opties Hallo mogelijkheid toovisualize gegevens en gemakkelijk leesbare dashboards maken en hello extra hulpprogramma's bieden tooenhance uw bewaking, zoals geautomatiseerde waarschuwingen.

Bovendien toohello platform dat u kiest, bij het instellen van een Service Fabric-cluster als een Azure-resource, u ook krijgen van toegang tooAzure out-of-the-box-bewaking voor machines, die nuttig voor specifieke prestaties zijn kunnen en metrische gegevens controleren.

### <a name="azure-monitor"></a>Azure Monitor

U kunt [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md) toomonitor veel van hello Azure-resources waarop een Service Fabric-cluster is gebouwd. Een set van metrische gegevens voor Hallo [virtuele-machineschaalset](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets) en afzonderlijke [virtuele machines](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines) automatisch worden verzameld en weergegeven in hello Azure-portal. Hallo tooview in hello Azure-portal, selecteer Hallo resourcegroep Hallo Service Fabric-cluster met informatie verzameld. Selecteer Hallo virtuele-machineschaalset Stel dat u wilt dat tooview. In Hallo **bewaking** sectie **metrische gegevens** tooview een grafiek van Hallo waarden.

![Azure portal weergave van verzamelde metrische gegevens](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

toocustomize hello grafieken, volg de instructies Hallo in [metrische gegevens in Microsoft Azure](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md). Ook kunt u waarschuwingen op basis van deze metrische gegevens, zoals beschreven in [waarschuwingen in de Azure-Monitor maken voor Azure-services](../monitoring-and-diagnostics/insights-alerts-portal.md). U kunt waarschuwingen tooa meldingsservice verzenden met behulp van web-haken, zoals beschreven in [een haakje web configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Monitor voor Azure ondersteunt slechts één abonnement. Als u meerdere abonnementen toomonitor nodig, of als u extra functies, moet [logboekanalyse](https://azure.microsoft.com/documentation/services/log-analytics/), onderdeel van de Microsoft Operations Management Suite biedt een holistische oplossing voor IT-beheer voor on-premises en cloud-gebaseerde infrastructuur. U kunt gegevens uit Azure Monitor versturen rechtstreeks tooLog Analytics, zodat u Logboeken en metrische gegevens voor uw hele omgeving op één plaats kunt zien.

## <a name="next-steps"></a>Volgende stappen

### <a name="watchdogs"></a>Watchdogs

Een watchdog is een afzonderlijke service die u kunt health bekijken en laden tussen services en het rapport status voor alles in Hallo health modelhiërarchie. Dit kan helpen voorkomen dat er fouten die niet kunnen worden gedetecteerd op basis van Hallo-weergave van een service. Watchdogs zijn ook een goede plaats toohost code waarmee corrigerende acties zonder tussenkomst van de gebruiker (bijvoorbeeld het opschonen van logboekbestanden in de opslag op bepaalde tijdsintervallen) wordt uitgevoerd. U vindt een steekproef watchdog service-implementatie [hier](https://github.com/Azure-Samples/service-fabric-watchdog-service).

Aan de slag met informatie over hoe gebeurtenissen en logboeken op Hallo ophalen gegenereerd [platform niveau](service-fabric-diagnostics-event-generation-infra.md) en Hallo [toepassingsniveau](service-fabric-diagnostics-event-generation-app.md).
