---
title: aaaStream Azure diagnostische logboeken tooan Event Hubs Namespace | Microsoft Docs
description: Meer informatie over hoe toostream diagnostische Azure Event Hubs-naamruimte tooan registreert.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>Tooan diagnostische logboeken van Azure Event Hubs Namespace Stream
**[Azure diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md)**  kan worden gestreamd bijna realtime tooany toepassing hello ingebouwde ' tooEvent Hubs ' optie exporteren in Hallo Portal of door in te schakelen Hallo Service Bus-regel-ID in een diagnostische instelling via hello Azure PowerShell Cmdlets of Azure CLI.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Wat u kunt doen met Logboeken met diagnostische en Event Hubs
Hier volgen slechts enkele manieren waarop u Hallo mogelijkheid streaming voor diagnostische logboeken kunt gebruiken:

* **Stroom logboeken logboekregistratie en telemetrie-systemen van derden too3rd** – gedurende een periode, streaming van Event Hubs wordt Hallo mechanisme toopipe worden uw diagnoselogboeken in toothird derden siem's en meld u analytics-oplossingen.
* **Servicestatus weergeven door het streaming 'hot pad' data tooPowerBI** – met behulp van Event Hubs, Stream Analytics en Power BI, u kunt eenvoudig uw diagnostics-gegevens in realtime-inzichten toonear transformeren op uw Azure-services. [Deze documentatie-artikel biedt een goed overzicht van hoe tooset van Event Hubs verwerken van gegevens met Stream Analytics en Power BI te gebruiken als uitvoer](../stream-analytics/stream-analytics-power-bi-dashboard.md). Hier volgen enkele tips voor het ophalen van instellen met Logboeken met diagnostische gegevens:
  
  * Een event hub voor een categorie van diagnostische logboeken wordt automatisch gemaakt wanneer u Hallo optie in de portal Hallo controleren of via PowerShell, inschakelen dus u tooselect Hallo event hub in de Hallo-naamruimte met Hallo-naam die met begint wilt **insights**.
  * Hallo volgende SQL-code is een voorbeeld van een Stream Analytics query waarmee u tooparse alle Hallo logboekgegevens in tooa PowerBI-tabel kunt:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Maken van een aangepaste Telemetrie en logboekregistratie platform** : als u al een op maat gemaakte telemetrie-platform of diagnostische zijn alleen rekening houdt met een uiterst schaalbare Hallo voor publiceren / abonneren gebouw aard van Event Hubs kunt u tooflexibly opnemen de logboeken. [Zie de Dan Rosanova handleiding toousing Event Hubs in een wereldwijde schaal telemetrie platform hier](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Streaming van logboeken met diagnostische gegevens inschakelen
U kunt inschakelen streaming van diagnostische logboeken programmatisch via Hallo-portal of met behulp van Hallo [Monitor REST-API's van Azure](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). In beide gevallen moet u een diagnostische instelling maken waarin u een naamruimte Event Hubs en Hallo logboek categorieën en metrische gegevens die u wilt dat toosend in toohello naamruimte opgeven. Een event hub wordt gemaakt in de naamruimte Hallo voor elke categorie logboek is ingeschakeld. Een diagnose **logboek categorie** is een type-log dat een resource kan verzamelen.

> [!WARNING]
> Inschakelen en streaming van diagnostische logboeken van rekenresources (bijvoorbeeld virtuele machines of Service Fabric) [vereist een andere set stappen](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Hello Service Bus- of Event Hubs naamruimte heeft geen toobe in Hallo hetzelfde abonnement als Hallo resource logboeken verzenden zolang Hallo-gebruiker die Hallo instelling configureert de juiste RBAC toegang tooboth abonnementen heeft.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Stroom diagnostische logboeken met Hallo-portal
1. Navigeer tooAzure Monitor in Hallo-portal en klikt u op **diagnostische instellingen**

    ![Sectie van de Monitor Azure bewaking](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. Eventueel Hallo lijst filteren op resourcegroep of brontype en klik vervolgens op Hallo resource waarvoor u een diagnostische instelling tooset wilt.

3. Als u geen instellingen bestaat op het Hallo-resource die u hebt geselecteerd, bent u na vragen aan gebruiker toocreate een instelling. Klik op "Diagnostische gegevens inschakelen."

   ![Diagnostische instelling - geen bestaande instellingen toevoegen](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Als er bestaande instellingen op Hallo resource, ziet u een lijst met instellingen die al zijn geconfigureerd op deze resource. Klik op 'Diagnostische instelling toevoegen'.

   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Geef een naam van de instelling en Hallo selectievakje voor **stroom tooan event hub**, selecteer vervolgens een Event Hubs-naamruimte.
   
   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Hallo naamruimte hebt geselecteerd, zijn waar Hallo event hub is gemaakt (als dit de eerste keer diagnostische logboeken streaming is) of gestreamd te (als er nog resources die zijn die naamruimte logboek categorie toothis streaming), en beleid Hallo Hallo definieert machtigingen die Hallo streaming mechanisme heeft. Vandaag de dag vereist tooan streaming event hub machtigingen beheren, verzenden en luisteren. U kunt maken of wijzigen van Event Hubs naamruimte gedeeld toegangsbeleid in Hallo-beheerportal onder tabblad Hallo-configureren voor de naamruimte. tooupdate een van deze diagnostische instellingen, Hallo-client moet gemachtigd Hallo ListKey op Hallo Event Hubs-autorisatieregel.

4. Klik op **Opslaan**.

Na enkele ogenblikken Hallo nieuwe instelling wordt weergegeven in de lijst met instellingen voor deze bron en diagnostische logboeken toothat storage-account worden gestreamd zodra er nieuwe gebeurtenisgegevens wordt gegenereerd.

### <a name="via-powershell-cmdlets"></a>Via PowerShell-Cmdlets
streaming via Hallo tooenable [Azure PowerShell-Cmdlets](insights-powershell-samples.md), kunt u Hallo `Set-AzureRmDiagnosticSetting` cmdlet met de volgende parameters:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Hallo Service Bus regel-ID is een tekenreeks met deze indeling: `{Service Bus resource ID}/authorizationrules/{key name}`, bijvoorbeeld `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.

### <a name="via-azure-cli"></a>Via Azure CLI
streaming via Hallo tooenable [Azure CLI](insights-cli-samples.md), kunt u Hallo `insights diagnostic set` opdracht als volgt:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Hallo dezelfde notatie voor Service Bus regel-ID, zoals uitgelegd voor Hallo PowerShell-Cmdlet gebruiken.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Hoe ik Hallo logboekgegevens van Event Hubs verbruiken?
Hier volgt een voorbeeld uitvoergegevens van Event Hubs:

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| Elementnaam | Beschrijving |
| --- | --- |
| records |Een matrix met alle gebeurtenissen in deze nettolading. |
| tijd |Tijd waarop hello gebeurtenis heeft plaatsgevonden. |
| category |De categorie van het logboek voor deze gebeurtenis. |
| resourceId |Bron-ID van het Hallo-bron die deze gebeurtenis wordt gegenereerd. |
| operationName |Naam van Hallo-bewerking. |
| niveau |Optioneel. Hiermee wordt aangegeven Hallo gebeurtenis logboekniveau. |
| properties |Eigenschappen van gebeurtenis Hallo. |

U kunt een lijst weergeven met alle resourceproviders die ondersteuning bieden voor streaming tooEvent Hubs [hier](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Stroomgegevens van rekenresources
U kunt ook diagnostische logboeken van rekenresources met behulp van Windows Azure Diagnostics-agent Hallo streamen. [Raadpleeg dit artikel](../event-hubs/event-hubs-streaming-azure-diags-data.md) voor het tooset die omhoog.

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Azure diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md)
* [Aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

