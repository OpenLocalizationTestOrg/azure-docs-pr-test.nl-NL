---
title: aaaAzure analyse van Service Fabric-gebeurtenis met Application Insights | Microsoft Docs
description: Meer informatie over het visualiseren en analyseren van gebeurtenissen met Application Insights voor controle en diagnostische gegevens van Azure Service Fabric-clusters.
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Analyse van gebeurtenis en visualisatie met Application Insights

Azure Application Insights is een uitbreidbaar platform voor bewaking en diagnostische gegevens. Er staan een krachtige analytics en gegevensquery's hulpprogramma, aanpasbare dashboard en visualisaties en meer opties, waaronder geautomatiseerde waarschuwingen. Is het Hallo aanbevolen platform voor controle en diagnostische gegevens voor Service Fabric-toepassingen en services.

## <a name="setting-up-application-insights"></a>Application Insights instellen

### <a name="creating-an-ai-resource"></a>Maken van een Resource AI

toocreate een AI-resource, head via Azure Marketplace toohello en zoek naar 'Application Insights'. Het moet als eerste Hallo-oplossing (het zich onder de categorie 'Web + Mobile') weergegeven. Klik op **maken** wanneer u bekijkt hello juiste resource (bevestigen dat het pad overeenkomt met Hallo in onderstaande afbeelding).

![Nieuwe Application Insights-resource](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

U moet correct toofill sommige informatie tooprovision Hallo-bron. In Hallo *toepassingstype* veld gebruik 'ASP.NET-webtoepassing' als u van een Service Fabric gebruikmaakt de programmering modellen of een cluster met .NET application toohello publiceren. Gebruik 'Algemene' als u Gast uitvoerbare bestanden en containers implementeren wilt. In het algemeen standaard toousing 'ASP.NET-webtoepassing' tookeep uw opties open Hallo toekomstige. Hallo-naam is van de voorkeursextensie tooyour en zowel Hallo-resourcegroep en abonnement zijn gewijzigd na de implementatie van resource Hallo. Het is raadzaam dat uw AI-resource in Hallo is dezelfde resourcegroep als uw cluster. Als u meer informatie nodig hebt, raadpleegt u [een Application Insights-resource maken](../application-insights/app-insights-create-new-resource.md)

Hallo AI Instrumentatiesleutel tooconfigure AI moet u met uw gebeurtenis aggregatie-hulpprogramma. Als uw AI-resource een (duurt een paar minuten nadat het Hallo-implementatie wordt gevalideerd) is ingesteld, navigeer tooit en Hallo zoeken **eigenschappen** sectie op de linkernavigatiebalk Hallo. Een nieuwe blade geopend waarin een *INSTRUMENTATIESLEUTEL*. Als u toochange Hallo abonnement of resourcegroep van Hallo resource nodig, kan het worden gedaan hier ook.

### <a name="configuring-ai-with-wad"></a>AI configureren met af

Er zijn twee manieren toosend-gegevens van af tooAzure AI, die wordt bereikt door het toevoegen van een AI sink toohello af-configuratie zoals beschreven in [in dit artikel](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Een Instrumentatiesleutel AI toevoegen bij het maken van een cluster in Azure-portal

![Toevoegen van een AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

Bij het maken van een cluster als Diagnostics 'Op' is ingeschakeld, een optioneel veld tooenter een Application Insights-instrumentatiesleutel wordt weergegeven. Als u uw AI IKey hier plakt, Hallo AI sink worden automatisch voor u geconfigureerd in Hallo Resource Manager-sjabloon die wordt gebruikt toodeploy uw cluster.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Hallo AI Sink toohello Resource Manager-sjabloon toevoegen

Voeg in Hallo 'WadCfg' hello Resource Manager-sjabloon, een 'Sink' door Hallo twee wijzigingen te volgen, waaronder:

1. Hallo sink configuratie toevoegen:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Hallo Sink opnemen in Hallo DiagnosticMonitorConfiguration door toe te voegen Hallo volgende regel in 'DiagnosticMonitorConfiguration' Hallo 'WadCfg':

    ```json
    "sinks": "applicationInsights"
    ```

In beide codefragmenten Hallo hierboven Hallo is de naam 'applicationInsights' gebruikte toodescribe Hallo sink. Dit is geen vereiste en zolang Hallo-naam van Hallo sink is opgenomen in een 'put', kunt u Hallo tooany tekenreeks instellen.

Op dit moment wordt logboeken van de cluster hello weergegeven als de traceringen in AI van Logboeken. Aangezien de meeste Hallo traceringen Hallo platform afkomstig zijn van niveau 'Ter informatie', kunt u ook overwegen Hallo sink configuratie tooonly verzenden logboeken van het type 'Kritiek' of 'Fout' wijzigen. Dit kan worden gedaan door toe te voegen 'Kanalen' tooyour sink, zoals wordt beschreven in [in dit artikel](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Als u een onjuiste AI IKey in de portal of in de Resource Manager-sjabloon gebruikt, hebt u toomanually Hallo sleutel wijzigen en Hallo cluster bijwerken / opnieuw te implementeren. 

### <a name="configuring-ai-with-eventflow"></a>AI met EventFlow configureren

Als u EventFlow tooaggregate gebeurtenissen gebruikt, zorg ervoor dat tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet-pakket. Hallo volgende is opgenomen in Hallo toobe *levert* sectie Hallo *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Ervoor toomake Hallo vereist wijzigingen aanbrengen in uw filters, evenals alle andere invoer (samen met hun respectieve NuGet-pakketten) bevatten.

## <a name="aisdk"></a>AI. SDK

Het is raadzaam toouse EventFlow en af als aggregatieoplossingen, omdat ze toestaan voor een meer modulaire benadering toodiagnostics en bewaking, dat wil zeggen als u de uitvoer van EventFlow toochange wilt, geen wijziging tooyour Werkelijke vereist instrumentatie, alleen een eenvoudige wijziging tooyour config-bestand. Als u tooinvest besluit in het gebruik van Application Insights en zijn echter niet waarschijnlijk toochange tooa verschillende platform, moet u zoeken naar met behulp van AI nieuwe SDK voor het aggregeren van gebeurtenissen en ze tooAI worden verzonden. Dit betekent dat u wordt niet meer beschikt over tooconfigure EventFlow toosend uw tooAI gegevens, maar in plaats daarvan Hallo ApplicationInsight van Service Fabric-NuGet-pakket installeert. Meer informatie over Hallo pakket vindt [hier](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Application Insights-ondersteuning voor Microservices en Containers](https://azure.microsoft.com/app-insights-microservices/) laat u een aantal nieuwe functies Hallo die wordt gewerkt (momenteel nog steeds in beta), waarmee u toohave uitgebreidere out-of-the-box-controle-opties met AI. Deze omvatten bijhouden van afhankelijkheid (gebruikt bij het bouwen van een AppMap van uw services en toepassingen in een cluster en Hallo communicatie tussen deze twee) en betere correlatie van traceringen afkomstig zijn van uw services (helpt u bij het beter een probleem in Hallo dicht werkstroom van een app of service).

Als u ontwikkelt in .NET en zal het waarschijnlijk worden gebruikmakend van de Service Fabric-programmeermodellen en bereid toouse AI als uw platform voor het visualiseren en analyseren van gebeurtenissen en logboek gegevens, en vervolgens het is raadzaam dat u via Hallo AI SDK route als de bewaking gaat zijn en Diagnostische gegevens van de workflow. Lees [dit](../application-insights/app-insights-asp-net-more.md) en [dit](../application-insights/app-insights-asp-net-trace-logs.md) tooget slag kunt met AI toocollect en uw logboeken weer te geven.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Hallo AI resource in Azure-portal te navigeren

Wanneer u AI hebt geconfigureerd als uitvoer voor uw gebeurtenissen en Logboeken, moet informatie starten tooshow in uw AI-resource in een paar minuten. Navigeer toohello AI resource, die u toohello AI resource dashboard te laten. Klik op **Search** in Hallo AI taakbalk toosee Hallo nieuwste traceringen die deze heeft ontvangen en toobe kunnen toofilter doorheen.

*Metrics Explorer* een handig hulpmiddel voor het maken van aangepaste dashboards die op basis van de metrische gegevens die uw toepassingen, services en cluster kunnen rapporteren. Zie [verkennen van metrische gegevens in Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset van enkele grafieken voor uzelf op basis van Hallo-gegevens die u verzamelt.

Te klikken op **Analytics** , gaat u toohello Application Insights Analytics-portal, waar u kunt een query gebeurtenissen en traceringen met een groter bereik en optionaliteit. Meer informatie over deze [analyses in Application Insights](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Volgende stappen

* [Stel waarschuwingen in AI](../application-insights/app-insights-alerts.md) toobe geïnformeerd over wijzigingen in de prestatie- of -gebruik
* [Detectie in Application Insights slimme](../application-insights/app-insights-proactive-diagnostics.md) voert een proactieve analyse Hallo telemetrie verstuurd tooAI toowarn u potentiële prestatieproblemen
