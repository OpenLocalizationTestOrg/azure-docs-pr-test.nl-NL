---
title: aaaArchive hello Azure Activity Log | Microsoft Docs
description: Meer informatie over hoe tooarchive uw Azure-activiteit zich aanmelden voor lange bewaartermijn in een opslagaccount.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Archief hello Azure Activity Log
In dit artikel, laten we zien hoe u kunt hello Azure-portal, PowerShell-Cmdlets of platformoverschrijdende CLI tooarchive uw [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) in een opslagaccount. Deze optie is handig als u tooretain langer is dan 90 dagen (met volledige controle over het bewaarbeleid Hallo) voor uw activiteitenlogboek controleren wilt, statische analysis of back-up. Als u alleen tooretain hoeft hoeft uw gebeurtenissen gedurende 90 dagen of minder u niet tooset up archivering tooa storage-account, omdat het activiteitenlogboek gebeurtenissen worden behouden in hello Azure-platform gedurende 90 dagen zonder in te schakelen archivering.

## <a name="prerequisites"></a>Vereisten
Voordat u begint, moet u deze te[een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich kunt u uw activiteitenlogboek archiveren. Het is raadzaam dat u niet een bestaand opslagaccount met andere, niet-bewaking gegevens die zijn opgeslagen in het gebruikt zodat u toegang tot toomonitoring gegevens beter kunt beheren. Als u ook van diagnostische logboeken en metrische gegevens tooa storage-account archiveren, deze mogelijk nog wel zin toouse die storage-account voor de activiteit zich ook tookeep alle bewakingsgegevens op een centrale locatie. Hallo storage account waarmee u moet een algemeen opslagaccount, niet een blob storage-account. Hallo storage-account heeft geen toobe in Hallo hetzelfde abonnement als Hallo abonnement logboeken verzenden zolang Hallo-gebruiker die Hallo instelling configureert de juiste RBAC toegang tooboth abonnementen heeft.

## <a name="log-profile"></a>Logboek-profiel
tooarchive Hallo activiteitenlogboek met behulp van een van onderstaande Hallo-methoden, u stelt Hallo **logboek profiel** voor een abonnement. Hallo logboek profiel definieert Hallo-type van gebeurtenissen die zijn opgeslagen of gestreamd en uitvoer Hallo-storage-account en/of event hub. Het definieert ook Hallo bewaarbeleid (aantal dagen tooretain) voor gebeurtenissen die zijn opgeslagen in een opslagaccount. Als het bewaarbeleid Hallo is toozero ingesteld, worden gebeurtenissen voor onbepaalde tijd opgeslagen. Anders wordt kan deze worden ingesteld tooany waarde tussen 1 en 2147483647. Bewaarbeleid toegepaste per dag, zodat Hallo einde van een dag (UTC) wordt vastgelegd vanaf Hallo dag dat is nu voorbij Hallo bewaarbeleid worden verwijderd. Bijvoorbeeld, als u had een bewaarbeleid van één dag, zou aan Hallo begin van vandaag de dag voor de Hallo Hallo logboeken van Hallo dag voordat gisteren worden verwijderd. [U kunt meer lezen over log profielen hier](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>Archief Hallo activiteitenlogboek met Hallo-portal
1. Klik in het Hallo-portal op Hallo **activiteitenlogboek** koppeling op Hallo aan de linkerkant navigatie. Als u een koppeling voor Hallo activiteitenlogboek niet ziet, klikt u op Hallo **meer Services** eerst koppelen.
   
    ![Navigeer tooActivity logboek-blade](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. Klik boven Hallo van Hallo-blade op **exporteren**.
   
    ![Klik op de knop exporteren Hallo](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. Hallo-blade die wordt weergegeven, selectievakje Hallo voor **tooa opslagaccount exporteren** en selecteer een opslagaccount.
   
    ![Een opslagaccount instellen](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. Hallo schuifregelaar of in het tekstvak, definieert een aantal dagen waarvoor activiteitenlogboek gebeurtenissen moeten worden opgeslagen in uw opslagaccount. Als u liever toohave die uw gegevens voor onbepaalde tijd bewaard in Hallo storage-account, stelt u dit nummer toozero.
5. Klik op **Opslaan**.

## <a name="archive-hello-activity-log-via-powershell"></a>Hallo activiteitenlogboek via PowerShell archiveren
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| StorageAccountId |Nee |Bron-ID van Hallo Opslagaccount toowhich activiteitenlogboeken moet worden opgeslagen. |
| Locaties |Ja |Door komma's gescheiden lijst met regio's waarvoor u toocollect activiteitenlogboek gebeurtenissen wilt. U kunt een lijst weergeven met alle regio's [via deze pagina](https://azure.microsoft.com/en-us/regions) of met behulp van [hello Azure Management REST-API](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Ja |Aantal dagen voor welke gebeurtenissen worden bewaard, tussen 1 en 2147483647. Een waarde van nul Hallo logboeken voor onbepaalde tijd opgeslagen (permanent). |
| Categorieën |Ja |Door komma's gescheiden lijst met categorieën van gebeurtenissen die moeten worden verzameld. Mogelijke waarden zijn schrijven, verwijderen en in te grijpen. |

## <a name="archive-hello-activity-log-via-cli"></a>Hallo activiteitenlogboek via CLI archiveren
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| naam |Ja |Naam van uw logboek-profiel. |
| storageId |Nee |Bron-ID van Hallo Opslagaccount toowhich activiteitenlogboeken moet worden opgeslagen. |
| Locaties |Ja |Door komma's gescheiden lijst met regio's waarvoor u toocollect activiteitenlogboek gebeurtenissen wilt. U kunt een lijst weergeven met alle regio's [via deze pagina](https://azure.microsoft.com/en-us/regions) of met behulp van [hello Azure Management REST-API](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Ja |Aantal dagen voor welke gebeurtenissen worden bewaard, tussen 1 en 2147483647. De waarde nul wordt Hallo logboeken voor onbepaalde tijd worden opgeslagen (permanent). |
| Categorieën |Ja |Door komma's gescheiden lijst met categorieën van gebeurtenissen die moeten worden verzameld. Mogelijke waarden zijn schrijven, verwijderen en in te grijpen. |

## <a name="storage-schema-of-hello-activity-log"></a>Schema van de opslag van Hallo Activity Log
Nadat u hebt ingesteld archivering, wordt een opslagcontainer gemaakt in Hallo storage-account zodra een activiteitenlogboek gebeurtenis plaatsvindt. Hallo blobs in de container Hallo Volg Hallo dezelfde notatie op Hallo activiteitenlogboek en diagnostische logboeken. Hallo-structuur van deze BLOB's is:

> Insights-operationele-logboeken/name = standaard/resourceId = / ABONNEMENTEN / {abonnements-ID} / y = {4-cijferige numerieke year} / m = {jaartallen met twee numerieke month} / d = {jaartallen met twee numerieke dag} /h = {jaartallen met twee 24-uurs klok hour}/m=00/PT1H.json
> 
> 

Zo mogelijk een blob-naam:

> Insights-Operational-Logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.JSON
> 
> 

Elke blob PT1H.json bevat een JSON-blob van gebeurtenissen die hebben plaatsgevonden binnen Hallo uur in Hallo blob-URL opgegeven (bijvoorbeeld h = 12). Gebeurtenissen zijn toegevoegde toohello PT1H.json bestand tijdens Hallo aanwezig uur, wanneer deze zich voordoen. Hallo minuut waarde (m = 00) is altijd 00, omdat het activiteitenlogboek gebeurtenissen worden onderverdeeld in afzonderlijke blobs per uur.

Elke gebeurtenis wordt binnen Hallo PT1H.json bestand opgeslagen in Hallo 'records' array, volgt deze indeling:

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
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
| category |Categorie van Hallo actie, bijvoorbeeld. Schrijven, lezen, in te grijpen. |
| resultType |Hallo type Hallo leiden bv. Geslaagd, mislukt, Start |
| resultSignature |Afhankelijk van het brontype Hallo. |
| durationMs |Duur van de bewerking Hallo in milliseconden |
| callerIpAddress |IP-adres van Hallo-gebruiker die is uitgevoerd op het Hallo-bewerking, UPN-claim of SPN claim op basis van beschikbaarheid. |
| correlationId |Meestal een GUID in de indeling van tekenreeks Hallo. Gebeurtenissen die een correlationId delen behoren toohello dezelfde uber actie. |
| identity |JSON-blob met een beschrijving van Hallo autorisatie en claims. |
| Autorisatie |De BLOB van eigenschappen van gebeurtenis Hallo RBAC. Omvat gewoonlijk Hallo 'action', 'rol' en 'bereik' Eigenschappen. |
| niveau |Niveau van het Hallo-gebeurtenis. Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose' |
| location |De regio op welke locatie Hallo opgetreden (of globale). |
| properties |Een set `<Key, Value>` paren (dat wil zeggen woordenboek) Hallo details van gebeurtenis Hallo beschrijven. |

> [!NOTE]
> Hallo-eigenschappen en het gebruik van deze eigenschappen kunnen variëren afhankelijk van Hallo resource.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Blobs voor analyse downloaden](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Hallo activiteitenlogboek tooEvent Hubs Stream](monitoring-stream-activity-logs-event-hubs.md)
* [Lees meer over Hallo Activity Log](monitoring-overview-activity-logs.md)

