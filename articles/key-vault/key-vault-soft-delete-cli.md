---
ms.assetid: 
title: aaaAzure Key Vault - hoe toouse voorlopig verwijderen met CLI
description: Case voorbeelden van voorlopig verwijderen gebruiken met CLI codefragmenten
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a>Hoe toouse Sleutelkluis voorlopig verwijderen met CLI

Azure Key Vault van voorlopige verwijderingen functie kunt herstellen van verwijderde kluizen en objecten van de kluis. In het bijzonder voorlopig verwijderen adressen Hallo volgen scenario's:

- Ondersteuning voor herstelbare verwijdering van een sleutelkluis
- Ondersteuning voor verwijdering van de herstelbare objecten van de sleutelkluis. sleutels, geheimen, en certificaten

## <a name="prerequisites"></a>Vereisten

- Azure CLI 2.0 - als u deze instelling niet voor uw omgeving hebt, Zie [Key Vault beheren met CLI 2.0](key-vault-manage-with-cli2.md).

Zie voor Sleutelkluis specifieke informatie voor CLI [Azure CLI 2.0 Sleutelkluis verwijzing](https://docs.microsoft.com/cli/azure/keyvault).

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

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a>Nieuwe sleutelkluis

Voorlopig verwijderen voor een nieuwe sleutelkluis inschakelen wordt uitgevoerd tijdens het maken door toe te voegen Hallo voorlopig verwijderen inschakelen vlag tooyour opdracht maken.

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a>Controleren inschakelen voor voorlopig verwijderen

tooverify die een sleutelkluis ingeschakeld is, zachte verwijderen uitvoeren Hallo *weergeven* opdracht en zoek naar 'Voorlopig verwijderen Enabled?' Hallo kenmerk en de instelling true of false.

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Verwijderen van een sleutelkluis beveiligd door voorlopig verwijderen

Hallo opdracht toodelete (of verwijderen) blijft een sleutelkluis Hallo dezelfde, maar de gedragswijzigingen afhankelijk van of u hebt ingeschakeld voorlopig verwijderen of niet.

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
>Als u de vorige opdracht Hallo voor een sleutelkluis die geen voorlopig verwijderen ingeschakeld uitvoert, wordt u deze sleutelkluis en alle bijbehorende inhoud zonder opties voor herstel permanent verwijderd.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Hoe voorlopig verwijderen beschermt uw sleutelkluizen

Ingeschakeld met voorlopig verwijderen:

- Wanneer een sleutelkluis wordt verwijderd, is deze verwijderd uit de resourcegroep en geplaatst in een gereserveerde naamruimte die alleen wordt gekoppeld aan het Hallo-locatie waar ze werden gemaakt. 
- Objecten in een verwijderde sleutel kluis, zoals sleutels, geheimen en certificaten, zijn niet toegankelijk en blijven ook wanneer hun insluitende sleutelkluis Hallo verwijderde status heeft. 
- Hallo DNS-naam voor een sleutelkluis in een verwijderde status is nog steeds gereserveerd, zodat een nieuwe sleutelkluis met dezelfde naam kan niet worden gemaakt.  

U kunt verwijderde status sleutelkluizen, dat wordt gekoppeld aan uw abonnement bekijken met behulp van de volgende opdracht Hallo:

```azurecli
az keyvault list-deleted
```

Hallo *Resource-ID* in Hallo uitvoer toohello oorspronkelijke bron-ID van deze kluis verwijst. Aangezien deze sleutelkluis nu in een verwijderde staat bevindt is, bestaat er is geen resource met die resource-ID. Hallo *Id* het veld mag gebruikte tooidentify Hallo resource als herstellen of verwijderen. Hallo *opschonen datum gepland* veld geeft aan wanneer Hallo kluis wordt definitief verwijderd (verwijderd) als er geen actie voor deze verwijderde kluis ondernomen. Hallo standaard bewaren periode, gebruikte toocalculate hello *opschonen datum gepland*, is 90 dagen.

## <a name="recovering-a-key-vault"></a>Een sleutelkluis herstellen

een sleutelkluis toorecover, moet u toospecify hello sleutelkluisnaam, de resourcegroep en locatie. Houd er rekening mee Hallo locatie en de resourcegroep Hallo van sleutelkluis Hallo verwijderd als u deze voor het herstelproces van een sleutelkluis nodig.

```azurecli
az keyvault recover --location westus --name ContosoVault
```

Een sleutelkluis is hersteld, Hallo resultaat is een nieuwe resource met Hallo sleutelkluis de oorspronkelijke bron-ID. Als de resourcegroep Hallo waar Hallo sleutelkluis bestond is verwijderd, moet een nieuwe resourcegroep met dezelfde naam worden gemaakt voordat de sleutelkluis Hallo kan worden hersteld.

## <a name="key-vault-objects-and-soft-delete"></a>Sleutelkluis-objecten en voorlopig verwijderen

Voor een sleutel 'ContosoFirstKey' in een sleutelkluis met de naam 'ContosoVault' met voorlopig verwijderen ingeschakeld, hier van wilt hoe u verwijderen die sleutel.

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

Aan de sleutelkluis is ingeschakeld voor voorlopig verwijderen, weergegeven een verwijderde sleutel nog steeds zoals deze wordt verwijderd, behalve, wanneer u expliciet aanbiedt of verwijderde sleutels ophalen. De meeste bewerkingen voor een sleutel in Hallo verwijderd status mislukt met uitzondering van de aanbieding een verwijderde sleutel, herstellen of leegmaakt. 

Bijvoorbeeld: toorequest toolist verwijderd sleutels in een sleutelkluis Hallo volgende opdracht gebruiken:

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a>Transitiestatus 

Wanneer u een sleutel in een sleutelkluis met de soft-delete is ingeschakeld verwijderen, wordt het duurt een paar seconden Hallo overgang toocomplete. Tijdens deze transitiestatus deze kan worden weergegeven die Hallo-sleutel niet in Hallo active of Hallo verwijderde staat. Met deze opdracht wordt een lijst alle verwijderde sleutels in de sleutelkluis met de naam 'ContosoVault'.

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Voorlopig verwijderen gebruiken met sleutelkluis-objecten

Net zoals sleutelkluizen, een verwijderde sleutel geheim of certificaat blijft in verwijderde staat bevindt voor too90 dagen tenzij u deze herstellen of het opschonen. 

#### <a name="keys"></a>Sleutels

een verwijderde sleutel toorecover:

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

toopermanently een sleutel verwijderen:

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
>Bezig met het verwijderen van een sleutel wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.

Hallo **herstellen** en **opschonen** acties hebben hun eigen machtigingen die zijn gekoppeld in een sleutelkluis-beleid. Voor een gebruiker of service principal toobe kunnen tooexecute een **herstellen** of **opschonen** ze gemachtigd Hallo respectieve voor dat object (sleutel of geheim) in Hallo sleutelkluis-beleid in te grijpen. Standaard Hallo **opschonen** machtiging tooa key vault-beleid niet is toegevoegd als Hallo 'all' snelkoppeling gebruikte toogrant tooa alle machtigingen van gebruiker. U moet expliciet verlenen **opschonen** machtiging. Bijvoorbeeld, Hallo opdracht verleent na user@contoso.com machtiging tooperform verschillende bewerkingen voor sleutels in *ContosoVault* inclusief **opschonen**.

#### <a name="set-a-key-vault-access-policy"></a>Beleid voor sleutelkluis toegang instellen

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> Als u een bestaande sleutelkluis die ingeschakeld voor voorlopig verwijderen NET heeft hebt, hebt u geen **herstellen** en **opschonen** machtigingen.

#### <a name="secrets"></a>Geheimen

Zoals sleutels, worden geheimen in een sleutelkluis met hun eigen opdrachten beheerd op. Te volgen, zijn Hallo-opdrachten voor het verwijderen van, aanbieden, herstellen en geheimen verwijderen.

- Een geheim dat met de naam SQLPassword verwijderen: 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- Lijst van alle verwijderde geheimen in een sleutelkluis: 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- Een geheim Hallo verwijderd status herstellen: 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- Opschonen van een geheim in verwijderde staat bevindt: 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
>Bezig met het verwijderen van een geheim wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.

## <a name="purging-and-key-vaults"></a>Hiervoor en sleutel kluizen

### <a name="key-vault-objects"></a>Sleutelkluis-objecten

Opruimen van een sleutel wordt geheim of certificaat permanent verwijderd, wat betekent dat deze kan niet worden hersteld. Hallo-sleutelkluis die Hallo verwijderd object bevat echter blijven behouden als alle andere objecten in de sleutelkluis Hallo. 

### <a name="key-vaults-as-containers"></a>Sleutel-kluizen als containers
Wanneer een sleutelkluis is opgeschoond, worden alle inhoud, met inbegrip van sleutels, geheimen en certificaten, permanent verwijderd. een sleutelkluis toopurge gebruiken Hallo `az keyvault purge` opdracht. U kunt zoeken naar Hallo locatie van uw abonnement verwijderd sleutelkluizen met Hallo opdracht `az keyvault list-deleted`.

```azurecli
az keyvault purge --location westus --name ContosoVault
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

