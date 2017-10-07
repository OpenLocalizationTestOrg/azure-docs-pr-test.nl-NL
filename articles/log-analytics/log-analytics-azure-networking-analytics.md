---
title: aaaAzure Networking Analytics-oplossing in Log Analytics | Microsoft Docs
description: U kunt hello Azure Networking Analytics-oplossing in Azure Application Gateway-logboeken en Log Analytics tooreview Azure-netwerk-beveiligingslogboeken groep gebruiken.
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Azure netwerken bewakingsoplossingen in Log Analytics

Log Analytics biedt Hallo oplossingen voor het bewaken van uw netwerken te volgen:
* Netwerk Prestatiemeter (NPM)
 * Controleprogramma Hallo de status van uw netwerk
* Azure Application Gateway analytics tooreview
 * Azure Application Gateway-Logboeken
 * Azure Application Gateway metrische gegevens
* Netwerkbeveiligingsgroep Azure analytics tooreview
 * De Netwerkbeveiligingsgroep voor Azure-Logboeken

## <a name="network-performance-monitor-npm"></a>Netwerk-Prestatiemeter (NPM)

Hallo [netwerk Prestatiemeter](log-analytics-network-performance-monitor.md) management-oplossing is een netwerk bewakingsoplossing die Hallo health, beschikbaarheid en bereikbaarheid van netwerken bewaakt.  Gebruikte toomonitor connectiviteit tussen is:

* openbare cloud en on-premises
* datacenters en gebruikerslocaties (filialen)
* de subnetten die als host fungeert voor verschillende lagen van een toepassing met meerdere lagen.

Zie voor meer informatie [netwerk Prestatiemeter](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure Application Gateway en de Netwerkbeveiligingsgroep analyses
toouse hello oplossingen:
1. Hallo management oplossing tooLog Analytics, toevoegen en
2. Diagnostische gegevens toodirect Hallo diagnostics tooa logboekanalyse workspace in te stellen. Het is niet nodig toowrite Hallo logboeken tooAzure Blob-opslag.

U kunt diagnostische gegevens en de bijbehorende oplossing Hallo inschakelen voor een of beide van de toepassingsgateway en beveiligingsgroepen netwerken.

Als u Diagnostische logboekregistratie voor een bepaald brontype niet is ingeschakeld, maar het Hallo-oplossing installeren, worden de Hallo dashboard blades voor die bron leeg zijn en een foutbericht weergegeven.

> [!NOTE]
> In januari 2017 ondersteund Hallo manier van het verzenden van Logboeken vanaf Toepassingsgateways en Netwerkbeveiligingsgroepen tooLog die Analytics gewijzigd. Als u Hallo ziet **Azure Networking Analytics (afgeschaft)** oplossing te verwijzen[migreren van de oude Networking Analytics-oplossing Hallo](#migrating-from-the-old-networking-analytics-solution) voor stappen die u moet toofollow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Azure verzameling Gegevensdetails toegang controleren
Hello Azure Application Gateway analytics en Hallo Netwerkbeveiligingsgroep analyseoplossingen management verzamelen van diagnostische logboeken rechtstreeks vanuit Azure Toepassingsgateways en Netwerkbeveiligingsgroepen. Het is niet nodig toowrite Hallo logboeken tooAzure Blob-opslag en geen agent is vereist voor het verzamelen van gegevens.

Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld voor Azure Application Gateway analytics en Hallo Netwerkbeveiligingsgroep analytics.

| Platform | Directe agent | Systems Center Operations Manager-agent | Azure | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Verzamelingsfrequentie |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  |Wanneer het logboek geregistreerd |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Azure Application Gateway analytics-oplossing in Log Analytics

![Azure Application Gateway Analytics symbool](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Hallo logboeken te volgen worden voor Toepassingsgateways ondersteund:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

Hallo volgende metrische gegevens worden voor Toepassingsgateways ondersteund:

* doorvoer van 5 minuten

### <a name="install-and-configure-hello-solution"></a>Installeer en configureer Hallo-oplossing
Gebruik Hallo tooinstall instructies te volgen en hello Azure Application Gateway analytics-oplossing te configureren:

1. Inschakelen van hello Azure Application Gateway analytics-oplossing van [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
2. Inschakelen van logboekregistratie van diagnostische gegevens voor Hallo [Toepassingsgateways](../application-gateway/application-gateway-diagnostics.md) gewenste toomonitor.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Azure Application Gateway diagnostische gegevens in de portal Hallo inschakelen

1. Navigeer in hello Azure-portal, toohello Application Gateway resource toomonitor
2. Selecteer *diagnostische logboeken* tooopen Hallo na pagina

   ![afbeelding van Azure Application Gateway resource](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Klik op *diagnostische gegevens inschakelen* tooopen Hallo na pagina

   ![afbeelding van Azure Application Gateway resource](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. tooturn diagnostische gegevens, klikt u op *op* onder *Status*
5. Klik op Hallo selectievakje voor *tooLog Analytics verzenden*
6. Selecteer een bestaande werkruimte voor logboekanalyse of een werkruimte maken
7. Klik op Hallo selectievakje onder **logboek** voor elk Hallo logboek typen toocollect
8. Klik op *opslaan* tooenable Hallo logboekregistratie van diagnostische gegevens tooLog Analytics

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Schakel Azure netwerkdiagnose met PowerShell

Hallo volgende PowerShell-script geeft een voorbeeld van hoe diagnostische logboekregistratie voor Toepassingsgateways tooenable.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Azure Application Gateway analytics gebruiken
![afbeelding van Azure Application Gateway analytics tegel](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Nadat u op Hallo **Azure Application Gateway analytics** tegel op Hallo overzicht, kunt u samenvattingen van uw logboeken weergeven en ga vervolgens omlaag in toodetails voor Hallo volgende categorieën:

* Toegang tot toepassingen Gateway-Logboeken
  * Client en server-fouten voor Application Gateway-Logboeken
  * Aanvragen per uur voor elke Application Gateway
  * Mislukte aanvragen per uur voor elke Application Gateway
  * Fouten door gebruikersagent voor Toepassingsgateways
* Gateway-toepassingsprestaties
  * Status van de host voor Application Gateway
  * Maximum- en 95e percentiel voor Application Gateway mislukte aanvragen

![afbeelding van een dashboard met analytische Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![afbeelding van een dashboard met analytische Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

Op Hallo **Azure Application Gateway analytics** dashboard samenvattingsinformatie in een van de blades Hallo Hallo controleren en klik op een tooview gedetailleerde informatie over de zoekpagina Hallo-logboek.

U kunt op een van de Hallo logboek zoekpagina's, resultaten weergeven door de tijd, gedetailleerde resultaten en uw Logboekgeschiedenis zoeken. U kunt ook facetten toonarrow Hallo resultaten filteren.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Netwerkbeveiligingsgroep Azure analytics-oplossing in Log Analytics

![Netwerkbeveiligingsgroep Azure Analytics symbool](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Hallo na logboeken worden ondersteund voor netwerkbeveiligingsgroepen:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Installeer en configureer Hallo-oplossing
Gebruik Hallo tooinstall instructies te volgen en hello Azure Networking Analytics-oplossing te configureren:

1. Inschakelen van hello Azure Netwerkbeveiligingsgroep analytics-oplossing van [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
2. Inschakelen van logboekregistratie van diagnostische gegevens voor Hallo [Netwerkbeveiligingsgroep](../virtual-network/virtual-network-nsg-manage-log.md) gewenste toomonitor resources.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Inschakelen van Azure security groep Netwerkdiagnose in Hallo-portal

1. Navigeer in hello Azure-portal, toohello Netwerkbeveiligingsgroep resource toomonitor
2. Selecteer *diagnostische logboeken* tooopen Hallo na pagina

   ![afbeelding van de Netwerkbeveiligingsgroep voor Azure resource](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Klik op *diagnostische gegevens inschakelen* tooopen Hallo na pagina

   ![afbeelding van de Netwerkbeveiligingsgroep voor Azure resource](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. tooturn diagnostische gegevens, klikt u op *op* onder *Status*
5. Klik op Hallo selectievakje voor *tooLog Analytics verzenden*
6. Selecteer een bestaande werkruimte voor logboekanalyse of een werkruimte maken
7. Klik op Hallo selectievakje onder **logboek** voor elk Hallo logboek typen toocollect
8. Klik op *opslaan* tooenable Hallo logboekregistratie van diagnostische gegevens tooLog Analytics

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Schakel Azure netwerkdiagnose met PowerShell

Hallo volgende PowerShell-script geeft een voorbeeld van het tooenable Diagnostische logboekregistratie voor netwerkbeveiligingsgroepen
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Gebruik Azure Netwerkbeveiligingsgroep analytics
Nadat u op Hallo **Netwerkbeveiligingsgroep Azure analytics** tegel op Hallo overzicht, kunt u samenvattingen van uw logboeken weergeven en ga vervolgens omlaag in toodetails voor Hallo volgende categorieën:

* Netwerkbeveiligingsgroep geblokkeerd stromen
  * Netwerkbeveiligingsgroepen met geblokkeerde stromen
  * MAC-adressen met geblokkeerde stromen
* Netwerkbeveiligingsgroep stromen toegestaan
  * Netwerkbeveiligingsgroepen met toegestane stromen
  * MAC-adressen met toegestane stromen

![afbeelding van een dashboard met analytische Azure Netwerkbeveiligingsgroep](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![afbeelding van een dashboard met analytische Azure Netwerkbeveiligingsgroep](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

Op Hallo **Netwerkbeveiligingsgroep Azure analytics** dashboard samenvattingsinformatie in een van de blades Hallo Hallo controleren en klik op een tooview gedetailleerde informatie over de zoekpagina Hallo-logboek.

U kunt op een van de Hallo logboek zoekpagina's, resultaten weergeven door de tijd, gedetailleerde resultaten en uw Logboekgeschiedenis zoeken. U kunt ook facetten toonarrow Hallo resultaten filteren.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Migreren van Hallo oude Networking Analytics-oplossing
In januari 2017 ondersteund Hallo manier van het verzenden van Logboeken vanaf Azure Toepassingsgateways en Azure Netwerkbeveiligingsgroepen tooLog die Analytics gewijzigd. Deze wijzigingen bieden Hallo volgende voordelen:
+ Logboeken worden rechtstreeks tooLog Analytics zonder Hallo toouse storage-account moet geschreven
+ Minder latentie van Hallo-tijd wanneer logboeken worden gegenereerd toothem beschikbaar worden gesteld in Log Analytics
+ Minder configuratiestappen
+ Een algemene indeling voor alle typen Azure diagnostics

toouse hello bijgewerkt oplossingen:

1. [Diagnostische gegevens toobe verzonden tooLog Analytics rechtstreeks vanuit Azure Toepassingsgateways configureren](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Diagnostische gegevens toobe verzonden tooLog Analytics rechtstreeks uit Azure Network-beveiligingsgroepen configureren](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Hallo inschakelen *Azure Application Gateway Analytics* en Hallo *Azure Network Security groep Analytics* oplossing met behulp van Hallo proces dat wordt beschreven in [oplossingen van logboekanalyse toevoegen Hallo galerie met oplossingen](log-analytics-add-solutions.md)
3. Bijwerken van een opgeslagen query's, dashboards of waarschuwingen toouse Hallo nieuwe gegevenstype
  + Het type is tooAzureDiagnostics. U kunt Hallo ResourceType toofilter tooAzure netwerken Logboeken kunt gebruiken.

    | In plaats van: | Gebruik: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Voor elk veld dat een achtervoegsel van \_s, \_d, of \_g in Hallo naam Hallo eerste teken toolower hoofdlettergebruik
   + Voor elk veld dat een achtervoegsel van \_o in naam Hallo gegevens is opgesplitst in afzonderlijke velden op basis van de veldnamen Hallo genest.
4. Hallo verwijderen *Azure Networking Analytics (afgeschaft)* oplossing.
  + Als u met behulp van PowerShell, gebruikt u`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`

Gegevens verzameld voordat Hallo wijziging niet zichtbaar in de nieuwe oplossing Hallo is. U kunt tooquery blijven voor deze gegevens met Hallo oude Type en de veldnamen.

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Volgende stappen
* Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens van Azure diagnostics.
