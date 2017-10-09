---
title: aaaDebug toepassingen met Azure Application Insights in Visual Studio | Microsoft Docs
description: Analyse van web-app-prestaties en diagnostische gegevens tijdens foutopsporing en algemeen gebruik.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="5c3a9-103">Fouten opsporen in uw toepassingen met Azure Application Insights in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5c3a9-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="5c3a9-104">In Visual Studio (2015 en hoger) kunt u de prestaties analyseren en problemen in uw ASP.NET web-app identificeren tijdens de foutopsporing en algemeen gebruik. Dit gebeurt aan de hand van telemetrie uit [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c3a9-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="5c3a9-105">Als u uw ASP.NET-web-app met behulp van Visual Studio 2017 gemaakt of hoger, er al Hallo Application Insights-SDK.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="5c3a9-106">Als u dit nog niet hebt gedaan, anders [Application Insights tooyour app toevoegen](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="5c3a9-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="5c3a9-107">toomonitor uw app wanneer deze in live productie is, u normaal gesproken Hallo Application Insights telemetrie weergeven in Hallo [Azure-portal](https://portal.azure.com), waar u kunt waarschuwingen instellen en krachtige bewakingsprogramma's toepassen.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="5c3a9-108">Maar voor foutopsporing, u kunt ook zoeken en analyseren Hallo telemetrie in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="5c3a9-109">U kunt Visual Studio tooanalyze telemetrie van uw productiesite en van foutopsporing wordt uitgevoerd op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="5c3a9-110">In het laatste geval hello, kunt u foutopsporing wordt uitgevoerd analyseren, zelfs als u Hallo SDK toosend telemetrie toohello Azure-portal nog niet hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="5c3a9-111"><a name="run"></a> Fouten opsporen in uw project</span><span class="sxs-lookup"><span data-stu-id="5c3a9-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="5c3a9-112">Voer uw web-app in de lokale foutopsporingsmodus door op F5 te drukken.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="5c3a9-113">Open verschillende pagina's toogenerate telemetrie.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="5c3a9-114">In Visual Studio ziet u een aantal Hallo-gebeurtenissen die zijn geregistreerd door Hallo Application Insights-module in uw project.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![In Visual Studio weergegeven de knop Application Insights Hallo tijdens de foutopsporing.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="5c3a9-116">Klik op deze knop toosearch uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="5c3a9-117">Application Insights-zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="5c3a9-117">Application Insights search</span></span>
<span data-ttu-id="5c3a9-118">Hallo Application Insights zoekvenster worden gebeurtenissen weergegeven die zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="5c3a9-119">(Als u tooAzure aangemeld bij het instellen van Application Insights, kunt u zoeken Hallo dezelfde gebeurtenissen in hello Azure-portal.)</span><span class="sxs-lookup"><span data-stu-id="5c3a9-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Met de rechtermuisknop op het Hallo-project en kies Application Insights zoeken](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="5c3a9-121">Nadat u selecteren of selectie filters opheffen, klikt u op Hallo zoekknop achter Hallo Hallo zoeken tekstveld.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="5c3a9-122">zoeken met vrije tekst Hello werkt voor alle velden in het Hallo-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="5c3a9-123">Bijvoorbeeld zoeken naar een deel van Hallo-URL van een pagina. of Hallo-waarde van een eigenschap, zoals de clientlocatie, of naar specifieke woorden in een traceringslogboek.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="5c3a9-124">Klik op een gebeurtenis toosee gedetailleerde eigenschappen ervan.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="5c3a9-125">U kunt de code toohello doorklikken voor aanvragen tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-125">For requests tooyour web app, you can click through toohello code.</span></span>

![Klik onder Details aanvragen door toohello code](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="5c3a9-127">U kunt ook verwante items openen toohelp onderzoeken mislukte aanvragen of uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![Onder aanvraaggegevens, schuif naar beneden toorelated items](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="5c3a9-129">Weergave uitzonderingen en mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="5c3a9-129">View exceptions and failed requests</span></span>
<span data-ttu-id="5c3a9-130">Uitzondering rapporten weergeven in het zoekvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="5c3a9-131">(In sommige oudere typen van ASP.NET-toepassing, hebt u te[instellen uitzonderingenmonitor](app-insights-asp-net-exceptions.md) toosee uitzonderingen die worden verwerkt door het Hallo-framework.)</span><span class="sxs-lookup"><span data-stu-id="5c3a9-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="5c3a9-132">Klik op een uitzondering tooget een stack-trace.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="5c3a9-133">Als Hallo-code van Hallo app openen in Visual Studio, kunt u zich kunt doorklikken van Hallo stack trace toohello relevante coderegel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![Uitzondering voor stack-trace](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="5c3a9-135">Samenvattingen van de aanvraag en uitzondering in Hallo code weergeven</span><span class="sxs-lookup"><span data-stu-id="5c3a9-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="5c3a9-136">In Hallo Code Lens regel boven elke handler-methode ziet u een aantal van Hallo aanvragen en uitzonderingen die zijn geregistreerd door Application Insights in Hallo afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![Uitzondering voor stack-trace](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="5c3a9-138">Code Lens toont alleen de gegevens voor de Application Insights als er [geconfigureerd van uw app toosend telemetrie toohello Application Insights-portal](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="5c3a9-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="5c3a9-139">Meer informatie over Application Insights in Code Lens</span><span class="sxs-lookup"><span data-stu-id="5c3a9-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="5c3a9-140">Trends</span><span class="sxs-lookup"><span data-stu-id="5c3a9-140">Trends</span></span>
<span data-ttu-id="5c3a9-141">Trends is een hulpprogramma waarmee u de werking van uw app gedurende een bepaalde periode kunt visualiseren.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="5c3a9-142">Kies **verkennen telemetrie Trends** van Application Insights-werkbalkknop Hallo of venster Application Insights zoeken.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="5c3a9-143">Kies een van vijf algemene query's tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="5c3a9-144">U kunt verschillende gegevenssets analyseren op basis van telemetrietypen, tijdsbereik en andere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="5c3a9-145">toofind afwijkingen in uw gegevens, kies een van de Hallo afwijkingsdetectie opties onder Hallo 'Weergavetype' vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="5c3a9-146">Hallo filteropties onderaan Hallo Hallo-venster maken het gemakkelijk toohone in op specifieke subreeksen van uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![Trends](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="5c3a9-148">[Meer informatie over Trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="5c3a9-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="5c3a9-149">Lokale bewaking</span><span class="sxs-lookup"><span data-stu-id="5c3a9-149">Local monitoring</span></span>
<span data-ttu-id="5c3a9-150">(Vanaf Visual Studio 2015 Update 2) Als u dit nog niet hebt Hallo SDK toosend telemetrie toohello Application Insights-portal (zo geconfigureerd dat er geen instrumentatiesleutel in ApplicationInsights.config is) geeft de diagnostics-venster Hallo telemetrie van de meest recente foutopsporingssessie.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="5c3a9-151">Dit is handig als u al een eerdere versie van uw app hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="5c3a9-152">U wilt niet dat Hallo telemetrie van uw foutopsporing sessies toobe verward met Hallo telemetrie over Hallo Hallo gepubliceerde app Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="5c3a9-153">Het is ook handig als u beschikt over sommige [aangepaste telemetrie](app-insights-api-custom-events-metrics.md) dat u wilt dat toodebug voor het verzenden van telemetrie toohello portal.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="5c3a9-154">*Volledig geconfigureerd ik aanvankelijk Application Insights toosend telemetrie toohello-portal. Maar nu wil ik toosee Hallo telemetrie alleen in Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="5c3a9-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="5c3a9-155">In de instellingen van Hallo zoekvenster is er een optie toosearch lokale diagnostische gegevens zelfs als uw app telemetrie toohello portal verzendt.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="5c3a9-156">toostop telemetrie verstuurd toohello portal commentaar Hallo regel `<instrumentationkey>...` in ApplicationInsights.config. Wanneer u klaar toosend telemetrie toohello portal opnieuw bent, verwijdert u het commentaarteken.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5c3a9-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5c3a9-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="5c3a9-158">**[Meer gegevens toevoegen](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="5c3a9-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="5c3a9-159">Bewaak het gebruik, de beschikbaarheid, de afhankelijkheden en de uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="5c3a9-160">Integreer bijgehouden informatie uit frameworks voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="5c3a9-161">Schrijf aangepaste telemetrie.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="5c3a9-163">**[Werken met Hallo Application Insights-portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="5c3a9-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="5c3a9-164">Dashboards, krachtige hulpprogramma's voor diagnose en analyse, waarschuwingen, een live afhankelijkheidskaart van uw toepassing en de geëxporteerde telemetriegegevens weergeven.</span><span class="sxs-lookup"><span data-stu-id="5c3a9-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

