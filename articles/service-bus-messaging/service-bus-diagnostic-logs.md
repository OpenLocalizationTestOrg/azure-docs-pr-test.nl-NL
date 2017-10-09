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
# <a name="service-bus-diagnostic-logs"></a>Diagnostische logboeken van Service Bus

U kunt twee soorten logboeken bekijken voor Azure Service Bus:
* **[Activiteitenlogboeken](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Deze logboeken bevatten informatie over de bewerkingen die worden uitgevoerd op een andere taak. Hallo logboeken zijn altijd ingeschakeld.
* **[Diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. U kunt diagnostische logboeken voor uitgebreidere informatie over alles wat er in een job gebeurt kunt configureren. Diagnostische logboeken behandeld activiteiten van Hallo tijd Hallo-taak is gemaakt totdat het Hallo-taak is verwijderd, inclusief updates en activiteiten die zich tijdens het Hallo-taak wordt uitgevoerd.

## <a name="turn-on-diagnostic-logs"></a>Logboeken met diagnostische gegevens inschakelen

Diagnostische logboeken zijn standaard uitgeschakeld. Diagnostische logboeken tooenable, Voer Hallo stappen te volgen:

1.  In Hallo [Azure-portal](https://portal.azure.com)onder **bewaking + Management**, klikt u op **diagnostische logboeken**.

    ![Blade navigatie toodiagnostic Logboeken](./media/service-bus-diagnostic-logs/image1.png)

2. Klik op de gewenste toomonitor Hallo-bron.  

3.  Klik op **diagnostische gegevens inschakelen**.

    ![Logboeken met diagnostische gegevens inschakelen](./media/service-bus-diagnostic-logs/image2.png)

4.  Voor **Status**, klikt u op **op**.

    ![Diagnostische logboeken status wijzigen](./media/service-bus-diagnostic-logs/image3.png)

5.  Set Hallo archief doel dat u wilt. bijvoorbeeld, een opslagaccount, een Event Hub of Azure-logboekanalyse.

6.  Hallo nieuwe diagnostische instellingen opslaan.

Nieuwe instellingen van kracht in ongeveer 10 minuten. Daarna logboeken worden weergegeven in de archivering doel Hallo geconfigureerd op Hallo **diagnostische logboeken** blade.

Zie voor meer informatie over het configureren van diagnostische gegevens Hallo [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Diagnostische logboeken schema

Alle logboeken worden opgeslagen in de notatie JSON (JavaScript Object)-indeling. Elk item heeft tekenreeksvelden die wordt beschreven in de volgende sectie Hallo Hallo-indeling gebruiken.

## <a name="operational-logs-schema"></a>Operationele logboeken schema

Hallo zich aanmeldt **OperationalLogs** categorie leggen wat er gebeurt tijdens de Service Bus-bewerkingen. In het bijzonder deze logboeken Hallo bewerkingstype, inclusief maken van de wachtrij, resources die worden gebruikt, vastleggen en status van de bewerking Hallo Hallo.

Operationeel logboek van JSON tekenreeksen bevatten die worden vermeld in de volgende tabel Hallo elementen:

Naam | Beschrijving
------- | -------
ActivityId | Interne ID, die wordt gebruikt voor bijhouden
EventName | De naam van bewerking           
resourceId | Azure Resource Manager-bron-ID
SubscriptionId | Abonnements-id
EventTimeString | Bewerkingstijd
EventProperties | Eigenschappen van bewerking
Status | De bewerkingsstatus
Caller | De aanroeper van bewerking (Azure portal of management-client)
category | OperationalLogs

Hier volgt een voorbeeld van een operationeel logboek van JSON-tekenreeks:

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

## <a name="next-steps"></a>Volgende stappen

Ga naar Hallo koppelingen toolearn meer over Service Bus te volgen:

* [Inleiding tooService Bus](service-bus-messaging-overview.md)
* [Aan de slag met Service Bus](service-bus-dotnet-get-started-with-queues.md)
