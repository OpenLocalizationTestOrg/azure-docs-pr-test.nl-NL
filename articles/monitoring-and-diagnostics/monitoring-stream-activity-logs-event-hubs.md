---
title: aaaStream hello Azure Activity Log tooEvent Hubs | Microsoft Docs
description: Meer informatie over hoe toostream hello Azure Activity Log tooEvent Hubs.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Stream hello Azure Activity Log tooEvent Hubs
Hallo [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) kan worden gestreamd bijna realtime tooany toepassing met behulp van Hallo ingebouwde optie voor 'Exporteren' in de portal Hallo of Hallo Service Bus-regel-Id in een logboek profiel via Hallo door in te schakelen. Azure PowerShell-Cmdlets of Azure CLI.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>Wat u kunt doen met Hallo activiteitenlogboek en Event Hubs
Hier volgen slechts enkele manieren kunt u Hallo streaming mogelijkheid voor het Hallo activiteitenlogboek:

* **Stream toothird derden logboekregistratie en telemetrie systemen** – gedurende een periode, streaming van Event Hubs wordt Hallo mechanisme toopipe uw activiteitenlogboek worden in de siem's van derden en meld u analytics-oplossingen.
* **Maken van een aangepaste Telemetrie en logboekregistratie platform** : als u al een op maat gemaakte telemetrie-platform of Hallo zijn alleen rekening houdt met een uiterst schaalbare Hallo voor publiceren / abonneren gebouw aard van Event Hubs kunt u tooflexibly opnemen activiteitenlogboek. [Zie de Dan Rosanova handleiding toousing Event Hubs in een hier wereldwijde schaal telemetrie-platform.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Streaming Hallo activiteitenlogboek activeren
U kunt inschakelen streaming Hallo activiteitenlogboek via programmacode of via Hallo-portal. In beide gevallen moet u kiest een Service Bus-Namespace en een gedeeld toegangsbeleid voor die naamruimte en een Event Hub wordt gemaakt in die naamruimte als Hallo eerste nieuwe activiteitenlogboek gebeurtenis plaatsvindt. Als u een Service Bus-Namespace niet hebt, moet u eerst toocreate een. Als u hebt eerder gestreamd activiteitenlogboek gebeurtenissen toothis Service Bus Namespace, wordt opnieuw gebruikt Hallo Event Hub die eerder is gemaakt. Hallo gedeeld toegangsbeleid definieert Hallo machtigingen Hallo streaming-mechanisme. Vandaag de dag tooan Event Hubs streaming vereist **beheren**, **verzenden**, en **luisteren** machtigingen. U kunt maken of wijzigen van Service Bus Namespace gedeeld toegangsbeleid in de klassieke portal Hallo Hallo 'Configureren' tabblad voor uw Service Bus-Namespace. tooupdate Hallo activiteitenlogboek logboek profiel tooinclude streaming, Hallo gebruiker Hallo wijziging moet machtiging Hallo ListKey voor die Service Bus-autorisatieregel.

Hallo service bus- of event hub-naamruimte heeft geen toobe in Hallo hetzelfde abonnement als Hallo abonnement logboeken verzenden zolang Hallo-gebruiker die Hallo instelling configureert de juiste RBAC toegang tooboth abonnementen heeft.

### <a name="via-azure-portal"></a>Via de Azure-portal
1. Navigeer toohello **activiteitenlogboek** blade met Hallo-menu op Hallo linkerkant van Hallo-portal.
   
    ![Navigeer tooActivity logboek in de portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Klik op Hallo **exporteren** knop Hallo boven aan het Hallo-blade.
   
    ![Knop exporteren in de portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Hallo-blade die wordt weergegeven, kunt u Hallo regio's waarvoor u dat wilt toostream gebeurtenissen en Hallo Service Bus Namespace waarin u een Event Hub toobe gemaakt voor het streamen van deze gebeurtenissen wilt selecteren.
   
    ![Activiteitenlogboek blade exporteren](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Klik op **opslaan** toosave deze instellingen. Hallo-instellingen zijn onmiddellijk toegepaste tooyour abonnement zijn.

### <a name="via-powershell-cmdlets"></a>Via PowerShell-Cmdlets
Als een profiel voor een logboek al bestaat, moet u eerst tooremove dit profiel.

1. Gebruik `Get-AzureRmLogProfile` tooidentify als een profiel voor een logboek bestaat
2. Als dit het geval is, gebruik `Remove-AzureRmLogProfile` tooremove deze.
3. Gebruik `Set-AzureRmLogProfile` toocreate een profiel:

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

Hallo Service Bus regel-ID is een tekenreeks met deze indeling: {service bus resource ID} /authorizationrules/ {sleutelnaam}, bijvoorbeeld 

### <a name="via-azure-cli"></a>Via Azure CLI
Als een profiel voor een logboek al bestaat, moet u eerst tooremove dit profiel.

1. Gebruik `azure insights logprofile list` tooidentify als een profiel voor een logboek bestaat
2. Als dit het geval is, gebruik `azure insights logprofile delete` tooremove deze.
3. Gebruik `azure insights logprofile add` toocreate een profiel:

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

Hallo Service Bus regel-ID is een tekenreeks met deze indeling: `{service bus resource ID}/authorizationrules/{key name}`.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Hoe ik Hallo logboekgegevens van Event Hubs verbruiken?
[Hallo-schema voor Hallo activiteitenlogboek is hier beschikbaar](monitoring-overview-activity-logs.md). Elke gebeurtenis wordt in een matrix met JSON-blobs aangeroepen "records."

## <a name="next-steps"></a>Volgende stappen
* [Archief Hallo activiteitenlogboek tooa storage-account](monitoring-archive-activity-log.md)
* [Hallo-overzicht van hello Azure Activity Log lezen](monitoring-overview-activity-logs.md)
* [Een waarschuwing op basis van een gebeurtenis activiteitenlogboek instellen](insights-auditlog-to-webhook-email.md)

