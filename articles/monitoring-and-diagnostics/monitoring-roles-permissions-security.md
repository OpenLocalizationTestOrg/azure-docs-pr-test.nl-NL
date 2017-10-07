---
title: aaaGet gestart met rollen, machtigingen en beveiliging met Azure Monitor | Microsoft Docs
description: Meer informatie over hoe de ingebouwde rollen en machtigingen toorestrict toouse Azure Monitor toegang krijgen toomonitoring bronnen tot.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Aan de slag met rollen, machtigingen en -beveiliging met Azure-Monitor
Veel teams moeten toostrictly reguleren toegang toomonitoring gegevens en instellingen. Bijvoorbeeld, als er teamleden die werken alleen op de bewaking (ondersteuningsmedewerkers, devops engineers) of als u een provider van beheerde services gebruikt, u ze toegang tot bewakingsgegevens kunt tijdens het beperken van hun mogelijkheid toocreate tooonly toogrant, wijzigen, of resources verwijderen. Dit artikel laat zien hoe tooquickly toepassen van een ingebouwde bewaking RBAC-rol tooa gebruiker in Azure of uw eigen aangepaste rol voor een gebruiker aan wie beperkte machtigingen voor controle moet bouwen. Beveiligingsoverwegingen voor uw Azure-Monitor-gerelateerde resources vervolgens besproken en hoe u toegang tot toohello gegevens kunt beperken bevatten.

## <a name="built-in-monitoring-roles"></a>Ingebouwde bewaking rollen
De ingebouwde rollen Azure Monitor ontworpen toohelp limiet toegang tooresources in een abonnement terwijl nog steeds die verantwoordelijk zijn voor bewaking van infrastructuur tooobtain en configureer Hallo gegevens die ze nodig. Azure biedt twee out-of-the-box-rollen: een bewaking lezer en Inzender bewaking.

### <a name="monitoring-reader"></a>Bewaking van de lezer
Personen die zijn toegewezen met de rol Lezer bewaking Hallo kunnen alle bewakingsgegevens weergeven in een abonnement, maar kan wijzigen een resource of instellingen gerelateerde toomonitoring bronnen bewerken. Deze rol is geschikt voor gebruikers in een organisatie, zoals ondersteuning of bewerkingen engineers hoeven toobe kunnen:

* Monitoring dashboards in Hallo portal weergeven en maken van hun eigen persoonlijke dashboards voor bewaking.
* Query voor de metrische gegevens met behulp van Hallo [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell-cmdlets](insights-powershell-samples.md), of [platformoverschrijdende CLI](insights-cli-samples.md).
* Query Hallo activiteitenlogboek met Hallo-portal, Azure Monitor REST-API, PowerShell-cmdlets of platformoverschrijdende CLI.
* Weergave Hallo [diagnostische instellingen](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) voor een resource.
* Weergave Hallo [Meld profiel](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) voor een abonnement.
* Weergave-instellingen voor automatisch schalen.
* Waarschuwing activiteit weergeven en instellingen.
* Toegang tot gegevens van Application Insights en gegevens weergeven in AI Analytics.
* Zoeken naar gegevens in de werkruimte logboekanalyse (OMS) met inbegrip van gebruiksgegevens voor Hallo-werkruimte.
* Beheergroepen logboekanalyse (OMS) weer.
* Hallo logboekanalyse (OMS) search schema ophalen.
* Lijst met logboekanalyse (OMS) intelligence packs.
* Ophalen en uitvoeren van logboekanalyse (OMS) opgeslagen zoekopdrachten.
* Hallo-opslagconfiguratie voor logboekanalyse (OMS) ophalen.

> [!NOTE]
> Deze rol geeft geen leestoegang toolog gegevens dat is gestroomd tooan event hub of opgeslagen in een opslagaccount. [Zie hieronder](#security-considerations-for-monitoring-data) voor informatie over het configureren van toegang tot toothese bronnen.
> 
> 

### <a name="monitoring-contributor"></a>Inzender bewaking
Personen die zijn toegewezen Hallo bewaking Inzender rol kan alle bewakingsgegevens weergeven in een abonnement en maak of controle-instellingen wijzigen, maar niet alle andere resources wijzigen. Deze rol is een hoofdverzameling van met de rol Lezer bewaking Hallo en geschikt is voor leden van de bewaking team een organisatie of de beheerde service-providers die bovendien toohello machtigingen hierboven, moet ook toobe kunnen:

* Monitoring dashboards publiceren als een gedeelde dashboard.
* Stel [diagnostische instellingen](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) voor een resource.*
* Set Hallo [Meld profiel](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) voor een subscription.*
* Waarschuwing activiteit en -instellingen instellen.
* Maak webtests Application Insights en onderdelen.
* Lijst met logboekanalyse (OMS) werkruimte gedeelde sleutels.
* In- of uitschakelen van logboekanalyse (OMS) intelligence packs.
* Maken en verwijderen en logboekanalyse (OMS) opgeslagen zoekopdrachten uitvoeren.
* Maken en verwijderen van de opslagconfiguratie voor logboekanalyse (OMS) Hallo.

* gebruiker moet ook afzonderlijk worden gemachtigd ListKeys op Hallo doel resource (storage-account of event hub naamruimte) tooset een profiel voor een logboek of de diagnostische instelling.

> [!NOTE]
> Deze rol geeft geen leestoegang toolog gegevens dat is gestroomd tooan event hub of opgeslagen in een opslagaccount. [Zie hieronder](#security-considerations-for-monitoring-data) voor informatie over het configureren van toegang tot toothese bronnen.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>Bewaking van aangepaste RBAC-rollen en machtigingen
Als Hallo hierboven ingebouwde rollen niet voldoen aan Hallo exacte behoeften van uw team, kunt u [maakt u een aangepaste RBAC-rol](../active-directory/role-based-access-control-custom-roles.md) met meer gedetailleerde machtigingen. Hieronder vindt Hallo algemene Azure Monitor RBAC-bewerkingen met de bijbehorende beschrijvingen.

| Bewerking | Beschrijving |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, schrijven, verwijderen] |Waarschuwingsregels voor lezen, schrijven, verwijderen. |
| Microsoft.Insights/AlertRules/Incidents/Read |Lijst met incidenten (geschiedenis van de waarschuwingsregel hello wordt geactiveerd) voor regels voor waarschuwingen. Dit geldt alleen toohello-portal. |
| Microsoft.Insights/AutoscaleSettings/[Read, schrijven, verwijderen] |Instellingen voor automatisch schalen die lezen/schrijven/verwijderen. |
| Microsoft.Insights/DiagnosticSettings/[Read, schrijven, verwijderen] |Diagnostische instellingen voor lezen, schrijven, verwijderen. |
| Microsoft.Insights/eventtypes/digestevents/Read |Deze machtiging is vereist voor gebruikers die toegang moeten hebben tot tooActivity logboeken via Hallo-portal. |
| Microsoft.Insights/eventtypes/values/Read |Activiteitenlogboek gebeurtenissen (management gebeurtenissen) in een abonnement weergeven. Deze machtiging is van toepassing tooboth programmatische en portal toegang toohello activiteitenlogboek. |
| Microsoft.Insights/LogDefinitions/Read |Deze machtiging is vereist voor gebruikers die toegang moeten hebben tot tooActivity logboeken via Hallo-portal. |
| Microsoft.Insights/MetricDefinitions/Read |Metrische definities (lijst met beschikbare metrische gegevens typen voor een resource) lezen. |
| Microsoft.Insights/Metrics/Read |Metrische gegevens voor een resource lezen. |

> [!NOTE]
> Toegang tot tooalerts diagnostische instellingen en metrische gegevens voor een resource vereist dat die Hallo de gebruiker heeft leestoegang toohello resourcetype en bereik van de bron. ('Schrijven') maken een diagnostisch profiel instelling of een logboekbestand dat archieven tooa storage-account of streams tooevent hubs Hallo gebruiker tooalso vereist ListKeys machtiging hebben voor de doelbron Hallo.
> 
> 

Met de Hallo boven tabel kan u bijvoorbeeld een aangepaste RBAC-rol voor een 'activiteit logboekweergave' als volgt maken:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Beveiligingsoverwegingen voor het bewaken van gegevens
Bewakingsgegevens, met name de logboekbestanden: vertrouwelijke gegevens, zoals IP-adressen of namen van gebruikers kan bevatten. Het bewaken van gegevens van Azure wordt geleverd in drie basic formulieren:

1. Hallo activiteitenlogboek waarin alle besturingselement vlak acties op uw Azure-abonnement.
2. Diagnostische logboeken die verzonden door een resource van Logboeken zijn.
3. Metrieken worden gegenereerd door de bronnen.

Alle drie van de volgende gegevenstypen kunnen worden opgeslagen in een opslagaccount of tooEvent Hub, beide met de Azure-resources voor algemene doeleinden worden gestreamd. Omdat dit algemene bronnen, is maken, verwijderen en toegang hebben tot deze een bewerking met bevoegdheid doorgaans gereserveerd voor een beheerder. Het is raadzaam om de volgende procedures voor de bewaking-gerelateerde resources tooprevent misbruik hello te gebruiken:

* Een enkele, speciaal opslagaccount gebruiken voor het bewaken van gegevens. Als u het bewaken van gegevens in meerdere opslagaccounts tooseparate nodig, nooit delen informatie over het gebruik van een opslagaccount tussen bewaking en niet-bewaking gegevens, zoals dit mogelijk per ongeluk geven degenen die alleen moet toegang hebben tot toomonitoring gegevens (bv. een derde partij SIEM) toegang krijgen tot gegevens toonon bewaking.
* Een enkele, toegewezen Service Bus- of Event Hub-naamruimte gebruiken in alle diagnostische instellingen voor Hallo dezelfde als hierboven reden.
* Beperken van toegang toomonitoring-gerelateerde storage-accounts of event hubs doordat ze op een afzonderlijke resourcegroep en [gebruik scope](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) op uw bewaking rollen toolimit access tooonly die resourcegroep.
* Nooit machtigen Hallo ListKeys storage-accounts of event hubs op abonnementsbereik wanneer een gebruiker alleen toegang tot toomonitoring gegevens nodig. In plaats daarvan geven de gebruiker van deze machtigingen toohello op een resource of resourcegroep (als u een speciale bewaking resourcegroep hebt) bereik.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Beperken van toegang toomonitoring-gerelateerde storage-accounts
Wanneer een gebruiker of toepassing toegang krijgen gegevens in een opslagaccount toomonitoring tot moet, moet u [genereren van een Account-SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx) op Hallo storage-account dat bewakingsgegevens met serviceniveau alleen-lezentoegang tooblob storage bevat. In PowerShell dit als volgt uitzien:

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

U kunt vervolgens Hallo token toohello entiteit die tooread uit dat opslagaccount moet geven en kan weergeven en lezen uit alle blobs in dit opslagaccount.

Als u deze machtiging met RBAC toocontrol moet, kunt u ook verlenen die entiteit Hallo Microsoft.Storage/storageAccounts/listkeys/action machtiging op dat bepaalde storage-account. Dit is nodig voor gebruikers die toobe kunnen tooset een diagnostische instelling of logboek profiel tooarchive tooa storage-account nodig. U kunt bijvoorbeeld Hallo aangepaste RBAC-rol voor een gebruiker of toepassing die alleen tooread van één opslagaccount opgeven moet na maken:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> Hallo ListKeys machtiging kunt Hallo gebruiker toolist Hallo primaire en secundaire sleutels van opslagaccount. Deze sleutels verlenen Hallo gebruiker alle ondertekende machtigingen (lezen, schrijven, BLOB's maken, verwijderen van blobs, etc.) voor alle ondertekend services (blob, queue, table, bestand) in die storage-account. U wordt aangeraden met een Account-SAS hierboven wordt beschreven indien mogelijk.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Beperken van toegang toomonitoring-gerelateerde event hubs
Een vergelijkbaar patroon met event hubs kan worden uitgevoerd, maar u moet eerst toocreate een speciale Listen-autorisatieregel. Als u toogrant toegang tooan-toepassing die alleen toolisten toomonitoring-gerelateerde event hubs wilt, Hallo te volgen:

1. Een gedeeld toegangsbeleid maken op Hallo event hub die zijn gemaakt voor streaming bewakingsgegevens met alleen Listen claims. Dit kan worden gedaan in Hallo-portal. Bijvoorbeeld, u mogelijk deze aanroepen 'monitoringReadOnly'. Indien mogelijk, zult u toogive die sleutel rechtstreeks toohello consumer en Hallo volgende stap overslaan.
2. Als Hallo consumer toobe kunnen tooget Hallo sleutel ad-hoc moet, verleent u Hallo Hallo ListKeys in te grijpen voor deze event hub. Dit is ook nodig zijn voor gebruikers die moeten toobe kunnen tooset een diagnostische instelling of meld u profiel toostream tooevent hubs. U kunt bijvoorbeeld een regel RBAC maken:
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over RBAC en machtigingen in Resource Manager](../active-directory/role-based-access-control-what-is.md)
* [Overzicht van de bewaking in Azure Hallo lezen](monitoring-overview.md)

