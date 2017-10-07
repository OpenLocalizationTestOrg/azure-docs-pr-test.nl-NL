---
title: aaaApplication Insights voor Java web-apps die al live zijn
description: Bewaking van een webtoepassing die al wordt uitgevoerd op uw server starten
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="a9302-103">Application Insights voor Java-web-apps die al live</span><span class="sxs-lookup"><span data-stu-id="a9302-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="a9302-104">Als u een webtoepassing die al wordt uitgevoerd op uw J2EE-server hebt, kunt u starten met bewaking [Application Insights](app-insights-overview.md) zonder Hallo toomake moet wijzigingen code of opnieuw moet compileren uw project.</span><span class="sxs-lookup"><span data-stu-id="a9302-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="a9302-105">Met deze optie krijgt u informatie over HTTP-aanvragen verzonden tooyour server, niet-verwerkte uitzonderingen en prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="a9302-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="a9302-106">U hebt een abonnement te[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9302-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="a9302-107">Hallo-procedure op deze pagina wordt Hallo SDK tooyour web-app toegevoegd tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="a9302-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="a9302-108">Deze instrumentation runtime is handig als u niet wilt dat tooupdate of opnieuw opbouwen van de broncode.</span><span class="sxs-lookup"><span data-stu-id="a9302-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="a9302-109">Maar indien mogelijk, raden we u [Hallo SDK toohello broncode toevoegen](app-insights-java-get-started.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="a9302-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="a9302-110">Die biedt u meer mogelijkheden, zoals het schrijven van code tootrack gebruikersactiviteit.</span><span class="sxs-lookup"><span data-stu-id="a9302-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="a9302-111">1. Een Application Insights-instrumentatiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="a9302-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="a9302-112">Meld u aan toohello [Microsoft Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a9302-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="a9302-113">Maak een nieuwe Application Insights-resource en stel Hallo toepassing type tooJava-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="a9302-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![Een naam invoeren, Java-web-app kiezen en op Maken klikken](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="a9302-115">Hallo-resource is gemaakt in een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="a9302-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="a9302-116">Open de nieuwe resource Hallo en de instrumentatiesleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="a9302-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="a9302-117">U moet toopaste deze sleutel in uw CodeProject binnenkort.</span><span class="sxs-lookup"><span data-stu-id="a9302-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="a9302-119">2. Hallo SDK downloaden</span><span class="sxs-lookup"><span data-stu-id="a9302-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="a9302-120">Hallo downloaden [Application Insights-SDK voor Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="a9302-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="a9302-121">Pak op uw server Hallo SDK inhoud toohello-map van waaruit u de binaire project worden geladen.</span><span class="sxs-lookup"><span data-stu-id="a9302-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="a9302-122">Als u Tomcat, zou deze map normaal zijn onder`webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="a9302-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="a9302-123">Houd er rekening mee dat u toorepeat dit op elke server-exemplaar en voor elke app moet.</span><span class="sxs-lookup"><span data-stu-id="a9302-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="a9302-124">3. Een Application Insights XML-bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="a9302-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="a9302-125">Maak ApplicationInsights.xml in Hallo map waarin u Hallo SDK hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a9302-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="a9302-126">In deze geplaatst Hallo na XML.</span><span class="sxs-lookup"><span data-stu-id="a9302-126">Put into it hello following XML.</span></span>

<span data-ttu-id="a9302-127">Vervang Hallo instrumentatiesleutel die u hebt gekregen hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a9302-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="a9302-128">Hallo-instrumentatiesleutel samen met elk telemetrie-item is verzonden en instrueert Application Insights toodisplay in de resource.</span><span class="sxs-lookup"><span data-stu-id="a9302-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="a9302-129">Hallo onderdeel HTTP-aanvraag is optioneel.</span><span class="sxs-lookup"><span data-stu-id="a9302-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="a9302-130">Het verzendt automatisch telemetrie over aanvragen en -antwoord keren toohello portal.</span><span class="sxs-lookup"><span data-stu-id="a9302-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="a9302-131">Correlatie tussen gebeurtenissen is een onderdeel toevoeging toohello HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="a9302-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="a9302-132">Het wijst een id tooeach-aanvraag is ontvangen door Hallo-server en deze id wordt als een item van de eigenschap tooevery telemetrie als Hallo-eigenschap 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="a9302-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="a9302-133">Hiermee kunt u toocorrelate Hallo telemetrie die is gekoppeld aan elke aanvraag door een filter in te stellen [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="a9302-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="a9302-134">4. Een HTTP-filter toevoegen</span><span class="sxs-lookup"><span data-stu-id="a9302-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="a9302-135">Zoek en open het web.xml-bestand Hallo in uw project en merge Hallo volgende codefragment onder Hallo web-app-knooppunt, waar de toepassingsfilters zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a9302-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="a9302-136">tooget hello nauwkeurigste resultaten Hallo filter moeten vóór alle andere filters worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a9302-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="a9302-137">5. Controleer de firewall-uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="a9302-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="a9302-138">U moet mogelijk te[uitzonderingen instellen toosend uitgaande gegevens](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="a9302-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="a9302-139">6. Opnieuw opstarten van uw web-app</span><span class="sxs-lookup"><span data-stu-id="a9302-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="a9302-140">7. Uw telemetrie in Application Insights weergeven</span><span class="sxs-lookup"><span data-stu-id="a9302-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="a9302-141">Application Insights-resource in tooyour retourneren [Microsoft Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9302-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="a9302-142">Telemetrie over HTTP-aanvragen wordt weergegeven op de overzichtsblade Hallo.</span><span class="sxs-lookup"><span data-stu-id="a9302-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="a9302-143">(Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)</span><span class="sxs-lookup"><span data-stu-id="a9302-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![voorbeeldgegevens](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="a9302-145">Klik op via een grafiek toosee gedetailleerdere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a9302-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="a9302-146">En wanneer u bekijkt hello eigenschappen van een aanvraag, ziet u Hallo telemetrische gebeurtenissen gekoppeld zoals aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="a9302-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="a9302-147">Meer informatie over metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a9302-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="a9302-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a9302-148">Next steps</span></span>
* <span data-ttu-id="a9302-149">[Voeg telemetrie tooyour webpagina's](app-insights-javascript.md) toomonitor pagina weergaven en metrische gegevens over gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a9302-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="a9302-150">[Webtests instellen](app-insights-monitor-web-app-availability.md) toomake zorgen dat uw toepassing live en responsief blijft.</span><span class="sxs-lookup"><span data-stu-id="a9302-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="a9302-151">Logboektraceringen vastleggen</span><span class="sxs-lookup"><span data-stu-id="a9302-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="a9302-152">[Zoek naar gebeurtenissen en logboeken](app-insights-diagnostic-search.md) toohelp analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="a9302-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

