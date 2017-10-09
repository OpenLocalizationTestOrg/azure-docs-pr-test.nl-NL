---
title: aaaArchive diagnostische Azure-Logboeken | Microsoft Docs
description: Meer informatie over hoe tooarchive uw Azure diagnostische logboeken voor lange bewaartermijn in een opslagaccount.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Azure logboeken met diagnostische gegevens archiveren
In dit artikel wordt gedemonstreerd hoe u kunt gebruiken van hello Azure-portal, PowerShell-Cmdlets, CLI of REST-API tooarchive uw [Azure diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md) in een opslagaccount. Deze optie is handig als u wilt tooretain uw diagnostische met een optionele bewaarbeleid voor controle, statische analyses of back-up Logboeken. Hallo storage-account heeft geen toobe in Hallo hetzelfde abonnement als Hallo resource logboeken verzenden zolang Hallo-gebruiker die Hallo instelling configureert de juiste RBAC toegang tooboth abonnementen heeft.

## <a name="prerequisites"></a>Vereisten
Voordat u begint, moet u deze te[een opslagaccount maken](../storage/storage-create-storage-account.md) toowhich kunt u uw diagnoselogboeken archiveren. Het is raadzaam dat u niet een bestaand opslagaccount met andere, niet-bewaking gegevens die zijn opgeslagen in het gebruikt zodat u toegang tot toomonitoring gegevens beter kunt beheren. Als u ook van uw activiteitenlogboek en diagnostische metrische gegevens tooa storage-account archiveren, deze mogelijk nog wel zin toouse dit opslagaccount voor uw diagnostische ook tookeep alle bewakingsgegevens op een centrale locatie Logboeken. Hallo storage account waarmee u moet een algemeen opslagaccount, niet een blob storage-account.

## <a name="diagnostic-settings"></a>Diagnostische instellingen
tooarchive uw diagnostische logboeken met behulp van een van onderstaande Hallo-methoden, stel een **diagnostische instelling** voor een bepaalde resource. Een diagnostische instelling voor een resource definieert Hallo categorieën van Logboeken en metrische gegevens verzonden tooa doel (storage-account, Event Hubs-naamruimte of Log Analytics). Het definieert ook Hallo bewaarbeleid (aantal dagen tooretain) voor gebeurtenissen van elke categorie logboek en metrische gegevens die zijn opgeslagen in een opslagaccount. Als u een bewaarbeleid toozero instelt, worden gebeurtenissen voor die categorie logboek opgeslagen voor onbepaalde tijd (d.w.z. toosay, permanent). Een bewaarbeleid kan anders zijn voor een willekeurig aantal dagen tussen 1 en 2147483647. [U kunt meer lezen over de diagnostische instellingen hier](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). Bewaarbeleid toegepaste per dag, zodat Hallo einde van een dag (UTC) wordt vastgelegd vanaf Hallo dag dat is nu voorbij Hallo bewaarbeleid worden verwijderd. Bijvoorbeeld, als u had een bewaarbeleid van één dag, worden aan Hallo begin van vandaag de dag voor de Hallo Hallo logboeken van Hallo dag voordat gisteren verwijderd

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Archief diagnostische logboeken met Hallo-portal
1. Navigeer tooAzure Monitor in Hallo-portal en klikt u op **diagnostische instellingen**

    ![Sectie van de Monitor Azure bewaking](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. Eventueel Hallo lijst filteren op resourcegroep of brontype en klik vervolgens op Hallo resource waarvoor u een diagnostische instelling tooset wilt.

3. Als u geen instellingen bestaat op het Hallo-resource die u hebt geselecteerd, bent u na vragen aan gebruiker toocreate een instelling. Klik op "Diagnostische gegevens inschakelen."

   ![Diagnostische instelling - geen bestaande instellingen toevoegen](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   Als er bestaande instellingen op Hallo resource, ziet u een lijst met instellingen die al zijn geconfigureerd op deze resource. Klik op 'Diagnostische instelling toevoegen'.

   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. Geef een naam van de instelling en Hallo selectievakje voor **tooStorage Account exporteren**, selecteert u een opslagaccount. Desgewenst instellen een aantal dagen tooretain deze logboeken via Hallo **bewaartermijn (dagen)** schuifregelaars. Een bewaartermijn van nul dagen Hallo logboeken voor onbepaalde tijd worden opgeslagen.
   
   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Klik op **Opslaan**.

Na enkele ogenblikken Hallo nieuwe instelling wordt weergegeven in de lijst met instellingen voor deze bron en diagnostische logboeken zijn gearchiveerde toothat storage account zodra er nieuwe gebeurtenisgegevens wordt gegenereerd.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Diagnostische logboeken archief via Azure PowerShell
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| ResourceId |Ja |Bron-ID van Hallo resource waarop tooset een diagnostische instelling. |
| StorageAccountId |Nee |Bron-ID van Hallo Opslagaccount toowhich diagnostische logboeken moet worden opgeslagen. |
| Categorieën |Nee |Door komma's gescheiden lijst met logboekbestanden categorieën tooenable. |
| Ingeschakeld |Ja |Een Boolean die aangeeft of diagnostische gegevens zijn ingeschakeld of uitgeschakeld op deze resource. |
| RetentionEnabled |Nee |Een Boolean die aangeeft of een bewaarbeleid zijn ingeschakeld op deze resource. |
| RetentionInDays |Nee |Aantal dagen waarvoor gebeurtenissen moeten worden gehandhaafd tussen 1 en 2147483647. De waarde nul wordt Hallo logboeken voor onbepaalde tijd opgeslagen. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>Diagnostische logboeken via Hallo platformoverschrijdende CLI archief
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| resourceId |Ja |Bron-ID van Hallo resource waarop tooset een diagnostische instelling. |
| storageId |Nee |Bron-ID van Hallo Opslagaccount toowhich diagnostische logboeken moet worden opgeslagen. |
| Categorieën |Nee |Door komma's gescheiden lijst met logboekbestanden categorieën tooenable. |
| ingeschakeld |Ja |Een Boolean die aangeeft of diagnostische gegevens zijn ingeschakeld of uitgeschakeld op deze resource. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Diagnostische logboeken archief via Hallo REST-API
[Dit document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) voor meer informatie over hoe u een diagnostische instelling Hallo Monitor REST-API van Azure kunt instellen.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Schema van diagnostische logboeken in Hallo storage-account
Nadat u hebt ingesteld archivering, wordt een storage-container gemaakt in Hallo storage-account zodra een gebeurtenis optreedt in een Hallo logboek categorieën die u hebt ingeschakeld. Hallo blobs in de container Hallo volgen Hallo dezelfde notatie over diagnostische logboeken en Hallo activiteitenlogboek. Hallo-structuur van deze BLOB's is:

> Insights - logs-{categorie logboeknaam} / resourceId = / ABONNEMENTEN / {abonnements-ID} /RESOURCEGROUPS/ {Resourcegroepnaam} /PROVIDERS/ {resource provider name} / {brontype} / {resourcenaam} / y = {4-cijferige numerieke year} / m = {jaartallen met twee numerieke month} / d = {jaartallen met twee numerieke dag} /h = {jaartallen met twee 24-uurs klok hour}/m=00/PT1H.json
> 
> 

Of eenvoudigweg

> Insights - logs-{categorie logboeknaam} / resourceId = / {resource Id} / y = {4-cijferige numerieke year} / m = {jaartallen met twee numerieke month} / d = {jaartallen met twee numerieke dag} /h = {jaartallen met twee 24-uurs klok hour}/m=00/PT1H.json
> 
> 

Zo mogelijk een blob-naam:

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Elke blob PT1H.json bevat een JSON-blob van gebeurtenissen die hebben plaatsgevonden binnen Hallo uur in Hallo blob-URL opgegeven (bijvoorbeeld, h = 12). Gebeurtenissen zijn toegevoegde toohello PT1H.json bestand tijdens Hallo aanwezig uur, wanneer deze zich voordoen. Hallo minuut waarde (m = 00) is altijd 00, aangezien diagnostische gebeurtenissen worden onderverdeeld in afzonderlijke blobs per uur.

Elke gebeurtenis wordt binnen Hallo PT1H.json bestand opgeslagen in Hallo 'records' array, volgt deze indeling:

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| Elementnaam | Beschrijving |
| --- | --- |
| tijd |Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis. |
| resourceId |Bron-ID van Hallo beïnvloed resource. |
| operationName |Naam van Hallo-bewerking. |
| category |Logboek categorie van Hallo-gebeurtenis. |
| properties |Een set `<Key, Value>` paren (dat wil zeggen woordenboek) Hallo details van gebeurtenis Hallo beschrijven. |

> [!NOTE]
> Hallo-eigenschappen en het gebruik van deze eigenschappen kunnen variëren afhankelijk van Hallo resource.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Blobs voor analyse downloaden](../storage/storage-dotnet-how-to-use-blobs.md)
* [Stroom diagnostische logboeken tooan Event Hubs-naamruimte](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Lees meer over de logboeken met diagnostische gegevens](monitoring-overview-of-diagnostic-logs.md)
