---
title: aaaCollect logboeken rechtstreeks vanaf een Azure Service Fabric-service proces | Microsoft Azure
description: Beschrijving van Service Fabric-toepassingen logboeken verzenden kunnen direct tooa centrale locatie zoals Azure Application Insights of Elasticsearch, zonder afhankelijk te zijn op Azure Diagnostics-agent.
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>Logboeken rechtstreeks vanaf een Azure Service Fabric-serviceproces verzamelen
## <a name="in-process-log-collection"></a>In-process-logboekgegevens verzameld
Verzamelen van de toepassing registreert met behulp van [extensie voor diagnostische gegevens van Azure](service-fabric-diagnostics-how-to-setup-wad.md) is een goede optie voor **Azure Service Fabric** services als Hallo reeks logboek bronnen en bestemmingen klein is, verandert niet vaak en er is een eenvoudige toewijzing tussen Hallo bronnen en hun bestemmingen. Als dat niet het geval is, moet u een alternatief is toohave services hun logboeken verzenden rechtstreeks tooa centrale locatie. Dit proces wordt ook wel **proces logboekverzameling** en heeft verschillende mogelijke voordelen:

* *Eenvoudige configuratie en implementatie*

    * Hallo-configuratie van verzamelen van diagnostische gegevens net is onderdeel van de serviceconfiguratie Hallo. Het is gemakkelijk tooalways Houd deze 'synchroon' Hello rest van de toepassing hello.
    * Configuratie van per toepassing of per-service is eenvoudig haalbare.
        * Verzamelen op basis van een agent vereist gewoonlijk een afzonderlijke implementatie en configuratie van Hallo diagnostische agent, die een extra beheertaak en een mogelijke oorzaak van fouten is. Vaak is er slechts één exemplaar van Hallo agent toegestaan per virtuele machine (knooppunt) en de agentconfiguratie hello wordt gedeeld door alle toepassingen en services die op dat knooppunt worden uitgevoerd. 

* *Flexibiliteit*
   
    * Hallo-toepassing kunt hello gegevens verzenden waar het toogo, moet, zolang er is een clientbibliotheek die ondersteuning biedt voor systeem voor gegevensopslag Hallo gericht. Nieuwe doelen kunnen worden toegevoegd naar wens.
    * Complexe regels voor het vastleggen, filteren en samenvoegen van gegevens kunnen worden geïmplementeerd.
    * Verzamelen op basis van een agent wordt vaak beperkt door Hallo gegevens put die Hallo agent ondersteunt. Sommige agents worden uitgebreid.

* *Toegang toointernal toepassingsgegevens en -context*
   
    * Hallo diagnostische subsysteem uitvoering binnen Hallo toepassing/service-proces kan eenvoudig hello traceringen met contextafhankelijke informatie verbeteren.
    * Met op basis van een agent logboekverzameling moet op Hallo gegevens tooan agent via een mechanisme voor communicatie tussen processen, zoals Event Tracing for Windows worden verzonden. Dit mechanisme kan aanvullende beperkingen opleggen.

Het is mogelijk toocombine en voordelen van beide methoden verzameling. Inderdaad, mogelijk de beste oplossing Hallo voor veel toepassingen. Verzameling op basis van een agent is een natuurlijke oplossing voor het verzamelen van Logboeken gerelateerde toohello gehele cluster en afzonderlijke clusterknooppunten. Het is veel meer betrouwbare manier, dan in-process logboekgegevens verzameld, toodiagnose service opstartproblemen en crashes. Ook met veel services actief zijn binnen een Service Fabric-cluster, resulteert elke service tijdens het doorzoeken van de eigen logboekverzameling in-process in talloze uitgaande verbindingen van Hallo-cluster. Groot aantal uitgaande verbindingen is voor Hallo netwerksubsysteem en Hallo logboekbestemming belasten. Een agent zoals [ **Azure Diagnostics** ](../cloud-services/cloud-services-dotnet-diagnostics.md) kunt verzamelen van gegevens uit meerdere services en verzenden van alle gegevens via een aantal verbindingen, doorvoer te verbeteren. 

In dit artikel wordt gedemonstreerd hoe tooset van een proces Meld verzameling met [ **EventFlow open source bibliotheek**](https://github.com/Azure/diagnostics-eventflow). Andere bibliotheken kunnen worden gebruikt voor Hallo hetzelfde doel, maar EventFlow Hallo voordeel dat is speciaal ontworpen voor proces logboek verzameling en toosupport Service Fabric-services heeft. We gebruiken [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) als Hallo logboekbestemming. Andere bestemmingen zoals [ **Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) of [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) worden ook ondersteund. Het is alleen een kwestie van het juiste NuGet-pakket installeren en configureren van Hallo bestemming in Hallo EventFlow-configuratiebestand. Zie voor meer informatie over bestemmingen logboek dan Application Insights [EventFlow documentatie](https://github.com/Azure/diagnostics-eventflow).

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>EventFlow bibliotheek tooa Service Fabric-service-project toe te voegen
EventFlow binaire bestanden zijn beschikbaar als een reeks NuGet-pakketten. tooadd EventFlow tooa Service Fabric-service-project met de rechtermuisknop op het Hallo-project in Solution Explorer Hallo en kiest u 'Manage NuGet packages'. Overschakelen toohello 'Zoeken' tabblad en zoek naar '`Diagnostics.EventFlow`':

![EventFlow NuGet-pakketten in Visual Studio-NuGet-Pakketbeheer gebruikersinterface][1]

Hallo-service die als host fungeert voor EventFlow bevatten juiste pakketten, afhankelijk van het Hallo-bron en bestemming voor toepassingslogboeken Hallo. Hallo volgende pakketten toevoegen: 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (toocapture gegevens uit Hallo van EventSource serviceklasse, en standard EventSources zoals *ServiceFabric-Microsoft-Services* en *Microsoft-ServiceFabric-Actors*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * (we gaan toosend Hallo logboeken tooan Azure Application Insights-resource)  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * (Hiermee initialisatie van Hallo EventFlow pijplijn van de configuratie van de Service Fabric-service en eventuele problemen met het verzenden van diagnostische gegevens als Service Fabric-statusrapporten rapporten)

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`pakket moeten Hallo service project tootarget .NET Framework 4.6 of hoger. Zorg ervoor dat u Hallo juiste doel-framework in Projecteigenschappen instellen voordat u dit pakket installeert. 

Nadat alle hello-pakketten worden geïnstalleerd, de volgende stap Hallo tooconfigure is en EventFlow inschakelen in Hallo-service.

## <a name="configuring-and-enabling-log-collection"></a>Configureren en inschakelen van verzamelen
EventFlow pipeline, verantwoordelijk voor het verzenden van Hallo zich aanmeldt, wordt gemaakt van een specificatie die is opgeslagen in een configuratiebestand. `Microsoft.Diagnostics.EventFlow.ServiceFabric`pakket installeert u een eerste EventFlow configuratiebestand onder `PackageRoot\Config` oplossingenmap. Hallo-bestandsnaam is `eventFlowConfig.json`. Dit configuratiebestand moet toobe gewijzigd toocapture gegevens van de standaardservice Hallo `EventSource` klasse en het verzenden van gegevens tooApplication Insights-service.

> [!NOTE]
> We gaan ervan uit dat u bekend met bent **Azure Application Insights** -service en of er een Application Insights-resource dat u van plan toouse toomonitor uw Service Fabric-service bent. Als u meer informatie, Zie [een Application Insights-resource maken](../application-insights/app-insights-create-new-resource.md).

Open Hallo `eventFlowConfig.json` -bestand in Hallo-editor en de inhoud ervan wijzigen, zoals hieronder wordt weergegeven. Zorg ervoor dat tooreplace hello ServiceEventSource naam en het Application Insights-instrumentatiesleutel volgens toocomments. 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> Hallo-naam van ServiceEventSource van de service is Hallo-waarde van Name-eigenschap van Hallo Hallo `EventSourceAttribute` toohello ServiceEventSource klasse toegepast. Deze al is opgegeven in Hallo `ServiceEventSource.cs` bestand, dat deel uitmaakt van de servicecode Hallo. Bijvoorbeeld, in Hallo volgende codefragment Hallo codenaam Hallo ServiceEventSource is *mijnbedrijf-Toepassing1-Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

Houd er rekening mee dat `eventFlowConfig.json` bestand maakt deel uit van het configuratiepakket service. Wijzigingen toothis bestand kan worden opgenomen in de volledige - of configuratie-only upgrades van Hallo-service, het onderwerp tooService Fabric statuscontroles en automatisch terugdraaien als er een mislukte upgrade. Zie voor meer informatie [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).

de laatste stap Hallo is tooinstantiate EventFlow pijplijn in uw service starten van de code, zich in `Program.cs` bestand. In Hallo volgende voorbeeld EventFlow-gerelateerde toevoegingen zijn gemarkeerd met opmerkingen beginnen met `****`:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    
                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

Hallo naam doorgegeven als parameter Hallo Hallo `CreatePipeline` methode Hallo `ServiceFabricDiagnosticsPipelineFactory` heet Hallo Hallo *health entiteit* hello EventFlow logboek verzameling pipeline die aangeeft. Deze naam wordt gebruikt als EventFlow aantreft en de fout en via Service Fabric health subsysteem Hallo gerapporteerd.

## <a name="verification"></a>Verificatie
De service starten en houd rekening met Hallo foutopsporing uitvoervenster in Visual Studio. Nadat het Hallo-service is gestart, moet u eerst zien bewijs dat uw service 'Application Insights Telemetry' records verzendt. Open een webbrowser en navigeer Ga tooyour Application Insights-resource. Open het tabblad "Zoeken" (bovenaan Hallo Hallo 'Overview' standaardblade). Na een korte vertraging leest u eerst de traceringen in Hallo Application Insights-portal te zien:

![Application Insights-portal met Logboeken van een Service Fabric-toepassing][2]

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over het diagnosticeren en controleren van een Service Fabric-service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [EventFlow documentatie](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
