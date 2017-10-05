---
title: Azure diagnostische logboeken ondersteunde Services en schema's | Microsoft Docs
description: De ondersteunde schema van de services en evenementen voor Azure diagnostische logboeken kennen.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: aa4fa6e0310b2725005dfa34e3225c89fb4282d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="supported-services-schemas-and-categories-for-azure-diagnostic-logs"></a>Ondersteunde services, schema's en categorieën voor Azure diagnostische logboeken

[Diagnostische logboeken van Azure-resource](monitoring-overview-of-diagnostic-logs.md) logboeken die door uw Azure-resources die de werking van die bron te beschrijven. Deze logboeken vormen een resourcetype specifieke. In dit artikel, geven we een overzicht op de set ondersteunde services en het schema van de gebeurtenis voor gebeurtenissen die door elke service. Dit artikel bevat ook een volledige lijst met beschikbare logboek categorieën per resourcetype.

## <a name="supported-services-and-schemas-for-resource-diagnostic-logs"></a>Ondersteunde services en schema's voor resource diagnostische logboeken
Het schema voor resource diagnostische logboeken varieert, afhankelijk van de bron- en logboekbestanden categorie.   

| Service | Schema & Docs |
| --- | --- |
| API Management | Het schema is niet beschikbaar. |
| Toepassingsgateways |[Logboekregistratie van diagnostische gegevens voor de toepassingsgateway](../application-gateway/application-gateway-diagnostics.md) |
| Azure Automation |[Log analytics voor Azure Automation](../automation/automation-manage-send-joblogs-log-analytics.md) |
| Azure Batch |[Diagnostische logboekregistratie van Azure Batch](../batch/batch-diagnostics.md) |
| Klant-inzichten | Het schema is niet beschikbaar. |
| CDN (Content Delivery Network) | Het schema is niet beschikbaar. |
| CosmosDB | Het schema is niet beschikbaar. |
| Data Lake Analytics |[Diagnostische logboeken openen voor Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) |
| Data Lake Store |[Toegang tot diagnoselogboeken voor Azure Data Lake Store](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| Event Hubs |[Diagnostische logboeken van Azure Event Hubs](../event-hubs/event-hubs-diagnostic-logs.md) |
| Key Vault |[Logboekregistratie van Azure Key Vault](../key-vault/key-vault-logging.md) |
| Load balancer |[Logboekanalyse voor Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md) |
| Logic Apps |[Aangepast Logic Apps B2B-volgschema](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| Netwerkbeveiligingsgroepen |[Logboekanalyses voor netwerkbeveiligingsgroepen (NSG's)](../virtual-network/virtual-network-nsg-manage-log.md) |
| Recovery Services | Het schema is niet beschikbaar.|
| Search |[Inschakelen en gebruiken van Search Traffic Analytics](../search/search-traffic-analytics.md) |
| Server Management | Het schema is niet beschikbaar. |
| Service Bus |[Diagnostische logboeken van Azure Service Bus](../service-bus-messaging/service-bus-diagnostic-logs.md) |
| Stream Analytics |[Diagnostische logboeken van taak](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |

## <a name="supported-log-categories-per-resource-type"></a>Logboek categorieën per resourcetype ondersteund
|Resourcetype|Category|Weergavenaam van de categorie|
|---|---|---|
|Microsoft.ApiManagement/service|GatewayLogs|Logboeken die betrekking hebben op ApiManagement Gateway|
|Microsoft.Automation/automationAccounts|JobLogs|Taaklogboeken|
|Microsoft.Automation/automationAccounts|JobStreams|Taak stromen|
|Microsoft.Automation/automationAccounts|DscNodeStatus|Status van de DSC-knooppunt|
|Microsoft.Batch/batchAccounts|ServiceLog|Service-Logboeken|
|Microsoft.Cdn/profiles/endpoints|CoreAnalytics|Hiermee haalt u de metrische gegevens van het eindpunt, zoals bandbreedte, uitgaande, enzovoort.|
|Microsoft.CustomerInsights/hubs|AuditEvents|AuditEvents|
|Microsoft.DataLakeAnalytics/accounts|Controleren|Controlelogboeken|
|Microsoft.DataLakeAnalytics/accounts|Aanvragen|Logboeken aanvragen|
|Microsoft.DataLakeStore/accounts|Controleren|Controlelogboeken|
|Microsoft.DataLakeStore/accounts|Aanvragen|Logboeken aanvragen|
|Microsoft.DocumentDB/databaseAccounts|DataPlaneRequests|DataPlaneRequests|
|Microsoft.EventHub/namespaces|ArchiveLogs|Archief Logboeken|
|Microsoft.EventHub/namespaces|OperationalLogs|Operationele Logboeken|
|Microsoft.EventHub/namespaces|AutoScaleLogs|Logboeken voor automatisch schalen|
|Microsoft.KeyVault/vaults|AuditEvent|Controlelogboeken|
|Microsoft.Logic/workflows|WorkflowRuntime|Workflow runtime diagnostische gebeurtenissen|
|Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|Houd gebeurtenissen bij integratie-Account|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|Gebeurtenis van Netwerkbeveiligingsgroep|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|Regelteller van Netwerkbeveiligingsgroep|
|Microsoft.Network/loadBalancers|LoadBalancerAlertEvent|Load Balancer waarschuwingsgebeurtenissen|
|Microsoft.Network/loadBalancers|LoadBalancerProbeHealthStatus|Gezondheidsstatus van Load Balancer-test|
|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|Toegangslogboek voor Application Gateway|
|Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|Toepassingslogboek van het Gateway-prestaties|
|Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|Toepassingslogboek van het Gateway-Firewall|
|Microsoft.RecoveryServices/Vaults|AzureBackupReport|Azure Backup rapportgegevens|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryJobs|Azure Site Recovery-taken|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryEvents|Azure Site Recovery-gebeurtenissen|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicatedItems|Azure Site Recovery gerepliceerde Items|
|Microsoft.Search/searchServices|OperationLogs|Bewerkingslogboeken|
|Microsoft.ServiceBus/namespaces|OperationalLogs|Operationele Logboeken|
|Microsoft.StreamAnalytics/streamingjobs|Uitvoering|Uitvoering|
|Microsoft.StreamAnalytics/streamingjobs|Ontwerpen|Ontwerpen|

## <a name="next-steps"></a>Volgende stappen

* [Meer informatie over diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md)
* [Diagnostische logboeken van de resource te streamen **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Diagnostische instellingen voor bronnen met de REST-API van Azure Monitor wijzigen](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Logboeken van de Azure-opslag met logboekanalyse analyseren](../log-analytics/log-analytics-azure-storage.md)
