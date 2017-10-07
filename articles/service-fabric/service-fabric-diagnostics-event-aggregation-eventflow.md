---
title: Aggregatie van Service Fabric-gebeurtenis met EventFlow aaaAzure | Microsoft Docs
description: Meer informatie over het aggregeren en het verzamelen van gebeurtenissen met EventFlow voor controle en diagnostische gegevens van Azure Service Fabric-clusters.
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
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a>Gebeurtenis-aggregatie en verzameling op basis van EventFlow

[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) gebeurtenissen van een knooppunt tooone of meer controle bestemmingen kunt versturen. Omdat het is opgenomen als een NuGet-pakket in uw serviceproject, reizen EventFlow code en configuratie met Hallo-service, elimineren Hallo per knooppunt probleem met de eerder genoemde over Azure Diagnostics. EventFlow binnen uw serviceproces wordt uitgevoerd en verbindt rechtstreeks toohello geconfigureerd uitvoer. Vanwege de rechtstreekse verbinding hello werkt EventFlow voor Azure-container en on-premises service-implementaties. Let als u EventFlow in high-density scenario's, zoals in een container uitvoert, omdat elke EventFlow pijplijn een externe verbinding wordt. Dus als u verschillende processen host, u verschillende uitgaande verbindingen krijgt! Is dit niet zo veel mogelijk een probleem voor Service Fabric-toepassingen, omdat alle replica's van een `ServiceType` uitgevoerd in Hallo dezelfde verwerken en Hiermee wordt het aantal uitgaande verbindingen Hallo beperkt. EventFlow biedt ook filteren van gebeurtenissen, zodat alleen Hallo-gebeurtenissen die overeenkomen met het opgegeven filter Hallo worden verzonden.

## <a name="setting-up-eventflow"></a>EventFlow instellen

EventFlow binaire bestanden zijn beschikbaar als een reeks NuGet-pakketten. tooadd EventFlow tooa Service Fabric-service-project met de rechtermuisknop op het Hallo-project in Solution Explorer Hallo en kiest u 'Manage NuGet packages'. Overschakelen toohello 'Zoeken' tabblad en zoek naar '`Diagnostics.EventFlow`':

![EventFlow NuGet-pakketten in Visual Studio-NuGet-Pakketbeheer gebruikersinterface](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

U ziet een lijst met verschillende pakketten die worden weergegeven, met labels met 'Invoer' en 'Levert'. EventFlow ondersteunt verschillende andere logboekregistratie providers en analyzers. Hallo-service die als host fungeert voor EventFlow bevatten juiste pakketten, afhankelijk van het Hallo-bron en bestemming voor toepassingslogboeken Hallo. Bovendien toohello core ServiceFabric pakket, moet u ook minimaal één invoer en uitvoer geconfigureerd. Voor het voorbeeld, kunt u hello-pakketten toosent EventSource gebeurtenissen tooApplication Insights volgende toevoegen:

* `Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture gegevens uit Hallo van EventSource serviceklasse, en standard EventSources zoals *ServiceFabric-Microsoft-Services* en *Microsoft-ServiceFabric-Actors*)
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(we gaan toosend Hallo logboeken tooan Azure Application Insights-resource)
* `Microsoft.Diagnostics.EventFlow.ServiceFabric`(Hiermee initialisatie van Hallo EventFlow pijplijn van de configuratie van de Service Fabric-service en eventuele problemen met het verzenden van diagnostische gegevens als Service Fabric-statusrapporten rapporten)

>[!NOTE]
>`Microsoft.Diagnostics.EventFlow.Input.EventSource`pakket moeten Hallo service project tootarget .NET Framework 4.6 of hoger. Zorg ervoor dat u Hallo juiste doel-framework in Projecteigenschappen instellen voordat u dit pakket installeert.

Nadat alle hello-pakketten worden geïnstalleerd, de volgende stap Hallo tooconfigure is en EventFlow inschakelen in Hallo-service.

## <a name="configuring-and-enabling-log-collection"></a>Configureren en inschakelen van verzamelen
Hallo EventFlow pijplijn verantwoordelijk voor het verzenden van Hallo Logboeken wordt gemaakt van een specificatie die is opgeslagen in een configuratiebestand. Hallo `Microsoft.Diagnostics.EventFlow.ServiceFabric` pakket installeert u een eerste EventFlow configuratiebestand onder `PackageRoot\Config` oplossingenmap met de naam `eventFlowConfig.json`. Dit configuratiebestand moet toobe gewijzigd toocapture gegevens van de standaardservice Hallo `EventSource` klasse en alle andere invoer die u wilt tooconfigure en verzenden van gegevens toohello geschikte plaats.

Hier volgt een voorbeeld *eventFlowConfig.json* op basis van Hallo bovengenoemde NuGet-pakketten:
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

Hallo-naam van ServiceEventSource van de service is Hallo-waarde van Name-eigenschap van Hallo Hallo `EventSourceAttribute` toohello ServiceEventSource klasse toegepast. Deze al is opgegeven in Hallo `ServiceEventSource.cs` bestand, dat deel uitmaakt van de servicecode Hallo. Bijvoorbeeld, in Hallo volgende codefragment Hallo codenaam Hallo ServiceEventSource is *mijnbedrijf-Toepassing1-Stateless1*:

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

Houd er rekening mee dat `eventFlowConfig.json` bestand maakt deel uit van het configuratiepakket service. Wijzigingen toothis bestand kan worden opgenomen in de volledige - of configuratie-only upgrades van Hallo-service, het onderwerp tooService Fabric statuscontroles en automatisch terugdraaien als er een mislukte upgrade. Zie voor meer informatie [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).

Hallo *filters* sectie van het Hallo-configuratie kunt u toofurther Hallo-informatie die gaat toogo hello EventFlow pijplijn toohello uitvoer, zodat u toodrop in aanpassen of bepaalde informatie te bevatten of Hallo wijzigen structuur van Hallo gebeurtenisgegevens. Zie voor meer informatie over filters [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).

de laatste stap Hallo is tooinstantiate EventFlow pijplijn in uw service starten van de code, zich in `Program.cs` bestand:

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

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a>Met behulp van Service Fabric-instellingen en toepassing parameters tooin eventFlowConfig

EventFlow ondersteunt het gebruik van Service Fabric-instellingen en parameters tooconfigure EventFlow toepassingsinstellingen. U kunt tooService Fabric instellingen parameters met deze specifieke syntaxis voor waarden verwijzen:

```json
servicefabric:/<section-name>/<setting-name>
``` 

`<section-name>`Hallo-naam van Service Fabric-configuratiesectie, Hallo en `<setting-name>` Hallo Hallo-waarde die wordt gebruikt tooconfigure bieden een instelling EventFlow configuratie-instelling is. meer informatie over hoe tooread toodo daarvoor, gaat u te[ondersteuning voor Service Fabric-instellingen en parameters voor de toepassing](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).

## <a name="verification"></a>Verificatie

De service starten en houd rekening met Hallo foutopsporing uitvoervenster in Visual Studio. Nadat het Hallo-service is gestart, moet u eerst zien bewijs dat uw service verzendt registreert toohello uitvoer die u hebt geconfigureerd. Navigeer tooyour gebeurtenis analyse en visualisatie platform en Bevestig dat Logboeken tooshow hebt gestart omhoog (kan enkele minuten duren).

## <a name="next-steps"></a>Volgende stappen

* [Analyse van gebeurtenis en visualisatie met Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Analyse van gebeurtenis en visualisatie met OMS](service-fabric-diagnostics-event-analysis-oms.md)
* [EventFlow documentatie](https://github.com/Azure/diagnostics-eventflow)