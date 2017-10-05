---
title: Aggregatie van Azure Service Fabric-gebeurtenis met EventFlow | Microsoft Docs
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
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="eff39-103">Gebeurtenis-aggregatie en verzameling op basis van EventFlow</span><span class="sxs-lookup"><span data-stu-id="eff39-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="eff39-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) gebeurtenissen van een knooppunt naar een of meer controle bestemmingen kunt versturen.</span><span class="sxs-lookup"><span data-stu-id="eff39-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="eff39-105">Omdat het is opgenomen als een NuGet-pakket in uw serviceproject, reizen EventFlow code en configuratie met de service, het incompatibiliteitsprobleem per knooppunt configuratie eerder genoemde over Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="eff39-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="eff39-106">EventFlow binnen uw serviceproces wordt uitgevoerd en rechtstreeks verbinding maakt met de geconfigureerde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="eff39-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="eff39-107">Vanwege de rechtstreekse verbinding werkt EventFlow voor Azure-container en on-premises service-implementaties.</span><span class="sxs-lookup"><span data-stu-id="eff39-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="eff39-108">Let als u EventFlow in high-density scenario's, zoals in een container uitvoert, omdat elke EventFlow pijplijn een externe verbinding wordt.</span><span class="sxs-lookup"><span data-stu-id="eff39-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="eff39-109">Dus als u verschillende processen host, u verschillende uitgaande verbindingen krijgt!</span><span class="sxs-lookup"><span data-stu-id="eff39-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="eff39-110">Is dit niet zo veel mogelijk een probleem voor Service Fabric-toepassingen, omdat alle replica's van een `ServiceType` in hetzelfde proces worden uitgevoerd en dit beperkt het aantal uitgaande verbindingen.</span><span class="sxs-lookup"><span data-stu-id="eff39-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="eff39-111">EventFlow biedt ook filteren van gebeurtenissen, zodat alleen de gebeurtenissen die overeenkomen met het opgegeven filter worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="eff39-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="eff39-112">EventFlow instellen</span><span class="sxs-lookup"><span data-stu-id="eff39-112">Setting up EventFlow</span></span>

<span data-ttu-id="eff39-113">EventFlow binaire bestanden zijn beschikbaar als een reeks NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="eff39-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="eff39-114">EventFlow toevoegen aan een Service Fabric-service-project, met de rechtermuisknop op het project in Solution Explorer en kiest u 'Manage NuGet packages'.</span><span class="sxs-lookup"><span data-stu-id="eff39-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="eff39-115">Overschakelen naar het tabblad 'Zoeken' en zoek naar '`Diagnostics.EventFlow`':</span><span class="sxs-lookup"><span data-stu-id="eff39-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![EventFlow NuGet-pakketten in Visual Studio-NuGet-Pakketbeheer gebruikersinterface](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="eff39-117">U ziet een lijst met verschillende pakketten die worden weergegeven, met labels met 'Invoer' en 'Levert'.</span><span class="sxs-lookup"><span data-stu-id="eff39-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="eff39-118">EventFlow ondersteunt verschillende andere logboekregistratie providers en analyzers.</span><span class="sxs-lookup"><span data-stu-id="eff39-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="eff39-119">De service die als host fungeert voor EventFlow moet de juiste pakketten, afhankelijk van de bron en bestemming voor de toepassingslogboeken bevatten.</span><span class="sxs-lookup"><span data-stu-id="eff39-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="eff39-120">Naast het core ServiceFabric pakket, moet u ook minimaal één invoer en uitvoer geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="eff39-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="eff39-121">Voor het voorbeeld, kunt u de volgende pakketten toevoegen aan verzonden EventSource gebeurtenissen naar Application Insights:</span><span class="sxs-lookup"><span data-stu-id="eff39-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="eff39-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`voor het vastleggen van gegevens uit de serviceklasse EventSource, en standard EventSources zoals *ServiceFabric-Microsoft-Services* en *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="eff39-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="eff39-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(we gaan de logboeken verzenden naar een Azure Application Insights-resource)</span><span class="sxs-lookup"><span data-stu-id="eff39-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="eff39-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(Hiermee initialisatie van de pijplijn EventFlow van de configuratie van de Service Fabric-service en eventuele problemen met het verzenden van diagnostische gegevens als Service Fabric-statusrapporten rapporten)</span><span class="sxs-lookup"><span data-stu-id="eff39-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="eff39-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`pakket is de service-project toe te passen van .NET Framework 4.6 of hoger vereist.</span><span class="sxs-lookup"><span data-stu-id="eff39-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="eff39-126">Zorg ervoor dat u het juiste doel-framework in Projecteigenschappen instellen voordat u dit pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="eff39-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="eff39-127">Nadat alle pakketten zijn geïnstalleerd, wordt de volgende stap is het configureren en inschakelen van EventFlow in de service.</span><span class="sxs-lookup"><span data-stu-id="eff39-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="eff39-128">Configureren en inschakelen van verzamelen</span><span class="sxs-lookup"><span data-stu-id="eff39-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="eff39-129">De pijplijn EventFlow verantwoordelijk voor het verzenden van de logboeken wordt gemaakt van een specificatie die is opgeslagen in een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="eff39-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="eff39-130">De `Microsoft.Diagnostics.EventFlow.ServiceFabric` pakket installeert u een eerste EventFlow configuratiebestand onder `PackageRoot\Config` oplossingenmap met de naam `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="eff39-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="eff39-131">Dit configuratiebestand moet worden gewijzigd voor het vastleggen van gegevens van de standaardservice `EventSource` klasse en alle andere invoer die u wilt configureren en gegevens verzenden naar de juiste plaats.</span><span class="sxs-lookup"><span data-stu-id="eff39-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="eff39-132">Hier volgt een voorbeeld *eventFlowConfig.json* op basis van de hierboven genoemde NuGet-pakketten:</span><span class="sxs-lookup"><span data-stu-id="eff39-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
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
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="eff39-133">De naam van de ServiceEventSource van de service is de waarde van de eigenschap Name van de `EventSourceAttribute` toegepast op de klasse ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="eff39-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="eff39-134">Deze al is opgegeven in de `ServiceEventSource.cs` -bestand, dat deel uitmaakt van de servicecode.</span><span class="sxs-lookup"><span data-stu-id="eff39-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="eff39-135">In het volgende codefragment de naam van de ServiceEventSource is bijvoorbeeld *mijnbedrijf-Toepassing1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="eff39-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="eff39-136">Houd er rekening mee dat `eventFlowConfig.json` bestand maakt deel uit van het configuratiepakket service.</span><span class="sxs-lookup"><span data-stu-id="eff39-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="eff39-137">Wijzigingen in dit bestand kunnen worden opgenomen in de volledige - of configuratie-only upgrades van de service, zijn de Service Fabric-upgrade statuscontroles en automatisch terugdraaien als er een mislukte upgrade.</span><span class="sxs-lookup"><span data-stu-id="eff39-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="eff39-138">Zie voor meer informatie [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="eff39-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="eff39-139">De *filters* sectie van de configuratie kunt u verder aanpassen van de informatie die u naar de uitvoer, zodat u kunt verwijderen of bepaalde informatie bevatten die via de pipeline EventFlow of wijzig de structuur van de gebeurtenisgegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="eff39-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="eff39-140">Zie voor meer informatie over filters [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="eff39-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="eff39-141">De laatste stap is het instantiëren van EventFlow pijplijn in uw service starten van de code, zich in `Program.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="eff39-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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
        /// This is the entry point of the service host process.
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

<span data-ttu-id="eff39-142">Naam van de doorgegeven als parameter van de `CreatePipeline` methode van de `ServiceFabricDiagnosticsPipelineFactory` is de naam van de *health entiteit* die de pijplijn EventFlow logboek verzameling vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="eff39-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="eff39-143">Deze naam wordt gebruikt als EventFlow aantreft en de fout en gerapporteerd via het subsysteem van de health Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eff39-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="eff39-144">Service Fabric-instellingen en parameters voor de toepassing te gebruiken in eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="eff39-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="eff39-145">EventFlow ondersteunt het gebruik van Service Fabric-instellingen en parameters van de toepassing om EventFlow instellingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="eff39-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="eff39-146">U kunt verwijzen naar Service Fabric-instellingen parameters in met behulp van deze speciale syntaxis voor waarden:</span><span class="sxs-lookup"><span data-stu-id="eff39-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="eff39-147">`<section-name>`de naam van de configuratiesectie Service Fabric en `<setting-name>` is de configuratieinstelling de waarde die wordt gebruikt voor het configureren van een instelling EventFlow op te geven.</span><span class="sxs-lookup"><span data-stu-id="eff39-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="eff39-148">Om te lezen over hoe u dit doet, gaat u naar [ondersteuning voor Service Fabric-instellingen en parameters voor de toepassing](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="eff39-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="eff39-149">Verificatie</span><span class="sxs-lookup"><span data-stu-id="eff39-149">Verification</span></span>

<span data-ttu-id="eff39-150">De service starten en houd rekening met de opdracht Debug uitvoervenster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eff39-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="eff39-151">Nadat de service is gestart, moet u eerst zien bewijs dat uw service records verzendt naar de uitvoer die u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="eff39-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="eff39-152">Navigeer naar uw platform voor analyse en visualisatie van gebeurtenis en controleer of de logboeken hebt gestart om weer te geven tot (kan enkele minuten duren).</span><span class="sxs-lookup"><span data-stu-id="eff39-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eff39-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eff39-153">Next steps</span></span>

* [<span data-ttu-id="eff39-154">Analyse van gebeurtenis en visualisatie met Application Insights</span><span class="sxs-lookup"><span data-stu-id="eff39-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="eff39-155">Analyse van gebeurtenis en visualisatie met OMS</span><span class="sxs-lookup"><span data-stu-id="eff39-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="eff39-156">EventFlow documentatie</span><span class="sxs-lookup"><span data-stu-id="eff39-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)