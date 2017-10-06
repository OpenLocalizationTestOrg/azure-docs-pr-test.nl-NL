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
# <a name="event-hubs-diagnostic-logs"></a>Diagnostische logboeken van Event Hubs

U kunt twee soorten logboeken voor Azure Event Hubs bekijken:
* **[Activiteitenlogboeken](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Deze logboeken bevat gegevens over de bewerkingen die worden uitgevoerd op een andere taak. Hallo logboeken zijn altijd ingeschakeld.
* **[Diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. U kunt diagnostische logboeken voor een uitgebreidere weergave van alles wat er gebeurt met een taak configureren. Diagnostische logboeken behandeld activiteiten van Hallo tijd Hallo-taak is gemaakt totdat het Hallo-taak is verwijderd, inclusief updates en activiteiten die zich tijdens het Hallo-taak wordt uitgevoerd.

## <a name="turn-on-diagnostic-logs"></a>Logboeken met diagnostische gegevens inschakelen
Diagnostische logboeken zijn standaard uitgeschakeld. Diagnostische logboeken tooenable:

1.  In Hallo [Azure-portal](https://portal.azure.com)onder **bewaking + Management**, klikt u op **diagnostische logboeken**.

    ![Blade navigatie toodiagnostic Logboeken](./media/event-hubs-diagnostic-logs/image1.png)

2.  Klik op de gewenste toomonitor Hallo-bron.

3.  Klik op **diagnostische gegevens inschakelen**.

    ![Logboeken met diagnostische gegevens inschakelen](./media/event-hubs-diagnostic-logs/image2.png)

4.  Voor **Status**, klikt u op **op**.

    ![Hallo-status van diagnostische logboeken wijzigen](./media/event-hubs-diagnostic-logs/image3.png)

5.  Set Hallo archief doel dat u wilt. bijvoorbeeld, een opslagaccount, een event hub of Azure-logboekanalyse.

6.  Hallo nieuwe diagnostische instellingen opslaan.

Nieuwe instellingen van kracht in ongeveer 10 minuten. Daarna logboeken worden weergegeven in de archivering doel Hallo geconfigureerd op Hallo **diagnostische logboeken** blade.

Zie voor meer informatie over het configureren van diagnostische gegevens Hallo [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-categories"></a>Diagnostische logboeken categorieën
Event Hubs worden vastgelegd diagnostische logboeken voor twee categorieën:

* **ArchiveLogs**: Logboeken gerelateerde tooEvent Hubs archieven, in het bijzonder tooarchive gerelateerde fouten registreert.
* **OperationalLogs**: informatie over wat er gebeurt tijdens Event Hubs-bewerkingen in het bijzonder Hallo bewerkingstype, met inbegrip van de event hub is gemaakt, resources die worden gebruikt, en status van de bewerking Hallo Hallo.

## <a name="diagnostic-logs-schema"></a>Diagnostische logboeken schema
Alle logboeken worden opgeslagen in de notatie JSON (JavaScript Object)-indeling. Elk item heeft tekenreeksvelden die gebruikmaken van Hallo-indeling die wordt beschreven in Hallo uit te voeren.

### <a name="archive-logs-schema"></a>Archief logboeken schema

Archief logboek JSON tekenreeksen bevatten die worden vermeld in de volgende tabel Hallo elementen:

Naam | Beschrijving
------- | -------
Taaknaam | Beschrijving van het Hallo-taak die is mislukt.
ActivityId | Interne ID gebruikt om te worden bijgehouden.
trackingId | Interne ID gebruikt om te worden bijgehouden.
resourceId | Azure Resource Manager resource-ID.
EventHub | Event hub volledige naam (inclusief naamruimtenaam).
partitionId | Event Hub-partitie wordt geschreven.
archiveStep | ArchiveFlushWriter
startTime | De begintijd is mislukt.
fouten | Aantal keren is een fout opgetreden.
durationInSeconds | De duur van de fout.
Bericht | Foutbericht.
category | ArchiveLogs

Hallo is volgende code een voorbeeld van een logboek archiveren JSON-tekenreeks:

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

### <a name="operational-logs-schema"></a>Operationele logboeken schema

Operationeel logboek van JSON tekenreeksen bevatten die worden vermeld in de volgende tabel Hallo elementen:

Naam | Beschrijving
------- | -------
ActivityId | Interne ID tootrack doel gebruikt.
EventName | Naam van de bewerking.  
resourceId | Azure Resource Manager resource-ID.
SubscriptionId | Abonnements-ID.
EventTimeString | Bewerkingstijd.
EventProperties | Eigenschappen van de bewerking.
Status | Status van de bewerking.
Caller | De aanroeper van bewerking (Azure portal of management-client).
category | OperationalLogs

Hallo is volgende code een voorbeeld van een operationeel logboek van JSON-tekenreeks:

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

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooEvent Hubs](event-hubs-what-is-event-hubs.md)
* [Event Hubs-API-overzicht](event-hubs-api-overview.md)
* [Aan de slag met Event Hubs](event-hubs-csharp-ephcs-getstarted.md)
