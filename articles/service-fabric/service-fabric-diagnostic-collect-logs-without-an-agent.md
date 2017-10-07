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
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="c6720-103">Logboeken rechtstreeks vanaf een Azure Service Fabric-serviceproces verzamelen</span><span class="sxs-lookup"><span data-stu-id="c6720-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="c6720-104">In-process-logboekgegevens verzameld</span><span class="sxs-lookup"><span data-stu-id="c6720-104">In-process log collection</span></span>
<span data-ttu-id="c6720-105">Verzamelen van de toepassing registreert met behulp van [extensie voor diagnostische gegevens van Azure](service-fabric-diagnostics-how-to-setup-wad.md) is een goede optie voor **Azure Service Fabric** services als Hallo reeks logboek bronnen en bestemmingen klein is, verandert niet vaak en er is een eenvoudige toewijzing tussen Hallo bronnen en hun bestemmingen.</span><span class="sxs-lookup"><span data-stu-id="c6720-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="c6720-106">Als dat niet het geval is, moet u een alternatief is toohave services hun logboeken verzenden rechtstreeks tooa centrale locatie.</span><span class="sxs-lookup"><span data-stu-id="c6720-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="c6720-107">Dit proces wordt ook wel **proces logboekverzameling** en heeft verschillende mogelijke voordelen:</span><span class="sxs-lookup"><span data-stu-id="c6720-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="c6720-108">*Eenvoudige configuratie en implementatie*</span><span class="sxs-lookup"><span data-stu-id="c6720-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="c6720-109">Hallo-configuratie van verzamelen van diagnostische gegevens net is onderdeel van de serviceconfiguratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6720-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="c6720-110">Het is gemakkelijk tooalways Houd deze 'synchroon' Hello rest van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="c6720-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="c6720-111">Configuratie van per toepassing of per-service is eenvoudig haalbare.</span><span class="sxs-lookup"><span data-stu-id="c6720-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="c6720-112">Verzamelen op basis van een agent vereist gewoonlijk een afzonderlijke implementatie en configuratie van Hallo diagnostische agent, die een extra beheertaak en een mogelijke oorzaak van fouten is.</span><span class="sxs-lookup"><span data-stu-id="c6720-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="c6720-113">Vaak is er slechts één exemplaar van Hallo agent toegestaan per virtuele machine (knooppunt) en de agentconfiguratie hello wordt gedeeld door alle toepassingen en services die op dat knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6720-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="c6720-114">*Flexibiliteit*</span><span class="sxs-lookup"><span data-stu-id="c6720-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="c6720-115">Hallo-toepassing kunt hello gegevens verzenden waar het toogo, moet, zolang er is een clientbibliotheek die ondersteuning biedt voor systeem voor gegevensopslag Hallo gericht.</span><span class="sxs-lookup"><span data-stu-id="c6720-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="c6720-116">Nieuwe doelen kunnen worden toegevoegd naar wens.</span><span class="sxs-lookup"><span data-stu-id="c6720-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="c6720-117">Complexe regels voor het vastleggen, filteren en samenvoegen van gegevens kunnen worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c6720-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="c6720-118">Verzamelen op basis van een agent wordt vaak beperkt door Hallo gegevens put die Hallo agent ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="c6720-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="c6720-119">Sommige agents worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="c6720-119">Some agents are extensible.</span></span>

* <span data-ttu-id="c6720-120">*Toegang toointernal toepassingsgegevens en -context*</span><span class="sxs-lookup"><span data-stu-id="c6720-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="c6720-121">Hallo diagnostische subsysteem uitvoering binnen Hallo toepassing/service-proces kan eenvoudig hello traceringen met contextafhankelijke informatie verbeteren.</span><span class="sxs-lookup"><span data-stu-id="c6720-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="c6720-122">Met op basis van een agent logboekverzameling moet op Hallo gegevens tooan agent via een mechanisme voor communicatie tussen processen, zoals Event Tracing for Windows worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="c6720-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="c6720-123">Dit mechanisme kan aanvullende beperkingen opleggen.</span><span class="sxs-lookup"><span data-stu-id="c6720-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="c6720-124">Het is mogelijk toocombine en voordelen van beide methoden verzameling.</span><span class="sxs-lookup"><span data-stu-id="c6720-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="c6720-125">Inderdaad, mogelijk de beste oplossing Hallo voor veel toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c6720-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="c6720-126">Verzameling op basis van een agent is een natuurlijke oplossing voor het verzamelen van Logboeken gerelateerde toohello gehele cluster en afzonderlijke clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="c6720-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="c6720-127">Het is veel meer betrouwbare manier, dan in-process logboekgegevens verzameld, toodiagnose service opstartproblemen en crashes.</span><span class="sxs-lookup"><span data-stu-id="c6720-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="c6720-128">Ook met veel services actief zijn binnen een Service Fabric-cluster, resulteert elke service tijdens het doorzoeken van de eigen logboekverzameling in-process in talloze uitgaande verbindingen van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="c6720-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="c6720-129">Groot aantal uitgaande verbindingen is voor Hallo netwerksubsysteem en Hallo logboekbestemming belasten.</span><span class="sxs-lookup"><span data-stu-id="c6720-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="c6720-130">Een agent zoals [ **Azure Diagnostics** ](../cloud-services/cloud-services-dotnet-diagnostics.md) kunt verzamelen van gegevens uit meerdere services en verzenden van alle gegevens via een aantal verbindingen, doorvoer te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="c6720-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="c6720-131">In dit artikel wordt gedemonstreerd hoe tooset van een proces Meld verzameling met [ **EventFlow open source bibliotheek**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="c6720-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="c6720-132">Andere bibliotheken kunnen worden gebruikt voor Hallo hetzelfde doel, maar EventFlow Hallo voordeel dat is speciaal ontworpen voor proces logboek verzameling en toosupport Service Fabric-services heeft.</span><span class="sxs-lookup"><span data-stu-id="c6720-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="c6720-133">We gebruiken [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) als Hallo logboekbestemming.</span><span class="sxs-lookup"><span data-stu-id="c6720-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="c6720-134">Andere bestemmingen zoals [ **Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) of [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) worden ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c6720-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="c6720-135">Het is alleen een kwestie van het juiste NuGet-pakket installeren en configureren van Hallo bestemming in Hallo EventFlow-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="c6720-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="c6720-136">Zie voor meer informatie over bestemmingen logboek dan Application Insights [EventFlow documentatie](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="c6720-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="c6720-137">EventFlow bibliotheek tooa Service Fabric-service-project toe te voegen</span><span class="sxs-lookup"><span data-stu-id="c6720-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="c6720-138">EventFlow binaire bestanden zijn beschikbaar als een reeks NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="c6720-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="c6720-139">tooadd EventFlow tooa Service Fabric-service-project met de rechtermuisknop op het Hallo-project in Solution Explorer Hallo en kiest u 'Manage NuGet packages'.</span><span class="sxs-lookup"><span data-stu-id="c6720-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="c6720-140">Overschakelen toohello 'Zoeken' tabblad en zoek naar '`Diagnostics.EventFlow`':</span><span class="sxs-lookup"><span data-stu-id="c6720-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![EventFlow NuGet-pakketten in Visual Studio-NuGet-Pakketbeheer gebruikersinterface][1]

<span data-ttu-id="c6720-142">Hallo-service die als host fungeert voor EventFlow bevatten juiste pakketten, afhankelijk van het Hallo-bron en bestemming voor toepassingslogboeken Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6720-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="c6720-143">Hallo volgende pakketten toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c6720-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="c6720-144">(toocapture gegevens uit Hallo van EventSource serviceklasse, en standard EventSources zoals *ServiceFabric-Microsoft-Services* en *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="c6720-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="c6720-145">(we gaan toosend Hallo logboeken tooan Azure Application Insights-resource)</span><span class="sxs-lookup"><span data-stu-id="c6720-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="c6720-146">(Hiermee initialisatie van Hallo EventFlow pijplijn van de configuratie van de Service Fabric-service en eventuele problemen met het verzenden van diagnostische gegevens als Service Fabric-statusrapporten rapporten)</span><span class="sxs-lookup"><span data-stu-id="c6720-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="c6720-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`pakket moeten Hallo service project tootarget .NET Framework 4.6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="c6720-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="c6720-148">Zorg ervoor dat u Hallo juiste doel-framework in Projecteigenschappen instellen voordat u dit pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="c6720-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="c6720-149">Nadat alle hello-pakketten worden geïnstalleerd, de volgende stap Hallo tooconfigure is en EventFlow inschakelen in Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="c6720-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="c6720-150">Configureren en inschakelen van verzamelen</span><span class="sxs-lookup"><span data-stu-id="c6720-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="c6720-151">EventFlow pipeline, verantwoordelijk voor het verzenden van Hallo zich aanmeldt, wordt gemaakt van een specificatie die is opgeslagen in een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="c6720-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="c6720-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric`pakket installeert u een eerste EventFlow configuratiebestand onder `PackageRoot\Config` oplossingenmap.</span><span class="sxs-lookup"><span data-stu-id="c6720-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="c6720-153">Hallo-bestandsnaam is `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="c6720-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="c6720-154">Dit configuratiebestand moet toobe gewijzigd toocapture gegevens van de standaardservice Hallo `EventSource` klasse en het verzenden van gegevens tooApplication Insights-service.</span><span class="sxs-lookup"><span data-stu-id="c6720-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="c6720-155">We gaan ervan uit dat u bekend met bent **Azure Application Insights** -service en of er een Application Insights-resource dat u van plan toouse toomonitor uw Service Fabric-service bent.</span><span class="sxs-lookup"><span data-stu-id="c6720-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="c6720-156">Als u meer informatie, Zie [een Application Insights-resource maken](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c6720-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="c6720-157">Open Hallo `eventFlowConfig.json` -bestand in Hallo-editor en de inhoud ervan wijzigen, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c6720-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="c6720-158">Zorg ervoor dat tooreplace hello ServiceEventSource naam en het Application Insights-instrumentatiesleutel volgens toocomments.</span><span class="sxs-lookup"><span data-stu-id="c6720-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

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
> <span data-ttu-id="c6720-159">Hallo-naam van ServiceEventSource van de service is Hallo-waarde van Name-eigenschap van Hallo Hallo `EventSourceAttribute` toohello ServiceEventSource klasse toegepast.</span><span class="sxs-lookup"><span data-stu-id="c6720-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="c6720-160">Deze al is opgegeven in Hallo `ServiceEventSource.cs` bestand, dat deel uitmaakt van de servicecode Hallo.</span><span class="sxs-lookup"><span data-stu-id="c6720-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="c6720-161">Bijvoorbeeld, in Hallo volgende codefragment Hallo codenaam Hallo ServiceEventSource is *mijnbedrijf-Toepassing1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="c6720-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="c6720-162">Houd er rekening mee dat `eventFlowConfig.json` bestand maakt deel uit van het configuratiepakket service.</span><span class="sxs-lookup"><span data-stu-id="c6720-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="c6720-163">Wijzigingen toothis bestand kan worden opgenomen in de volledige - of configuratie-only upgrades van Hallo-service, het onderwerp tooService Fabric statuscontroles en automatisch terugdraaien als er een mislukte upgrade.</span><span class="sxs-lookup"><span data-stu-id="c6720-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="c6720-164">Zie voor meer informatie [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="c6720-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="c6720-165">de laatste stap Hallo is tooinstantiate EventFlow pijplijn in uw service starten van de code, zich in `Program.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="c6720-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="c6720-166">In Hallo volgende voorbeeld EventFlow-gerelateerde toevoegingen zijn gemarkeerd met opmerkingen beginnen met `****`:</span><span class="sxs-lookup"><span data-stu-id="c6720-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="c6720-167">Hallo naam doorgegeven als parameter Hallo Hallo `CreatePipeline` methode Hallo `ServiceFabricDiagnosticsPipelineFactory` heet Hallo Hallo *health entiteit* hello EventFlow logboek verzameling pipeline die aangeeft.</span><span class="sxs-lookup"><span data-stu-id="c6720-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="c6720-168">Deze naam wordt gebruikt als EventFlow aantreft en de fout en via Service Fabric health subsysteem Hallo gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="c6720-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="c6720-169">Verificatie</span><span class="sxs-lookup"><span data-stu-id="c6720-169">Verification</span></span>
<span data-ttu-id="c6720-170">De service starten en houd rekening met Hallo foutopsporing uitvoervenster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6720-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="c6720-171">Nadat het Hallo-service is gestart, moet u eerst zien bewijs dat uw service 'Application Insights Telemetry' records verzendt.</span><span class="sxs-lookup"><span data-stu-id="c6720-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="c6720-172">Open een webbrowser en navigeer Ga tooyour Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="c6720-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="c6720-173">Open het tabblad "Zoeken" (bovenaan Hallo Hallo 'Overview' standaardblade).</span><span class="sxs-lookup"><span data-stu-id="c6720-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="c6720-174">Na een korte vertraging leest u eerst de traceringen in Hallo Application Insights-portal te zien:</span><span class="sxs-lookup"><span data-stu-id="c6720-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![Application Insights-portal met Logboeken van een Service Fabric-toepassing][2]

## <a name="next-steps"></a><span data-ttu-id="c6720-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6720-176">Next steps</span></span>
* [<span data-ttu-id="c6720-177">Meer informatie over het diagnosticeren en controleren van een Service Fabric-service</span><span class="sxs-lookup"><span data-stu-id="c6720-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="c6720-178">EventFlow documentatie</span><span class="sxs-lookup"><span data-stu-id="c6720-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
