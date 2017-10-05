---
title: Application Insights voor Java-web-apps die al live
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
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="1c2e1-103">Application Insights voor Java-web-apps die al live</span><span class="sxs-lookup"><span data-stu-id="1c2e1-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="1c2e1-104">Als u een webtoepassing die al wordt uitgevoerd op uw J2EE-server hebt, kunt u starten met bewaking [Application Insights](app-insights-overview.md) zonder te hoeven codewijzigingen aanbrengen of opnieuw moet compileren uw project.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="1c2e1-105">Met deze optie krijgt u informatie over HTTP-aanvragen verzonden naar uw server, niet-verwerkte uitzonderingen en prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="1c2e1-106">U hebt een abonnement op [Microsoft Azure](https://azure.com) nodig.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="1c2e1-107">De procedure op deze pagina voegt de SDK toe aan uw web-app tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="1c2e1-108">Deze instrumentation runtime is handig als u niet wilt bijwerken of opnieuw opbouwen van de broncode.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="1c2e1-109">Maar indien mogelijk, raden we u [de SDK toevoegen aan de broncode](app-insights-java-get-started.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="1c2e1-110">Dat kunt u meer opties zoals het schrijven van code voor het bijhouden van gebruikersactiviteit.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="1c2e1-111">1. Een Application Insights-instrumentatiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="1c2e1-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="1c2e1-112">Aanmelden bij de [Microsoft Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1c2e1-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="1c2e1-113">Maak een nieuwe Application Insights-resource en het toepassingstype ingesteld op Java-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![Een naam invoeren, Java-web-app kiezen en op Maken klikken](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="1c2e1-115">De resource is gemaakt binnen een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="1c2e1-116">Open de nieuwe resource en de instrumentatiesleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="1c2e1-117">U moet deze sleutel zo dadelijk in de code van uw project plakken.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![Op Eigenschappen klikken in het overzicht van de nieuwe resource en de instrumentatiesleutel kopiëren](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="1c2e1-119">2. De SDK downloaden</span><span class="sxs-lookup"><span data-stu-id="1c2e1-119">2. Download the SDK</span></span>
1. <span data-ttu-id="1c2e1-120">Download de [Application Insights-SDK voor Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="1c2e1-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="1c2e1-121">Pak op uw server, de SDK-inhoud naar de map van waaruit u de binaire project worden geladen.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="1c2e1-122">Als u Tomcat, zou deze map normaal zijn onder`webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="1c2e1-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="1c2e1-123">Houd er rekening mee dat u moet dit herhalen op elke server-exemplaar en voor elke app.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="1c2e1-124">3. Een Application Insights XML-bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c2e1-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="1c2e1-125">ApplicationInsights.xml maken in de map waarin u de SDK hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="1c2e1-126">De volgende XML-code in het geplaatst.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-126">Put into it the following XML.</span></span>

<span data-ttu-id="1c2e1-127">Vervang de instrumentatiesleutel die u in de Azure Portal hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="1c2e1-128">De instrumentatiesleutel wordt samen met alle telemetrie-items verzonden en instrueert Application Insights om deze in de resource weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="1c2e1-129">Het onderdeel voor de HTTP-aanvraag is optioneel.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="1c2e1-130">Het verzendt automatisch telemetrie over aanvragen en reactietijden naar de portal.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="1c2e1-131">Correlatie tussen gebeurtenissen is een aanvulling op het onderdeel voor de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="1c2e1-132">Deze aanvulling wijst een id toe aan elke aanvraag die door de server wordt ontvangen en voegt deze id als de eigenschap 'Operation.Id' toe aan elk telemetrie-item.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="1c2e1-133">Hiermee kunt u correlaties zichtbaar maken tussen de telemetrie die is gekoppeld aan elke aanvraag door een filter in te stellen [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1c2e1-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="1c2e1-134">4. Een HTTP-filter toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c2e1-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="1c2e1-135">Zoek en open het web.xml-bestand in uw project en samenvoegen van het volgende codefragment onder het knooppunt web-app, waar de toepassingsfilters zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="1c2e1-136">Voor de nauwkeurigste resultaten moet het filter vóór alle andere filters worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="1c2e1-137">5. Controleer de firewall-uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="1c2e1-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="1c2e1-138">Mogelijk moet u [uitzonderingen uitgaande gegevens verzenden instellen](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="1c2e1-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="1c2e1-139">6. Opnieuw opstarten van uw web-app</span><span class="sxs-lookup"><span data-stu-id="1c2e1-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="1c2e1-140">7. Uw telemetrie in Application Insights weergeven</span><span class="sxs-lookup"><span data-stu-id="1c2e1-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="1c2e1-141">Ga terug naar uw Application Insights-resource in de [Microsoft Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c2e1-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="1c2e1-142">Telemetrie over HTTP-aanvragen wordt weergegeven op de overzichtsblade.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="1c2e1-143">(Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)</span><span class="sxs-lookup"><span data-stu-id="1c2e1-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![voorbeeldgegevens](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="1c2e1-145">Klik in een grafiek voor gedetailleerdere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="1c2e1-146">En wanneer u de eigenschappen van een aanvraag bekijkt, ziet u de telemetriegebeurtenissen die zijn gekoppeld aan deze zoals aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="1c2e1-147">Meer informatie over metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="1c2e1-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c2e1-148">Next steps</span></span>
* <span data-ttu-id="1c2e1-149">[Voeg telemetrie toe aan uw webpagina's](app-insights-javascript.md) bewaken van paginaweergaven en metrische gegevens over gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="1c2e1-150">[Webtests instellen](app-insights-monitor-web-app-availability.md) om ervoor te zorgen dat uw toepassing blijft live en responsief.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="1c2e1-151">Logboektraceringen vastleggen</span><span class="sxs-lookup"><span data-stu-id="1c2e1-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="1c2e1-152">[Zoek naar gebeurtenissen en logboeken](app-insights-diagnostic-search.md) om u te helpen bij het analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="1c2e1-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>

