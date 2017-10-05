---
title: De bewaking van Docker-toepassingen in Azure Application Insights | Microsoft Docs
description: Docker-prestatiemeteritems, gebeurtenissen en uitzonderingen kunnen worden weergegeven op de Application Insights, samen met de telemetrie van de beperkte apps.
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
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="1915c-103">Docker-toepassingen bewaken in Application Insights</span><span class="sxs-lookup"><span data-stu-id="1915c-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="1915c-104">Prestatiemeteritems van de levenscyclus van gebeurtenissen en de prestaties van [Docker](https://www.docker.com/) containers kunnen diagram op Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1915c-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="1915c-105">Installeer de [Application Insights](app-insights-overview.md) installatiekopie in een container in de host en prestatiemeteritems worden weergegeven voor de host en de andere afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="1915c-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="1915c-106">Met Docker, moet u uw apps in lightweight containers met alle afhankelijkheden voltooid distribueren.</span><span class="sxs-lookup"><span data-stu-id="1915c-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="1915c-107">Ze kunnen worden uitgevoerd op elke host waarop een Docker-Engine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1915c-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="1915c-108">Bij het uitvoeren van de [Application Insights installatiekopie](https://hub.docker.com/r/microsoft/applicationinsights/) op uw host Docker dat u deze voordelen:</span><span class="sxs-lookup"><span data-stu-id="1915c-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="1915c-109">De levenscyclus van telemetrie over de containers die zijn uitgevoerd op de host - starten, stoppen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="1915c-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="1915c-110">Prestatiemeteritems voor alle containers.</span><span class="sxs-lookup"><span data-stu-id="1915c-110">Performance counters for all the containers.</span></span> <span data-ttu-id="1915c-111">CPU, geheugen, netwerkgebruik en meer.</span><span class="sxs-lookup"><span data-stu-id="1915c-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="1915c-112">Als u [Application Insights-SDK voor Java geïnstalleerd](app-insights-java-live.md) de telemetrie van deze apps heeft in de apps die worden uitgevoerd in de containers, extra eigenschappen voor het identificeren van de container en host-machine.</span><span class="sxs-lookup"><span data-stu-id="1915c-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="1915c-113">Als u exemplaren van een app in meer dan één host worden uitgevoerd, kunt u dus bijvoorbeeld eenvoudig uw app telemetrie door host filteren.</span><span class="sxs-lookup"><span data-stu-id="1915c-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![Voorbeeld](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="1915c-115">Instellen van uw Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="1915c-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="1915c-116">Meld u aan bij [Microsoft Azure-portal](https://azure.com) en open de Application Insights-resource voor uw app of [Maak een nieuwe](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1915c-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="1915c-117">*Welke resource moet ik gebruiken?*</span><span class="sxs-lookup"><span data-stu-id="1915c-117">*Which resource should I use?*</span></span> <span data-ttu-id="1915c-118">Als de apps die u op de host uitvoert zijn ontwikkeld door iemand anders, moet u [Maak een nieuwe Application Insights-resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1915c-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="1915c-119">Dit is waar u weergeven en analyseren van de telemetrie.</span><span class="sxs-lookup"><span data-stu-id="1915c-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="1915c-120">(Selecteer algemene voor het type app.)</span><span class="sxs-lookup"><span data-stu-id="1915c-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="1915c-121">Maar als u de ontwikkelaar van de apps bent, moet we hopen u dat [Application Insights-SDK toegevoegd](app-insights-java-live.md) aan elk van deze.</span><span class="sxs-lookup"><span data-stu-id="1915c-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="1915c-122">Als ze alle echt onderdelen van een enkele business-toepassing, vervolgens u configureert deze voor het verzenden van telemetrie naar één resource en gebruikt u die dezelfde bron om de Docker en prestaties van de levenscyclus van de gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1915c-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="1915c-123">Een derde scenario is dat u de meeste van de apps ontwikkeld, maar u afzonderlijke resources gebruikt om de telemetrie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1915c-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="1915c-124">In dat geval u waarschijnlijk ook wilt maken van een afzonderlijke resource voor de Docker-gegevens.</span><span class="sxs-lookup"><span data-stu-id="1915c-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="1915c-125">Toevoegen van de Docker-tegel: kies **toevoegen tegel**, sleept u de Docker-tegel in de galerie en klik vervolgens op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="1915c-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![Voorbeeld](./media/app-insights-docker/03.png)
3. <span data-ttu-id="1915c-127">Klik op de **Essentials** vervolgkeuzelijst en de Instrumentatiesleutel kopiëren.</span><span class="sxs-lookup"><span data-stu-id="1915c-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="1915c-128">Met dit kunt u instellen dat de SDK waar u de telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="1915c-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![Voorbeeld](./media/app-insights-docker/02-props.png)

<span data-ttu-id="1915c-130">Houd dat browservenster handig wanneer u zult keert u terug naar deze snel om te kijken naar uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="1915c-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="1915c-131">De Application Insights-monitor op uw host worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="1915c-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="1915c-132">Nu dat u hebt een andere locatie om de telemetrie weer te geven, kunt u de beperkte-app die wordt verzameld en verzonden instellen.</span><span class="sxs-lookup"><span data-stu-id="1915c-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="1915c-133">Verbinding maken met de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="1915c-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="1915c-134">De instrumentatiesleutel in deze opdracht bewerken en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="1915c-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="1915c-135">U hoeft slechts één installatiekopie van de Application Insights per Docker-host.</span><span class="sxs-lookup"><span data-stu-id="1915c-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="1915c-136">Als uw toepassing wordt geïmplementeerd op meerdere Docker-hosts, herhaalt u de opdracht op elke host.</span><span class="sxs-lookup"><span data-stu-id="1915c-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="1915c-137">Uw app bijwerken</span><span class="sxs-lookup"><span data-stu-id="1915c-137">Update your app</span></span>
<span data-ttu-id="1915c-138">Als uw toepassing is uitgerust met de [Application Insights-SDK voor Java](app-insights-java-get-started.md), voeg de volgende regel in het ApplicationInsights.xml-bestand in uw project, onder de `<TelemetryInitializers>` element:</span><span class="sxs-lookup"><span data-stu-id="1915c-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="1915c-139">Docker informatie zoals container en host-id wordt toegevoegd aan elk telemetrie-item dat is verzonden van uw app.</span><span class="sxs-lookup"><span data-stu-id="1915c-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="1915c-140">Uw telemetrie weergeven</span><span class="sxs-lookup"><span data-stu-id="1915c-140">View your telemetry</span></span>
<span data-ttu-id="1915c-141">Ga terug naar uw Application Insights-resource in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1915c-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="1915c-142">Klik in de Docker-tegel.</span><span class="sxs-lookup"><span data-stu-id="1915c-142">Click through the Docker tile.</span></span>

<span data-ttu-id="1915c-143">Binnen enkele ogenblikken ziet u gegevens die binnenkomen vanuit de Docker-app, met name als u andere containers uitgevoerd op uw Docker-engine.</span><span class="sxs-lookup"><span data-stu-id="1915c-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="1915c-144">Hier zijn enkele van de weergaven die u kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="1915c-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="1915c-145">Prestatiemeteritems door host activiteit door de installatiekopie</span><span class="sxs-lookup"><span data-stu-id="1915c-145">Perf counters by host, activity by image</span></span>
![Voorbeeld](./media/app-insights-docker/10.png)

![Voorbeeld](./media/app-insights-docker/11.png)

<span data-ttu-id="1915c-148">Klik op een host- of image-naam voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1915c-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="1915c-149">Klik op een grafiek, het raster kop, of gebruik grafiek toevoegen voor het aanpassen van de weergave.</span><span class="sxs-lookup"><span data-stu-id="1915c-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="1915c-150">[Meer informatie over metrics explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="1915c-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="1915c-151">Gebeurtenissen van docker-container</span><span class="sxs-lookup"><span data-stu-id="1915c-151">Docker container events</span></span>
![Voorbeeld](./media/app-insights-docker/13.png)

<span data-ttu-id="1915c-153">Voor het onderzoeken van afzonderlijke gebeurtenissen, klikt u op [Search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1915c-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="1915c-154">Zoeken en filteren op de gebeurtenissen die u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="1915c-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="1915c-155">Klik op een gebeurtenis als u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1915c-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="1915c-156">Uitzonderingen op de naam van de container</span><span class="sxs-lookup"><span data-stu-id="1915c-156">Exceptions by container name</span></span>
![Voorbeeld](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="1915c-158">Docker-context toegevoegd aan app telemetrie</span><span class="sxs-lookup"><span data-stu-id="1915c-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="1915c-159">Aanvraagtelemetrie van de toepassing is uitgerust met AI-SDK, verrijkt met Docker-context verzonden:</span><span class="sxs-lookup"><span data-stu-id="1915c-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![Voorbeeld](./media/app-insights-docker/16.png)

<span data-ttu-id="1915c-161">Tijd van processor en geheugen prestatiemeteritems, uitgebreid en gegroepeerd op de naam van de Docker-container:</span><span class="sxs-lookup"><span data-stu-id="1915c-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![Voorbeeld](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="1915c-163">Vragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="1915c-163">Q & A</span></span>
<span data-ttu-id="1915c-164">*Wat Application Insights opleveren die ik bij Docker ophalen kan?*</span><span class="sxs-lookup"><span data-stu-id="1915c-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="1915c-165">Detail van prestatiemeteritems door container en de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="1915c-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="1915c-166">Integreer container en app-gegevens in één dashboard.</span><span class="sxs-lookup"><span data-stu-id="1915c-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="1915c-167">[Exporteren van telemetrie](app-insights-export-telemetry.md) voor verdere analyse naar een database, Power BI of andere dashboard.</span><span class="sxs-lookup"><span data-stu-id="1915c-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="1915c-168">*Hoe krijg ik telemetrie van de app zelf?*</span><span class="sxs-lookup"><span data-stu-id="1915c-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="1915c-169">De Application Insights-SDK installeren in de app.</span><span class="sxs-lookup"><span data-stu-id="1915c-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="1915c-170">Meer informatie over hoe voor: [Java-web-apps](app-insights-java-get-started.md), [Windows web-apps](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="1915c-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="1915c-171">Video</span><span class="sxs-lookup"><span data-stu-id="1915c-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="1915c-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1915c-172">Next steps</span></span>

* [<span data-ttu-id="1915c-173">Application Insights voor Java</span><span class="sxs-lookup"><span data-stu-id="1915c-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="1915c-174">Application Insights voor Node.js</span><span class="sxs-lookup"><span data-stu-id="1915c-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="1915c-175">Application Insights voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1915c-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
