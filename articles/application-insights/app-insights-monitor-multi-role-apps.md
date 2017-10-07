---
title: aaaAzure Application Insights-ondersteuning voor meerdere onderdelen, microservices en containers | Microsoft Docs
description: Bewaken van apps die bestaan uit meerdere onderdelen of rollen voor prestaties en het gebruik.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>De bewaking van meerdere onderdeel toepassingen met Application Insights (preview)

U kunt apps die bestaan uit meerdere server-onderdelen, functies of services met bewaken [Azure Application Insights](app-insights-overview.md). Hallo-status van Hallo-onderdelen en Hallo onderlinge relaties worden weergegeven op een kaart met één toepassing. U kunt afzonderlijke bewerkingen via meerdere onderdelen met automatische HTTP correlatie traceren. Container diagnostische gegevens kan worden geïntegreerd en worden gecorreleerd met de toepassingstelemetrie. Gebruik één Application Insights-resource voor alle Hallo onderdelen van uw toepassing. 

![Meerdere onderdeel toepassingstoewijzing](./media/app-insights-monitor-multi-role-apps/app-map.png)

We gebruiken 'onderdeel' hier toomean een werkende deel van een grote aanvraag. Bijvoorbeeld, de meeste zakelijke toepassingen kan bestaan uit clientcode die wordt uitgevoerd in de webbrowser, praten tooone of meer web-app services, die op zijn beurt back gebruiken-end services. Server-onderdelen mogelijk gehoste on-premises worden op in de cloud Hallo, of mogelijk Azure web- en werkrollen rollen of mogelijk worden uitgevoerd in containers zoals Docker of Service Fabric. 

### <a name="sharing-a-single-application-insights-resource"></a>Een enkele Application Insights-resource delen 

Hallo belangrijke techniek hier is toosend telemetrie van elk onderdeel in uw toepassing toohello dezelfde Application Insights-resource, maar gebruik Hallo `cloud_RoleName` eigenschap toodistinguish onderdelen indien nodig. Hallo Application Insights-SDK wordt toegevoegd Hallo `cloud_RoleName` eigenschap toohello telemetrie onderdelen verzenden. Bijvoorbeeld, Hallo SDK wordt toegevoegd een naam van de website of service rol naam toohello `cloud_RoleName` eigenschap. U kunt deze waarde met een telemetryinitializer overschrijven. Hallo toepassingstoewijzing gebruikt Hallo `cloud_RoleName` eigenschap tooidentify Hallo onderdelen op Hallo-kaart.

Voor meer informatie over het Hallo overschrijven `cloud_RoleName` eigenschap Zie [eigenschappen toevoegen: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

In sommige gevallen kan dit niet altijd geschikt en gewenste toouse afzonderlijke bronnen voor verschillende groepen van onderdelen. U wellicht bijvoorbeeld toouse verschillende bronnen voor beheer of facturering. Met behulp van afzonderlijke resources betekent dat er geen alle Hallo onderdelen weergegeven op een kaart met één toepassing; en dat u geen query uitvoeren voor onderdelen in [Analytics](app-insights-analytics.md). Hebt u ook tooset Hallo afzonderlijke resources.

Met dat hoewel we gaan ervan uit dat in de rest van dit document Hallo die u wilt dat toosend gegevens uit meerdere onderdelen tooone Application Insights-resource.

## <a name="configure-multi-component-applications"></a>Meerdere onderdeel toepassingen configureren

tooget een toepassing met meerdere onderdelen toewijzen, moet u tooachieve na deze doelstellingen:

* **Installeer de meest recente voorlopige Hallo** Application Insights-pakket in elk onderdeel van de toepassing hello. 
* **Een enkele Application Insights-resource delen** voor alle onderdelen van uw toepassing hello.
* **Inschakelen van de toepassing van meerdere rollenoverzicht** Hallo Previews blade.

Configureer elk onderdeel van uw toepassing met de juiste methode Hallo voor het type. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)

### <a name="1-install-hello-latest-pre-release-package"></a>1. Hallo meest recente voorlopige versie pakket installeren

Bijwerken of Hallo toepassing Insights pakketten in Hallo-project voor elk serveronderdeel worden geïnstalleerd. Als u Visual Studio:

1. Met de rechtermuisknop op een project en selecteer **NuGet-pakketten beheren**. 
2. Selecteer **Include prerelease**.
3. Als de Application Insights-pakketten in de Updates worden weergegeven, selecteert u deze. 

    Anders zoeken en installeren van het juiste pakket Hallo:
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric - voor de onderdelen die worden uitgevoerd als gast uitvoerbare bestanden en Docker-containers in Service Fabric-toepassing wordt uitgevoerd
    * Microsoft.ApplicationInsights.ServiceFabric.Native - voor betrouwbare services in ServiceFabric toepassingen
    * Microsoft.ApplicationInsights.Kubernetes voor onderdelen die worden uitgevoerd in Docker op Kubernetes

### <a name="2-share-a-single-application-insights-resource"></a>2. Een enkele Application Insights-resource delen

* In Visual Studio met de rechtermuisknop op een project en selecteer **Configure Application Insights**, of **Application Insights > configureren**. Gebruik voor de eerste project hello, Hallo wizard toocreate Application Insights-resource. Selecteer Hallo voor latere projecten dezelfde resource.
* Als er geen Application Insights-menu, handmatig configureren:

   1. In [Azure-portal](https://portal,azure.com), opent u Application Insights-resource Hallo u al hebt gemaakt voor een ander onderdeel.
   2. In overzichtsblade hello, open Hallo Essentials vervolgkeuzelijst tabblad en kopiëren Hallo **Instrumentatiesleutel.**
   3. Open ApplicationInsights.config en invoegen in uw project:`<InstrumentationKey>your copied key</InstrumentationKey>`

![Hallo instrumentation sleutel toohello .config-bestand kopiëren](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Toepassing van meerdere rollenoverzicht inschakelen

Open in hello Azure-portal, Hallo bron voor uw toepassing. Hallo Previews blade inschakelen *toepassing van meerdere rollenoverzicht*.

### <a name="4-enable-docker-metrics-optional"></a>4. Docker metrische gegevens (optioneel) inschakelen 

Als een onderdeel in een Docker gehost op een Windows Azure VM wordt uitgevoerd, kunt u aanvullende gegevens kunt verzamelen uit Hallo-container. Voeg dit in uw [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuratiebestand:

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Gebruik cloud_RoleName tooseparate onderdelen

Hallo `cloud_RoleName` eigenschap is aangesloten tooall telemetrie. Het identificeert Hallo-onderdeel - Hallo functie of service - die afkomstig is van Hallo telemetrie. (Dit is dezelfde niet Hallo als cloud_RoleInstance die identiek functies die parallel worden uitgevoerd op meerdere serverprocessen of machines scheidt.)

U kunt filteren en uw gebruik van deze eigenschap telemetrie segmenteren in Hallo-portal. In dit voorbeeld is Hallo fouten blade gefilterde tooshow alleen op de gegevens van Hallo front-webservice, worden uitgefilterd fouten vanuit Hallo CRM-API-back-end:

![Metrische gesegmenteerd op naam van de Cloud-rol-grafiek](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Trace-bewerkingen tussen onderdelen

U kunt traceren vanuit één onderdeel tooanother, Hallo aanroepen tijdens het verwerken van een afzonderlijke bewerking.


![Telemetrie voor bewerking weergeven](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Klik op door tooa gecorreleerde lijst telemetrie voor deze bewerking via Hallo-front-endwebserver en Hallo back-end-API:

![Zoeken in onderdelen](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Volgende stappen

* [Afzonderlijke telemetrie van ontwikkeling, testen en productie](app-insights-separate-resources.md)
