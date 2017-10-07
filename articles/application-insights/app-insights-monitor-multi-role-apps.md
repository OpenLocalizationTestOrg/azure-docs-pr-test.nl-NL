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
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="0a843-103">De bewaking van meerdere onderdeel toepassingen met Application Insights (preview)</span><span class="sxs-lookup"><span data-stu-id="0a843-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="0a843-104">U kunt apps die bestaan uit meerdere server-onderdelen, functies of services met bewaken [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a843-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="0a843-105">Hallo-status van Hallo-onderdelen en Hallo onderlinge relaties worden weergegeven op een kaart met één toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a843-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="0a843-106">U kunt afzonderlijke bewerkingen via meerdere onderdelen met automatische HTTP correlatie traceren.</span><span class="sxs-lookup"><span data-stu-id="0a843-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="0a843-107">Container diagnostische gegevens kan worden geïntegreerd en worden gecorreleerd met de toepassingstelemetrie.</span><span class="sxs-lookup"><span data-stu-id="0a843-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="0a843-108">Gebruik één Application Insights-resource voor alle Hallo onderdelen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a843-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Meerdere onderdeel toepassingstoewijzing](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="0a843-110">We gebruiken 'onderdeel' hier toomean een werkende deel van een grote aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0a843-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="0a843-111">Bijvoorbeeld, de meeste zakelijke toepassingen kan bestaan uit clientcode die wordt uitgevoerd in de webbrowser, praten tooone of meer web-app services, die op zijn beurt back gebruiken-end services.</span><span class="sxs-lookup"><span data-stu-id="0a843-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="0a843-112">Server-onderdelen mogelijk gehoste on-premises worden op in de cloud Hallo, of mogelijk Azure web- en werkrollen rollen of mogelijk worden uitgevoerd in containers zoals Docker of Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0a843-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="0a843-113">Een enkele Application Insights-resource delen</span><span class="sxs-lookup"><span data-stu-id="0a843-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="0a843-114">Hallo belangrijke techniek hier is toosend telemetrie van elk onderdeel in uw toepassing toohello dezelfde Application Insights-resource, maar gebruik Hallo `cloud_RoleName` eigenschap toodistinguish onderdelen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="0a843-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="0a843-115">Hallo Application Insights-SDK wordt toegevoegd Hallo `cloud_RoleName` eigenschap toohello telemetrie onderdelen verzenden.</span><span class="sxs-lookup"><span data-stu-id="0a843-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="0a843-116">Bijvoorbeeld, Hallo SDK wordt toegevoegd een naam van de website of service rol naam toohello `cloud_RoleName` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="0a843-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="0a843-117">U kunt deze waarde met een telemetryinitializer overschrijven.</span><span class="sxs-lookup"><span data-stu-id="0a843-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="0a843-118">Hallo toepassingstoewijzing gebruikt Hallo `cloud_RoleName` eigenschap tooidentify Hallo onderdelen op Hallo-kaart.</span><span class="sxs-lookup"><span data-stu-id="0a843-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="0a843-119">Voor meer informatie over het Hallo overschrijven `cloud_RoleName` eigenschap Zie [eigenschappen toevoegen: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="0a843-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="0a843-120">In sommige gevallen kan dit niet altijd geschikt en gewenste toouse afzonderlijke bronnen voor verschillende groepen van onderdelen.</span><span class="sxs-lookup"><span data-stu-id="0a843-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="0a843-121">U wellicht bijvoorbeeld toouse verschillende bronnen voor beheer of facturering.</span><span class="sxs-lookup"><span data-stu-id="0a843-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="0a843-122">Met behulp van afzonderlijke resources betekent dat er geen alle Hallo onderdelen weergegeven op een kaart met één toepassing; en dat u geen query uitvoeren voor onderdelen in [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="0a843-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="0a843-123">Hebt u ook tooset Hallo afzonderlijke resources.</span><span class="sxs-lookup"><span data-stu-id="0a843-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="0a843-124">Met dat hoewel we gaan ervan uit dat in de rest van dit document Hallo die u wilt dat toosend gegevens uit meerdere onderdelen tooone Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="0a843-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="0a843-125">Meerdere onderdeel toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="0a843-125">Configure multi-component applications</span></span>

<span data-ttu-id="0a843-126">tooget een toepassing met meerdere onderdelen toewijzen, moet u tooachieve na deze doelstellingen:</span><span class="sxs-lookup"><span data-stu-id="0a843-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="0a843-127">**Installeer de meest recente voorlopige Hallo** Application Insights-pakket in elk onderdeel van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="0a843-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="0a843-128">**Een enkele Application Insights-resource delen** voor alle onderdelen van uw toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="0a843-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="0a843-129">**Inschakelen van de toepassing van meerdere rollenoverzicht** Hallo Previews blade.</span><span class="sxs-lookup"><span data-stu-id="0a843-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="0a843-130">Configureer elk onderdeel van uw toepassing met de juiste methode Hallo voor het type.</span><span class="sxs-lookup"><span data-stu-id="0a843-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="0a843-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="0a843-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="0a843-132">1. Hallo meest recente voorlopige versie pakket installeren</span><span class="sxs-lookup"><span data-stu-id="0a843-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="0a843-133">Bijwerken of Hallo toepassing Insights pakketten in Hallo-project voor elk serveronderdeel worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0a843-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="0a843-134">Als u Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="0a843-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="0a843-135">Met de rechtermuisknop op een project en selecteer **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="0a843-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="0a843-136">Selecteer **Include prerelease**.</span><span class="sxs-lookup"><span data-stu-id="0a843-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="0a843-137">Als de Application Insights-pakketten in de Updates worden weergegeven, selecteert u deze.</span><span class="sxs-lookup"><span data-stu-id="0a843-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="0a843-138">Anders zoeken en installeren van het juiste pakket Hallo:</span><span class="sxs-lookup"><span data-stu-id="0a843-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="0a843-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="0a843-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="0a843-140">Microsoft.ApplicationInsights.ServiceFabric - voor de onderdelen die worden uitgevoerd als gast uitvoerbare bestanden en Docker-containers in Service Fabric-toepassing wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="0a843-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="0a843-141">Microsoft.ApplicationInsights.ServiceFabric.Native - voor betrouwbare services in ServiceFabric toepassingen</span><span class="sxs-lookup"><span data-stu-id="0a843-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="0a843-142">Microsoft.ApplicationInsights.Kubernetes voor onderdelen die worden uitgevoerd in Docker op Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0a843-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="0a843-143">2. Een enkele Application Insights-resource delen</span><span class="sxs-lookup"><span data-stu-id="0a843-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="0a843-144">In Visual Studio met de rechtermuisknop op een project en selecteer **Configure Application Insights**, of **Application Insights > configureren**.</span><span class="sxs-lookup"><span data-stu-id="0a843-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="0a843-145">Gebruik voor de eerste project hello, Hallo wizard toocreate Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="0a843-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="0a843-146">Selecteer Hallo voor latere projecten dezelfde resource.</span><span class="sxs-lookup"><span data-stu-id="0a843-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="0a843-147">Als er geen Application Insights-menu, handmatig configureren:</span><span class="sxs-lookup"><span data-stu-id="0a843-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="0a843-148">In [Azure-portal](https://portal,azure.com), opent u Application Insights-resource Hallo u al hebt gemaakt voor een ander onderdeel.</span><span class="sxs-lookup"><span data-stu-id="0a843-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="0a843-149">In overzichtsblade hello, open Hallo Essentials vervolgkeuzelijst tabblad en kopiëren Hallo **Instrumentatiesleutel.**</span><span class="sxs-lookup"><span data-stu-id="0a843-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="0a843-150">Open ApplicationInsights.config en invoegen in uw project:`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="0a843-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Hallo instrumentation sleutel toohello .config-bestand kopiëren](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="0a843-152">3. Toepassing van meerdere rollenoverzicht inschakelen</span><span class="sxs-lookup"><span data-stu-id="0a843-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="0a843-153">Open in hello Azure-portal, Hallo bron voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a843-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="0a843-154">Hallo Previews blade inschakelen *toepassing van meerdere rollenoverzicht*.</span><span class="sxs-lookup"><span data-stu-id="0a843-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="0a843-155">4. Docker metrische gegevens (optioneel) inschakelen</span><span class="sxs-lookup"><span data-stu-id="0a843-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="0a843-156">Als een onderdeel in een Docker gehost op een Windows Azure VM wordt uitgevoerd, kunt u aanvullende gegevens kunt verzamelen uit Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="0a843-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="0a843-157">Voeg dit in uw [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="0a843-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="0a843-158">Gebruik cloud_RoleName tooseparate onderdelen</span><span class="sxs-lookup"><span data-stu-id="0a843-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="0a843-159">Hallo `cloud_RoleName` eigenschap is aangesloten tooall telemetrie.</span><span class="sxs-lookup"><span data-stu-id="0a843-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="0a843-160">Het identificeert Hallo-onderdeel - Hallo functie of service - die afkomstig is van Hallo telemetrie.</span><span class="sxs-lookup"><span data-stu-id="0a843-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="0a843-161">(Dit is dezelfde niet Hallo als cloud_RoleInstance die identiek functies die parallel worden uitgevoerd op meerdere serverprocessen of machines scheidt.)</span><span class="sxs-lookup"><span data-stu-id="0a843-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="0a843-162">U kunt filteren en uw gebruik van deze eigenschap telemetrie segmenteren in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="0a843-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="0a843-163">In dit voorbeeld is Hallo fouten blade gefilterde tooshow alleen op de gegevens van Hallo front-webservice, worden uitgefilterd fouten vanuit Hallo CRM-API-back-end:</span><span class="sxs-lookup"><span data-stu-id="0a843-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Metrische gesegmenteerd op naam van de Cloud-rol-grafiek](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="0a843-165">Trace-bewerkingen tussen onderdelen</span><span class="sxs-lookup"><span data-stu-id="0a843-165">Trace operations between components</span></span>

<span data-ttu-id="0a843-166">U kunt traceren vanuit één onderdeel tooanother, Hallo aanroepen tijdens het verwerken van een afzonderlijke bewerking.</span><span class="sxs-lookup"><span data-stu-id="0a843-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![Telemetrie voor bewerking weergeven](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="0a843-168">Klik op door tooa gecorreleerde lijst telemetrie voor deze bewerking via Hallo-front-endwebserver en Hallo back-end-API:</span><span class="sxs-lookup"><span data-stu-id="0a843-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Zoeken in onderdelen](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="0a843-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a843-170">Next steps</span></span>

* [<span data-ttu-id="0a843-171">Afzonderlijke telemetrie van ontwikkeling, testen en productie</span><span class="sxs-lookup"><span data-stu-id="0a843-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
