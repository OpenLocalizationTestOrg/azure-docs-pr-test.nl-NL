---
title: Diagnostische logboekregistratie voor gebeurtenissen van de Batch - Azure aaaEnable | Microsoft Docs
description: Registreren en analyseren van diagnostische gebeurtenissen voor Azure Batch-account resources zoals pools en taken.
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="7f329-103">Gebeurtenissen voor diagnostische evaluatie en bewaking van Batch-oplossingen</span><span class="sxs-lookup"><span data-stu-id="7f329-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="7f329-104">Net als bij veel Azure-services, verzendt Hallo Batch-service voor bepaalde bronnen tijdens de levensduur van Hallo resource Hallo logboekgebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="7f329-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="7f329-105">U kunt Azure Batch diagnostische logboeken toorecord gebeurtenissen voor resources zoals pools en taken inschakelen en vervolgens gebruiken Hallo logboeken voor diagnostische evaluatie en bewaking.</span><span class="sxs-lookup"><span data-stu-id="7f329-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="7f329-106">Gebeurtenissen, zoals toepassingen maken, verwijderen van de groep van toepassingen, taak start, taak voltooid en anderen zijn opgenomen in Batch diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="7f329-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="7f329-107">Dit artikel wordt beschreven logboekgebeurtenissen voor resources van de Batch-account zelf, geen taken en uitvoergegevens van de taak.</span><span class="sxs-lookup"><span data-stu-id="7f329-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="7f329-108">Zie voor meer informatie over het opslaan van de uitvoergegevens Hallo van uw jobs en taken [behouden Azure Batch-taak en uitvoer](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="7f329-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7f329-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7f329-109">Prerequisites</span></span>
* [<span data-ttu-id="7f329-110">Azure Batch-account</span><span class="sxs-lookup"><span data-stu-id="7f329-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="7f329-111">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="7f329-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="7f329-112">Diagnostische logboeken toopersist Batch, moet u een Azure Storage-account waarin Azure Hallo logboeken worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7f329-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="7f329-113">U dit opslagaccount opgeven wanneer u [Diagnostische logboekregistratie inschakelen](#enable-diagnostic-logging) voor uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="7f329-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="7f329-114">Hallo Storage account dat u opgeeft wanneer u het inschakelen van logboekverzameling is dezelfde niet Hallo als een gekoppelde storage-account waarnaar wordt verwezen tooin hello [toepassingspakketten](batch-application-packages.md) en [taak uitvoer persistentie](batch-task-output.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="7f329-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="7f329-115">U bent **in rekening gebracht** Hallo gegevens worden opgeslagen in uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="7f329-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="7f329-116">Dit omvat Hallo diagnostische logboeken die in dit artikel wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="7f329-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="7f329-117">Houd er rekening mee houden bij het ontwerpen van uw [Meld bewaarbeleid](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7f329-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="7f329-118">Bijhouden van diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="7f329-118">Enable diagnostic logging</span></span>
<span data-ttu-id="7f329-119">Diagnostische logboekregistratie is niet standaard ingeschakeld voor uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="7f329-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="7f329-120">Diagnostische logboekregistratie voor elke gewenste toomonitor Batch-account, moet u expliciet inschakelen:</span><span class="sxs-lookup"><span data-stu-id="7f329-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="7f329-121">Hoe tooenable verzamelen van diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="7f329-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="7f329-122">Aangeraden Hallo volledig te lezen [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artikel toogain een goed begrip van het niet alleen hoe tooenable logboekregistratie, maar Hallo Meld categorieën die worden ondersteund door Hallo verschillende Azure-services.</span><span class="sxs-lookup"><span data-stu-id="7f329-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="7f329-123">Azure Batch ondersteunt bijvoorbeeld momenteel één logboek categorie: **servicelogboeken**.</span><span class="sxs-lookup"><span data-stu-id="7f329-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="7f329-124">Service-Logboeken</span><span class="sxs-lookup"><span data-stu-id="7f329-124">Service Logs</span></span>
<span data-ttu-id="7f329-125">Azure Batch-Service-logboeken bevatten gebeurtenissen die door hello Azure Batch-service tijdens het Hallo-levensduur van een Batch-bron, zoals een groep of de taak.</span><span class="sxs-lookup"><span data-stu-id="7f329-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="7f329-126">Elke gebeurtenis verzonden door de Batch wordt opgeslagen in de opgegeven Hallo Storage-account in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="7f329-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="7f329-127">Dit is bijvoorbeeld Hallo hoofdtekst van een steekproef **groep maken gebeurtenis**:</span><span class="sxs-lookup"><span data-stu-id="7f329-127">For example, this is hello body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="7f329-128">Hoofdtekst van de gebeurtenis bevindt zich in een .json-bestand in hello Azure Storage-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7f329-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="7f329-129">Als u wilt dat tooaccess Hallo logboeken rechtstreeks, kunt u tooreview hello [schema van diagnostische logboeken in Hallo opslagaccount](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="7f329-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="7f329-130">Service-logboekgebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="7f329-130">Service Log events</span></span>
<span data-ttu-id="7f329-131">Hallo Batch-service verzendt momenteel Hallo Service logboekgebeurtenissen te volgen.</span><span class="sxs-lookup"><span data-stu-id="7f329-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="7f329-132">Deze lijst zijn mogelijk niet volledig, omdat er aanvullende gebeurtenissen zijn toegevoegd sinds dit artikel voor het laatst is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="7f329-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="7f329-133">**Service-logboekgebeurtenissen**</span><span class="sxs-lookup"><span data-stu-id="7f329-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="7f329-134">[Groep maken][pool_create]</span><span class="sxs-lookup"><span data-stu-id="7f329-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="7f329-135">[Toepassingen verwijderen starten][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="7f329-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="7f329-136">[Groep verwijderen is voltooid][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="7f329-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="7f329-137">[Groep formaat starten][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="7f329-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="7f329-138">[Groep formaat voltooid][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="7f329-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="7f329-139">[Taak starten][task_start]</span><span class="sxs-lookup"><span data-stu-id="7f329-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="7f329-140">[De taak is voltooid][task_complete]</span><span class="sxs-lookup"><span data-stu-id="7f329-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="7f329-141">[Taak is mislukt][task_fail]</span><span class="sxs-lookup"><span data-stu-id="7f329-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7f329-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f329-142">Next steps</span></span>
<span data-ttu-id="7f329-143">In de toevoeging toostoring diagnostische gebeurtenissen in een Azure Storage-account, kunt u ook logboek van de Batch-Service gebeurtenissen tooan streamen [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), en ze te verzenden[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7f329-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="7f329-144">Diagnostische logboeken van Azure tooEvent Hubs Stream</span><span class="sxs-lookup"><span data-stu-id="7f329-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="7f329-145">Stream Batch diagnostische gebeurtenissen toohello zeer schaalbare service voor inkomende gegevens, Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="7f329-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="7f329-146">Event Hubs kunnen miljoenen gebeurtenissen per seconde die u kunt vervolgens transformeren en opslaan met behulp van een realtime-analyseprovider opnemen.</span><span class="sxs-lookup"><span data-stu-id="7f329-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="7f329-147">Azure diagnostische logboeken met logboekanalyse analyseren</span><span class="sxs-lookup"><span data-stu-id="7f329-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="7f329-148">Uw diagnoselogboeken tooLog Analytics kunt u ze in Hallo Operations Management Suite (OMS)-portal te analyseren, of ze te exporteren voor analyse in Power BI of Excel verzenden.</span><span class="sxs-lookup"><span data-stu-id="7f329-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
