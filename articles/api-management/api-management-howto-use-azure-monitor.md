---
title: API Management bewaken met Azure Monitor | Microsoft Docs
description: Informatie over het bewaken van Azure API Management-service met behulp van Azure-Monitor.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="43d59-103">Monitor voor API Management met Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="43d59-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="43d59-104">Monitor voor Azure is een Azure-service met één bron voor de bewaking van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="43d59-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="43d59-105">Met Azure-Monitor kunt u visualiseren, query, routeren, archiveren en acties uitvoeren op de metrische gegevens en de logboeken die afkomstig zijn van de Azure-bronnen zoals API Management.</span><span class="sxs-lookup"><span data-stu-id="43d59-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="43d59-106">De volgende video toont het bewaken van API Management met behulp van Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="43d59-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="43d59-107">Zie voor meer informatie over Azure Monitor [aan de slag met Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="43d59-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="43d59-108">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="43d59-108">Metrics</span></span>
<span data-ttu-id="43d59-109">API Management momenteel vijf metrische gegevens verzendt en meer in de toekomst toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="43d59-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="43d59-110">Deze metrische gegevens worden gegenereerd per minuut, zodat u bijna real-time inzicht in de status en gezondheid van uw API's.</span><span class="sxs-lookup"><span data-stu-id="43d59-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="43d59-111">Hier volgt een samenvatting van de metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="43d59-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="43d59-112">Totaal aantal verzoeken van de Gateway: het aantal API-aanvragen in de periode.</span><span class="sxs-lookup"><span data-stu-id="43d59-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="43d59-113">Geslaagde aanvragen voor de Gateway: het aantal API-aanvragen dat geslaagde HTTP-antwoordcodes waaronder 304, 307 en iets kleiner is dan 301 (bijvoorbeeld 200) ontvangen.</span><span class="sxs-lookup"><span data-stu-id="43d59-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="43d59-114">Mislukte aanvragen van de Gateway: het aantal API-aanvragen dat foutieve HTTP-antwoordcodes waaronder 400 en iets groter zijn dan 500 ontvangen.</span><span class="sxs-lookup"><span data-stu-id="43d59-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="43d59-115">Niet-geautoriseerde Gateway verzoeken: het aantal API-aanvragen die HTTP-antwoordcodes waaronder 401, 403 en 429 ontvangen.</span><span class="sxs-lookup"><span data-stu-id="43d59-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="43d59-116">Andere Gateway verzoeken: het aantal API-aanvragen die HTTP-antwoordcodes die niet bij een van de voorgaande categorieën (bijvoorbeeld 418 horen) ontvangen.</span><span class="sxs-lookup"><span data-stu-id="43d59-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="43d59-117">U kunt toegang tot metrische gegevens in uw API Management-service of toegang tot metrische gegevens van alle Azure-resources in Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="43d59-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="43d59-118">Metrische gegevens weergeven in uw API Management-service:</span><span class="sxs-lookup"><span data-stu-id="43d59-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="43d59-119">Open de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="43d59-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="43d59-120">Ga naar uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="43d59-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="43d59-121">Klik op **metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="43d59-121">Click **Metrics**.</span></span>

![Blade metrische gegevens][metrics-blade]

<span data-ttu-id="43d59-123">Zie voor meer informatie over het gebruik van metrische gegevens [overzicht van metrische gegevens].</span><span class="sxs-lookup"><span data-stu-id="43d59-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="43d59-124">Activiteitenlogboeken</span><span class="sxs-lookup"><span data-stu-id="43d59-124">Activity Logs</span></span>
<span data-ttu-id="43d59-125">Activiteitenlogboeken bieden inzicht in de bewerkingen die zijn uitgevoerd op uw API Management-services.</span><span class="sxs-lookup"><span data-stu-id="43d59-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="43d59-126">Het was voorheen bekend als 'controlelogboeken' of 'operationele logs'.</span><span class="sxs-lookup"><span data-stu-id="43d59-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="43d59-127">Met activiteitenlogboeken, kunt u bepalen de ' wat, wie, en wanneer ' voor een (PUT, POST, verwijderen schrijfbewerkingen) die op uw API Management-services worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="43d59-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="43d59-128">Activiteitenlogboeken bevatten geen leesbewerkingen (GET) of bewerkingen uitgevoerd in de klassieke Portal van de uitgever of met de oorspronkelijke Management-API's.</span><span class="sxs-lookup"><span data-stu-id="43d59-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="43d59-129">U kunt toegang krijgen tot activiteitenlogboeken in uw API Management-service of toegang tot de logboeken van alle Azure-resources in Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="43d59-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="43d59-130">Registreert activiteit weergeven in uw API Management-service:</span><span class="sxs-lookup"><span data-stu-id="43d59-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="43d59-131">Open de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="43d59-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="43d59-132">Ga naar uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="43d59-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="43d59-133">Klik op **activiteitenlogboek**.</span><span class="sxs-lookup"><span data-stu-id="43d59-133">Click **Activity log**.</span></span>

![Activiteit logboeken blade][activity-logs-blade]

<span data-ttu-id="43d59-135">Zie voor meer informatie over het gebruik van metrische gegevens [overzicht activiteitenlogboeken].</span><span class="sxs-lookup"><span data-stu-id="43d59-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="43d59-136">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="43d59-136">Alerts</span></span>
<span data-ttu-id="43d59-137">U kunt configureren voor het ontvangen van meldingen op basis van de logboeken van metrische gegevens en de activiteit.</span><span class="sxs-lookup"><span data-stu-id="43d59-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="43d59-138">Azure Monitor kunt u de volgende handelingen uit als er wordt een waarschuwing configureren:</span><span class="sxs-lookup"><span data-stu-id="43d59-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="43d59-139">E-mailmelding verzenden</span><span class="sxs-lookup"><span data-stu-id="43d59-139">Send an email notification</span></span>
* <span data-ttu-id="43d59-140">een webhook aanroepen</span><span class="sxs-lookup"><span data-stu-id="43d59-140">Call a webhook</span></span>
* <span data-ttu-id="43d59-141">Een Azure Logic App aanroepen</span><span class="sxs-lookup"><span data-stu-id="43d59-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="43d59-142">U kunt regels voor waarschuwingen configureren in uw API Management-service of in de Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="43d59-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="43d59-143">Ze configureren in API Management:</span><span class="sxs-lookup"><span data-stu-id="43d59-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="43d59-144">Open de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="43d59-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="43d59-145">Ga naar uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="43d59-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="43d59-146">Klik op **waarschuwing regels**.</span><span class="sxs-lookup"><span data-stu-id="43d59-146">Click **Alert rules**.</span></span>

![Regels voor waarschuwingen-blade][alert-rules-blade]

<span data-ttu-id="43d59-148">Zie voor meer informatie over het gebruik van waarschuwingen [overzicht van waarschuwingen].</span><span class="sxs-lookup"><span data-stu-id="43d59-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="43d59-149">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="43d59-149">Diagnostic Logs</span></span>
<span data-ttu-id="43d59-150">Logboeken met diagnostische gegevens bevatten uitgebreide informatie over bewerkingen en fouten die belangrijk zijn voor controle, evenals het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="43d59-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="43d59-151">Diagnostische logboeken verschillen van activiteitenlogboeken.</span><span class="sxs-lookup"><span data-stu-id="43d59-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="43d59-152">Activiteitenlogboeken bieden inzicht in de bewerkingen die zijn uitgevoerd op uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="43d59-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="43d59-153">Diagnostische logboeken bieden inzicht in bewerkingen dat de bron zelf uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="43d59-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="43d59-154">API Management biedt momenteel diagnostische logboeken (batch verwerkt per uur) over de API van afzonderlijke aanvragen met elk item met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="43d59-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="43d59-155">U kunt toegang tot diagnoselogboeken in uw API Management-service of toegang tot de logboeken van alle Azure-resources in Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="43d59-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="43d59-156">Diagnostische logboeken weergeven in uw API Management-service:</span><span class="sxs-lookup"><span data-stu-id="43d59-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="43d59-157">Open de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="43d59-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="43d59-158">Ga naar uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="43d59-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="43d59-159">Klik op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="43d59-159">Click **Diagnostic log**.</span></span>

![Blade met diagnostische logboeken][diagnostic-logs-blade]

<span data-ttu-id="43d59-161">Zie voor meer informatie over het gebruik van metrische gegevens [overzicht van diagnostische logboeken].</span><span class="sxs-lookup"><span data-stu-id="43d59-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="43d59-162">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="43d59-162">Next Step</span></span>

* <span data-ttu-id="43d59-163">[aan de slag met Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="43d59-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="43d59-164">[overzicht van metrische gegevens]</span><span class="sxs-lookup"><span data-stu-id="43d59-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="43d59-165">[overzicht activiteitenlogboeken]</span><span class="sxs-lookup"><span data-stu-id="43d59-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="43d59-166">[overzicht van diagnostische logboeken]</span><span class="sxs-lookup"><span data-stu-id="43d59-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="43d59-167">[overzicht van waarschuwingen]</span><span class="sxs-lookup"><span data-stu-id="43d59-167">[Overview of Alerts]</span></span>

<span data-ttu-id="43d59-168">[aan de slag met Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="43d59-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="43d59-169">[overzicht van metrische gegevens]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="43d59-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="43d59-170">[overzicht activiteitenlogboeken]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="43d59-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="43d59-171">[overzicht van diagnostische logboeken]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="43d59-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="43d59-172">[overzicht van waarschuwingen]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="43d59-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
