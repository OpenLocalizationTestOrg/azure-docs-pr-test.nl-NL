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
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Gebeurtenissen voor diagnostische evaluatie en bewaking van Batch-oplossingen

Net als bij veel Azure-services, verzendt Hallo Batch-service voor bepaalde bronnen tijdens de levensduur van Hallo resource Hallo logboekgebeurtenissen. U kunt Azure Batch diagnostische logboeken toorecord gebeurtenissen voor resources zoals pools en taken inschakelen en vervolgens gebruiken Hallo logboeken voor diagnostische evaluatie en bewaking. Gebeurtenissen, zoals toepassingen maken, verwijderen van de groep van toepassingen, taak start, taak voltooid en anderen zijn opgenomen in Batch diagnostische logboeken.

> [!NOTE]
> Dit artikel wordt beschreven logboekgebeurtenissen voor resources van de Batch-account zelf, geen taken en uitvoergegevens van de taak. Zie voor meer informatie over het opslaan van de uitvoergegevens Hallo van uw jobs en taken [behouden Azure Batch-taak en uitvoer](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Vereisten
* [Azure Batch-account](batch-account-create-portal.md)
* [Azure Storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  Diagnostische logboeken toopersist Batch, moet u een Azure Storage-account waarin Azure Hallo logboeken worden opgeslagen. U dit opslagaccount opgeven wanneer u [Diagnostische logboekregistratie inschakelen](#enable-diagnostic-logging) voor uw Batch-account. Hallo Storage account dat u opgeeft wanneer u het inschakelen van logboekverzameling is dezelfde niet Hallo als een gekoppelde storage-account waarnaar wordt verwezen tooin hello [toepassingspakketten](batch-application-packages.md) en [taak uitvoer persistentie](batch-task-output.md) artikelen.
  
  > [!WARNING]
  > U bent **in rekening gebracht** Hallo gegevens worden opgeslagen in uw Azure Storage-account. Dit omvat Hallo diagnostische logboeken die in dit artikel wordt besproken. Houd er rekening mee houden bij het ontwerpen van uw [Meld bewaarbeleid](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Bijhouden van diagnostische gegevens inschakelen
Diagnostische logboekregistratie is niet standaard ingeschakeld voor uw Batch-account. Diagnostische logboekregistratie voor elke gewenste toomonitor Batch-account, moet u expliciet inschakelen:

[Hoe tooenable verzamelen van diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

Aangeraden Hallo volledig te lezen [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artikel toogain een goed begrip van het niet alleen hoe tooenable logboekregistratie, maar Hallo Meld categorieën die worden ondersteund door Hallo verschillende Azure-services. Azure Batch ondersteunt bijvoorbeeld momenteel één logboek categorie: **servicelogboeken**.

## <a name="service-logs"></a>Service-Logboeken
Azure Batch-Service-logboeken bevatten gebeurtenissen die door hello Azure Batch-service tijdens het Hallo-levensduur van een Batch-bron, zoals een groep of de taak. Elke gebeurtenis verzonden door de Batch wordt opgeslagen in de opgegeven Hallo Storage-account in JSON-indeling. Dit is bijvoorbeeld Hallo hoofdtekst van een steekproef **groep maken gebeurtenis**:

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

Hoofdtekst van de gebeurtenis bevindt zich in een .json-bestand in hello Azure Storage-account opgegeven. Als u wilt dat tooaccess Hallo logboeken rechtstreeks, kunt u tooreview hello [schema van diagnostische logboeken in Hallo opslagaccount](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>Service-logboekgebeurtenissen
Hallo Batch-service verzendt momenteel Hallo Service logboekgebeurtenissen te volgen. Deze lijst zijn mogelijk niet volledig, omdat er aanvullende gebeurtenissen zijn toegevoegd sinds dit artikel voor het laatst is bijgewerkt.

| **Service-logboekgebeurtenissen** |
| --- |
| [Groep maken][pool_create] |
| [Toepassingen verwijderen starten][pool_delete_start] |
| [Groep verwijderen is voltooid][pool_delete_complete] |
| [Groep formaat starten][pool_resize_start] |
| [Groep formaat voltooid][pool_resize_complete] |
| [Taak starten][task_start] |
| [De taak is voltooid][task_complete] |
| [Taak is mislukt][task_fail] |

## <a name="next-steps"></a>Volgende stappen
In de toevoeging toostoring diagnostische gebeurtenissen in een Azure Storage-account, kunt u ook logboek van de Batch-Service gebeurtenissen tooan streamen [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), en ze te verzenden[Azure Log Analytics](../log-analytics/log-analytics-overview.md).

* [Diagnostische logboeken van Azure tooEvent Hubs Stream](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Stream Batch diagnostische gebeurtenissen toohello zeer schaalbare service voor inkomende gegevens, Event Hubs. Event Hubs kunnen miljoenen gebeurtenissen per seconde die u kunt vervolgens transformeren en opslaan met behulp van een realtime-analyseprovider opnemen.
* [Azure diagnostische logboeken met logboekanalyse analyseren](../log-analytics/log-analytics-azure-storage.md)
  
  Uw diagnoselogboeken tooLog Analytics kunt u ze in Hallo Operations Management Suite (OMS)-portal te analyseren, of ze te exporteren voor analyse in Power BI of Excel verzenden.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
