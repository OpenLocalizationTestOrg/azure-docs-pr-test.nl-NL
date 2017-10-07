---
ms.assetid: 
title: 'aaaAzure Key Vault: hoe toouse voorlopig verwijderen met PowerShell'
description: Case voorbeelden van voorlopig verwijderen gebruiken met PowerShell codefragmenten
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>Hoe toouse Sleutelkluis voorlopig verwijderen met PowerShell

Azure Key Vault van voorlopige verwijderingen functie kunt herstellen van verwijderde kluizen en objecten van de kluis. In het bijzonder voorlopig verwijderen adressen Hallo volgen scenario's:

- Ondersteuning voor herstelbare verwijdering van een sleutelkluis
- Ondersteuning voor verwijdering van de herstelbare objecten van de sleutelkluis. sleutels, geheimen, en certificaten

## <a name="prerequisites"></a>Vereisten

- Azure PowerShell 4.0.0 of later - als u niet dat al ingesteld hebt, Azure PowerShell installeren en deze aan uw Azure-abonnement koppelen, Zie [hoe tooinstall en configureren van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> Er is een verouderde versie van de uitvoer van onze Sleutelkluis PowerShell opmaak bestand dat **kan** in uw omgeving in plaats van de juiste versie Hallo worden geladen. We zijn anticiperen op dat een bijgewerkte versie van PowerShell toocontain Hallo correcties nodig voor Hallo uitvoer opmaak en dit onderwerp wordt bijgewerkt op dat moment. Hallo huidige tijdelijke oplossing, moet u dit opmaak probleem ondervindt is:
> - Gebruik Hallo query volgen als u merkt dat u niet ziet, Hallo voorlopig verwijderen die in dit onderwerp worden beschreven van de eigenschap enabled: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Zie voor Sleutelkluis refernece voor specifieke informatie voor PowerShell [Azure Key Vault PowerShell-referentie](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

## <a name="required-permissions"></a>Vereiste machtigingen

Sleutelkluis worden afzonderlijk beheerd via op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC) als volgt:

| Bewerking | Beschrijving | Machtigingen van gebruiker |
|:--|:--|:--|
|Lijst|Een lijst met sleutelkluizen verwijderd.|Microsoft.KeyVault/deletedVaults/read|
|Herstellen|Hiermee herstelt u een verwijderde sleutelkluis.|Microsoft.KeyVault/vaults/write|
|Opschonen|Een verwijderde sleutelkluis en alle bijbehorende inhoud verwijderd permanent.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Zie voor meer informatie over de machtigingen en toegangsbeheer [beveiligen van uw sleutelkluis](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Inschakelen van voorlopig verwijderen

toobe kunnen toorecover een verwijderde sleutelkluis of objecten die zijn opgeslagen in een sleutel-kluis, moet u eerst soft-het verwijderen van die sleutelkluis inschakelen.

### <a name="existing-key-vault"></a>Bestaande sleutelkluis

Voor een bestaande sleutelkluis ContosoVault met de naam, moet u voorlopig verwijderen als volgt inschakelen. 

>[!NOTE]
>Op dit moment moet u toouse Azure Resource Manager resource manipulatie toodirectly schrijven Hallo *enableSoftDelete* eigenschap toohello Sleutelkluis-resource.

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Nieuwe sleutelkluis

Voorlopig verwijderen voor een nieuwe sleutelkluis inschakelen wordt uitgevoerd tijdens het maken door toe te voegen Hallo voorlopig verwijderen inschakelen vlag tooyour opdracht maken.

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Controleren inschakelen voor voorlopig verwijderen

tooverify die een sleutelkluis ingeschakeld is, zachte verwijderen uitvoeren Hallo *ophalen* opdracht en zoek naar 'Voorlopig verwijderen Enabled?' Hallo kenmerk en de instelling true of false.

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Verwijderen van een sleutelkluis beveiligd door voorlopig verwijderen

Hallo opdracht toodelete (of verwijderen) blijft een sleutelkluis Hallo dezelfde, maar de gedragswijzigingen afhankelijk van of u hebt ingeschakeld voorlopig verwijderen of niet.

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>Als u de vorige opdracht Hallo voor een sleutelkluis die geen voorlopig verwijderen ingeschakeld uitvoert, wordt u deze sleutelkluis en alle bijbehorende inhoud zonder opties voor herstel permanent verwijderd.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Hoe voorlopig verwijderen beschermt uw sleutelkluizen

Ingeschakeld met voorlopig verwijderen:

- Wanneer een sleutelkluis wordt verwijderd, is deze verwijderd uit de resourcegroep en geplaatst in een gereserveerde naamruimte die alleen wordt gekoppeld aan het Hallo-locatie waar ze werden gemaakt. 
- Objecten in een verwijderde sleutel kluis, zoals sleutels, geheimen en certificaten, zijn niet toegankelijk en blijven ook wanneer hun insluitende sleutelkluis Hallo verwijderde status heeft. 
- Hallo DNS-naam voor een sleutelkluis in een verwijderde status is nog steeds gereserveerd, zodat een nieuwe sleutelkluis met dezelfde naam kan niet worden gemaakt.  

U kunt verwijderde status sleutelkluizen, dat wordt gekoppeld aan uw abonnement bekijken met behulp van de volgende opdracht Hallo:

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

Hallo *Resource-ID* in Hallo uitvoer toohello oorspronkelijke bron-ID van deze kluis verwijst. Aangezien deze sleutelkluis nu in een verwijderde staat bevindt is, bestaat er is geen resource met die resource-ID. Hallo *Id* het veld mag gebruikte tooidentify Hallo resource als herstellen of verwijderen. Hallo *opschonen datum gepland* veld geeft aan wanneer Hallo kluis wordt definitief verwijderd (verwijderd) als er geen actie voor deze verwijderde kluis ondernomen. Hallo standaard bewaren periode, gebruikte toocalculate hello *opschonen datum gepland*, is 90 dagen.

## <a name="recovering-a-key-vault"></a>Een sleutelkluis herstellen

een sleutelkluis toorecover, moet u toospecify hello sleutelkluisnaam, de resourcegroep en locatie. Houd er rekening mee Hallo locatie en de resourcegroep Hallo van sleutelkluis Hallo verwijderd als u deze voor het herstelproces van een sleutelkluis nodig.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

Een sleutelkluis is hersteld, Hallo resultaat is een nieuwe resource met Hallo sleutelkluis de oorspronkelijke bron-ID. Als de resourcegroep Hallo waar Hallo sleutelkluis bestond is verwijderd, moet een nieuwe resourcegroep met dezelfde naam worden gemaakt voordat de sleutelkluis Hallo kan worden hersteld.

## <a name="key-vault-objects-and-soft-delete"></a>Sleutelkluis-objecten en voorlopig verwijderen

Voor een sleutel 'ContosoFirstKey' in een sleutelkluis met de naam 'ContosoVault' met voorlopig verwijderen ingeschakeld, hier van wilt hoe u verwijderen die sleutel.

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

Aan de sleutelkluis is ingeschakeld voor voorlopig verwijderen, weergegeven een verwijderde sleutel nog steeds zoals deze wordt verwijderd, behalve, wanneer u expliciet aanbiedt of verwijderde sleutels ophalen. De meeste bewerkingen voor een sleutel in Hallo verwijderd status mislukt met uitzondering van de aanbieding een verwijderde sleutel, herstellen of leegmaakt. 

Bijvoorbeeld: toorequest toolist verwijderd sleutels in een sleutelkluis Hallo volgende opdracht gebruiken:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>Transitiestatus 

Wanneer u een sleutel in een sleutelkluis met de soft-delete is ingeschakeld verwijderen, wordt het duurt een paar seconden Hallo overgang toocomplete. Tijdens deze transitiestatus deze kan worden weergegeven die Hallo-sleutel niet in Hallo active of Hallo verwijderde staat. Met deze opdracht wordt een lijst alle verwijderde sleutels in de sleutelkluis met de naam 'ContosoVault'.

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Voorlopig verwijderen gebruiken met sleutelkluis-objecten

Net zoals sleutelkluizen, een verwijderde sleutel geheim of certificaat blijft in verwijderde staat bevindt voor too90 dagen tenzij u deze herstellen of het opschonen. 

#### <a name="keys"></a>Sleutels

een verwijderde sleutel toorecover:

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently een sleutel verwijderen:

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>Bezig met het verwijderen van een sleutel wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.

Hallo **herstellen** en **opschonen** acties hebben hun eigen machtigingen die zijn gekoppeld in een sleutelkluis-beleid. Voor een gebruiker of service principal toobe kunnen tooexecute een **herstellen** of **opschonen** ze gemachtigd Hallo respectieve voor dat object (sleutel of geheim) in Hallo sleutelkluis-beleid in te grijpen. Standaard Hallo **opschonen** machtiging tooa key vault-beleid niet is toegevoegd als Hallo 'all' snelkoppeling gebruikte toogrant tooa alle machtigingen van gebruiker. U moet expliciet verlenen **opschonen** machtiging. Bijvoorbeeld, Hallo opdracht verleent na user@contoso.com machtiging tooperform verschillende bewerkingen voor sleutels in *ContosoVault* inclusief **opschonen**.

#### <a name="set-a-key-vault-access-policy"></a>Beleid voor sleutelkluis toegang instellen

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Als u een bestaande sleutelkluis die ingeschakeld voor voorlopig verwijderen NET heeft hebt, hebt u geen **herstellen** en **opschonen** machtigingen.

#### <a name="secrets"></a>Geheimen

Zoals sleutels, worden geheimen in een sleutelkluis met hun eigen opdrachten beheerd op. Te volgen, zijn Hallo-opdrachten voor het verwijderen van, aanbieden, herstellen en geheimen verwijderen.

- Een geheim dat met de naam SQLPassword verwijderen: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Lijst van alle verwijderde geheimen in een sleutelkluis: 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Een geheim Hallo verwijderd status herstellen: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Opschonen van een geheim in verwijderde staat bevindt: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>Bezig met het verwijderen van een geheim wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.

## <a name="purging-and-key-vaults"></a>Hiervoor en sleutel kluizen

### <a name="key-vault-objects"></a>Sleutelkluis-objecten

Opruimen van een sleutel wordt geheim of certificaat permanent verwijderd, wat betekent dat deze kan niet worden hersteld. Hallo-sleutelkluis die Hallo verwijderd object bevat echter blijven behouden als alle andere objecten in de sleutelkluis Hallo. 

### <a name="key-vaults-as-containers"></a>Sleutel-kluizen als containers
Wanneer een sleutelkluis is opgeschoond, worden alle inhoud, met inbegrip van sleutels, geheimen en certificaten, permanent verwijderd. een sleutelkluis toopurge gebruiken Hallo `Remove-AzureRmKeyVault` opdracht met de optie Hallo `-InRemovedState` en door te geven Hallo-locatie van de sleutelkluis Hallo verwijderd met Hallo `-Location location` argument. U vindt Hallo-locatie van een verwijderde kluis met Hallo opdracht `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
>Bezig met het verwijderen van een sleutelkluis wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.

### <a name="purge-permissions-required"></a>Opschonen van de vereiste machtigingen
- een verwijderde sleutelkluis toopurge, zodat het Hallo-kluis en alle bijbehorende inhoud permanent worden verwijderd, Hallo gebruiker RBAC-machtiging tooperform moet een *Microsoft.KeyVault/locations/deletedVaults/purge/action* bewerking. 
- toolist hello verwijderd sleutel Hallo kluis een gebruiker moet RBAC-machtiging tooperform *Microsoft.KeyVault/deletedVaults/read* machtiging. 
- Alleen de abonnementsbeheerder van een heeft standaard deze machtigingen. 

### <a name="scheduled-purge"></a>Geplande opschonen

Uw sleutelkluis verwijderde objecten weergeven geeft aan wanneer ze schedled toobe Sleutelkluis opgeschoond. Hallo *opschonen datum gepland* veld geeft aan wanneer een object van de sleutelkluis, worden definitief verwijderd, als er geen actie ondernomen. Hallo bewaarperiode voor een object verwijderde sleutelkluis is standaard 90 dagen.

>[!NOTE]
>Een object opgeschoonde kluis, geactiveerd door de *opschonen datum gepland* veld, wordt definitief verwijderd. Het is niet hersteld.

## <a name="other-resources"></a>Meer informatie

- Zie voor een overzicht van de Sleutelkluis voorlopig verwijderen functie [overzicht van Azure Sleutelkluis voorlopig verwijderen](key-vault-ovw-soft-delete.md).
- Zie voor een algemeen overzicht van Azure Sleutelkluis gebruik [aan de slag met Azure Key Vault](key-vault-get-started.md).

