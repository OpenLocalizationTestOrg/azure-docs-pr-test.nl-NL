---
title: metrische gegevens & logboekregistratie van diagnostische gegevens van de aaaAzure SQL database | Microsoft Docs
description: Meer informatie over het configureren van Azure SQL Database resource toostore Resourcegebruik, connectiviteit en Uitvoeringsstatistieken query.
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Azure SQL Database metrische gegevens en logboekregistratie van diagnostische gegevens 
Azure SQL Database kunt verzenden metrische gegevens en de logboeken met diagnostische gegevens voor het bewaken van eenvoudiger. U kunt Azure SQL Database toostore Resourcegebruik, werknemers en sessies en verbindingen in een van deze Azure-resources configureren:
- **Azure Storage**: voor het archiveren van grote hoeveelheden telemetriegegevens voor een lage prijs
- **Azure Event Hub**: voor het integreren van telemetrie van Azure SQL Database met uw aangepaste bewakingsoplossing of hot pijplijnen
- **Azure Log Analytics**: voor out of box van Hallo bewakingsoplossing met rapportage, waarschuwingen en beperkende mogelijkheden 

    ![architectuur](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a>Logboekregistratie inschakelen

Metrische gegevens en diagnostische logboekregistratie is standaard niet ingeschakeld. U kunt inschakelen en beheren van metrische gegevens en logboekregistratie van diagnostische gegevens met een van de volgende methoden Hallo:
- Azure Portal
- PowerShell
- Azure CLI
- REST API 
- Resource Manager-sjabloon

Wanneer u metrische gegevens en logboekregistratie van diagnostische gegevens inschakelen, moet u toospecify hello Azure-resource waar de geselecteerde gegevens worden verzameld. Beschikbare opties:
- Log Analytics
- Event Hub
- Azure Storage 

U kunt inrichten van een nieuwe Azure resource of Selecteer een bestaande resource. Na het selecteren van opslagresource hello, moet u toospecify welke toocollect gegevens. Beschikbare opties zijn:

- **[1 minuut metrieken](sql-database-metrics-diag-logging.md#1-minute-metrics)**  -DTU-percentage, DTU limiet, CPU-percentage, bevat gegevens van fysieke percentage lezen, schrijven logboek percentage, mislukt-geslaagd/geblokkeerd door de firewall-verbindingen, sessies percentage, werknemers percentage, opslag, opslagpercentage, XTP-opslagpercentage

Als u Event Hub of een AzureStorage-account opgeeft, kunt u een beleid bewaren toospecify gegevens die ouder is dan een geselecteerde periode wordt verwijderd. Als u Log Analytics opgeeft, is Hallo bewaarbeleid voor afhankelijk van de geselecteerde prijscategorie Hallo. Lees meer over [logboekanalyse prijzen](https://azure.microsoft.com/pricing/details/log-analytics/). 

Het is raadzaam dat u beide Hallo leest [overzicht van metrische gegevens in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) en [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain niet alleen hoe een goed begrip van artikelen tooenable logboekregistratie, maar Hallo metrische gegevens en logboekbestanden categorieën ondersteund door Hallo verschillende Azure-services.

### <a name="azure-portal"></a>Azure Portal

tooenable metrische gegevens en logboeken met diagnostische gegevens verzamelen in hello Azure-portal navigeert tooyour Azure SQL database of de pagina van de elastische groep en klik vervolgens op **diagnostische instellingen**.

   ![inschakelen in hello Azure-portal](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a>PowerShell

tooenable metrische gegevens en logboekregistratie van diagnostische gegevens met behulp van PowerShell, gebruikt u Hallo volgende opdrachten:

- tooenable opslag van diagnostische logboeken in een Opslagaccount, gebruikt u deze opdracht:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   Hallo Storage Account-ID is Hallo resource-id voor Hallo storage account toowhich gewenste toosend Hallo registreert.

- tooenable streaming van diagnostische logboeken tooan Event Hub, gebruikt u deze opdracht:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   Hallo Service Bus regel-ID is een tekenreeks met deze indeling:

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- tooenable verzending van diagnostische logboeken tooa Log Analytics-werkruimte, gebruikt u deze opdracht:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- U kunt Hallo bron-id van de werkruimte voor logboekanalyse met behulp van de volgende opdracht Hallo verkrijgen:

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

U kunt deze parameters tooenable meerdere uitvoeropties combineren.

### <a name="cli"></a>CLI

tooenable metrische gegevens en diagnostische gegevens met behulp van logboekregistratie hello Azure CLI, gebruik Hallo volgende opdrachten:

- tooenable opslag van diagnostische logboeken in een Opslagaccount, gebruikt u deze opdracht:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   Hallo Storage Account-ID is Hallo resource-id voor Hallo storage account toowhich gewenste toosend Hallo registreert.

- tooenable streaming van diagnostische logboeken tooan Event Hub, gebruikt u deze opdracht:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   Hallo Service Bus regel-ID is een tekenreeks met deze indeling:

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- tooenable verzending van diagnostische logboeken tooa Log Analytics-werkruimte, gebruikt u deze opdracht:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

U kunt deze parameters tooenable meerdere uitvoeropties combineren.

### <a name="rest-api"></a>REST API

Meer informatie over het te[diagnostische instellingen wijzigen met hello Azure Monitor REST-API](https://msdn.microsoft.com/library/azure/dn931931.aspx). 

### <a name="resource-manager-template"></a>Resource Manager-sjabloon

Meer informatie over het te[Schakel de diagnostische instellingen bij het maken van de resource met Resource Manager-sjabloon](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md). 

## <a name="stream-into-log-analytics"></a>Stream in Log Analytics 
Azure SQL Database metrische gegevens en logboeken met diagnostische gegevens kunnen worden gestreamd naar logboekanalyse met behulp van de optie ingebouwde 'verzenden tooLog Analytics' Hallo in Hallo portal of met logboekanalyse inschakelen in een diagnostische instelling via Azure PowerShell-cmdlets, Azure CLI of Azure Monitor REST API.

### <a name="installation-overview"></a>Installatie-overzicht

Azure SQL Database wagenpark bewaking is heel eenvoudig met logboekanalyse. Er zijn drie stappen vereist:

1.  Log Analytics-resource maken
2.  Configureer databases toorecord metrische gegevens en diagnostische logboeken in Hallo gemaakt Log Analytics
3.  Installeer **Azure SQL Analytics** oplossing van galerie in Log Analytics

### <a name="create-log-analytics-resource"></a>Log Analytics-resource maken

1. Klik op **nieuw** in het menu links van Hallo.
2. Klik op **bewaking en beheer**
3. Klik op **Analytics melden**
4. Hallo logboekanalyse formulier invullen met Hallo vereiste aanvullende informatie: de Werkruimtenaam van de, abonnement, resourcegroep, locatie en prijscategorie.

   ![log analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a>Databases toorecord metrische gegevens en de logboeken met diagnostische gegevens configureren

Hallo gemakkelijkste manier tooconfigure waarin databases hun metrische gegevens registreren is via hello Azure-portal. In hello Azure-portal, gaat u tooyour Azure SQL Database resource en klikt u op **diagnostische instellingen**. 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a>Hello Azure SQL Analytics-oplossing installeren vanuit galerie  

1. Zodra Hallo Log Analytics-resource is gemaakt en uw gegevens die in deze binnenkomen is, installeer Azure SQL Analytics-oplossing. Dit kan worden gedaan via Hallo **galerie met oplossingen** die u kunt vinden op Hallo OMS-startpagina en in Hallo side menu. Zoek in de galerie hello, en klik op **Azure SQL Analytics** oplossing en op **toevoegen**.

   ![oplossing voor controle](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. Uw startpagina OMS een nieuwe tegel opgeroepen **Azure SQL Analytics** wordt weergegeven. Als u deze tegel wordt geopend hello Azure SQL Analytics dashboard.

### <a name="using-azure-sql-analytics-solution"></a>Met behulp van Azure SQL Analytics-oplossing

Azure SQL-Analytics is een hiërarchische dashboard waarmee u toonavigate via Hallo hiërarchie van Azure SQL Database-resources. Deze mogelijkheid kunt u toodo op hoog niveau bewaking maar ook kunt u tooscope uw bewaking toojust Hallo rechts set resources.
Dashboard bevat Hallo lijsten van verschillende bronnen onder Hallo geselecteerd resource. Ziet u voor een geselecteerde abonnement Hallo servers, elastische pools en databases die deel uitmaken van toohello geselecteerde abonnement. U kunt bovendien voor elastische Pools en databases Hallo resource meetgegevens voor softwaregebruik van de bron zien. Dit omvat grafieken voor DTU, CPU, IO, logboek, sessies, werknemers, verbindingen en opslag in GB.

## <a name="stream-into-azure-event-hub"></a>Stream in Azure Event Hub

Azure SQL Database metrische gegevens en logboeken met diagnostische gegevens kunnen worden gestreamd naar Event Hub gebruiken Hallo ingebouwde 'Stream tooan event hub' in de portal hello, of doordat de Service Bus regel-Id in een diagnostische instelling via Azure PowerShell-Cmdlets, Azure CLI of Azure Monitor REST API. 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a>Welke toodo met metrische gegevens en de logboeken met diagnostische gegevens in de Event Hub?
Zodra het Hallo geselecteerd gegevens gestreamd in Event Hub, bent u een stap dichter tooenabling geavanceerde bewakingsscenario's. Event Hubs fungeert als Hallo 'voordeur' van een gebeurtenispijplijn en zodra gegevens zijn verzameld in een Event Hub, kunnen worden omgezet en opgeslagen met een realtime-analyseprovider of batchverwerking/opslagadapters. Event Hubs worden losgekoppeld Hallo productie van een stream van gebeurtenissen van Hallo gebruik van deze gebeurtenissen, zodat gebeurtenisconsumers Hallo gebeurtenissen op basis van hun eigen planning kunnen openen. Zie voor meer informatie over Event Hub:

- [Wat is Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?
- [Aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


Hier volgen slechts enkele manieren kunt u Hallo streaming mogelijkheid:

-   Servicestatus weergeven door streaming 'hot pad' data tooPowerBI - met behulp van Event Hubs, Stream Analytics en Power BI, kunt u eenvoudig uw metrische gegevens en diagnostische gegevens in bijna realtime-inzichten transformeren op uw Azure-services. Zie voor een overzicht van hoe tooset van een Event Hubs verwerken van gegevens met Stream Analytics en Power BI te gebruiken als uitvoer, [Stream Analytics en Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).
-   Stroom logboeken toothird derden logboekregistratie en telemetrie streams – Event Hubs met behulp van streaming-u kunnen krijgen de metrische gegevens en de logboeken met diagnostische gegevens in toodifferent van derden bewaking en log analytics-oplossingen. 
-   Maak een aangepaste Telemetrie en de logboekregistratie-platform als er al een op maat gemaakte telemetrie-platform of diagnostische logboeken zijn alleen rekening houdt met een uiterst schaalbare Hallo voor publiceren / abonneren gebouw aard van Event Hubs kunt u tooflexibly opnemen. Zie [Dan Rosanova van handleiding toousing Event Hubs in een wereldwijde schaal telemetrie platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="stream-into-azure-storage"></a>Stream in Azure Storage

Azure SQL Database metrische gegevens en logboeken met diagnostische gegevens kunnen worden opgeslagen in Azure Storage met optie voor ingebouwde 'Archiveren tooa storage-account' hello in hello Azure-portal, of door het inschakelen van Azure Storage in een diagnostische instelling via Azure PowerShell-Cmdlets, Azure CLI of Azure Monitor voor REST-API.

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a>Schema van de metrische gegevens en diagnostische logboeken in Hallo storage-account

Nadat u metrische gegevens en diagnostische logboeken verzameling hebt ingesteld, wordt een storage-container gemaakt in Hallo storage-account die u hebt geselecteerd tijdens de eerste rijen Hallo van gegevens beschikbaar zijn. Hallo-structuur van deze BLOB's is:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
Of gewoon meer:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

Zo mogelijk een blob-naam voor 1 minuut metrieken:

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

Als u wilt dat toorecord Hallo gegevens uit de elastische groep hello, verschilt blob-naam enigszins:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a>Metrische gegevens en logboeken downloaden vanaf de Azure-opslag

Zie [metrische gegevens en diagnostische logboeken downloaden vanaf Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)

## <a name="1-minute-metrics"></a>1 minuut metrische gegevens

| |  |
|---|---|
|**Resource**|**Metrische gegevens**|
|Database|DTU-percentage DTU gebruikt, DTU limiet, CPU-percentage, fysieke gegevens gelezen percentage, logboek schrijven percentage, mislukt-geslaagd/geblokkeerd door de firewall-verbindingen, sessies percentage, werknemers percentage, opslag, opslagpercentage, XTP-opslagpercentage, impassen |
|Elastische pool|percentage van de eDTU, eDTU gebruikt, eDTU limiet, CPU-percentage, fysieke gegevens gelezen percentage, logboek schrijven percentage, sessies percentage, werknemers percentage, opslag, opslagpercentage, opslaglimiet bereikt, XTP-opslagpercentage |
|||

## <a name="next-steps"></a>Volgende stappen

- Lezen van beide Hallo [overzicht van metrische gegevens in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) en [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain een goed begrip van het niet alleen hoe tooenable aan te melden, maar Hallo metrische gegevens en meld u categorieën artikelen ondersteund door Hallo verschillende Azure-services.
- Lees deze toolearn artikelen over event hubs:
   - [Wat is Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?
   - [Aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- Zie [metrische gegevens en diagnostische logboeken downloaden vanaf Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
