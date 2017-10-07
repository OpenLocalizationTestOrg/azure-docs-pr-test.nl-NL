---
title: aaaOverview van diagnostische Azure-Logboeken | Microsoft Docs
description: Informatie over wat Azure diagnostische logboeken zijn en hoe u ze kunt gebruiken toounderstand gebeurtenissen binnen een Azure-resource.
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
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Verzamelen en gebruiken van de logboekgegevens van uw Azure-resources

## <a name="what-are-azure-resource-diagnostic-logs"></a>Wat zijn Azure-resource diagnostische logboeken
**Diagnostische logboeken van Azure resource niveau** logboeken die door een resource die uitgebreide, regelmatig gegevens over Hallo-bewerking van de bron. Hallo-inhoud van deze logboeken varieert per resourcetype. Netwerkbeveiligingsgroep regel tellers en Sleutelkluis audits zijn bijvoorbeeld twee categorieën van Logboeken van de resource.

Diagnostische logboeken niveau resource verschillen van Hallo [activiteitenlogboek](monitoring-overview-activity-logs.md). Hallo activiteitenlogboek verschaft inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement met behulp van Resource Manager, bijvoorbeeld een virtuele machine maken of verwijderen van een logische app. Hallo activiteitenlogboek is een logboek abonnement. Niveau van de resource diagnostische logboeken bieden inzicht in bewerkingen die zijn uitgevoerd binnen die bron zelf, bijvoorbeeld een geheim ophalen uit een Sleutelkluis.

Diagnostische logboeken niveau resource afwijken van de Gast OS-niveau diagnostische logboeken. Gastbesturingssysteem diagnostische logboeken zijn deze die worden verzameld door een agent wordt uitgevoerd binnen een virtuele machine of andere ondersteund resourcetype. Diagnostische logboeken niveau resource vereisen geen gegevens van de resource-specifieke agent en vastleggen van hello Azure-platform zelf, terwijl de Gast OS-niveau diagnostische logboeken vastleggen van gegevens uit het Hallo-besturingssysteem en toepassingen die worden uitgevoerd op een virtuele machine.

Niet alle resources ondersteuning Hallo nieuwe type resource diagnostische logboeken die hier wordt beschreven. Dit artikel bevat een sectie aanbieding brontypen Hallo nieuwe niveau resource diagnostische logboeken ondersteunen.

![Resource diagnostische logboeken tegenover andere typen logboeken ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>Wat u kunt doen met het niveau van de resource diagnostische logboeken
Hier volgen enkele Hallo dingen die u met resource diagnostische logboeken doen kunt:

![Logische plaatsing van diagnostische logboeken van Resource](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Deze tooa opslaan [ **Opslagaccount** ](monitoring-archive-diagnostic-logs.md) voor inspectie controle of handmatig. U kunt opgeven met behulp Hallo bewaren (in dagen) **diagnostische broninstellingen**.
* [Ze te streamen**Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) voor opname door een service van derden of aangepaste analytics-oplossing zoals Power BI.
* Analyseer ze met [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)

U kunt een opslagaccount of Event Hubs-naamruimte die zich niet in hetzelfde abonnement Hallo zoals Hallo een tekensetcodering Logboeken. Hallo-gebruiker die Hallo instelling configureert, moet Hallo juiste RBAC toegang tooboth abonnementen hebben.

## <a name="resource-diagnostic-settings"></a>Diagnostische instellingen voor bronnen
Diagnostische logboeken van de resource voor niet-Compute bronnen worden geconfigureerd met behulp van de diagnostische instellingen resource. **Diagnostische instellingen voor resource** voor een besturingselement resource:

* Waar resource diagnostische logboeken en metrische gegevens worden verzonden (Storage-Account, Event Hubs en/of logboekanalyse OMS).
* Welke categorieën logboek worden verzonden en of u metrische gegevens ook verzonden.
* Hoe lang elke categorie van het logboek moet worden bewaard in een opslagaccount
    - Een bewaartermijn van nul dagen betekent logboeken permanent worden bewaard. Hallo-waarden zijn anders wordt een willekeurig aantal dagen tussen 1 en 2147483647.
    - Als bewaarbeleid worden ingesteld, maar Logboeken opslaan in een Opslagaccount is uitgeschakeld (bijvoorbeeld, als er alleen Event Hubs of OMS-opties zijn geselecteerd), is het bewaarbeleid Hallo hebben geen effect.
    - Bewaarbeleid toegepaste per dag, zodat Hallo einde van een dag (UTC) wordt vastgelegd vanaf Hallo dag dat is nu voorbij Hallo bewaarbeleid worden verwijderd. Bijvoorbeeld, als u had een bewaarbeleid van één dag, zou aan Hallo begin van vandaag de dag voor de Hallo Hallo logboeken van Hallo dag voordat gisteren worden verwijderd.

Deze instellingen gemakkelijk worden geconfigureerd via Hallo diagnostische instellingen voor een resource in hello Azure-portal, via Azure PowerShell en CLI-opdrachten of via Hallo [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> Diagnostische logboeken en metrische gegevens voor uit Hallo Gast OS laag van Compute-resources (bijvoorbeeld virtuele machines of Service Fabric) Gebruik [een afzonderlijk mechanisme voor configuratie en de selectie van uitvoer](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>Hoe tooenable verzamelen van diagnostische logboeken van resource
Verzamelen van diagnostische logboeken resource kan worden ingeschakeld [als onderdeel van het maken van een resource in het Resource Manager-sjabloon](./monitoring-enable-diagnostic-logs-using-template.md) of nadat een bron wordt gemaakt van de pagina die resource in Hallo-portal. U kunt ook de verzameling op elk gewenst moment Azure PowerShell of CLI-opdrachten gebruikt of als Hallo Monitor REST-API van Azure inschakelen.

> [!TIP]
> Deze instructies kunnen niet van toepassing rechtstreeks tooevery resource. Zie Hallo schema koppelingen op Hallo onder aan deze pagina toounderstand speciale stappen die mogelijk toocertain brontypen die van toepassing.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Verzamelen van diagnostische logboeken van de resource in Hallo-portal
U kunt verzamelen van diagnostische logboeken van de resource in hello Azure inschakelen portal nadat een resource is gemaakt door specifieke resource tooa gaat of door te navigeren tooAzure Monitor. tooenable via Azure Monitor:

1. In Hallo [Azure-portal](http://portal.azure.com), gaat u tooAzure Monitor en klikt u op **diagnostische instellingen**

    ![Sectie van de Monitor Azure bewaking](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. Eventueel Hallo lijst filteren op resourcegroep of brontype en klik vervolgens op Hallo resource waarvoor u een diagnostische instelling tooset wilt.

3. Als u geen instellingen bestaat op het Hallo-resource die u hebt geselecteerd, bent u na vragen aan gebruiker toocreate een instelling. Klik op "Diagnostische gegevens inschakelen."

   ![Diagnostische instelling - geen bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Als er bestaande instellingen op Hallo resource, ziet u een lijst met instellingen die al zijn geconfigureerd op deze resource. Klik op 'Diagnostische instelling toevoegen'.

   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Geef een naam van de instelling, Hallo selectievakjes voor elke doel toowhich u wilt toosend gegevens, en welke resource configureren voor elk doel wordt gebruikt. Desgewenst instellen een aantal dagen tooretain deze logboeken via Hallo **bewaartermijn (dagen)** schuifregelaars (alleen van toepassing toohello storage account doel). Een bewaartermijn van nul dagen Hallo logboeken voor onbepaalde tijd worden opgeslagen.
   
   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Klik op **Opslaan**.

Na enkele ogenblikken opgegeven Hallo nieuwe instelling wordt weergegeven in de lijst met instellingen voor deze bron en logboeken met diagnostische gegevens worden verzonden toohello bestemmingen zodra er nieuwe gebeurtenisgegevens wordt gegenereerd.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Verzamelen van diagnostische logboeken van de resource via PowerShell
tooenable verzamelen van diagnostische logboeken van de resource via Azure PowerShell, gebruik Hallo volgende opdrachten:

tooenable opslag van diagnostische logboeken in een opslagaccount, gebruikt u deze opdracht:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

Hallo storage account-ID is Hallo resource-ID voor Hallo storage account toowhich gewenste toosend Hallo registreert.

tooenable streaming van diagnostische logboeken tooan event hub, gebruikt u deze opdracht:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

Hallo service bus regel-ID is een tekenreeks met deze indeling: `{Service Bus resource ID}/authorizationrules/{key name}`.

tooenable verzending van diagnostische logboeken tooa Log Analytics-werkruimte, gebruikt u deze opdracht:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

U kunt Hallo bron-ID van de werkruimte voor logboekanalyse met behulp van de volgende opdracht Hallo verkrijgen:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

U kunt deze parameters tooenable meerdere uitvoeropties combineren.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>Verzamelen van diagnostische logboeken van de resource via CLI
tooenable verzamelen van diagnostische logboeken van de resource via hello Azure CLI gebruiken Hallo volgende opdrachten:

tooenable opslag van diagnostische logboeken in een Opslagaccount, gebruikt u deze opdracht:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

Hallo storage account-ID is Hallo resource-ID voor Hallo storage account toowhich gewenste toosend Hallo registreert.

tooenable streaming van diagnostische logboeken tooan event hub, gebruikt u deze opdracht:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

Hallo service bus regel-ID is een tekenreeks met deze indeling: `{Service Bus resource ID}/authorizationrules/{key name}`.

tooenable verzending van diagnostische logboeken tooa Log Analytics-werkruimte, gebruikt u deze opdracht:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

U kunt deze parameters tooenable meerdere uitvoeropties combineren.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Verzamelen van diagnostische logboeken van de resource via REST-API
Diagnostische instellingen voor toochange hello Azure Monitor REST API, gebruik Zie [dit document](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Diagnostische instellingen van de resource in Hallo portal beheren
Zorg ervoor dat alle resources met diagnostische instellingen zijn ingesteld. Navigeer te**Monitor** in Hallo portal en open **diagnostische instellingen**.

![Diagnostische logboeken blade in Hallo-portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

Mogelijk hebt u tooclick meer gedeelte ' ' toofind Hallo Monitor.

Hier kunt u bekijken en alle resources die ondersteuning bieden voor diagnostische instellingen toosee als ze ingeschakeld diagnostische gegevens hebben filteren. U kunt ook inzoomen toosee als meerdere instellingen is ingesteld op een resource en welke storage-account, de Event Hubs-naamruimte en/of de werkruimte voor logboekanalyse die gegevens om te stromen controleren.

![Diagnostische logboeken resultaten in de portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Resource toevoegen van dat een diagnostische instelling wordt Hallo diagnostische instellingen weergeven, waarin u kunt inschakelen, uitschakelen of wijzigen van de diagnostische instellingen voor Hallo worden geselecteerd.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Ondersteunde services, categorieën en schema's voor resource diagnostische logboeken
[Raadpleeg dit artikel](monitoring-diagnostic-logs-schema.md) voor een volledige lijst van ondersteunde diensten en Hallo logboek categorieën en schema's die worden gebruikt door deze services.

## <a name="next-steps"></a>Volgende stappen

* [Resource diagnostische logboeken te streamen**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Resource diagnostische instellingen wijzigen met hello Azure Monitor REST-API](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Logboeken van de Azure-opslag met logboekanalyse analyseren](../log-analytics/log-analytics-azure-storage.md)
