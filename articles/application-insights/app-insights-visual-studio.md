---
title: Fouten opsporen in toepassingen met Azure Application Insights in Visual Studio | Microsoft Docs
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
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="51742-103">Fouten opsporen in uw toepassingen met Azure Application Insights in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51742-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="51742-104">In Visual Studio (2015 en hoger) kunt u de prestaties analyseren en problemen in uw ASP.NET web-app identificeren tijdens de foutopsporing en algemeen gebruik. Dit gebeurt aan de hand van telemetrie uit [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51742-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="51742-105">Als u uw ASP.NET-web-app hebt gemaakt met Visual Studio 2017 of hoger, beschikt deze al over de Application Insights-SDK.</span><span class="sxs-lookup"><span data-stu-id="51742-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="51742-106">Anders [voegt u Application Insights aan uw app toe](app-insights-asp-net.md) als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="51742-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="51742-107">Als uw app wilt bewaken wanneer deze in live productie is, bekijkt u normaal gesproken de Application Insights-telemetrie in de [Azure-portal](https://portal.azure.com), waar u waarschuwingen kunt instellen en krachtige bewakingsprogramma's kunt toepassen.</span><span class="sxs-lookup"><span data-stu-id="51742-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="51742-108">Voor foutopsporing kunt u echter ook de telemetrie in Visual Studio zoeken en analyseren.</span><span class="sxs-lookup"><span data-stu-id="51742-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="51742-109">U kunt Visual Studio gebruiken voor het analyseren van telemetrie van uw productiesite en van foutopsporing wordt uitgevoerd op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="51742-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="51742-110">In het laatste geval kunt u foutopsporingsruns al analyseren nog voordat u de SDK hebt geconfigureerd om telemetrie naar de Azure-portal te verzenden.</span><span class="sxs-lookup"><span data-stu-id="51742-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="51742-111"><a name="run"></a> Fouten opsporen in uw project</span><span class="sxs-lookup"><span data-stu-id="51742-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="51742-112">Voer uw web-app in de lokale foutopsporingsmodus door op F5 te drukken.</span><span class="sxs-lookup"><span data-stu-id="51742-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="51742-113">Open verschillende pagina's om telemetrie te genereren.</span><span class="sxs-lookup"><span data-stu-id="51742-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="51742-114">In Visual Studio ziet u een aantal van de gebeurtenissen die zijn geregistreerd door de Application Insights-module in uw project.</span><span class="sxs-lookup"><span data-stu-id="51742-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![Tijdens het opsporen van fouten wordt in Visual Studio de knop Application Insights weergegeven.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="51742-116">Klik op deze knop om uw telemetrie te doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="51742-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="51742-117">Application Insights-zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="51742-117">Application Insights search</span></span>
<span data-ttu-id="51742-118">In het zoekvenster van Application Insights worden geregistreerde gebeurtenissen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="51742-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="51742-119">(Als u aangemeld bij Azure bij het instellen van Application Insights, kunt u dezelfde gebeurtenissen zoeken in de Azure portal.)</span><span class="sxs-lookup"><span data-stu-id="51742-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![Klik met de rechtermuisknop op het project en kies Application Insights > Zoeken.](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="51742-121">Nadat u filters hebt in- of uitgeschakeld, klikt u op de knop Zoeken aan het einde van het veld Tekst zoeken.</span><span class="sxs-lookup"><span data-stu-id="51742-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="51742-122">U kunt zoeken met vrije tekst gebruiken voor alle velden in de gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="51742-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="51742-123">Zoek bijvoorbeeld naar een deel van de URl van een pagina, naar de waarde van een eigenschap, zoals de clientlocatie, of naar specifieke woorden in een traceringslogboek.</span><span class="sxs-lookup"><span data-stu-id="51742-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="51742-124">Klik op een gebeurtenis om de gedetailleerde eigenschappen ervan weer te geven.</span><span class="sxs-lookup"><span data-stu-id="51742-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="51742-125">Voor aanvragen voor uw web-app, kunt u verder klikken naar de code.</span><span class="sxs-lookup"><span data-stu-id="51742-125">For requests to your web app, you can click through to the code.</span></span>

![Klik onder Aanvraagdetails door naar de code](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="51742-127">U kunt ook de Verwante items openen om mislukte aanvragen of uitzonderingen te diagnosticeren.</span><span class="sxs-lookup"><span data-stu-id="51742-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![Blader onder Aanvraagdetails naar beneden, naar gerelateerde items](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="51742-129">Weergave uitzonderingen en mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="51742-129">View exceptions and failed requests</span></span>
<span data-ttu-id="51742-130">Uitzonderingsrapporten worden weergegeven in het venster Zoeken.</span><span class="sxs-lookup"><span data-stu-id="51742-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="51742-131">(In enkele oudere typen ASP.NET-toepassingen moet u [uitzonderingencontrole instellen](app-insights-asp-net-exceptions.md) om te zien welke uitzonderingen door het framework worden afgehandeld.)</span><span class="sxs-lookup"><span data-stu-id="51742-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="51742-132">Klik op een uitzondering voor een stack-trace.</span><span class="sxs-lookup"><span data-stu-id="51742-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="51742-133">Als de code van de app in Visual Studio is geopend, kunt u via de stack-trace doorklikken naar de relevante coderegel.</span><span class="sxs-lookup"><span data-stu-id="51742-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![Uitzondering voor stack-trace](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="51742-135">Samenvattingen van de aanvraag en uitzonderingen in de code weergeven</span><span class="sxs-lookup"><span data-stu-id="51742-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="51742-136">In de regel Code Lens boven elke handler-methode ziet u een aantal van de aanvragen en uitzonderingen die zijn geregistreerd door Application Insights in de afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="51742-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![Uitzondering voor stack-trace](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="51742-138">Code Lens toont alleen Application Insights-gegevens als u [uw app hebt geconfigureerd om telemetrie te verzenden naar de Application Insights-portal](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="51742-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="51742-139">Meer informatie over Application Insights in Code Lens</span><span class="sxs-lookup"><span data-stu-id="51742-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="51742-140">Trends</span><span class="sxs-lookup"><span data-stu-id="51742-140">Trends</span></span>
<span data-ttu-id="51742-141">Trends is een hulpprogramma waarmee u de werking van uw app gedurende een bepaalde periode kunt visualiseren.</span><span class="sxs-lookup"><span data-stu-id="51742-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="51742-142">Kies **Telemetrietrends verkennen** op de Application Insights-werkbalkknop of in het Application Insights-zoekvenster.</span><span class="sxs-lookup"><span data-stu-id="51742-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="51742-143">Kies een van de vijf algemene query's om te beginnen.</span><span class="sxs-lookup"><span data-stu-id="51742-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="51742-144">U kunt verschillende gegevenssets analyseren op basis van telemetrietypen, tijdsbereik en andere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="51742-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="51742-145">Als u wilt zoeken naar afwijkingen in uw gegevens, kiest u een van de afwijkingsopties onder de vervolgkeuzelijst Type weergave.</span><span class="sxs-lookup"><span data-stu-id="51742-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="51742-146">Met de filteropties aan de onderkant van het venster kunt u eenvoudig specifieke subreeksen van uw telemetrie selecteren.</span><span class="sxs-lookup"><span data-stu-id="51742-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![Trends](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="51742-148">[Meer informatie over Trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="51742-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="51742-149">Lokale bewaking</span><span class="sxs-lookup"><span data-stu-id="51742-149">Local monitoring</span></span>
<span data-ttu-id="51742-150">(Vanaf Visual Studio 2015 Update 2) Als u dit nog niet hebt geconfigureerd voor de SDK voor het verzenden van telemetrie naar de Application Insights-portal (zodat er geen instrumentatiesleutel in ApplicationInsights.config is) geeft de diagnostics-venster weer telemetrie van de meest recente foutopsporingssessie.</span><span class="sxs-lookup"><span data-stu-id="51742-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="51742-151">Dit is handig als u al een eerdere versie van uw app hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="51742-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="51742-152">Zo voorkomt u dat de telemetrie van uw foutopsporingssessies in de Application Insights-portal wordt verward met de telemetrie over de gepubliceerde app.</span><span class="sxs-lookup"><span data-stu-id="51742-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="51742-153">Ook als u beschikt over [aangepaste telemetrie](app-insights-api-custom-events-metrics.md) waarin u fouten wilt opsporen voordat u deze naar de portal verzendt, komt deze functie van pas.</span><span class="sxs-lookup"><span data-stu-id="51742-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="51742-154">*Aanvankelijk heb ik Application Insights volledig geconfigureerd om telemetrie naar de portal te verzenden. Maar nu wil ik de telemetrie alleen bekijken in Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="51742-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="51742-155">De instellingen van het venster Zoeken bevat een optie om lokale diagnostische gegevens te doorzoeken, zelfs als uw app telemetrie verzendt naar de portal.</span><span class="sxs-lookup"><span data-stu-id="51742-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="51742-156">Als u geen telemetrie meer naar de portal wilt verzenden, moet u de regel `<instrumentationkey>...` in ApplicationInsights.config uitcommentariëren. Als u weer telemetrie naar de portal wilt verzenden, verwijdert u het commentaarteken.</span><span class="sxs-lookup"><span data-stu-id="51742-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="51742-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51742-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="51742-158">**[Meer gegevens toevoegen](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="51742-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="51742-159">Bewaak het gebruik, de beschikbaarheid, de afhankelijkheden en de uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="51742-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="51742-160">Integreer bijgehouden informatie uit frameworks voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="51742-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="51742-161">Schrijf aangepaste telemetrie.</span><span class="sxs-lookup"><span data-stu-id="51742-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="51742-163">**[Werken met de Application Insights-portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="51742-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="51742-164">Dashboards, krachtige hulpprogramma's voor diagnose en analyse, waarschuwingen, een live afhankelijkheidskaart van uw toepassing en de geëxporteerde telemetriegegevens weergeven.</span><span class="sxs-lookup"><span data-stu-id="51742-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

