---
title: Diagnostische logboeken van aaaAzure Service Bus | Microsoft Docs
description: Meer informatie over hoe tooset van diagnostische logboeken voor Service Bus in Azure.
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="beb86-103">Diagnostische logboeken van Service Bus</span><span class="sxs-lookup"><span data-stu-id="beb86-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="beb86-104">U kunt twee soorten logboeken bekijken voor Azure Service Bus:</span><span class="sxs-lookup"><span data-stu-id="beb86-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="beb86-105">**[Activiteitenlogboeken](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="beb86-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="beb86-106">Deze logboeken bevatten informatie over de bewerkingen die worden uitgevoerd op een andere taak.</span><span class="sxs-lookup"><span data-stu-id="beb86-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="beb86-107">Hallo logboeken zijn altijd ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="beb86-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="beb86-108">**[Diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="beb86-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="beb86-109">U kunt diagnostische logboeken voor uitgebreidere informatie over alles wat er in een job gebeurt kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="beb86-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="beb86-110">Diagnostische logboeken behandeld activiteiten van Hallo tijd Hallo-taak is gemaakt totdat het Hallo-taak is verwijderd, inclusief updates en activiteiten die zich tijdens het Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="beb86-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="beb86-111">Logboeken met diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="beb86-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="beb86-112">Diagnostische logboeken zijn standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="beb86-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="beb86-113">Diagnostische logboeken tooenable, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="beb86-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="beb86-114">In Hallo [Azure-portal](https://portal.azure.com)onder **bewaking + Management**, klikt u op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="beb86-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Blade navigatie toodiagnostic Logboeken](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="beb86-116">Klik op de gewenste toomonitor Hallo-bron.</span><span class="sxs-lookup"><span data-stu-id="beb86-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="beb86-117">Klik op **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="beb86-117">Click **Turn on diagnostics**.</span></span>

    ![Logboeken met diagnostische gegevens inschakelen](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="beb86-119">Voor **Status**, klikt u op **op**.</span><span class="sxs-lookup"><span data-stu-id="beb86-119">For **Status**, click **On**.</span></span>

    ![Diagnostische logboeken status wijzigen](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="beb86-121">Set Hallo archief doel dat u wilt. bijvoorbeeld, een opslagaccount, een Event Hub of Azure-logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="beb86-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="beb86-122">Hallo nieuwe diagnostische instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="beb86-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="beb86-123">Nieuwe instellingen van kracht in ongeveer 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="beb86-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="beb86-124">Daarna logboeken worden weergegeven in de archivering doel Hallo geconfigureerd op Hallo **diagnostische logboeken** blade.</span><span class="sxs-lookup"><span data-stu-id="beb86-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="beb86-125">Zie voor meer informatie over het configureren van diagnostische gegevens Hallo [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="beb86-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="beb86-126">Diagnostische logboeken schema</span><span class="sxs-lookup"><span data-stu-id="beb86-126">Diagnostic logs schema</span></span>

<span data-ttu-id="beb86-127">Alle logboeken worden opgeslagen in de notatie JSON (JavaScript Object)-indeling.</span><span class="sxs-lookup"><span data-stu-id="beb86-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="beb86-128">Elk item heeft tekenreeksvelden die wordt beschreven in de volgende sectie Hallo Hallo-indeling gebruiken.</span><span class="sxs-lookup"><span data-stu-id="beb86-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="beb86-129">Operationele logboeken schema</span><span class="sxs-lookup"><span data-stu-id="beb86-129">Operational logs schema</span></span>

<span data-ttu-id="beb86-130">Hallo zich aanmeldt **OperationalLogs** categorie leggen wat er gebeurt tijdens de Service Bus-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="beb86-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="beb86-131">In het bijzonder deze logboeken Hallo bewerkingstype, inclusief maken van de wachtrij, resources die worden gebruikt, vastleggen en status van de bewerking Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="beb86-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="beb86-132">Operationeel logboek van JSON tekenreeksen bevatten die worden vermeld in de volgende tabel Hallo elementen:</span><span class="sxs-lookup"><span data-stu-id="beb86-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="beb86-133">Naam</span><span class="sxs-lookup"><span data-stu-id="beb86-133">Name</span></span> | <span data-ttu-id="beb86-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="beb86-134">Description</span></span>
------- | -------
<span data-ttu-id="beb86-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="beb86-135">ActivityId</span></span> | <span data-ttu-id="beb86-136">Interne ID, die wordt gebruikt voor bijhouden</span><span class="sxs-lookup"><span data-stu-id="beb86-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="beb86-137">EventName</span><span class="sxs-lookup"><span data-stu-id="beb86-137">EventName</span></span> | <span data-ttu-id="beb86-138">De naam van bewerking</span><span class="sxs-lookup"><span data-stu-id="beb86-138">Operation name</span></span>           
<span data-ttu-id="beb86-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="beb86-139">resourceId</span></span> | <span data-ttu-id="beb86-140">Azure Resource Manager-bron-ID</span><span class="sxs-lookup"><span data-stu-id="beb86-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="beb86-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="beb86-141">SubscriptionId</span></span> | <span data-ttu-id="beb86-142">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="beb86-142">Subscription ID</span></span>
<span data-ttu-id="beb86-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="beb86-143">EventTimeString</span></span> | <span data-ttu-id="beb86-144">Bewerkingstijd</span><span class="sxs-lookup"><span data-stu-id="beb86-144">Operation time</span></span>
<span data-ttu-id="beb86-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="beb86-145">EventProperties</span></span> | <span data-ttu-id="beb86-146">Eigenschappen van bewerking</span><span class="sxs-lookup"><span data-stu-id="beb86-146">Operation properties</span></span>
<span data-ttu-id="beb86-147">Status</span><span class="sxs-lookup"><span data-stu-id="beb86-147">Status</span></span> | <span data-ttu-id="beb86-148">De bewerkingsstatus</span><span class="sxs-lookup"><span data-stu-id="beb86-148">Operation status</span></span>
<span data-ttu-id="beb86-149">Caller</span><span class="sxs-lookup"><span data-stu-id="beb86-149">Caller</span></span> | <span data-ttu-id="beb86-150">De aanroeper van bewerking (Azure portal of management-client)</span><span class="sxs-lookup"><span data-stu-id="beb86-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="beb86-151">category</span><span class="sxs-lookup"><span data-stu-id="beb86-151">category</span></span> | <span data-ttu-id="beb86-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="beb86-152">OperationalLogs</span></span>

<span data-ttu-id="beb86-153">Hier volgt een voorbeeld van een operationeel logboek van JSON-tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="beb86-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="beb86-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="beb86-154">Next steps</span></span>

<span data-ttu-id="beb86-155">Ga naar Hallo koppelingen toolearn meer over Service Bus te volgen:</span><span class="sxs-lookup"><span data-stu-id="beb86-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="beb86-156">Inleiding tooService Bus</span><span class="sxs-lookup"><span data-stu-id="beb86-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="beb86-157">Aan de slag met Service Bus</span><span class="sxs-lookup"><span data-stu-id="beb86-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
