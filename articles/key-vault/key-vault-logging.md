---
title: Logboekregistratie van Sleutelkluis aaaAzure | Microsoft Docs
description: Gebruik deze zelfstudie toohelp die u aan de slag met Azure Key Vault logboekregistratie.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Logboekregistratie van Azure Sleutelkluis
Azure Sleutelkluis is beschikbaar in de meeste regio's. Zie voor meer informatie, Hallo [pagina prijzen van Sleutelkluis](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Inleiding
Wanneer u een of meer sleutelkluizen hebt gemaakt, wilt u waarschijnlijk toomonitor hoe en wanneer uw sleutel kluizen toegankelijk zijn en door wie. U kunt dit doen door logboekregistratie in te schakelen voor Sleutelkluis. Hierbij wordt de informatie opgeslagen in een Azure-opslagaccount dat u opgeeft. Er wordt automatisch een nieuwe container met de naam **insights-logboeken-auditevent** gemaakt voor het opgegeven opslagaccount en u kunt hetzelfde opslagaccount gebruiken voor het verzamelen van logboeken voor meerdere sleutelkluizen.

U kunt uw logboekgegevens maximaal openen, 10 minuten nadat de Hallo sleutel sleutelkluisbewerking is uitgevoerd. In de meeste gevallen gaat het echter veel sneller.  Het is tooyou toomanage uw logboeken in uw opslagaccount:

* Gebruik standaard Azure access control methoden toosecure uw logboeken door te beperken wie er toegang toe.
* Logboeken die u niet meer tookeep in uw opslagaccount wilt verwijderen.

Gebruik deze zelfstudie toohelp die u aan de slag met Azure Key Vault aan te melden, toocreate uw storage-account inschakelen van logboekregistratie en interpreteren Hallo logboekgegevens die worden verzameld.  

> [!NOTE]
> Deze zelfstudie bevat geen instructies voor hoe toocreate sleutel kluizen, sleutels of geheimen. Zie [Aan de slag met Azure Key Vault](key-vault-get-started.md) voor meer informatie. Zie [deze equivalente zelfstudie](key-vault-manage-with-cli2.md) voor instructies voor het maken van een platformonafhankelijke opdrachtregelinterface.
>
> U kunt op dit moment is Azure Sleutelkluis in hello Azure-portal configureren. Gebruik in plaats daarvan deze instructies voor Azure PowerShell.
>
>

Zie [Wat is Azure Key Vault?](key-vault-whatis.md) voor algemene informatie over Azure Key Vault.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie hebt u hello te volgen:

* Een bestaande sleutelkluis die u hebt gebruikt.  
* Azure PowerShell, **versie 1.0.1 of hoger**. tooinstall Azure PowerShell en deze koppelen aan uw Azure-abonnement, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). Als u Azure PowerShell al hebt geïnstalleerd en het Hallo-versie van hello Azure PowerShell-console niet weet, typt u `(Get-Module azure -ListAvailable).Version`.  
* Voldoende opslagruimte op Azure voor uw Sleutelkluis-logboeken.

## <a id="connect"></a>Verbinding maken met tooyour abonnementen
Start een Azure PowerShell-sessie en meld u aan tooyour Azure-account met de volgende opdracht Hallo:  

    Login-AzureRmAccount

In het pop-browservenster hello, Voer uw Azure-account, gebruikersnaam en wachtwoord. Azure PowerShell haalt alle Hallo-abonnementen die gekoppeld aan dit account en standaard zijn, gebruikt de eerste Hallo.

Als u meerdere abonnementen hebt, moet u wellicht toospecify een specifiek abonnement dat gebruikt toocreate is uw Azure Sleutelkluis. Type Hallo toosee Hallo abonnementen voor uw account te volgen:

    Get-AzureRmSubscription

Vervolgens toospecify Hallo abonnement is gekoppeld aan de sleutelkluis die u logboekregistratie inschakelen wilt, type:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> Dit is een belangrijke stap, die met name handig is als er meerdere abonnementen zijn gekoppeld aan uw account. U krijgt een fout tooregister Microsoft.Insights als deze stap overgeslagen.
>   
>

Zie voor meer informatie over het configureren van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a id="storage"></a>Een nieuw opslagaccount voor uw logboeken maken
Hoewel u een bestaand opslagaccount voor uw Logboeken gebruiken kunt, maakt een nieuw opslagaccount die toegewezen tooKey kluis logboeken worden. Voor het gemak wanneer we toospecify dit hebt later Hallo details hebt opgeslagen in een variabele met de naam **sa**.

Voor extra beheer te vereenvoudigen, gebruiken we Hallo van dezelfde resourcegroep als een bestand met onze sleutelkluis Hallo. Van Hallo [zelfstudie aan de slag](key-vault-get-started.md), deze resourcegroep de naam **ContosoResourceGroup** en we toouse Hallo Oost-Azië locatie. Vervang deze waarden voor uzelf, indien van toepassing:

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Als u een bestaand opslagaccount toouse beslist, moet hiervoor hetzelfde abonnement Hallo als uw sleutelkluis en deze Hallo Resource Manager-implementatiemodel, in plaats van Hallo klassieke implementatiemodel gebruiken moeten.
>
>

## <a id="identify"></a>Hallo sleutelkluis voor uw logboeken identificeren
In onze zelfstudie aan de slag is de naam van onze sleutelkluis **ContosoKeyVault**, zodat we toouse die een naam Hallo details opslaan in een variabele met de naam ook **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Logboekregistratie inschakelen
tooenable logboekregistratie voor Sleutelkluis, gebruiken we de cmdlet Set-AzureRmDiagnosticSetting hello, samen met de Hallo variabelen die we voor ons nieuwe opslagaccount en onze sleutelkluis hebt gemaakt. We ook Hallo hebt ingesteld **-ingeschakeld** te markeren**$true** en stel Hallo categorie tooAuditEvent (Hallo enige categorie voor logboekregistratie van Sleutelkluis):

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

Hallo-uitvoer hiervoor bevat:

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Hiermee bevestigt u dat logboekregistratie nu is ingeschakeld voor uw sleutelkluis, het opslaan van informatie tooyour storage-account.

U kunt eventueel ook een retentiebeleid instellen voor uw logboeken, zodat oudere logboeken automatisch worden verwijderd. Bijvoorbeeld ingesteld bewaren beleid met **- RetentionEnabled** te markeren**$true** en stel **- RetentionInDays** parameter te**90** zodat dat Logboeken ouder is dan 90 dagen automatisch worden verwijderd.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

Wat wordt in het logboek vastgelegd?

* Alle geverifieerde REST-API-aanvragen worden vastgelegd, ook mislukte aanvragen als gevolg van toegangsmachtigingen, systeemfouten of ongeldige aanvragen.
* Bewerkingen op Hallo sleutel sleutelkluis zelf, waaronder het maken, verwijderen, instelling toegangsbeleid voor sleutelkluizen, en bijwerken van de kenmerken, zoals tags.
* Bewerkingen voor sleutels en geheimen in Hallo sleutelkluis, waaronder maken, wijzigen of verwijderen van deze sleutels of geheimen; bewerkingen zoals het ondertekenen, controleren, versleutelen, ontsleutelen, Inpakken en uitpakken van sleutels, geheimen, lijst met sleutels en geheimen en hun versies ophalen.
* Niet-geverifieerde aanvragen die in een 401-respons resulteren. Dit zijn bijvoorbeeld aanvragen die geen Bearer-token hebben, ongeldige of verlopen aanvragen of aanvragen met een ongeldig token.  

## <a id="access"></a>Toegang tot uw logboeken
Sleutelkluis-logboeken worden opgeslagen in Hallo **insights-logs-auditevent** container in Hallo storage-account u hebt opgegeven. toolist alle Hallo blobs in deze container, typt u:

Maak eerst een variabele voor naam van de container Hallo. Deze wordt gebruikt in de rest Hallo van Hallo doorlopen.

    $container = 'insights-logs-auditevent'

toolist alle Hallo blobs in deze container, typt u:

    Get-AzureStorageBlob -Container $container -Context $sa.Context
Hallo-uitvoer ziet er iets dergelijks toothis:

**Container-URI: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Naam**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Als u in deze uitvoer zien kunt, Hallo blobs de volgende naamgevingsregels: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**

de datum- en tijdwaarden Hallo gebruik UTC.

Omdat hello hetzelfde opslagaccount kan gebruikte toocollect logboeken voor meerdere resources, is hello volledige resource-ID in de blob-naam Hallo zeer nuttig tooaccess of download alleen Hallo blobs die u nodig hebt. Maar voordat we dat doen, eerst aan bod hoe toodownload alle blobs Hallo.

Maak een map toodownload Hallo eerst blobs. Bijvoorbeeld:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

Haal vervolgens een lijst met alle blobs op:  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Sluis deze lijst via 'Get-AzureStorageBlobContent' toodownload Hallo blobs in de doelmap:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

Wanneer u deze tweede opdracht uitvoert, Hallo  **/**  scheidingsteken in Hallo blobnamen een volledige mapstructuur onder de doelmap Hallo maken en deze structuur worden gebruikte toodownload en store Hallo blobs als bestanden.

tooselectively blobs downloaden, jokertekens gebruiken. Bijvoorbeeld:

* Als u meerdere sleutelkluizen hebt en toodownload logboeken voor slechts één sleutelkluis wilt instellen, met de naam CONTOSOKEYVAULT3:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Als u meerdere resourcegroepen hebt en toodownload logboeken voor slechts één resourcegroep wilt instellen, gebruikt u `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Als u alle Hallo logboeken toodownload Hallo maand januari 2016 wilt, gebruik `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

U bent nu klaar toostart kijken wat is er in Hallo registreert. Maar eerst die twee parameters voor Get-AzureRmDiagnosticSetting tooknow moet mogelijk:

* tooquery hello status van diagnostische instellingen voor uw sleutelkluisresource:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* toodisable logboekregistratie in voor uw sleutelkluisresource:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>De Sleutelkluis-logboekgegevens interpreteren
Afzonderlijke blobs worden opgeslagen als tekst, die is opgemaakt als een JSON-blob. Dit is een voorbeeld van een logboekvermelding van het uitvoeren van `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Hallo volgende tabel bevat Hallo veldnamen en beschrijvingen.

| Veldnaam | Beschrijving |
| --- | --- |
| tijd |Datum en tijd (UTC). |
| resourceId |Azure Resource Manager-resource-id. Voor Sleutelkluis-Logboeken is dit altijd Hallo Sleutelkluis bron-ID. |
| operationName |Naam van het Hallo-bewerking, zoals beschreven in de volgende tabel Hallo. |
| operationVersion |Dit is Hallo REST-API-versie door Hallo-client wordt aangevraagd. |
| category |Voor Sleutelkluis-Logboeken is AuditEvent Hallo enige beschikbare waarde. |
| resultType |Resultaat van de REST-API-aanvraag. |
| resultSignature |HTTP-status. |
| resultDescription |Extra beschrijving van Hallo resultaat, indien beschikbaar. |
| durationMs |De tijd die nodig tooservice Hallo REST-API-aanvraag in milliseconden was. Dit omvat geen Hallo netwerklatentie, zodat u aan de clientzijde Hallo meten Hallo-tijd mogelijk niet overeenkomt met deze tijd. |
| callerIpAddress |IP-adres van Hallo-client die Hallo-aanvraag heeft ingediend. |
| correlationId |Een optionele GUID die client Hallo kunt toocorrelate doorgeven aan de clientzijde logboeken met servicezijde (Sleutelkluis-) Logboeken. |
| identity |De identiteit van de Hallo-token dat is opgegeven bij het maken van Hallo REST-API-aanvraag. Dit is meestal user, service principal of een combinatie user+ appId, bijvoorbeeld bij een aanvraag via een Azure PowerShell-cmdlet. |
| properties |Dit veld bevat verschillende gegevens op basis van het Hallo-bewerking (operationName). In de meeste gevallen bevat informatie over de client (Hallo useragent-tekenreeks doorgegeven door de client Hallo), Hallo exacte REST-API aanvraag-URI en HTTP-statuscode. Bovendien wanneer een object wordt geretourneerd als gevolg van een aanvraag (bijvoorbeeld KeyCreate of VaultGet) bevat ook Hallo Key URI (als 'id'), Vault URI of Secret URI. |

Hallo **operationName** veldwaarden hebben de ObjectVerb-indeling. Bijvoorbeeld:

* Alle sleutelkluisbewerkingen hebben Hallo ' kluis`<action>`'-indeling, zoals `VaultGet` en `VaultCreate`.
* Alle sleutelbewerkingen hebben Hallo ' sleutel`<action>`'-indeling, zoals `KeySign` en `KeyList`.
* Alle geheime bewerkingen hebben Hallo ' geheim`<action>`'-indeling, zoals `SecretGet` en `SecretListVersions`.

Hallo volgende tabel geeft een lijst Hallo operationName en de bijbehorende REST-API-opdracht.

| operationName | REST-API-opdracht |
| --- | --- |
| Authentication |Via het Azure Active Directory-eindpunt |
| VaultGet |[Informatie over een sleutelkluis ophalen](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Een sleutelkluis maken of bijwerken](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Een sleutelkluis verwijderen](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Een sleutelkluis bijwerken](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Alle sleutelkluizen in een resourcegroep weergeven](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Een sleutel maken](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Informatie over een sleutel ophalen](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Een sleutel in een kluis importeren](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Back-up maken van een sleutel](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx). |
| KeyDelete |[Een sleutel verwijderen](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Een sleutel herstellen](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Aanmelden met een sleutel](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Verifiëren met een sleutel](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Een sleutel inpakken](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Een sleutel uitpakken](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Versleutelen met een sleutel](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Ontsleutelen met een sleutel](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Een sleutel bijwerken](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Lijst Hallo sleutels in een kluis](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Lijst Hallo versies van een sleutel](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Een geheim maken](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Een geheim ophalen](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Een geheim bijwerken](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Een geheim verwijderen](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Geheimen in een kluis weergeven](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Versies van een geheim weergeven](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Log Analytics gebruiken

U kunt hello Azure Key Vault oplossing gebruiken in logboekanalyse tooreview die Azure Key Vault AuditEvent registreert. Voor meer informatie, inclusief hoe tooset, Zie [oplossing voor Azure Sleutelkluis in logboekanalyse](../log-analytics/log-analytics-azure-key-vault.md). In dit artikel bevat ook instructies als u nodig hebt toomigrate van het oude Sleutelkluis oplossing hello, die wordt aangeboden tijdens Hallo logboekanalyse preview, waarbij u eerst gerouteerd uw logboeken tooan Azure Storage-account en Log Analytics tooread van daaruit geconfigureerd.

## <a id="next"></a>Volgende stappen
Zie [Azure Key Vault in een webtoepassing gebruiken](key-vault-use-from-web-application.md) voor een zelfstudie over het gebruik van Azure Key Vault in een webtoepassing.

Zie voor het programmeren van verwijzingen [Hallo ontwikkelaarshandleiding Azure Key Vault](key-vault-developers-guide.md).

Zie [Cmdlets voor Azure Sleutelkluis](/powershell/module/azurerm.keyvault/#key_vault) voor een lijst met Azure PowerShell 1.0- cmdlets voor Azure Sleutelkluis.

Zie voor een zelfstudie over de sleutel worden gedraaid en logboek controle met Azure Sleutelkluis, [hoe toosetup Sleutelkluis met einde tooend sleutel worden gedraaid en controle](key-vault-key-rotation-log-monitoring.md).
