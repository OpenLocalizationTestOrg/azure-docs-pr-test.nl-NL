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
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="27843-103">Gebeurtenis-aggregatie en verzameling op basis van EventFlow</span><span class="sxs-lookup"><span data-stu-id="27843-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="27843-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) gebeurtenissen van een knooppunt tooone of meer controle bestemmingen kunt versturen.</span><span class="sxs-lookup"><span data-stu-id="27843-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="27843-105">Omdat het is opgenomen als een NuGet-pakket in uw serviceproject, reizen EventFlow code en configuratie met Hallo-service, elimineren Hallo per knooppunt probleem met de eerder genoemde over Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="27843-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="27843-106">EventFlow binnen uw serviceproces wordt uitgevoerd en verbindt rechtstreeks toohello geconfigureerd uitvoer.</span><span class="sxs-lookup"><span data-stu-id="27843-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="27843-107">Vanwege de rechtstreekse verbinding hello werkt EventFlow voor Azure-container en on-premises service-implementaties.</span><span class="sxs-lookup"><span data-stu-id="27843-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="27843-108">Let als u EventFlow in high-density scenario's, zoals in een container uitvoert, omdat elke EventFlow pijplijn een externe verbinding wordt.</span><span class="sxs-lookup"><span data-stu-id="27843-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="27843-109">Dus als u verschillende processen host, u verschillende uitgaande verbindingen krijgt!</span><span class="sxs-lookup"><span data-stu-id="27843-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="27843-110">Is dit niet zo veel mogelijk een probleem voor Service Fabric-toepassingen, omdat alle replica's van een `ServiceType` uitgevoerd in Hallo dezelfde verwerken en Hiermee wordt het aantal uitgaande verbindingen Hallo beperkt.</span><span class="sxs-lookup"><span data-stu-id="27843-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="27843-111">EventFlow biedt ook filteren van gebeurtenissen, zodat alleen Hallo-gebeurtenissen die overeenkomen met het opgegeven filter Hallo worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="27843-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="27843-112">EventFlow instellen</span><span class="sxs-lookup"><span data-stu-id="27843-112">Setting up EventFlow</span></span>

<span data-ttu-id="27843-113">EventFlow binaire bestanden zijn beschikbaar als een reeks NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="27843-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="27843-114">tooadd EventFlow tooa Service Fabric-service-project met de rechtermuisknop op het Hallo-project in Solution Explorer Hallo en kiest u 'Manage NuGet packages'.</span><span class="sxs-lookup"><span data-stu-id="27843-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="27843-115">Overschakelen toohello 'Zoeken' tabblad en zoek naar '`Diagnostics.EventFlow`':</span><span class="sxs-lookup"><span data-stu-id="27843-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![EventFlow NuGet-pakketten in Visual Studio-NuGet-Pakketbeheer gebruikersinterface](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="27843-117">U ziet een lijst met verschillende pakketten die worden weergegeven, met labels met 'Invoer' en 'Levert'.</span><span class="sxs-lookup"><span data-stu-id="27843-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="27843-118">EventFlow ondersteunt verschillende andere logboekregistratie providers en analyzers.</span><span class="sxs-lookup"><span data-stu-id="27843-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="27843-119">Hallo-service die als host fungeert voor EventFlow bevatten juiste pakketten, afhankelijk van het Hallo-bron en bestemming voor toepassingslogboeken Hallo.</span><span class="sxs-lookup"><span data-stu-id="27843-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="27843-120">Bovendien toohello core ServiceFabric pakket, moet u ook minimaal één invoer en uitvoer geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="27843-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="27843-121">Voor het voorbeeld, kunt u hello-pakketten toosent EventSource gebeurtenissen tooApplication Insights volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="27843-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="27843-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture gegevens uit Hallo van EventSource serviceklasse, en standard EventSources zoals *ServiceFabric-Microsoft-Services* en *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="27843-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="27843-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(we gaan toosend Hallo logboeken tooan Azure Application Insights-resource)</span><span class="sxs-lookup"><span data-stu-id="27843-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="27843-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(Hiermee initialisatie van Hallo EventFlow pijplijn van de configuratie van de Service Fabric-service en eventuele problemen met het verzenden van diagnostische gegevens als Service Fabric-statusrapporten rapporten)</span><span class="sxs-lookup"><span data-stu-id="27843-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="27843-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`pakket moeten Hallo service project tootarget .NET Framework 4.6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="27843-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="27843-126">Zorg ervoor dat u Hallo juiste doel-framework in Projecteigenschappen instellen voordat u dit pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="27843-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="27843-127">Nadat alle hello-pakketten worden geïnstalleerd, de volgende stap Hallo tooconfigure is en EventFlow inschakelen in Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="27843-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="27843-128">Configureren en inschakelen van verzamelen</span><span class="sxs-lookup"><span data-stu-id="27843-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="27843-129">Hallo EventFlow pijplijn verantwoordelijk voor het verzenden van Hallo Logboeken wordt gemaakt van een specificatie die is opgeslagen in een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="27843-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="27843-130">Hallo `Microsoft.Diagnostics.EventFlow.ServiceFabric` pakket installeert u een eerste EventFlow configuratiebestand onder `PackageRoot\Config` oplossingenmap met de naam `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="27843-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="27843-131">Dit configuratiebestand moet toobe gewijzigd toocapture gegevens van de standaardservice Hallo `EventSource` klasse en alle andere invoer die u wilt tooconfigure en verzenden van gegevens toohello geschikte plaats.</span><span class="sxs-lookup"><span data-stu-id="27843-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="27843-132">Hier volgt een voorbeeld *eventFlowConfig.json* op basis van Hallo bovengenoemde NuGet-pakketten:</span><span class="sxs-lookup"><span data-stu-id="27843-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="27843-133">Hallo-naam van ServiceEventSource van de service is Hallo-waarde van Name-eigenschap van Hallo Hallo `EventSourceAttribute` toohello ServiceEventSource klasse toegepast.</span><span class="sxs-lookup"><span data-stu-id="27843-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="27843-134">Deze al is opgegeven in Hallo `ServiceEventSource.cs` bestand, dat deel uitmaakt van de servicecode Hallo.</span><span class="sxs-lookup"><span data-stu-id="27843-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="27843-135">Bijvoorbeeld, in Hallo volgende codefragment Hallo codenaam Hallo ServiceEventSource is *mijnbedrijf-Toepassing1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="27843-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="27843-136">Houd er rekening mee dat `eventFlowConfig.json` bestand maakt deel uit van het configuratiepakket service.</span><span class="sxs-lookup"><span data-stu-id="27843-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="27843-137">Wijzigingen toothis bestand kan worden opgenomen in de volledige - of configuratie-only upgrades van Hallo-service, het onderwerp tooService Fabric statuscontroles en automatisch terugdraaien als er een mislukte upgrade.</span><span class="sxs-lookup"><span data-stu-id="27843-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="27843-138">Zie voor meer informatie [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="27843-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="27843-139">Hallo *filters* sectie van het Hallo-configuratie kunt u toofurther Hallo-informatie die gaat toogo hello EventFlow pijplijn toohello uitvoer, zodat u toodrop in aanpassen of bepaalde informatie te bevatten of Hallo wijzigen structuur van Hallo gebeurtenisgegevens.</span><span class="sxs-lookup"><span data-stu-id="27843-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="27843-140">Zie voor meer informatie over filters [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="27843-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="27843-141">de laatste stap Hallo is tooinstantiate EventFlow pijplijn in uw service starten van de code, zich in `Program.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="27843-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="27843-142">Hallo naam doorgegeven als parameter Hallo Hallo `CreatePipeline` methode Hallo `ServiceFabricDiagnosticsPipelineFactory` heet Hallo Hallo *health entiteit* hello EventFlow logboek verzameling pipeline die aangeeft.</span><span class="sxs-lookup"><span data-stu-id="27843-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="27843-143">Deze naam wordt gebruikt als EventFlow aantreft en de fout en via Service Fabric health subsysteem Hallo gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="27843-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="27843-144">Met behulp van Service Fabric-instellingen en toepassing parameters tooin eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="27843-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="27843-145">EventFlow ondersteunt het gebruik van Service Fabric-instellingen en parameters tooconfigure EventFlow toepassingsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="27843-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="27843-146">U kunt tooService Fabric instellingen parameters met deze specifieke syntaxis voor waarden verwijzen:</span><span class="sxs-lookup"><span data-stu-id="27843-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="27843-147">`<section-name>`Hallo-naam van Service Fabric-configuratiesectie, Hallo en `<setting-name>` Hallo Hallo-waarde die wordt gebruikt tooconfigure bieden een instelling EventFlow configuratie-instelling is.</span><span class="sxs-lookup"><span data-stu-id="27843-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="27843-148">meer informatie over hoe tooread toodo daarvoor, gaat u te[ondersteuning voor Service Fabric-instellingen en parameters voor de toepassing](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="27843-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="27843-149">Verificatie</span><span class="sxs-lookup"><span data-stu-id="27843-149">Verification</span></span>

<span data-ttu-id="27843-150">De service starten en houd rekening met Hallo foutopsporing uitvoervenster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27843-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="27843-151">Nadat het Hallo-service is gestart, moet u eerst zien bewijs dat uw service verzendt registreert toohello uitvoer die u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="27843-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="27843-152">Navigeer tooyour gebeurtenis analyse en visualisatie platform en Bevestig dat Logboeken tooshow hebt gestart omhoog (kan enkele minuten duren).</span><span class="sxs-lookup"><span data-stu-id="27843-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27843-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="27843-153">Next steps</span></span>

* [<span data-ttu-id="27843-154">Analyse van gebeurtenis en visualisatie met Application Insights</span><span class="sxs-lookup"><span data-stu-id="27843-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="27843-155">Analyse van gebeurtenis en visualisatie met OMS</span><span class="sxs-lookup"><span data-stu-id="27843-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="27843-156">EventFlow documentatie</span><span class="sxs-lookup"><span data-stu-id="27843-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)