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
# <a name="monitor-api-management-with-azure-monitor"></a>Monitor voor API Management met Azure-Monitor
Monitor voor Azure is een Azure-service met één bron voor de bewaking van alle Azure-resources. Met Azure-Monitor kunt u visualiseren, query, routeren, archiveren en acties uitvoeren op Hallo metrische gegevens en afkomstig is van de Azure-bronnen zoals API Management-Logboeken. 

Hallo volgende video toont hoe toomonitor API-beheer met behulp van Azure-Monitor. Zie voor meer informatie over Azure Monitor [aan de slag met Azure Monitor]. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>Metrische gegevens
API Management momenteel vijf metrische gegevens verzendt en we zullen tooadd in toekomstige Hallo meer. Deze metrische gegevens worden gegenereerd per minuut, zodat u bijna realtime zicht krijgt op Hallo status en gezondheid van uw API's. Hier volgt een samenvatting van Hallo metrische gegevens:
* Totaal aantal verzoeken van de Gateway: Hallo aantal API-aanvragen in Hallo periode. 
* Geslaagde aanvragen voor de Gateway: Hallo aantal API-aanvragen dat geslaagde HTTP-antwoordcodes waaronder 304, 307 en iets kleiner is dan 301 (bijvoorbeeld 200) ontvangen. 
* Mislukte aanvragen van de Gateway: Hallo aantal API-aanvragen dat foutieve HTTP-antwoordcodes waaronder 400 en iets groter zijn dan 500 ontvangen.
* Ongeautoriseerde aanvragen van de Gateway: Hallo aantal API-aanvragen die HTTP-antwoordcodes waaronder 401, 403 en 429 ontvangen. 
* Andere aanvragen voor de Gateway: Hallo aantal API-aanvragen die HTTP-antwoordcodes die geen deel uitmaken van tooany Hallo voorgaande categorieën (bijvoorbeeld 418) ontvangen.

U kunt toegang tot metrische gegevens in uw API Management-service of toegang tot metrische gegevens van alle Azure-resources in Azure-Monitor. tooview metrische gegevens in uw API Management-service:
1. Open hello Azure-portal.
2. Ga tooyour API Management-service.
3. Klik op **metrische gegevens**.

![Blade metrische gegevens][metrics-blade]

Voor meer informatie over het toouse metrische gegevens, Zie [overzicht van metrische gegevens].

## <a name="activity-logs"></a>Activiteitenlogboeken
Activiteitenlogboeken bieden inzicht in Hallo-bewerkingen die zijn uitgevoerd op uw API Management-services. Het was voorheen bekend als 'controlelogboeken' of 'operationele logs'. Met activiteitenlogboeken, kunt u Hallo bepalen ' wat, wie, en wanneer ' voor een (PUT, POST, verwijderen schrijfbewerkingen) die op uw API Management-services worden uitgevoerd. 

> [!NOTE]
> Activiteitenlogboeken bevatten geen leesbewerkingen (GET) of bewerkingen die worden uitgevoerd klassieke Publicatieportal Hallo of met behulp van Hallo oorspronkelijke Management-API's.

U kunt toegang krijgen tot activiteitenlogboeken in uw API Management-service of toegang tot de logboeken van alle Azure-resources in Azure-Monitor. tooview activiteit geregistreerd in uw API Management-service:
1. Open hello Azure-portal.
2. Ga tooyour API Management-service.
3. Klik op **activiteitenlogboek**.

![Activiteit logboeken blade][activity-logs-blade]

Voor meer informatie over het toouse metrische gegevens, Zie [overzicht activiteitenlogboeken].

## <a name="alerts"></a>Waarschuwingen
U kunt tooreceive waarschuwingen op basis van de logboeken van metrische gegevens en activiteit kunt configureren. Azure Monitor kunt u een waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd tooconfigure:

* E-mailmelding verzenden
* een webhook aanroepen
* Een Azure Logic App aanroepen

U kunt regels voor waarschuwingen configureren in uw API Management-service of in de Azure-Monitor. tooconfigure ze in API Management: 
1. Open hello Azure-portal.
2. Ga tooyour API Management-service.
3. Klik op **waarschuwing regels**.

![Regels voor waarschuwingen-blade][alert-rules-blade]

Zie voor meer informatie over het gebruik van waarschuwingen [overzicht van waarschuwingen].

## <a name="diagnostic-logs"></a>Diagnostische logboeken
Logboeken met diagnostische gegevens bevatten uitgebreide informatie over bewerkingen en fouten die belangrijk zijn voor controle, evenals het oplossen van problemen. Diagnostische logboeken verschillen van activiteitenlogboeken. Activiteitenlogboeken bieden inzicht in het Hallo-bewerkingen die zijn uitgevoerd op uw Azure-resources. Diagnostische logboeken bieden inzicht in bewerkingen dat de bron zelf uitgevoerd.

API Management biedt momenteel diagnostische logboeken (batch verwerkt per uur) over de API van afzonderlijke aanvragen met elke vermelding met Hallo structuur te volgen:

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

U kunt toegang tot diagnoselogboeken in uw API Management-service of toegang tot de logboeken van alle Azure-resources in Azure-Monitor. tooview diagnostische logboeken in uw API Management-service:
1. Open hello Azure-portal.
2. Ga tooyour API Management-service.
3. Klik op **diagnostische logboeken**.

![Blade met diagnostische logboeken][diagnostic-logs-blade]

Voor meer informatie over het toouse metrische gegevens, Zie [overzicht van diagnostische logboeken].

## <a name="next-step"></a>Volgende stap

* [aan de slag met Azure Monitor]
* [overzicht van metrische gegevens]
* [overzicht activiteitenlogboeken]
* [overzicht van diagnostische logboeken]
* [overzicht van waarschuwingen]

[aan de slag met Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[overzicht van metrische gegevens]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[overzicht activiteitenlogboeken]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[overzicht van diagnostische logboeken]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[overzicht van waarschuwingen]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
