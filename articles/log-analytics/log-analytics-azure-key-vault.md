---
title: aaaAzure Sleutelkluis-oplossing in Log Analytics | Microsoft Docs
description: U kunt hello Azure Key Vault oplossing gebruiken in logboekanalyse tooreview die Azure Sleutelkluis-Logboeken.
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Azure Key Vault Analytics-oplossing in Log Analytics

![Sleutelkluis symbool](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

U kunt hello Azure Key Vault oplossing gebruiken in logboekanalyse tooreview die Azure Key Vault AuditEvent registreert.

toouse Hallo-oplossing, moet u tooenable logboekregistratie van Azure Sleutelkluis diagnostische gegevens en direct Hallo diagnostics tooa-werkruimte voor logboekanalyse. Het is niet nodig toowrite Hallo logboeken tooAzure Blob-opslag.

> [!NOTE]
> In januari 2017 ondersteund Hallo manier van het verzenden van Logboeken van de Sleutelkluis tooLog die Analytics gewijzigd. Als Hallo Sleutelkluis-oplossing u toont *(afgeschaft)* in Hallo-titel verwijzen te[migreren van de oude Sleutelkluis oplossing Hallo](#migrating-from-the-old-key-vault-solution) voor stappen die u moet toofollow.
>
>

## <a name="install-and-configure-hello-solution"></a>Installeer en configureer Hallo-oplossing
Gebruik Hallo tooinstall instructies te volgen en hello Azure Key Vault oplossing configureren:

1. Inschakelen van hello Azure Sleutelkluis-oplossing van [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
2. Schakel Diagnostische logboekregistratie voor Hallo Sleutelkluis resources toomonitor, met behulp van beide Hallo [portal](#enable-key-vault-diagnostics-in-the-portal) of [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Sleutelkluis diagnostische gegevens in de portal Hallo inschakelen

1. Navigeer in hello Azure-portal, toohello Sleutelkluis resource toomonitor
2. Selecteer *diagnostische logboeken* tooopen Hallo na pagina

   ![afbeelding van Azure Sleutelkluis-tegel](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Klik op *diagnostische gegevens inschakelen* tooopen Hallo na pagina

   ![afbeelding van Azure Sleutelkluis-tegel](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. tooturn diagnostische gegevens, klikt u op *op* onder *Status*
5. Klik op Hallo selectievakje voor *tooLog Analytics verzenden*
6. Selecteer een bestaande werkruimte voor logboekanalyse of een werkruimte maken
7. tooenable *AuditEvent* Logboeken, klikt u op Hallo selectievakje onder logboek
8. Klik op *opslaan* tooenable Hallo logboekregistratie van diagnostische gegevens tooLog Analytics

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Sleutelkluis diagnostische gegevens met behulp van PowerShell inschakelen
Hallo volgende PowerShell-script geeft een voorbeeld van het toouse `Set-AzureRmDiagnosticSetting` tooenable Diagnostische logboekregistratie voor Sleutelkluis:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Bekijk de details van Azure Sleutelkluis gegevens verzamelen
Azure Sleutelkluis-oplossing verzamelt logboeken met diagnostische gegevens rechtstreeks van Hallo Sleutelkluis.
Het is niet nodig toowrite Hallo logboeken tooAzure Blob-opslag en geen agent is vereist voor het verzamelen van gegevens.

Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld voor Azure Sleutelkluis.

| Platform | Directe agent | Systems Center Operations Manager-agent | Azure | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Verzamelingsfrequentie |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  | bij ontvangst |

## <a name="use-azure-key-vault"></a>Azure Key Vault gebruiken
Nadat u [Hallo oplossing installeren](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), Hallo Sleutelkluis gegevens weergeven door te klikken op Hallo **Azure Key Vault** tegel van Hallo **overzicht** pagina van logboekanalyse.

![afbeelding van Azure Sleutelkluis-tegel](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Nadat u op Hallo **overzicht** tegel, kunt u samenvattingen van uw logboeken en vervolgens inzoomen weergeven in toodetails voor Hallo volgende categorieën:

* Volume van alle sleutelkluisbewerkingen gedurende een periode
* Kan bewerking volumes gedurende een periode
* Gemiddelde latentie van operationele per bewerking
* Quality of service voor bewerkingen met Hallo aantal bewerkingen die meer dan 1000 ms te nemen en een lijst met bewerkingen die meer dan 1000 ms uitvoeren

![afbeelding van Azure Sleutelkluis-dashboard](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![afbeelding van Azure Sleutelkluis-dashboard](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>details voor elke bewerking tooview
1. Op Hallo **overzicht** pagina, klikt u op Hallo **Azure Key Vault** tegel.
2. Op Hallo **Azure Key Vault** dashboard samenvattingsinformatie in een van de blades Hallo Hallo controleren en klik op een tooview gedetailleerde informatie over het in de zoekpagina Hallo-logboek.

    U kunt op een van de Hallo logboek zoekpagina's, resultaten weergeven door de tijd, gedetailleerde resultaten en uw Logboekgeschiedenis zoeken. U kunt ook facetten toonarrow Hallo resultaten filteren.

## <a name="log-analytics-records"></a>Log Analytics-records
Hello Azure Key Vault oplossing analyseert records die een soort **KeyVaults** die worden verzameld van [AuditEvent logboeken](../key-vault/key-vault-logging.md) in Azure Diagnostics.  Eigenschappen voor deze records zijn in de volgende tabel Hallo:  

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type |*AzureDiagnostics* |
| SourceSystem |*Azure* |
| CallerIpAddress |IP-adres van het Hallo-client die Hallo-aanvraag heeft ingediend |
| Category | *AuditEvent* |
| CorrelationId |Een optionele GUID die client Hallo kunt toocorrelate doorgeven aan de clientzijde logboeken met servicezijde (Sleutelkluis-) Logboeken. |
| DurationMs |De tijd die nodig tooservice Hallo REST-API-aanvraag in milliseconden was. Dit is niet opgenomen netwerklatentie, zodat Hallo-tijd die u aan de clientzijde Hallo meet mogelijk niet overeenkomt met deze tijd. |
| httpStatusCode_d |HTTP-statuscode geretourneerd door het Hallo-aanvraag (bijvoorbeeld *200*) |
| id_s |Unieke ID van het Hallo-aanvraag |
| identity_claim_appid_g | GUID voor Hallo toepassings-id |
| OperationName |Naam van het Hallo-bewerking, zoals beschreven [logboekregistratie van Azure Sleutelkluis](../key-vault/key-vault-logging.md) |
| OperationVersion |REST-API-versie aangevraagd door Hallo-client (bijvoorbeeld *2015-06-01*) |
| requestUri_s |URI van aanvraag Hallo |
| Resource |Naam van de sleutelkluis Hallo |
| ResourceGroup |Resourcegroep van de sleutelkluis Hallo |
| ResourceId |Azure Resource Manager-resource-id. Dit is voor Sleutelkluis-logboeken Hallo Sleutelkluis bron-ID. |
| ResourceProvider |*MICROSOFT CORPORATION. KEYVAULT* |
| ResourceType | *KLUIZEN* |
| ResultSignature |HTTP-status (bijvoorbeeld *OK*) |
| ResultType |Resultaat van de REST-API-aanvraag (bijvoorbeeld *geslaagd*) |
| SubscriptionId |Azure-abonnement-ID van het Hallo-abonnement met Hallo Sleutelkluis |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Migreren van Hallo oude Sleutelkluis-oplossing
In januari 2017 ondersteund Hallo manier van het verzenden van Logboeken van de Sleutelkluis tooLog die Analytics gewijzigd. Deze wijzigingen bieden Hallo volgende voordelen:
+ Logboeken worden rechtstreeks tooLog Analytics zonder Hallo toouse storage-account moet geschreven
+ Minder latentie van Hallo-tijd wanneer logboeken worden gegenereerd toothem beschikbaar worden gesteld in Log Analytics
+ Minder configuratiestappen
+ Een algemene indeling voor alle typen Azure diagnostics

toouse hello bijgewerkt oplossing:

1. [Diagnostische gegevens toobe verzonden rechtstreeks tooLog Analytics uit Sleutelkluis configureren](#enable-key-vault-diagnostics-in-the-portal)  
2. Hello Azure Key Vault oplossing inschakelen met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md)
3. Bijwerken van een opgeslagen query's, dashboards of waarschuwingen toouse Hallo nieuwe gegevenstype
  + Type is gewijzigd van: KeyVaults tooAzureDiagnostics. U kunt Hallo ResourceType toofilter tooKey kluis Logboeken kunt gebruiken.
  - In plaats van: `Type=KeyVaults`, gebruiken`Type=AzureDiagnostics ResourceType=VAULTS`
  + Velden: (veldnamen zijn hoofdlettergevoelig)
  - Voor elk veld dat een achtervoegsel van \_s, \_d, of \_g in Hallo naam Hallo eerste teken toolower hoofdlettergebruik
  - Voor elk veld dat een achtervoegsel van \_o in naam Hallo gegevens is opgesplitst in afzonderlijke velden op basis van de veldnamen Hallo genest. Bijvoorbeeld, wordt Hallo UPN van Hallo aanroepfunctie opgeslagen in een veld`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - Veld CallerIpAddress gewijzigd tooCallerIPAddress
   - Veld RemoteIPCountry is niet meer aanwezig
4. Hallo verwijderen *Sleutelkluis Analytics (afgeschaft)* oplossing. Als u met behulp van PowerShell, gebruikt u`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`

Gegevens verzameld voordat Hallo wijziging niet zichtbaar in de nieuwe oplossing Hallo is. U kunt tooquery blijven voor deze gegevens met Hallo oude Type en de veldnamen.

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Volgende stappen
* Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor Azure Sleutelkluis.
