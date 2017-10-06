---
title: Diagnostische logboeken van aaaAzure Event Hubs | Microsoft Docs
description: Meer informatie over hoe tooset van diagnostische logboeken voor event hubs in Azure.
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="63bef-103">Diagnostische logboeken van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="63bef-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="63bef-104">U kunt twee soorten logboeken voor Azure Event Hubs bekijken:</span><span class="sxs-lookup"><span data-stu-id="63bef-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="63bef-105">**[Activiteitenlogboeken](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="63bef-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="63bef-106">Deze logboeken bevat gegevens over de bewerkingen die worden uitgevoerd op een andere taak.</span><span class="sxs-lookup"><span data-stu-id="63bef-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="63bef-107">Hallo logboeken zijn altijd ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="63bef-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="63bef-108">**[Diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="63bef-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="63bef-109">U kunt diagnostische logboeken voor een uitgebreidere weergave van alles wat er gebeurt met een taak configureren.</span><span class="sxs-lookup"><span data-stu-id="63bef-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="63bef-110">Diagnostische logboeken behandeld activiteiten van Hallo tijd Hallo-taak is gemaakt totdat het Hallo-taak is verwijderd, inclusief updates en activiteiten die zich tijdens het Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="63bef-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="63bef-111">Logboeken met diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="63bef-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="63bef-112">Diagnostische logboeken zijn standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="63bef-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="63bef-113">Diagnostische logboeken tooenable:</span><span class="sxs-lookup"><span data-stu-id="63bef-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="63bef-114">In Hallo [Azure-portal](https://portal.azure.com)onder **bewaking + Management**, klikt u op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="63bef-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Blade navigatie toodiagnostic Logboeken](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="63bef-116">Klik op de gewenste toomonitor Hallo-bron.</span><span class="sxs-lookup"><span data-stu-id="63bef-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="63bef-117">Klik op **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="63bef-117">Click **Turn on diagnostics**.</span></span>

    ![Logboeken met diagnostische gegevens inschakelen](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="63bef-119">Voor **Status**, klikt u op **op**.</span><span class="sxs-lookup"><span data-stu-id="63bef-119">For **Status**, click **On**.</span></span>

    ![Hallo-status van diagnostische logboeken wijzigen](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="63bef-121">Set Hallo archief doel dat u wilt. bijvoorbeeld, een opslagaccount, een event hub of Azure-logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="63bef-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="63bef-122">Hallo nieuwe diagnostische instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="63bef-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="63bef-123">Nieuwe instellingen van kracht in ongeveer 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="63bef-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="63bef-124">Daarna logboeken worden weergegeven in de archivering doel Hallo geconfigureerd op Hallo **diagnostische logboeken** blade.</span><span class="sxs-lookup"><span data-stu-id="63bef-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="63bef-125">Zie voor meer informatie over het configureren van diagnostische gegevens Hallo [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="63bef-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="63bef-126">Diagnostische logboeken categorieën</span><span class="sxs-lookup"><span data-stu-id="63bef-126">Diagnostic logs categories</span></span>
<span data-ttu-id="63bef-127">Event Hubs worden vastgelegd diagnostische logboeken voor twee categorieën:</span><span class="sxs-lookup"><span data-stu-id="63bef-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="63bef-128">**ArchiveLogs**: Logboeken gerelateerde tooEvent Hubs archieven, in het bijzonder tooarchive gerelateerde fouten registreert.</span><span class="sxs-lookup"><span data-stu-id="63bef-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="63bef-129">**OperationalLogs**: informatie over wat er gebeurt tijdens Event Hubs-bewerkingen in het bijzonder Hallo bewerkingstype, met inbegrip van de event hub is gemaakt, resources die worden gebruikt, en status van de bewerking Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="63bef-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="63bef-130">Diagnostische logboeken schema</span><span class="sxs-lookup"><span data-stu-id="63bef-130">Diagnostic logs schema</span></span>
<span data-ttu-id="63bef-131">Alle logboeken worden opgeslagen in de notatie JSON (JavaScript Object)-indeling.</span><span class="sxs-lookup"><span data-stu-id="63bef-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="63bef-132">Elk item heeft tekenreeksvelden die gebruikmaken van Hallo-indeling die wordt beschreven in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="63bef-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="63bef-133">Archief logboeken schema</span><span class="sxs-lookup"><span data-stu-id="63bef-133">Archive logs schema</span></span>

<span data-ttu-id="63bef-134">Archief logboek JSON tekenreeksen bevatten die worden vermeld in de volgende tabel Hallo elementen:</span><span class="sxs-lookup"><span data-stu-id="63bef-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="63bef-135">Naam</span><span class="sxs-lookup"><span data-stu-id="63bef-135">Name</span></span> | <span data-ttu-id="63bef-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63bef-136">Description</span></span>
------- | -------
<span data-ttu-id="63bef-137">Taaknaam</span><span class="sxs-lookup"><span data-stu-id="63bef-137">TaskName</span></span> | <span data-ttu-id="63bef-138">Beschrijving van het Hallo-taak die is mislukt.</span><span class="sxs-lookup"><span data-stu-id="63bef-138">Description of hello task that failed.</span></span>
<span data-ttu-id="63bef-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="63bef-139">ActivityId</span></span> | <span data-ttu-id="63bef-140">Interne ID gebruikt om te worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="63bef-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="63bef-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="63bef-141">trackingId</span></span> | <span data-ttu-id="63bef-142">Interne ID gebruikt om te worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="63bef-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="63bef-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="63bef-143">resourceId</span></span> | <span data-ttu-id="63bef-144">Azure Resource Manager resource-ID.</span><span class="sxs-lookup"><span data-stu-id="63bef-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="63bef-145">EventHub</span><span class="sxs-lookup"><span data-stu-id="63bef-145">eventHub</span></span> | <span data-ttu-id="63bef-146">Event hub volledige naam (inclusief naamruimtenaam).</span><span class="sxs-lookup"><span data-stu-id="63bef-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="63bef-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="63bef-147">partitionId</span></span> | <span data-ttu-id="63bef-148">Event Hub-partitie wordt geschreven.</span><span class="sxs-lookup"><span data-stu-id="63bef-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="63bef-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="63bef-149">archiveStep</span></span> | <span data-ttu-id="63bef-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="63bef-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="63bef-151">startTime</span><span class="sxs-lookup"><span data-stu-id="63bef-151">startTime</span></span> | <span data-ttu-id="63bef-152">De begintijd is mislukt.</span><span class="sxs-lookup"><span data-stu-id="63bef-152">Failure start time.</span></span>
<span data-ttu-id="63bef-153">fouten</span><span class="sxs-lookup"><span data-stu-id="63bef-153">failures</span></span> | <span data-ttu-id="63bef-154">Aantal keren is een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="63bef-154">Number of times failure occurred.</span></span>
<span data-ttu-id="63bef-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="63bef-155">durationInSeconds</span></span> | <span data-ttu-id="63bef-156">De duur van de fout.</span><span class="sxs-lookup"><span data-stu-id="63bef-156">Duration of failure.</span></span>
<span data-ttu-id="63bef-157">Bericht</span><span class="sxs-lookup"><span data-stu-id="63bef-157">message</span></span> | <span data-ttu-id="63bef-158">Foutbericht.</span><span class="sxs-lookup"><span data-stu-id="63bef-158">Error message.</span></span>
<span data-ttu-id="63bef-159">category</span><span class="sxs-lookup"><span data-stu-id="63bef-159">category</span></span> | <span data-ttu-id="63bef-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="63bef-160">ArchiveLogs</span></span>

<span data-ttu-id="63bef-161">Hallo is volgende code een voorbeeld van een logboek archiveren JSON-tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="63bef-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="63bef-162">Operationele logboeken schema</span><span class="sxs-lookup"><span data-stu-id="63bef-162">Operational logs schema</span></span>

<span data-ttu-id="63bef-163">Operationeel logboek van JSON tekenreeksen bevatten die worden vermeld in de volgende tabel Hallo elementen:</span><span class="sxs-lookup"><span data-stu-id="63bef-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="63bef-164">Naam</span><span class="sxs-lookup"><span data-stu-id="63bef-164">Name</span></span> | <span data-ttu-id="63bef-165">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63bef-165">Description</span></span>
------- | -------
<span data-ttu-id="63bef-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="63bef-166">ActivityId</span></span> | <span data-ttu-id="63bef-167">Interne ID tootrack doel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63bef-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="63bef-168">EventName</span><span class="sxs-lookup"><span data-stu-id="63bef-168">EventName</span></span> | <span data-ttu-id="63bef-169">Naam van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="63bef-169">Operation name.</span></span>  
<span data-ttu-id="63bef-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="63bef-170">resourceId</span></span> | <span data-ttu-id="63bef-171">Azure Resource Manager resource-ID.</span><span class="sxs-lookup"><span data-stu-id="63bef-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="63bef-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="63bef-172">SubscriptionId</span></span> | <span data-ttu-id="63bef-173">Abonnements-ID.</span><span class="sxs-lookup"><span data-stu-id="63bef-173">Subscription ID.</span></span>
<span data-ttu-id="63bef-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="63bef-174">EventTimeString</span></span> | <span data-ttu-id="63bef-175">Bewerkingstijd.</span><span class="sxs-lookup"><span data-stu-id="63bef-175">Operation time.</span></span>
<span data-ttu-id="63bef-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="63bef-176">EventProperties</span></span> | <span data-ttu-id="63bef-177">Eigenschappen van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="63bef-177">Operation properties.</span></span>
<span data-ttu-id="63bef-178">Status</span><span class="sxs-lookup"><span data-stu-id="63bef-178">Status</span></span> | <span data-ttu-id="63bef-179">Status van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="63bef-179">Operation status.</span></span>
<span data-ttu-id="63bef-180">Caller</span><span class="sxs-lookup"><span data-stu-id="63bef-180">Caller</span></span> | <span data-ttu-id="63bef-181">De aanroeper van bewerking (Azure portal of management-client).</span><span class="sxs-lookup"><span data-stu-id="63bef-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="63bef-182">category</span><span class="sxs-lookup"><span data-stu-id="63bef-182">category</span></span> | <span data-ttu-id="63bef-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="63bef-183">OperationalLogs</span></span>

<span data-ttu-id="63bef-184">Hallo is volgende code een voorbeeld van een operationeel logboek van JSON-tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="63bef-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="63bef-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63bef-185">Next steps</span></span>
* [<span data-ttu-id="63bef-186">Inleiding tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="63bef-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="63bef-187">Event Hubs-API-overzicht</span><span class="sxs-lookup"><span data-stu-id="63bef-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="63bef-188">Aan de slag met Event Hubs</span><span class="sxs-lookup"><span data-stu-id="63bef-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
