---
title: Application Insights voor ASP.NET Core aaaAzure | Microsoft Docs
description: Bewaken van webtoepassingen voor beschikbaarheid, prestaties en het gebruik.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="0b575-103">Application Insights voor ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="0b575-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="0b575-104">[Application Insights](app-insights-overview.md) kunt u uw webtoepassing voor beschikbaarheid, prestaties en gebruik te bewaken.</span><span class="sxs-lookup"><span data-stu-id="0b575-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="0b575-105">Hallo feedback die u over Hallo prestaties en de effectiviteit van uw app in Hallo wilde krijgen, kunt u beslissen Hallo richting van het Hallo-ontwerp in elke ontwikkelingscyclus.</span><span class="sxs-lookup"><span data-stu-id="0b575-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![Voorbeeld](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="0b575-107">U hebt een abonnement met [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="0b575-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="0b575-108">Meld u aan met een Microsoft-account, dat u mogelijk al hebt voor Windows, XBox Live of andere Microsoft-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="0b575-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="0b575-109">Uw team wellicht een organisatie-abonnement tooAzure: Hallo eigenaar tooadd vraag tooit u met uw Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="0b575-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0b575-110">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="0b575-110">Getting started</span></span>

* <span data-ttu-id="0b575-111">In Visual Studio Solution Explorer met de rechtermuisknop op uw project en selecteer **Configure Application Insights**, of **toevoegen > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="0b575-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="0b575-112">[Meer informatie](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="0b575-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="0b575-113">Als u deze opdrachten niet ziet, voert u de Hallo [handmatige aan de slag](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="0b575-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="0b575-114">Mogelijk moet u toodo dit als uw project is gemaakt met een versie van Visual Studio voordat 2017.</span><span class="sxs-lookup"><span data-stu-id="0b575-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="0b575-115">Application Insights gebruiken</span><span class="sxs-lookup"><span data-stu-id="0b575-115">Using Application Insights</span></span>
<span data-ttu-id="0b575-116">Meld u aan bij Hallo [Microsoft Azure-portal](https://portal.azure.com), selecteer **alle Resources** of **Application Insights**, en selecteer vervolgens Hallo resource u toomonitor uw app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0b575-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="0b575-117">Gebruik uw app een tijdje in een apart browservenster.</span><span class="sxs-lookup"><span data-stu-id="0b575-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="0b575-118">Hier ziet u gegevens verschijnen in Hallo Application Insights-grafieken.</span><span class="sxs-lookup"><span data-stu-id="0b575-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="0b575-119">(U wellicht tooclick vernieuwen.) Er is een kleine hoeveelheid gegevens terwijl u ontwikkelt, maar deze grafieken echt tot leven komen wanneer u uw app publiceren en veel gebruikers hebben.</span><span class="sxs-lookup"><span data-stu-id="0b575-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="0b575-120">overzichtspagina Hallo toont prestatiegrafieken: serverreactietijd, paginalaadtijd en tellingen van mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="0b575-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="0b575-121">Klik op een grafiek toosee meer grafieken en gegevens.</span><span class="sxs-lookup"><span data-stu-id="0b575-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="0b575-122">Weergaven in de portal Hallo kunnen worden onderverdeeld in drie hoofdcategorieën:</span><span class="sxs-lookup"><span data-stu-id="0b575-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="0b575-123">[Metrics Explorer](app-insights-metrics-explorer.md) grafieken en tabellen van de metrische gegevens en aantallen zoals reactietijden, uitvalpercentage of metrische gegevens ziet u zelf maken met de Hallo [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0b575-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="0b575-124">Filter en segment Hallo-gegevens door de eigenschap waarden tooget een beter inzicht in uw app en de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0b575-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="0b575-125">[Zoek Explorer](app-insights-diagnostic-search.md) geeft een lijst van afzonderlijke gebeurtenissen, zoals een specifieke aanvragen, uitzonderingen, logboektraceringen of gebeurtenissen die u zelf hebt gemaakt met de Hallo [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0b575-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="0b575-126">Filteren op Hallo gebeurtenissen zoeken en navigeren tussen gerelateerde gebeurtenissen tooinvestigate problemen.</span><span class="sxs-lookup"><span data-stu-id="0b575-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="0b575-127">[Analytics](app-insights-analytics.md) kunt u SQL-achtige query's uitvoeren via uw Telemetrie en is een krachtig analytische en diagnostische hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="0b575-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="0b575-128">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="0b575-128">Alerts</span></span>
* <span data-ttu-id="0b575-129">Automatisch [proactieve diagnostische waarschuwingen](app-insights-proactive-diagnostics.md) waarmee wordt aangegeven dat u over afwijkende wijzigingen in uitvalpercentage en andere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="0b575-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="0b575-130">Instellen van [beschikbaarheidstests](app-insights-monitor-web-app-availability.md) tootest e-mails met uw website voortdurend van locaties wereldwijd en get zodra een mislukt test.</span><span class="sxs-lookup"><span data-stu-id="0b575-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="0b575-131">Instellen van [metrische waarschuwingen](app-insights-monitor-web-app-availability.md) tooknow als metrische gegevens zoals reactietijden of uitzondering tarieven buiten acceptabele grenzen gaat.</span><span class="sxs-lookup"><span data-stu-id="0b575-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="0b575-132">Video</span><span class="sxs-lookup"><span data-stu-id="0b575-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="0b575-133">Open source</span><span class="sxs-lookup"><span data-stu-id="0b575-133">Open source</span></span>
[<span data-ttu-id="0b575-134">Lezen en bij te dragen toohello code</span><span class="sxs-lookup"><span data-stu-id="0b575-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="0b575-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0b575-135">Next steps</span></span>
* <span data-ttu-id="0b575-136">[Voeg telemetrie tooyour webpagina's](app-insights-javascript.md) toomonitor pagina gebruik en prestaties.</span><span class="sxs-lookup"><span data-stu-id="0b575-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="0b575-137">[Afhankelijkheden bewaken](app-insights-asp-net-dependencies.md) toosee als REST, SQL of andere externe bronnen u vertragen.</span><span class="sxs-lookup"><span data-stu-id="0b575-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="0b575-138">[Hallo-API gebruiken](app-insights-api-custom-events-metrics.md) toosend uw eigen gebeurtenissen en metrische gegevens voor een meer gedetailleerde weergave van de prestaties en het gebruik van uw app.</span><span class="sxs-lookup"><span data-stu-id="0b575-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="0b575-139">[Beschikbaarheidstests](app-insights-monitor-web-app-availability.md) controleren van uw app continu uit Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="0b575-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

