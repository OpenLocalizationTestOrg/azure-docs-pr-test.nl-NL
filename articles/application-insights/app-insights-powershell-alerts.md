---
title: aaaUse Powershell tooset waarschuwingen in Application Insights | Microsoft Docs
description: Configuratie van Application Insights tooget e-mailberichten over metrische wijzigingen automatiseren.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="b10bc-103">Gebruik PowerShell tooset waarschuwingen in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b10bc-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="b10bc-104">U kunt de configuratie Hallo van automatiseren [waarschuwingen](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b10bc-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="b10bc-105">Bovendien kunt u [webhooks tooautomate uw antwoord tooan waarschuwing instellen](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b10bc-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b10bc-106">Als u wilt toocreate bronnen en waarschuwingen op Hallo dezelfde tijd, overweeg dan [met een Azure Resource Manager-sjabloon](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b10bc-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="b10bc-107">Eenmalige instelling</span><span class="sxs-lookup"><span data-stu-id="b10bc-107">One-time setup</span></span>
<span data-ttu-id="b10bc-108">Als u dit nog niet hebt PowerShell met uw Azure-abonnement voordat gebruikt:</span><span class="sxs-lookup"><span data-stu-id="b10bc-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="b10bc-109">Hello Azure Powershell-module installeren op Hallo machine waar u toorun Hallo scripts.</span><span class="sxs-lookup"><span data-stu-id="b10bc-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="b10bc-110">Installeer [Microsoft Web Platform Installer (v5 of hoger)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="b10bc-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="b10bc-111">Deze tooinstall Microsoft Azure Powershell gebruiken</span><span class="sxs-lookup"><span data-stu-id="b10bc-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="b10bc-112">Verbinding maken met tooAzure</span><span class="sxs-lookup"><span data-stu-id="b10bc-112">Connect tooAzure</span></span>
<span data-ttu-id="b10bc-113">Open Azure PowerShell en [tooyour abonnement verbinding](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="b10bc-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="b10bc-114">Ontvang waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="b10bc-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="b10bc-115">Waarschuwing toevoegen</span><span class="sxs-lookup"><span data-stu-id="b10bc-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="b10bc-116">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="b10bc-116">Example 1</span></span>
<span data-ttu-id="b10bc-117">Stuur mij een e-mail als Hallo-server antwoord tooHTTP aanvragen, meer dan 5 minuten, een gemiddelde waarde is lager dan 1 seconde.</span><span class="sxs-lookup"><span data-stu-id="b10bc-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="b10bc-118">Mijn Application Insights-resource IceCreamWebApp wordt genoemd en is in de resourcegroep Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="b10bc-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="b10bc-119">Ik ben eigenaar Hallo Hallo Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b10bc-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="b10bc-120">Hallo GUID is Hallo abonnements-ID (geen Hallo instrumentatiesleutel van de toepassing hello).</span><span class="sxs-lookup"><span data-stu-id="b10bc-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="b10bc-121">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="b10bc-121">Example 2</span></span>
<span data-ttu-id="b10bc-122">Ik heb een toepassing die ik gebruik [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport een waarde met de naam 'salesPerHour'.</span><span class="sxs-lookup"><span data-stu-id="b10bc-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="b10bc-123">Een e-mail sturen toomy collega's als 'salesPerHour' onder de 100, meer dan 24 uur een gemiddelde waarde komt.</span><span class="sxs-lookup"><span data-stu-id="b10bc-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="b10bc-124">Hallo dezelfde regel kan worden gebruikt voor de metriek Hallo gerapporteerd via Hallo [meting parameter](app-insights-api-custom-events-metrics.md#properties) van bijhouden van een andere aanroep zoals TrackEvent of trackPageView.</span><span class="sxs-lookup"><span data-stu-id="b10bc-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="b10bc-125">De namen van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="b10bc-125">Metric names</span></span>
| <span data-ttu-id="b10bc-126">Metrische naam</span><span class="sxs-lookup"><span data-stu-id="b10bc-126">Metric name</span></span> | <span data-ttu-id="b10bc-127">De schermnaam van het</span><span class="sxs-lookup"><span data-stu-id="b10bc-127">Screen name</span></span> | <span data-ttu-id="b10bc-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b10bc-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="b10bc-129">Browseruitzonderingen</span><span class="sxs-lookup"><span data-stu-id="b10bc-129">Browser exceptions</span></span> |<span data-ttu-id="b10bc-130">Het aantal niet-onderschepte uitzonderingen in de browser Hallo.</span><span class="sxs-lookup"><span data-stu-id="b10bc-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="b10bc-131">Serveruitzonderingen</span><span class="sxs-lookup"><span data-stu-id="b10bc-131">Server exceptions</span></span> |<span data-ttu-id="b10bc-132">Aantal niet-verwerkte uitzonderingen door Hallo-app</span><span class="sxs-lookup"><span data-stu-id="b10bc-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="b10bc-133">Verwerkingstijd van de client</span><span class="sxs-lookup"><span data-stu-id="b10bc-133">Client processing time</span></span> |<span data-ttu-id="b10bc-134">Tijd tussen ontvangst Hallo laatste byte van een document totdat Hallo DOM wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="b10bc-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="b10bc-135">Asynchrone aanvragen kunnen nog worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b10bc-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="b10bc-136">Paginalaadtijd netwerk verbinding maken</span><span class="sxs-lookup"><span data-stu-id="b10bc-136">Page load network connect time</span></span> |<span data-ttu-id="b10bc-137">Tijd Hallo browser duurt tooconnect toohello netwerk.</span><span class="sxs-lookup"><span data-stu-id="b10bc-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="b10bc-138">Kan niet 0 zijn als in de cache.</span><span class="sxs-lookup"><span data-stu-id="b10bc-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="b10bc-139">Ontvangende reactietijd</span><span class="sxs-lookup"><span data-stu-id="b10bc-139">Receiving response time</span></span> |<span data-ttu-id="b10bc-140">Tijd tussen de browser aanvraag toostarting tooreceive reactie wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="b10bc-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="b10bc-141">Aanvraagtijd verzenden</span><span class="sxs-lookup"><span data-stu-id="b10bc-141">Send request time</span></span> |<span data-ttu-id="b10bc-142">De tijd die een aanvraag toosend browser.</span><span class="sxs-lookup"><span data-stu-id="b10bc-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="b10bc-143">Laadtijd van browserpagina</span><span class="sxs-lookup"><span data-stu-id="b10bc-143">Browser page load time</span></span> |<span data-ttu-id="b10bc-144">Tijd vanaf gebruikersaanvraag totdat DOM, opmaakmodellen, scripts en afbeeldingen zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="b10bc-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="b10bc-145">Beschikbaar geheugen</span><span class="sxs-lookup"><span data-stu-id="b10bc-145">Available memory</span></span> |<span data-ttu-id="b10bc-146">Fysiek geheugen die direct beschikbaar is voor een proces of voor systeemgebruik.</span><span class="sxs-lookup"><span data-stu-id="b10bc-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="b10bc-147">Verwerkingssnelheid van i/o</span><span class="sxs-lookup"><span data-stu-id="b10bc-147">Process IO Rate</span></span> |<span data-ttu-id="b10bc-148">Totaal aantal bytes per tweede gelezen en geschreven toofiles, netwerk en apparaten.</span><span class="sxs-lookup"><span data-stu-id="b10bc-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="b10bc-149">snelheid van de uitzondering</span><span class="sxs-lookup"><span data-stu-id="b10bc-149">exception rate</span></span> |<span data-ttu-id="b10bc-150">Uitzonderingen per seconde.</span><span class="sxs-lookup"><span data-stu-id="b10bc-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="b10bc-151">Proces CPU</span><span class="sxs-lookup"><span data-stu-id="b10bc-151">Process CPU</span></span> |<span data-ttu-id="b10bc-152">Hallo percentage verstreken tijd van alle procesthreads die worden gebruikt door Hallo processor tooexecution instructies voor het toepassingsproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="b10bc-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="b10bc-153">Tijd van processor</span><span class="sxs-lookup"><span data-stu-id="b10bc-153">Processor time</span></span> |<span data-ttu-id="b10bc-154">Hallo percentage tijd dat de processor Hallo doorbrengt in niet-inactieve threads.</span><span class="sxs-lookup"><span data-stu-id="b10bc-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="b10bc-155">Eigen bytes van proces</span><span class="sxs-lookup"><span data-stu-id="b10bc-155">Process private bytes</span></span> |<span data-ttu-id="b10bc-156">Geheugen exclusief toegewezen toohello bewaakt processen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b10bc-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="b10bc-157">Uitvoeringstijd voor ASP.NET-aanvraag</span><span class="sxs-lookup"><span data-stu-id="b10bc-157">ASP.NET request execution time</span></span> |<span data-ttu-id="b10bc-158">Uitvoeringstijd van de meest recente aanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="b10bc-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="b10bc-159">ASP.NET-aanvragen in wachtrij voor uitvoering</span><span class="sxs-lookup"><span data-stu-id="b10bc-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="b10bc-160">Lengte van de wachtrij voor toepassingsaanvragen en Hallo.</span><span class="sxs-lookup"><span data-stu-id="b10bc-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="b10bc-161">Snelheid van aanvragen voor ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b10bc-161">ASP.NET request rate</span></span> |<span data-ttu-id="b10bc-162">De snelheid van alle aanvragen toohello toepassing per seconde van ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b10bc-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="b10bc-163">Afhankelijkheid fouten</span><span class="sxs-lookup"><span data-stu-id="b10bc-163">Dependency failures</span></span> |<span data-ttu-id="b10bc-164">Het aantal mislukte aanroepen van de toepassing hello-tooexternal serverbronnen.</span><span class="sxs-lookup"><span data-stu-id="b10bc-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="b10bc-165">Serverreactietijd</span><span class="sxs-lookup"><span data-stu-id="b10bc-165">Server response time</span></span> |<span data-ttu-id="b10bc-166">Tijd tussen ontvangst van een HTTP-aanvraag en antwoord Hallo verzenden is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b10bc-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="b10bc-167">Snelheid van aanvragen voor</span><span class="sxs-lookup"><span data-stu-id="b10bc-167">Request rate</span></span> |<span data-ttu-id="b10bc-168">De snelheid van alle aanvragen toohello toepassing per seconde.</span><span class="sxs-lookup"><span data-stu-id="b10bc-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="b10bc-169">Mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="b10bc-169">Failed requests</span></span> |<span data-ttu-id="b10bc-170">Aantal HTTP-aanvragen dat heeft geresulteerd in een responscode > = 400</span><span class="sxs-lookup"><span data-stu-id="b10bc-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="b10bc-171">Paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="b10bc-171">Page views</span></span> |<span data-ttu-id="b10bc-172">Het aantal aanvragen van clientgebruikers voor webpagina's.</span><span class="sxs-lookup"><span data-stu-id="b10bc-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="b10bc-173">Synthetisch verkeer is gefilterd.</span><span class="sxs-lookup"><span data-stu-id="b10bc-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="b10bc-174">{uw aangepaste metrische naam}</span><span class="sxs-lookup"><span data-stu-id="b10bc-174">{your custom metric name}</span></span> |<span data-ttu-id="b10bc-175">{De naam van de meetwaarde}</span><span class="sxs-lookup"><span data-stu-id="b10bc-175">{Your metric name}</span></span> |<span data-ttu-id="b10bc-176">De waarde van de metrische gegevens die zijn gerapporteerd door [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) of in Hallo [metingen parameter van een aanroep van bijhouden](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="b10bc-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="b10bc-177">Hallo metrische gegevens worden verzonden door verschillende telemetrie modules:</span><span class="sxs-lookup"><span data-stu-id="b10bc-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="b10bc-178">Metrische groep</span><span class="sxs-lookup"><span data-stu-id="b10bc-178">Metric group</span></span> | <span data-ttu-id="b10bc-179">Module collector</span><span class="sxs-lookup"><span data-stu-id="b10bc-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="b10bc-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="b10bc-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="b10bc-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="b10bc-181">clientPerformance,</span></span><br/><span data-ttu-id="b10bc-182">weergeven</span><span class="sxs-lookup"><span data-stu-id="b10bc-182">view</span></span> |[<span data-ttu-id="b10bc-183">Browser JavaScript</span><span class="sxs-lookup"><span data-stu-id="b10bc-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="b10bc-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="b10bc-184">performanceCounter</span></span> |[<span data-ttu-id="b10bc-185">Prestaties</span><span class="sxs-lookup"><span data-stu-id="b10bc-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="b10bc-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="b10bc-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="b10bc-187">Afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="b10bc-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="b10bc-188">aanvraag,</span><span class="sxs-lookup"><span data-stu-id="b10bc-188">request,</span></span><br/><span data-ttu-id="b10bc-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="b10bc-189">requestFailed</span></span> |[<span data-ttu-id="b10bc-190">Serveraanvraag</span><span class="sxs-lookup"><span data-stu-id="b10bc-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="b10bc-191">Webhooks.</span><span class="sxs-lookup"><span data-stu-id="b10bc-191">Webhooks</span></span>
<span data-ttu-id="b10bc-192">U kunt [automatiseren uw antwoord tooan waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b10bc-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="b10bc-193">Azure belt een webadres van uw keuze wanneer een waarschuwing wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b10bc-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="b10bc-194">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b10bc-194">See also</span></span>
* [<span data-ttu-id="b10bc-195">Script tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="b10bc-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="b10bc-196">Application Insights en test webbronnen van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="b10bc-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="b10bc-197">Koppeling van Microsoft Azure Diagnostics tooApplication Insights automatiseren</span><span class="sxs-lookup"><span data-stu-id="b10bc-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="b10bc-198">Uw antwoord tooan waarschuwing automatiseren</span><span class="sxs-lookup"><span data-stu-id="b10bc-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
