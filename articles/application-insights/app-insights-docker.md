---
title: aaaMonitor Docker-toepassingen in Azure Application Insights | Microsoft Docs
description: Docker-prestatiemeteritems, gebeurtenissen en uitzonderingen kunnen worden weergegeven op de Application Insights, samen met de Hallo telemetrie van Hallo beperkte apps.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="6c195-103">Docker-toepassingen bewaken in Application Insights</span><span class="sxs-lookup"><span data-stu-id="6c195-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="6c195-104">Prestatiemeteritems van de levenscyclus van gebeurtenissen en de prestaties van [Docker](https://www.docker.com/) containers kunnen diagram op Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6c195-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="6c195-105">Hallo installeren [Application Insights](app-insights-overview.md) installatiekopie in een container in de host en prestatiemeteritems voor het Hallo-host, worden weergegeven als Hallo als voor andere installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="6c195-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="6c195-106">Met Docker, moet u uw apps in lightweight containers met alle afhankelijkheden voltooid distribueren.</span><span class="sxs-lookup"><span data-stu-id="6c195-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="6c195-107">Ze kunnen worden uitgevoerd op elke host waarop een Docker-Engine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c195-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="6c195-108">Bij het uitvoeren van Hallo [Application Insights installatiekopie](https://hub.docker.com/r/microsoft/applicationinsights/) op uw host Docker dat u deze voordelen:</span><span class="sxs-lookup"><span data-stu-id="6c195-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="6c195-109">De levenscyclus van telemetrie over alle Hallo containers die worden uitgevoerd op host Hallo - starten, stoppen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="6c195-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="6c195-110">Prestatiemeteritems voor alle Hallo containers.</span><span class="sxs-lookup"><span data-stu-id="6c195-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="6c195-111">CPU, geheugen, netwerkgebruik en meer.</span><span class="sxs-lookup"><span data-stu-id="6c195-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="6c195-112">Als u [Application Insights-SDK voor Java geïnstalleerd](app-insights-java-live.md) Hallo apps die worden uitgevoerd in Hallo-containers, alle Hallo telemetrie van deze apps aanvullende eigenschappen identificeren Hallo-container en hostmachine zullen hebben.</span><span class="sxs-lookup"><span data-stu-id="6c195-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="6c195-113">Als u exemplaren van een app in meer dan één host worden uitgevoerd, kunt u dus bijvoorbeeld eenvoudig uw app telemetrie door host filteren.</span><span class="sxs-lookup"><span data-stu-id="6c195-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![Voorbeeld](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="6c195-115">Instellen van uw Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="6c195-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="6c195-116">Meld u aan bij [Microsoft Azure-portal](https://azure.com) en open Hallo Application Insights-resource voor uw app of [Maak een nieuwe](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6c195-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="6c195-117">*Welke resource moet ik gebruiken?*</span><span class="sxs-lookup"><span data-stu-id="6c195-117">*Which resource should I use?*</span></span> <span data-ttu-id="6c195-118">Als Hallo-apps die u op de host uitvoert zijn ontwikkeld door iemand anders, moet u te[Maak een nieuwe Application Insights-resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6c195-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="6c195-119">Dit is waar u weergeven en analyseren van Hallo telemetrie.</span><span class="sxs-lookup"><span data-stu-id="6c195-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="6c195-120">(Selecteer algemene voor Hallo app-type.)</span><span class="sxs-lookup"><span data-stu-id="6c195-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="6c195-121">Maar als u Hallo ontwikkelaar van Hallo apps bent, klikt u vervolgens we hopen dat u [Application Insights-SDK toegevoegd](app-insights-java-live.md) tooeach hiervan.</span><span class="sxs-lookup"><span data-stu-id="6c195-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="6c195-122">Als ze alle echt onderdelen van een enkele business-toepassing u ze allemaal toosend telemetrie tooone bron mogelijk configureert en gebruikt u dezelfde resource toodisplay hello Docker en prestaties van de levenscyclus van gegevens.</span><span class="sxs-lookup"><span data-stu-id="6c195-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="6c195-123">Een derde scenario is dat u de meeste Hallo apps ontwikkeld, maar u van afzonderlijke resources toodisplay hun telemetrie gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="6c195-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="6c195-124">In dat geval u waarschijnlijk ook wilt toocreate een afzonderlijke resource voor Hallo Docker-gegevens.</span><span class="sxs-lookup"><span data-stu-id="6c195-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="6c195-125">Add Hallo Docker tegel: kies **toevoegen tegel**Hallo Docker tegel slepen vanuit galerie Hallo en klik vervolgens op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="6c195-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![Voorbeeld](./media/app-insights-docker/03.png)
3. <span data-ttu-id="6c195-127">Klik op Hallo **Essentials** vervolgkeuzelijst en Hallo Instrumentatiesleutel kopiëren.</span><span class="sxs-lookup"><span data-stu-id="6c195-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="6c195-128">U gebruikt deze tootell Hallo SDK waar toosend de telemetrie.</span><span class="sxs-lookup"><span data-stu-id="6c195-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![Voorbeeld](./media/app-insights-docker/02-props.png)

<span data-ttu-id="6c195-130">Houd dat browservenster handig als u dan terug tooit snel krijgt toolook op uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="6c195-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="6c195-131">Hallo Application Insights monitor op uw host worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="6c195-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="6c195-132">Nu dat u ergens toodisplay Hallo telemetrie hebt, kunt u beperkte Hallo-app die wordt verzameld en verzonden instellen.</span><span class="sxs-lookup"><span data-stu-id="6c195-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="6c195-133">Verbinding maken met tooyour Docker-host.</span><span class="sxs-lookup"><span data-stu-id="6c195-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="6c195-134">De instrumentatiesleutel in deze opdracht bewerken en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="6c195-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="6c195-135">U hoeft slechts één installatiekopie van de Application Insights per Docker-host.</span><span class="sxs-lookup"><span data-stu-id="6c195-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="6c195-136">Als uw toepassing wordt geïmplementeerd op meerdere Docker-hosts, herhaalt u de opdracht Hallo op elke host.</span><span class="sxs-lookup"><span data-stu-id="6c195-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="6c195-137">Uw app bijwerken</span><span class="sxs-lookup"><span data-stu-id="6c195-137">Update your app</span></span>
<span data-ttu-id="6c195-138">Als uw toepassing is uitgerust met Hallo [Application Insights-SDK voor Java](app-insights-java-get-started.md), toevoegen van de volgende regel in Hallo ApplicationInsights.xml-bestand in uw project, onder Hallo Hallo `<TelemetryInitializers>` element:</span><span class="sxs-lookup"><span data-stu-id="6c195-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="6c195-139">Docker informatie zoals de container en host-id tooevery telemetrie-item dat verzonden vanuit uw app wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6c195-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="6c195-140">Uw telemetrie weergeven</span><span class="sxs-lookup"><span data-stu-id="6c195-140">View your telemetry</span></span>
<span data-ttu-id="6c195-141">Ga terug tooyour Application Insights-resource in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6c195-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="6c195-142">Klik in het Hallo Docker-tegel.</span><span class="sxs-lookup"><span data-stu-id="6c195-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="6c195-143">U ziet kort gegevens die binnenkomen in Hallo Docker-app, met name als u andere containers uitgevoerd op uw Docker-engine.</span><span class="sxs-lookup"><span data-stu-id="6c195-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="6c195-144">Hier zijn enkele Hallo weergaven die u kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="6c195-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="6c195-145">Prestatiemeteritems door host activiteit door de installatiekopie</span><span class="sxs-lookup"><span data-stu-id="6c195-145">Perf counters by host, activity by image</span></span>
![Voorbeeld](./media/app-insights-docker/10.png)

![Voorbeeld](./media/app-insights-docker/11.png)

<span data-ttu-id="6c195-148">Klik op een host- of image-naam voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6c195-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="6c195-149">toocustomize hello weergave, klikt u op een grafiek, Hallo raster kop, of gebruik grafiek toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6c195-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="6c195-150">[Meer informatie over metrics explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="6c195-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="6c195-151">Gebeurtenissen van docker-container</span><span class="sxs-lookup"><span data-stu-id="6c195-151">Docker container events</span></span>
![Voorbeeld](./media/app-insights-docker/13.png)

<span data-ttu-id="6c195-153">tooinvestigate afzonderlijke gebeurtenissen, klikt u op [Search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="6c195-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="6c195-154">Zoeken en toofind Hallo gebeurtenissen die u wilt filteren.</span><span class="sxs-lookup"><span data-stu-id="6c195-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="6c195-155">Klik op een gebeurtenis tooget meer details.</span><span class="sxs-lookup"><span data-stu-id="6c195-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="6c195-156">Uitzonderingen op de naam van de container</span><span class="sxs-lookup"><span data-stu-id="6c195-156">Exceptions by container name</span></span>
![Voorbeeld](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="6c195-158">Docker-context tooapp telemetrie toegevoegd</span><span class="sxs-lookup"><span data-stu-id="6c195-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="6c195-159">Telemetrie verzonden vanuit Hallo toepassing uitgerust met AI-SDK, verrijkt met Docker-context aanvragen:</span><span class="sxs-lookup"><span data-stu-id="6c195-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![Voorbeeld](./media/app-insights-docker/16.png)

<span data-ttu-id="6c195-161">Tijd van processor en geheugen prestatiemeteritems, uitgebreid en gegroepeerd op de naam van de Docker-container:</span><span class="sxs-lookup"><span data-stu-id="6c195-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![Voorbeeld](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="6c195-163">Vragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="6c195-163">Q & A</span></span>
<span data-ttu-id="6c195-164">*Wat Application Insights opleveren die ik bij Docker ophalen kan?*</span><span class="sxs-lookup"><span data-stu-id="6c195-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="6c195-165">Detail van prestatiemeteritems door container en de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="6c195-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="6c195-166">Integreer container en app-gegevens in één dashboard.</span><span class="sxs-lookup"><span data-stu-id="6c195-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="6c195-167">[Exporteren van telemetrie](app-insights-export-telemetry.md) voor verdere analyse tooa database, Power BI of andere dashboard.</span><span class="sxs-lookup"><span data-stu-id="6c195-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="6c195-168">*Hoe krijg ik telemetrie van Hallo app zelf?*</span><span class="sxs-lookup"><span data-stu-id="6c195-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="6c195-169">Hallo Application Insights-SDK installeren in Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="6c195-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="6c195-170">Meer informatie over hoe voor: [Java-web-apps](app-insights-java-get-started.md), [Windows web-apps](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="6c195-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="6c195-171">Video</span><span class="sxs-lookup"><span data-stu-id="6c195-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="6c195-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c195-172">Next steps</span></span>

* [<span data-ttu-id="6c195-173">Application Insights voor Java</span><span class="sxs-lookup"><span data-stu-id="6c195-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="6c195-174">Application Insights voor Node.js</span><span class="sxs-lookup"><span data-stu-id="6c195-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="6c195-175">Application Insights voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6c195-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
