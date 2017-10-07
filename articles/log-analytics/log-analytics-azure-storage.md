---
title: aaaCollect Azure service-logboeken en metrische gegevens voor Log Analytics | Microsoft Docs
description: Diagnostische gegevens configureren op Azure-resources toowrite logboeken en metrische gegevens tooLog Analytics.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Verzamelen van Logboeken van de Azure-service en metrische gegevens voor gebruik in Log Analytics

Er zijn vier verschillende manieren van het verzamelen van Logboeken en metrische gegevens voor Azure-services:

1. Azure diagnostics directe tooLog Analytics (*Diagnostics* in de volgende tabel Hallo)
2. Azure diagnostics tooAzure opslag tooLog Analytics (*opslag* in de volgende tabel Hallo)
3. Connectors voor Azure-services (*Connectors* in de volgende tabel Hallo)
4. Scripts toocollect en vervolgens postgegevens in logboekanalyse (lege cellen in de volgende tabel Hallo en voor services die niet worden weergegeven)


| Service                 | Resourcetype                           | Logboeken        | Metrische gegevens     | Oplossing |
| --- | --- | --- | --- | --- |
| Toepassingsgateways    | Microsoft.Network/applicationGateways   | Diagnostiek | Diagnostiek | [Azure Application Gateway Analytics](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application insights    |                                         | Connector   | Connector   | [Application Insights-Connector](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (Preview) |
| Automation-accounts     | Microsoft.Automation/AutomationAccounts | Diagnostiek |             | [Meer informatie](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Batch-accounts          | Microsoft.Batch/batchAccounts           | Diagnostiek | Diagnostiek | |
| Klassieke cloudservices  |                                         | Storage     |             | [Meer informatie](log-analytics-azure-storage-iis-table.md) |
| Cognitive Services      | Microsoft.CognitiveServices/accounts    |             | Diagnostiek | |
| Data Lake analytics     | Microsoft.DataLakeAnalytics/accounts    | Diagnostiek |             | |
| Data Lake store         | Microsoft.DataLakeStore/accounts        | Diagnostiek |             | |
| Event Hub-naamruimte     | Microsoft.EventHub/namespaces           | Diagnostiek | Diagnostiek | |
| IoT-Hubs                | Microsoft.Devices/IotHubs               |             | Diagnostiek | |
| Key Vault               | Microsoft.KeyVault/vaults               | Diagnostiek |             | [KeyVault Analytics](log-analytics-azure-key-vault.md) |
| Taakverdelers          | Microsoft.Network/loadBalancers         | Diagnostiek |             |  |
| Logic Apps              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Diagnostiek | Diagnostiek | |
| Netwerkbeveiligingsgroepen | Microsoft.Network/networksecuritygroups | Diagnostiek |             | [Netwerkbeveiligingsgroep Azure Analytics](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Recovery kluizen         | Microsoft.RecoveryServices/vaults       |             |             | [Azure Recovery Services-Analytics (Preview)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Services zoeken         | Microsoft.Search/searchServices         | Diagnostiek | Diagnostiek | |
| Service Bus-naamruimte   | Microsoft.ServiceBus/namespaces         | Diagnostiek | Diagnostiek | [Service Bus Analytics (Preview)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Storage     |             | [Service Fabric Analytics (Preview)](log-analytics-service-fabric.md) |
| SQL (v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Diagnostiek | [Azure SQL Analytics (Preview)](log-analytics-azure-sql.md) |
| Storage                 |                                         |             | Script      | [Azure Storage Analytics (Preview)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Virtuele machines        | Microsoft.Compute/virtualMachines       | Toestelnummer   | Toestelnummer <br> Diagnostiek  | |
| Virtuele Machines-schaalsets | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Diagnostiek | |
| Webserver-farms        | Microsoft.Web/serverfarms               |             | Diagnostiek | |
| Web Sites               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Diagnostiek | [Analytics met Azure-Web-Apps (Preview)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Voor het bewaken van virtuele machines in Azure (Linux en Windows), wordt aangeraden Hallo installeren [Log Analytics VM-extensie](log-analytics-azure-vm-extension.md). Hallo agent biedt u inzicht verzameld van binnen uw virtuele machines. U kunt ook Hallo-extensie voor de virtuele-machineschaalsets gebruiken.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Azure diagnostics direct tooLog Analytics
Veel Azure-resources zijn kunnen toowrite diagnostische logboeken en metrische gegevens rechtstreeks tooLog Analytics en dit is de manier Hallo voorkeur Hallo-gegevens voor analyse te verzamelen. Wanneer u Azure diagnostics, gegevens worden geschreven onmiddellijk tooLog Analytics en er is geen noodzaak toofirst schrijven Hallo gegevens toostorage.

Azure-resources die ondersteuning bieden voor [Azure monitor](../monitoring-and-diagnostics/monitoring-overview.md) hun logboeken en metrische gegevens kunt verzenden rechtstreeks tooLog Analytics.

* Raadpleeg te voor details van de beschikbare metrische gegevens Hallo Hallo[ondersteund met een Azure-Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Raadpleeg te voor details van de beschikbare logboeken Hallo Hallo[ondersteund services en het schema voor diagnostische logboeken](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>Diagnosefunctie inschakelen met PowerShell
U moet Hallo November 2016 (v2.3.0) of later release van [Azure PowerShell](/powershell/azure/overview).

Hallo volgende PowerShell-voorbeeld wordt getoond hoe toouse [Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable diagnostische gegevens op een netwerkbeveiligingsgroep. Hallo dezelfde methode werkt voor alle ondersteunde resources - ingesteld `$resourceId` toohello bron-id van de gewenste tooenable diagnostische gegevens voor Hallo-bron.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Diagnostische gegevens met Resource Manager-sjablonen inschakelen

tooenable diagnostische gegevens van een resource als deze wordt gemaakt en hebben verzonden hello diagnostics tooyour Log Analytics-werkruimte die kunt u een sjabloon vergelijkbare toohello een hieronder. In dit voorbeeld is voor een Automation-account, maar werkt voor alle ondersteunde resourcetypen.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Azure diagnostics toostorage vervolgens tooLog Analytics

Voor het verzamelen van Logboeken van binnen enkele informatiebronnen die mogelijk het is mogelijk toosend Hallo logboeken tooAzure opslag en configureer vervolgens logboekanalyse tooread Hallo logboeken van de opslag.

Log Analytics kunt deze benadering toocollect diagnostische gegevens naar Azure storage gebruiken voor Hallo resources en logboeken te volgen:

| Resource | Logboeken |
| --- | --- |
| Service Fabric |ETWEvent <br> Operationele gebeurtenissen <br> Betrouwbare Actor-gebeurtenis <br> Betrouwbare Service gebeurtenis |
| Virtuele machines |Linux Syslog <br> Windows-gebeurtenis <br> IIS-logboek <br> Windows ETWEvent |
| Web-rollen <br> Werkrollen |Linux Syslog <br> Windows-gebeurtenis <br> IIS-logboek <br> Windows ETWEvent |

> [!NOTE]
> U kunt de normale Azure gegevenskosten voor opslag en transacties wanneer u de tooa opslagaccount voor diagnostische gegevens verzendt en wanneer logboekanalyse Hallo gegevens uit uw storage-account leest worden aangerekend.
>
>

Zie [gebruik blob storage voor IIS en tabel opslag voor gebeurtenissen](log-analytics-azure-storage-iis-table.md) toolearn meer informatie over hoe logboekanalyse deze logboeken kan verzamelen.

## <a name="connectors-for-azure-services"></a>Connectors voor Azure-services

Er is een connector voor Application Insights, waarmee gegevens verzameld door Application Insights toobe tooLog Analytics verzonden.

Meer informatie over Hallo [Application Insights-connector](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Scripts toocollect en post gegevens tooLog Analytics

Voor Azure-services die geen een directe manier toosend logboeken en metrische gegevens tooLog bieden Hallo Analytics kunt u een Azure Automation script toocollect logboek en metrische gegevens. Hallo-script kan vervolgens verzenden Hallo gegevens tooLog Analytics met Hallo [gegevensverzamelaar API](log-analytics-data-collector-api.md)

Hello Azure sjablonengalerie heeft [voorbeelden van het gebruik van Azure Automation](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect gegevens van services en dit tooLog Analytics te verzenden.

## <a name="next-steps"></a>Volgende stappen

* [Blob storage gebruiken voor de opslag van IIS en de tabel voor gebeurtenissen](log-analytics-azure-storage-iis-table.md) tooread Hallo logboeken voor Azure-services die schrijven diagnostics tootable opslag of IIS-logboeken geschreven tooblob opslag.
* [Inschakelen van oplossingen](log-analytics-add-solutions.md) tooprovide inzicht in Hallo-gegevens.
* [Gebruik zoekquery's](log-analytics-log-searches.md) tooanalyze Hallo gegevens.
