---
title: aaaSeparating telemetrie van ontwikkeling, testen en release in Azure Application Insights | Microsoft Docs
description: Directe telemetrie toodifferent bronnen voor ontwikkeling, testen en productie stempels.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="24317-103">Telemetrie scheiden van ontwikkeling, testen en productie</span><span class="sxs-lookup"><span data-stu-id="24317-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="24317-104">Wanneer u de volgende versie van een webtoepassing Hallo ontwikkelt, u niet wilt dat toomix up Hallo [Application Insights](app-insights-overview.md) telemetrie van de nieuwe versie Hallo en Hallo al is vrijgegeven versie.</span><span class="sxs-lookup"><span data-stu-id="24317-104">When you are developing hello next version of a web application, you don't want toomix up hello [Application Insights](app-insights-overview.md) telemetry from hello new version and hello already released version.</span></span> <span data-ttu-id="24317-105">tooavoid verwarring verzenden Hallo telemetrie van de ontwikkeling van de verschillende fasen tooseparate Application Insights-resources, met afzonderlijke instrumentatiesleutels (ikeys).</span><span class="sxs-lookup"><span data-stu-id="24317-105">tooavoid confusion, send hello telemetry from different development stages tooseparate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="24317-106">toomake deze eenvoudiger toochange hello instrumentatiesleutel versie wordt verplaatst van één fase tooanother, kan het nuttig tooset Hallo ikey in de code in plaats van in het configuratiebestand Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="24317-106">toomake it easier toochange hello instrumentation key as a version moves from one stage tooanother, it can be useful tooset hello ikey in code instead of in hello configuration file.</span></span> 

<span data-ttu-id="24317-107">(Als u een Azure Cloud Service er [een andere methode voor het instellen van afzonderlijke ikeys](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="24317-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="24317-108">Over de resources en instrumentatiesleutels</span><span class="sxs-lookup"><span data-stu-id="24317-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="24317-109">Als u bewaking van de Application Insights voor uw web-app instelt, maakt u een Application Insights *resource* in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="24317-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="24317-110">U opent u deze resource in hello Azure-portal op volgorde toosee en analyseren van Hallo verzamelen van telemetriegegevens van uw app.</span><span class="sxs-lookup"><span data-stu-id="24317-110">You open this resource in hello Azure portal in order toosee and analyze hello telemetry collected from your app.</span></span> <span data-ttu-id="24317-111">Hallo resource wordt geïdentificeerd door een *instrumentatiesleutel* (ikey).</span><span class="sxs-lookup"><span data-stu-id="24317-111">hello resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="24317-112">Wanneer u Hallo installeert uw app-pakket toomonitor Application Insights, kunt u deze configureren met de instrumentatiesleutel hello, zodat deze weet waar toosend telemetrie Hallo.</span><span class="sxs-lookup"><span data-stu-id="24317-112">When you install hello Application Insights package toomonitor your app, you configure it with hello instrumentation key, so that it knows where toosend hello telemetry.</span></span>

<span data-ttu-id="24317-113">U meestal kiezen afzonderlijke resources toouse of één gedeelde resource in verschillende scenario's:</span><span class="sxs-lookup"><span data-stu-id="24317-113">You typically choose toouse separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="24317-114">Andere, onafhankelijke toepassingen - gebruik een afzonderlijke resource en ikey voor elke app.</span><span class="sxs-lookup"><span data-stu-id="24317-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="24317-115">Meerdere onderdelen of rollen zijn van een zakelijke toepassing - gebruiken een [één gedeelde bron](app-insights-monitor-multi-role-apps.md) voor alle Hallo onderdeel apps.</span><span class="sxs-lookup"><span data-stu-id="24317-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all hello component apps.</span></span> <span data-ttu-id="24317-116">Telemetrie worden gefilterd of gesegmenteerd op Hallo cloud_RoleName eigenschap.</span><span class="sxs-lookup"><span data-stu-id="24317-116">Telemetry can be filtered or segmented by hello cloud_RoleName property.</span></span>
* <span data-ttu-id="24317-117">Ontwikkeling, testen en Release - gebruik een afzonderlijke resource en ikey voor versies van het systeem in de tijdstempel' Hallo of fase van de productie.</span><span class="sxs-lookup"><span data-stu-id="24317-117">Development, Test, and Release - Use a separate resource and ikey for versions of hello system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="24317-118">EEN | B-tests - gebruik van één resource.</span><span class="sxs-lookup"><span data-stu-id="24317-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="24317-119">Maak een tooadd TelemetryInitializer een eigenschap toohello telemetrie die Hallo varianten identificeert.</span><span class="sxs-lookup"><span data-stu-id="24317-119">Create a TelemetryInitializer tooadd a property toohello telemetry that identifies hello variants.</span></span>


## <span data-ttu-id="24317-120"><a name="dynamic-ikey"></a>Dynamische instrumentatiesleutel</span><span class="sxs-lookup"><span data-stu-id="24317-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="24317-121">toomake is die het eenvoudiger toochange Hallo ikey als Hallo code worden verplaatst tussen stadia van de productie, stel deze in de code in plaats van in het Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="24317-121">toomake it easier toochange hello ikey as hello code moves between stages of production, set it in code instead of in hello configuration file.</span></span>

<span data-ttu-id="24317-122">Hallo-sleutel in een initialiseringsmethode, zoals global.aspx.cs in een ASP.NET-beheerservice ingesteld:</span><span class="sxs-lookup"><span data-stu-id="24317-122">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="24317-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="24317-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="24317-124">In dit voorbeeld worden in verschillende versies van het webconfiguratiebestand Hallo Hallo ikeys voor verschillende resources Hallo geplaatst.</span><span class="sxs-lookup"><span data-stu-id="24317-124">In this example, hello ikeys for hello different resources are placed in different versions of hello web configuration file.</span></span> <span data-ttu-id="24317-125">Wisselen Hallo webconfiguratiebestand - die u kunt doen als onderdeel van Hallo release script - wordt Hallo doelbron wisselen.</span><span class="sxs-lookup"><span data-stu-id="24317-125">Swapping hello web configuration file - which you can do as part of hello release script - will swap hello target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="24317-126">Webpagina's</span><span class="sxs-lookup"><span data-stu-id="24317-126">Web pages</span></span>
<span data-ttu-id="24317-127">Hallo iKey wordt ook gebruikt in uw app webpagina's in Hallo [script die u hebt verkregen via Snel starten-blade Hallo](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="24317-127">hello iKey is also used in your app's web pages, in hello [script that you got from hello quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="24317-128">In plaats van een bekend letterlijk in Hallo script, kunt u het genereren van Hallo server staat.</span><span class="sxs-lookup"><span data-stu-id="24317-128">Instead of coding it literally into hello script, generate it from hello server state.</span></span> <span data-ttu-id="24317-129">Bijvoorbeeld in een ASP.NET-app:</span><span class="sxs-lookup"><span data-stu-id="24317-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="24317-130">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="24317-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="24317-131">Aanvullende bronnen voor Application Insights maken</span><span class="sxs-lookup"><span data-stu-id="24317-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="24317-132">tooseparate telemetrie voor andere toepassingsonderdelen, of voor verschillende stempels (ontwikkeling/tests/productie) Hallo hetzelfde onderdeel, dan hebt u hebt toocreate een nieuwe Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="24317-132">tooseparate telemetry for different application components, or for different stamps (dev/test/production) of hello same component, then you'll have toocreate a new Application Insights resource.</span></span>

<span data-ttu-id="24317-133">In Hallo [portal.azure.com](https://portal.azure.com), een Application Insights-resource toevoegen:</span><span class="sxs-lookup"><span data-stu-id="24317-133">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Klik op Nieuw > Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="24317-135">**Toepassingstype** is van invloed op wat er op de blade overzicht Hallo en Hallo eigenschappen beschikbaar zijn in [metrische explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="24317-135">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="24317-136">Als u uw app-type niet ziet, kiest u een van Hallo webtypen voor webpagina's.</span><span class="sxs-lookup"><span data-stu-id="24317-136">If you don't see your type of app, choose one of hello web types for web pages.</span></span>
* <span data-ttu-id="24317-137">**Resourcegroep** is nuttig voor het beheren van eigenschappen zoals [toegangsbeheer](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="24317-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="24317-138">U kunt afzonderlijke resourcegroepen voor ontwikkeling, testen en productie.</span><span class="sxs-lookup"><span data-stu-id="24317-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="24317-139">**Abonnement** is uw betaling-account in Azure.</span><span class="sxs-lookup"><span data-stu-id="24317-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="24317-140">**Locatie** is waar we uw gegevens wilt bewaren.</span><span class="sxs-lookup"><span data-stu-id="24317-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="24317-141">Op dit moment worden niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="24317-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="24317-142">**Toevoegen van toodashboard** plaatst u een snelle toegang tegel voor uw resource op de startpagina van Azure.</span><span class="sxs-lookup"><span data-stu-id="24317-142">**Add toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="24317-143">Hallo-resource maken duurt een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="24317-143">Creating hello resource takes a few seconds.</span></span> <span data-ttu-id="24317-144">U ziet een waarschuwing wanneer deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="24317-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="24317-145">(U kunt schrijven een [PowerShell-script](app-insights-powershell-script-create-resource.md) toocreate een resource automatisch.)</span><span class="sxs-lookup"><span data-stu-id="24317-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) toocreate a resource automatically.)</span></span>

### <a name="getting-hello-instrumentation-key"></a><span data-ttu-id="24317-146">Hallo-instrumentatiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="24317-146">Getting hello instrumentation key</span></span>
<span data-ttu-id="24317-147">de instrumentatiesleutel Hallo identificeert Hallo resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="24317-147">hello instrumentation key identifies hello resource that you created.</span></span> 

![Klik op Essentials, Hallo Instrumentatiesleutel, CTRL + C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="24317-149">U Hallo instrumentatiesleutels nodig van alle Hallo resources toowhich uw app gegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="24317-149">You need hello instrumentation keys of all hello resources toowhich your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="24317-150">Filteren op build-nummer</span><span class="sxs-lookup"><span data-stu-id="24317-150">Filter on build number</span></span>
<span data-ttu-id="24317-151">Wanneer u een nieuwe versie van uw app publiceert, moet u toobe kunnen tooseparate Hallo telemetrie uit verschillende builds.</span><span class="sxs-lookup"><span data-stu-id="24317-151">When you publish a new version of your app, you'll want toobe able tooseparate hello telemetry from different builds.</span></span>

<span data-ttu-id="24317-152">U kunt Hallo toepassingsversie eigenschap instellen, zodat u kunt filteren [search](app-insights-diagnostic-search.md) en [metrische explorer](app-insights-metrics-explorer.md) resultaten.</span><span class="sxs-lookup"><span data-stu-id="24317-152">You can set hello Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filteren op een eigenschap](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="24317-154">Er zijn verschillende methoden gebruiken voor het instellen van Hallo toepassingsversie eigenschap.</span><span class="sxs-lookup"><span data-stu-id="24317-154">There are several different methods of setting hello Application Version property.</span></span>

* <span data-ttu-id="24317-155">Rechtstreeks worden ingesteld:</span><span class="sxs-lookup"><span data-stu-id="24317-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="24317-156">Inpakken van die regel in een [telemetrie initialisatiefunctie](app-insights-api-custom-events-metrics.md#defaults) tooensure die alle exemplaren van TelemetryClient consistent zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="24317-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) tooensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="24317-157">[ASP.NET] Stel de versie van de Hallo in `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="24317-157">[ASP.NET] Set hello version in `BuildInfo.config`.</span></span> <span data-ttu-id="24317-158">Hallo-versie van het Hallo BuildLabel knooppunt Hallo webmodule opgehaald.</span><span class="sxs-lookup"><span data-stu-id="24317-158">hello web module will pick up hello version from hello BuildLabel node.</span></span> <span data-ttu-id="24317-159">Dit bestand opnemen in uw project en vergeet niet tooset Hallo kopie altijd eigenschap in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="24317-159">Include this file in your project and remember tooset hello Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="24317-160">[ASP.NET] BuildInfo.config automatisch genereren in MSBuild.</span><span class="sxs-lookup"><span data-stu-id="24317-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="24317-161">toodo hiervan kan een paar regels tooyour toevoegen `.csproj` bestand:</span><span class="sxs-lookup"><span data-stu-id="24317-161">toodo this, add a few lines tooyour `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="24317-162">Hiermee wordt een bestand met de naam gegenereerd *yourProjectName*. BuildInfo.config. Hallo publicatieproces wijzigt de naam van het tooBuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="24317-162">This generates a file called *yourProjectName*.BuildInfo.config. hello Publish process renames it tooBuildInfo.config.</span></span>

    <span data-ttu-id="24317-163">Hallo build-label bevat een tijdelijke aanduiding (AutoGen_...) wanneer u bij het maken van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24317-163">hello build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="24317-164">Maar wanneer gebouwd met MSBuild, wordt dit ingevuld met de juiste versienummer Hallo.</span><span class="sxs-lookup"><span data-stu-id="24317-164">But when built with MSBuild, it is populated with hello correct version number.</span></span>

    <span data-ttu-id="24317-165">tooallow MSBuild toogenerate versienummers, stel de versie in hello, zoals `1.0.*` in AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="24317-165">tooallow MSBuild toogenerate version numbers, set hello version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="24317-166">Versie en release bijhouden</span><span class="sxs-lookup"><span data-stu-id="24317-166">Version and release tracking</span></span>
<span data-ttu-id="24317-167">toepassingsversie tootrack hello, zorg ervoor dat `buildinfo.config` wordt gegenereerd door de Engine voor het bouwen van Microsoft wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="24317-167">tootrack hello application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="24317-168">Voeg het volgende toe in uw .csproj-bestand:</span><span class="sxs-lookup"><span data-stu-id="24317-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="24317-169">Wanneer Hallo Buildgegevens beschikbaar zijn, voegt Hallo Application Insights-webmodule automatisch **toepassingsversie** als een item van de eigenschap tooevery telemetrie.</span><span class="sxs-lookup"><span data-stu-id="24317-169">When it has hello build info, hello Application Insights web module automatically adds **Application version** as a property tooevery item of telemetry.</span></span> <span data-ttu-id="24317-170">Hierdoor kunt u toofilter door versie bij het uitvoeren van [diagnostische zoekopdrachten](app-insights-diagnostic-search.md), of wanneer u [verkennen van metrische gegevens](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="24317-170">That allows you toofilter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="24317-171">Let er echter op dat Hallo buildversienummer alleen wordt gegenereerd door Hallo Microsoft bouwen Engine, niet door de ontwikkelaar van de Hallo bouwen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24317-171">However, notice that hello build version number is generated only by hello Microsoft Build Engine, not by hello developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="24317-172">Release-aantekeningen</span><span class="sxs-lookup"><span data-stu-id="24317-172">Release annotations</span></span>
<span data-ttu-id="24317-173">Als u Visual Studio Team Services gebruikt, kunt u [ophalen van de markering van een aantekening](app-insights-annotations.md) tooyour grafieken toegevoegd wanneer u een nieuwe versie.</span><span class="sxs-lookup"><span data-stu-id="24317-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added tooyour charts whenever you release a new version.</span></span> <span data-ttu-id="24317-174">Hallo volgende afbeelding ziet u hoe deze markering wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="24317-174">hello following image shows how this marker appears.</span></span>

![Schermopname van aantekening bij voorbeeldrelease in een grafiek](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="24317-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24317-176">Next steps</span></span>

* [<span data-ttu-id="24317-177">Gedeelde bronnen voor meerdere functies</span><span class="sxs-lookup"><span data-stu-id="24317-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="24317-178">Maken van een telemetrie initialisatiefunctie toodistinguish A | Varianten B</span><span class="sxs-lookup"><span data-stu-id="24317-178">Create a Telemetry Initializer toodistinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
