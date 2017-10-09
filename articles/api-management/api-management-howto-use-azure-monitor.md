---
title: aaaMonitor API Management met Azure Monitor | Microsoft Docs
description: Meer informatie over hoe toomonitor Azure API Management-service met behulp van Azure-Monitor.
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
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="3003d-103">Monitor voor API Management met Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="3003d-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="3003d-104">Monitor voor Azure is een Azure-service met één bron voor de bewaking van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3003d-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="3003d-105">Met Azure-Monitor kunt u visualiseren, query, routeren, archiveren en acties uitvoeren op Hallo metrische gegevens en afkomstig is van de Azure-bronnen zoals API Management-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="3003d-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="3003d-106">Hallo volgende video toont hoe toomonitor API-beheer met behulp van Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="3003d-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="3003d-107">Zie voor meer informatie over Azure Monitor [aan de slag met Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="3003d-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="3003d-108">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="3003d-108">Metrics</span></span>
<span data-ttu-id="3003d-109">API Management momenteel vijf metrische gegevens verzendt en we zullen tooadd in toekomstige Hallo meer.</span><span class="sxs-lookup"><span data-stu-id="3003d-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="3003d-110">Deze metrische gegevens worden gegenereerd per minuut, zodat u bijna realtime zicht krijgt op Hallo status en gezondheid van uw API's.</span><span class="sxs-lookup"><span data-stu-id="3003d-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="3003d-111">Hier volgt een samenvatting van Hallo metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="3003d-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="3003d-112">Totaal aantal verzoeken van de Gateway: Hallo aantal API-aanvragen in Hallo periode.</span><span class="sxs-lookup"><span data-stu-id="3003d-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="3003d-113">Geslaagde aanvragen voor de Gateway: Hallo aantal API-aanvragen dat geslaagde HTTP-antwoordcodes waaronder 304, 307 en iets kleiner is dan 301 (bijvoorbeeld 200) ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3003d-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="3003d-114">Mislukte aanvragen van de Gateway: Hallo aantal API-aanvragen dat foutieve HTTP-antwoordcodes waaronder 400 en iets groter zijn dan 500 ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3003d-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="3003d-115">Ongeautoriseerde aanvragen van de Gateway: Hallo aantal API-aanvragen die HTTP-antwoordcodes waaronder 401, 403 en 429 ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3003d-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="3003d-116">Andere aanvragen voor de Gateway: Hallo aantal API-aanvragen die HTTP-antwoordcodes die geen deel uitmaken van tooany Hallo voorgaande categorieën (bijvoorbeeld 418) ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3003d-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="3003d-117">U kunt toegang tot metrische gegevens in uw API Management-service of toegang tot metrische gegevens van alle Azure-resources in Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="3003d-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="3003d-118">tooview metrische gegevens in uw API Management-service:</span><span class="sxs-lookup"><span data-stu-id="3003d-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="3003d-119">Open hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3003d-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="3003d-120">Ga tooyour API Management-service.</span><span class="sxs-lookup"><span data-stu-id="3003d-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="3003d-121">Klik op **metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="3003d-121">Click **Metrics**.</span></span>

![Blade metrische gegevens][metrics-blade]

<span data-ttu-id="3003d-123">Voor meer informatie over het toouse metrische gegevens, Zie [overzicht van metrische gegevens].</span><span class="sxs-lookup"><span data-stu-id="3003d-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="3003d-124">Activiteitenlogboeken</span><span class="sxs-lookup"><span data-stu-id="3003d-124">Activity Logs</span></span>
<span data-ttu-id="3003d-125">Activiteitenlogboeken bieden inzicht in Hallo-bewerkingen die zijn uitgevoerd op uw API Management-services.</span><span class="sxs-lookup"><span data-stu-id="3003d-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="3003d-126">Het was voorheen bekend als 'controlelogboeken' of 'operationele logs'.</span><span class="sxs-lookup"><span data-stu-id="3003d-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="3003d-127">Met activiteitenlogboeken, kunt u Hallo bepalen ' wat, wie, en wanneer ' voor een (PUT, POST, verwijderen schrijfbewerkingen) die op uw API Management-services worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3003d-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="3003d-128">Activiteitenlogboeken bevatten geen leesbewerkingen (GET) of bewerkingen die worden uitgevoerd klassieke Publicatieportal Hallo of met behulp van Hallo oorspronkelijke Management-API's.</span><span class="sxs-lookup"><span data-stu-id="3003d-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="3003d-129">U kunt toegang krijgen tot activiteitenlogboeken in uw API Management-service of toegang tot de logboeken van alle Azure-resources in Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="3003d-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="3003d-130">tooview activiteit geregistreerd in uw API Management-service:</span><span class="sxs-lookup"><span data-stu-id="3003d-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="3003d-131">Open hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3003d-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="3003d-132">Ga tooyour API Management-service.</span><span class="sxs-lookup"><span data-stu-id="3003d-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="3003d-133">Klik op **activiteitenlogboek**.</span><span class="sxs-lookup"><span data-stu-id="3003d-133">Click **Activity log**.</span></span>

![Activiteit logboeken blade][activity-logs-blade]

<span data-ttu-id="3003d-135">Voor meer informatie over het toouse metrische gegevens, Zie [overzicht activiteitenlogboeken].</span><span class="sxs-lookup"><span data-stu-id="3003d-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="3003d-136">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="3003d-136">Alerts</span></span>
<span data-ttu-id="3003d-137">U kunt tooreceive waarschuwingen op basis van de logboeken van metrische gegevens en activiteit kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="3003d-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="3003d-138">Azure Monitor kunt u een waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="3003d-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="3003d-139">E-mailmelding verzenden</span><span class="sxs-lookup"><span data-stu-id="3003d-139">Send an email notification</span></span>
* <span data-ttu-id="3003d-140">een webhook aanroepen</span><span class="sxs-lookup"><span data-stu-id="3003d-140">Call a webhook</span></span>
* <span data-ttu-id="3003d-141">Een Azure Logic App aanroepen</span><span class="sxs-lookup"><span data-stu-id="3003d-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="3003d-142">U kunt regels voor waarschuwingen configureren in uw API Management-service of in de Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="3003d-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="3003d-143">tooconfigure ze in API Management:</span><span class="sxs-lookup"><span data-stu-id="3003d-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="3003d-144">Open hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3003d-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="3003d-145">Ga tooyour API Management-service.</span><span class="sxs-lookup"><span data-stu-id="3003d-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="3003d-146">Klik op **waarschuwing regels**.</span><span class="sxs-lookup"><span data-stu-id="3003d-146">Click **Alert rules**.</span></span>

![Regels voor waarschuwingen-blade][alert-rules-blade]

<span data-ttu-id="3003d-148">Zie voor meer informatie over het gebruik van waarschuwingen [overzicht van waarschuwingen].</span><span class="sxs-lookup"><span data-stu-id="3003d-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="3003d-149">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="3003d-149">Diagnostic Logs</span></span>
<span data-ttu-id="3003d-150">Logboeken met diagnostische gegevens bevatten uitgebreide informatie over bewerkingen en fouten die belangrijk zijn voor controle, evenals het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="3003d-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="3003d-151">Diagnostische logboeken verschillen van activiteitenlogboeken.</span><span class="sxs-lookup"><span data-stu-id="3003d-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="3003d-152">Activiteitenlogboeken bieden inzicht in het Hallo-bewerkingen die zijn uitgevoerd op uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3003d-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="3003d-153">Diagnostische logboeken bieden inzicht in bewerkingen dat de bron zelf uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3003d-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="3003d-154">API Management biedt momenteel diagnostische logboeken (batch verwerkt per uur) over de API van afzonderlijke aanvragen met elke vermelding met Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="3003d-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

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

<span data-ttu-id="3003d-155">U kunt toegang tot diagnoselogboeken in uw API Management-service of toegang tot de logboeken van alle Azure-resources in Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="3003d-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="3003d-156">tooview diagnostische logboeken in uw API Management-service:</span><span class="sxs-lookup"><span data-stu-id="3003d-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="3003d-157">Open hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3003d-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="3003d-158">Ga tooyour API Management-service.</span><span class="sxs-lookup"><span data-stu-id="3003d-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="3003d-159">Klik op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="3003d-159">Click **Diagnostic log**.</span></span>

![Blade met diagnostische logboeken][diagnostic-logs-blade]

<span data-ttu-id="3003d-161">Voor meer informatie over het toouse metrische gegevens, Zie [overzicht van diagnostische logboeken].</span><span class="sxs-lookup"><span data-stu-id="3003d-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="3003d-162">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="3003d-162">Next Step</span></span>

* <span data-ttu-id="3003d-163">[aan de slag met Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="3003d-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="3003d-164">[overzicht van metrische gegevens]</span><span class="sxs-lookup"><span data-stu-id="3003d-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="3003d-165">[overzicht activiteitenlogboeken]</span><span class="sxs-lookup"><span data-stu-id="3003d-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="3003d-166">[overzicht van diagnostische logboeken]</span><span class="sxs-lookup"><span data-stu-id="3003d-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="3003d-167">[overzicht van waarschuwingen]</span><span class="sxs-lookup"><span data-stu-id="3003d-167">[Overview of Alerts]</span></span>

[aan de slag met Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[overzicht van metrische gegevens]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[overzicht activiteitenlogboeken]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[overzicht van diagnostische logboeken]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[overzicht van waarschuwingen]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
