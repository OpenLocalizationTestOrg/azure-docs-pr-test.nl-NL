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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="18cea-103">Hoe toouse Sleutelkluis voorlopig verwijderen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="18cea-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="18cea-104">Azure Key Vault van voorlopige verwijderingen functie kunt herstellen van verwijderde kluizen en objecten van de kluis.</span><span class="sxs-lookup"><span data-stu-id="18cea-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="18cea-105">In het bijzonder voorlopig verwijderen adressen Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="18cea-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="18cea-106">Ondersteuning voor herstelbare verwijdering van een sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="18cea-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="18cea-107">Ondersteuning voor verwijdering van de herstelbare objecten van de sleutelkluis. sleutels, geheimen, en certificaten</span><span class="sxs-lookup"><span data-stu-id="18cea-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18cea-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="18cea-108">Prerequisites</span></span>

- <span data-ttu-id="18cea-109">Azure PowerShell 4.0.0 of later - als u niet dat al ingesteld hebt, Azure PowerShell installeren en deze aan uw Azure-abonnement koppelen, Zie [hoe tooinstall en configureren van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="18cea-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="18cea-110">Er is een verouderde versie van de uitvoer van onze Sleutelkluis PowerShell opmaak bestand dat **kan** in uw omgeving in plaats van de juiste versie Hallo worden geladen.</span><span class="sxs-lookup"><span data-stu-id="18cea-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="18cea-111">We zijn anticiperen op dat een bijgewerkte versie van PowerShell toocontain Hallo correcties nodig voor Hallo uitvoer opmaak en dit onderwerp wordt bijgewerkt op dat moment.</span><span class="sxs-lookup"><span data-stu-id="18cea-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="18cea-112">Hallo huidige tijdelijke oplossing, moet u dit opmaak probleem ondervindt is:</span><span class="sxs-lookup"><span data-stu-id="18cea-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="18cea-113">Gebruik Hallo query volgen als u merkt dat u niet ziet, Hallo voorlopig verwijderen die in dit onderwerp worden beschreven van de eigenschap enabled: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="18cea-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="18cea-114">Zie voor Sleutelkluis refernece voor specifieke informatie voor PowerShell [Azure Key Vault PowerShell-referentie](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="18cea-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="18cea-115">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="18cea-115">Required permissions</span></span>

<span data-ttu-id="18cea-116">Sleutelkluis worden afzonderlijk beheerd via op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC) als volgt:</span><span class="sxs-lookup"><span data-stu-id="18cea-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="18cea-117">Bewerking</span><span class="sxs-lookup"><span data-stu-id="18cea-117">Operation</span></span> | <span data-ttu-id="18cea-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="18cea-118">Description</span></span> | <span data-ttu-id="18cea-119">Machtigingen van gebruiker</span><span class="sxs-lookup"><span data-stu-id="18cea-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="18cea-120">Lijst</span><span class="sxs-lookup"><span data-stu-id="18cea-120">List</span></span>|<span data-ttu-id="18cea-121">Een lijst met sleutelkluizen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="18cea-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="18cea-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="18cea-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="18cea-123">Herstellen</span><span class="sxs-lookup"><span data-stu-id="18cea-123">Recover</span></span>|<span data-ttu-id="18cea-124">Hiermee herstelt u een verwijderde sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="18cea-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="18cea-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="18cea-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="18cea-126">Opschonen</span><span class="sxs-lookup"><span data-stu-id="18cea-126">Purge</span></span>|<span data-ttu-id="18cea-127">Een verwijderde sleutelkluis en alle bijbehorende inhoud verwijderd permanent.</span><span class="sxs-lookup"><span data-stu-id="18cea-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="18cea-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="18cea-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="18cea-129">Zie voor meer informatie over de machtigingen en toegangsbeheer [beveiligen van uw sleutelkluis](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="18cea-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="18cea-130">Inschakelen van voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="18cea-130">Enabling soft-delete</span></span>

<span data-ttu-id="18cea-131">toobe kunnen toorecover een verwijderde sleutelkluis of objecten die zijn opgeslagen in een sleutel-kluis, moet u eerst soft-het verwijderen van die sleutelkluis inschakelen.</span><span class="sxs-lookup"><span data-stu-id="18cea-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="18cea-132">Bestaande sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="18cea-132">Existing key vault</span></span>

<span data-ttu-id="18cea-133">Voor een bestaande sleutelkluis ContosoVault met de naam, moet u voorlopig verwijderen als volgt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="18cea-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="18cea-134">Op dit moment moet u toouse Azure Resource Manager resource manipulatie toodirectly schrijven Hallo *enableSoftDelete* eigenschap toohello Sleutelkluis-resource.</span><span class="sxs-lookup"><span data-stu-id="18cea-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="18cea-135">Nieuwe sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="18cea-135">New key vault</span></span>

<span data-ttu-id="18cea-136">Voorlopig verwijderen voor een nieuwe sleutelkluis inschakelen wordt uitgevoerd tijdens het maken door toe te voegen Hallo voorlopig verwijderen inschakelen vlag tooyour opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="18cea-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="18cea-137">Controleren inschakelen voor voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="18cea-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="18cea-138">tooverify die een sleutelkluis ingeschakeld is, zachte verwijderen uitvoeren Hallo *ophalen* opdracht en zoek naar 'Voorlopig verwijderen Enabled?' Hallo</span><span class="sxs-lookup"><span data-stu-id="18cea-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="18cea-139">kenmerk en de instelling true of false.</span><span class="sxs-lookup"><span data-stu-id="18cea-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="18cea-140">Verwijderen van een sleutelkluis beveiligd door voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="18cea-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="18cea-141">Hallo opdracht toodelete (of verwijderen) blijft een sleutelkluis Hallo dezelfde, maar de gedragswijzigingen afhankelijk van of u hebt ingeschakeld voorlopig verwijderen of niet.</span><span class="sxs-lookup"><span data-stu-id="18cea-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="18cea-142">Als u de vorige opdracht Hallo voor een sleutelkluis die geen voorlopig verwijderen ingeschakeld uitvoert, wordt u deze sleutelkluis en alle bijbehorende inhoud zonder opties voor herstel permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="18cea-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="18cea-143">Hoe voorlopig verwijderen beschermt uw sleutelkluizen</span><span class="sxs-lookup"><span data-stu-id="18cea-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="18cea-144">Ingeschakeld met voorlopig verwijderen:</span><span class="sxs-lookup"><span data-stu-id="18cea-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="18cea-145">Wanneer een sleutelkluis wordt verwijderd, is deze verwijderd uit de resourcegroep en geplaatst in een gereserveerde naamruimte die alleen wordt gekoppeld aan het Hallo-locatie waar ze werden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="18cea-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="18cea-146">Objecten in een verwijderde sleutel kluis, zoals sleutels, geheimen en certificaten, zijn niet toegankelijk en blijven ook wanneer hun insluitende sleutelkluis Hallo verwijderde status heeft.</span><span class="sxs-lookup"><span data-stu-id="18cea-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="18cea-147">Hallo DNS-naam voor een sleutelkluis in een verwijderde status is nog steeds gereserveerd, zodat een nieuwe sleutelkluis met dezelfde naam kan niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="18cea-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="18cea-148">U kunt verwijderde status sleutelkluizen, dat wordt gekoppeld aan uw abonnement bekijken met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="18cea-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="18cea-149">Hallo *Resource-ID* in Hallo uitvoer toohello oorspronkelijke bron-ID van deze kluis verwijst.</span><span class="sxs-lookup"><span data-stu-id="18cea-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="18cea-150">Aangezien deze sleutelkluis nu in een verwijderde staat bevindt is, bestaat er is geen resource met die resource-ID.</span><span class="sxs-lookup"><span data-stu-id="18cea-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="18cea-151">Hallo *Id* het veld mag gebruikte tooidentify Hallo resource als herstellen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="18cea-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="18cea-152">Hallo *opschonen datum gepland* veld geeft aan wanneer Hallo kluis wordt definitief verwijderd (verwijderd) als er geen actie voor deze verwijderde kluis ondernomen.</span><span class="sxs-lookup"><span data-stu-id="18cea-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="18cea-153">Hallo standaard bewaren periode, gebruikte toocalculate hello *opschonen datum gepland*, is 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="18cea-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="18cea-154">Een sleutelkluis herstellen</span><span class="sxs-lookup"><span data-stu-id="18cea-154">Recovering a key vault</span></span>

<span data-ttu-id="18cea-155">een sleutelkluis toorecover, moet u toospecify hello sleutelkluisnaam, de resourcegroep en locatie.</span><span class="sxs-lookup"><span data-stu-id="18cea-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="18cea-156">Houd er rekening mee Hallo locatie en de resourcegroep Hallo van sleutelkluis Hallo verwijderd als u deze voor het herstelproces van een sleutelkluis nodig.</span><span class="sxs-lookup"><span data-stu-id="18cea-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="18cea-157">Een sleutelkluis is hersteld, Hallo resultaat is een nieuwe resource met Hallo sleutelkluis de oorspronkelijke bron-ID.</span><span class="sxs-lookup"><span data-stu-id="18cea-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="18cea-158">Als de resourcegroep Hallo waar Hallo sleutelkluis bestond is verwijderd, moet een nieuwe resourcegroep met dezelfde naam worden gemaakt voordat de sleutelkluis Hallo kan worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="18cea-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="18cea-159">Sleutelkluis-objecten en voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="18cea-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="18cea-160">Voor een sleutel 'ContosoFirstKey' in een sleutelkluis met de naam 'ContosoVault' met voorlopig verwijderen ingeschakeld, hier van wilt hoe u verwijderen die sleutel.</span><span class="sxs-lookup"><span data-stu-id="18cea-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="18cea-161">Aan de sleutelkluis is ingeschakeld voor voorlopig verwijderen, weergegeven een verwijderde sleutel nog steeds zoals deze wordt verwijderd, behalve, wanneer u expliciet aanbiedt of verwijderde sleutels ophalen.</span><span class="sxs-lookup"><span data-stu-id="18cea-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="18cea-162">De meeste bewerkingen voor een sleutel in Hallo verwijderd status mislukt met uitzondering van de aanbieding een verwijderde sleutel, herstellen of leegmaakt.</span><span class="sxs-lookup"><span data-stu-id="18cea-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="18cea-163">Bijvoorbeeld: toorequest toolist verwijderd sleutels in een sleutelkluis Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="18cea-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="18cea-164">Transitiestatus</span><span class="sxs-lookup"><span data-stu-id="18cea-164">Transition state</span></span> 

<span data-ttu-id="18cea-165">Wanneer u een sleutel in een sleutelkluis met de soft-delete is ingeschakeld verwijderen, wordt het duurt een paar seconden Hallo overgang toocomplete.</span><span class="sxs-lookup"><span data-stu-id="18cea-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="18cea-166">Tijdens deze transitiestatus deze kan worden weergegeven die Hallo-sleutel niet in Hallo active of Hallo verwijderde staat.</span><span class="sxs-lookup"><span data-stu-id="18cea-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="18cea-167">Met deze opdracht wordt een lijst alle verwijderde sleutels in de sleutelkluis met de naam 'ContosoVault'.</span><span class="sxs-lookup"><span data-stu-id="18cea-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="18cea-168">Voorlopig verwijderen gebruiken met sleutelkluis-objecten</span><span class="sxs-lookup"><span data-stu-id="18cea-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="18cea-169">Net zoals sleutelkluizen, een verwijderde sleutel geheim of certificaat blijft in verwijderde staat bevindt voor too90 dagen tenzij u deze herstellen of het opschonen.</span><span class="sxs-lookup"><span data-stu-id="18cea-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="18cea-170">Sleutels</span><span class="sxs-lookup"><span data-stu-id="18cea-170">Keys</span></span>

<span data-ttu-id="18cea-171">een verwijderde sleutel toorecover:</span><span class="sxs-lookup"><span data-stu-id="18cea-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="18cea-172">toopermanently een sleutel verwijderen:</span><span class="sxs-lookup"><span data-stu-id="18cea-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="18cea-173">Bezig met het verwijderen van een sleutel wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="18cea-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="18cea-174">Hallo **herstellen** en **opschonen** acties hebben hun eigen machtigingen die zijn gekoppeld in een sleutelkluis-beleid.</span><span class="sxs-lookup"><span data-stu-id="18cea-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="18cea-175">Voor een gebruiker of service principal toobe kunnen tooexecute een **herstellen** of **opschonen** ze gemachtigd Hallo respectieve voor dat object (sleutel of geheim) in Hallo sleutelkluis-beleid in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="18cea-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="18cea-176">Standaard Hallo **opschonen** machtiging tooa key vault-beleid niet is toegevoegd als Hallo 'all' snelkoppeling gebruikte toogrant tooa alle machtigingen van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="18cea-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="18cea-177">U moet expliciet verlenen **opschonen** machtiging.</span><span class="sxs-lookup"><span data-stu-id="18cea-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="18cea-178">Bijvoorbeeld, Hallo opdracht verleent na user@contoso.com machtiging tooperform verschillende bewerkingen voor sleutels in *ContosoVault* inclusief **opschonen**.</span><span class="sxs-lookup"><span data-stu-id="18cea-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="18cea-179">Beleid voor sleutelkluis toegang instellen</span><span class="sxs-lookup"><span data-stu-id="18cea-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="18cea-180">Als u een bestaande sleutelkluis die ingeschakeld voor voorlopig verwijderen NET heeft hebt, hebt u geen **herstellen** en **opschonen** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="18cea-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="18cea-181">Geheimen</span><span class="sxs-lookup"><span data-stu-id="18cea-181">Secrets</span></span>

<span data-ttu-id="18cea-182">Zoals sleutels, worden geheimen in een sleutelkluis met hun eigen opdrachten beheerd op.</span><span class="sxs-lookup"><span data-stu-id="18cea-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="18cea-183">Te volgen, zijn Hallo-opdrachten voor het verwijderen van, aanbieden, herstellen en geheimen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="18cea-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="18cea-184">Een geheim dat met de naam SQLPassword verwijderen:</span><span class="sxs-lookup"><span data-stu-id="18cea-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="18cea-185">Lijst van alle verwijderde geheimen in een sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="18cea-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="18cea-186">Een geheim Hallo verwijderd status herstellen:</span><span class="sxs-lookup"><span data-stu-id="18cea-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="18cea-187">Opschonen van een geheim in verwijderde staat bevindt:</span><span class="sxs-lookup"><span data-stu-id="18cea-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="18cea-188">Bezig met het verwijderen van een geheim wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="18cea-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="18cea-189">Hiervoor en sleutel kluizen</span><span class="sxs-lookup"><span data-stu-id="18cea-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="18cea-190">Sleutelkluis-objecten</span><span class="sxs-lookup"><span data-stu-id="18cea-190">Key vault objects</span></span>

<span data-ttu-id="18cea-191">Opruimen van een sleutel wordt geheim of certificaat permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="18cea-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="18cea-192">Hallo-sleutelkluis die Hallo verwijderd object bevat echter blijven behouden als alle andere objecten in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="18cea-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="18cea-193">Sleutel-kluizen als containers</span><span class="sxs-lookup"><span data-stu-id="18cea-193">Key vaults as containers</span></span>
<span data-ttu-id="18cea-194">Wanneer een sleutelkluis is opgeschoond, worden alle inhoud, met inbegrip van sleutels, geheimen en certificaten, permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="18cea-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="18cea-195">een sleutelkluis toopurge gebruiken Hallo `Remove-AzureRmKeyVault` opdracht met de optie Hallo `-InRemovedState` en door te geven Hallo-locatie van de sleutelkluis Hallo verwijderd met Hallo `-Location location` argument.</span><span class="sxs-lookup"><span data-stu-id="18cea-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="18cea-196">U vindt Hallo-locatie van een verwijderde kluis met Hallo opdracht `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="18cea-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="18cea-197">Bezig met het verwijderen van een sleutelkluis wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="18cea-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="18cea-198">Opschonen van de vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="18cea-198">Purge permissions required</span></span>
- <span data-ttu-id="18cea-199">een verwijderde sleutelkluis toopurge, zodat het Hallo-kluis en alle bijbehorende inhoud permanent worden verwijderd, Hallo gebruiker RBAC-machtiging tooperform moet een *Microsoft.KeyVault/locations/deletedVaults/purge/action* bewerking.</span><span class="sxs-lookup"><span data-stu-id="18cea-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="18cea-200">toolist hello verwijderd sleutel Hallo kluis een gebruiker moet RBAC-machtiging tooperform *Microsoft.KeyVault/deletedVaults/read* machtiging.</span><span class="sxs-lookup"><span data-stu-id="18cea-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="18cea-201">Alleen de abonnementsbeheerder van een heeft standaard deze machtigingen.</span><span class="sxs-lookup"><span data-stu-id="18cea-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="18cea-202">Geplande opschonen</span><span class="sxs-lookup"><span data-stu-id="18cea-202">Scheduled purge</span></span>

<span data-ttu-id="18cea-203">Uw sleutelkluis verwijderde objecten weergeven geeft aan wanneer ze schedled toobe Sleutelkluis opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="18cea-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="18cea-204">Hallo *opschonen datum gepland* veld geeft aan wanneer een object van de sleutelkluis, worden definitief verwijderd, als er geen actie ondernomen.</span><span class="sxs-lookup"><span data-stu-id="18cea-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="18cea-205">Hallo bewaarperiode voor een object verwijderde sleutelkluis is standaard 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="18cea-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="18cea-206">Een object opgeschoonde kluis, geactiveerd door de *opschonen datum gepland* veld, wordt definitief verwijderd.</span><span class="sxs-lookup"><span data-stu-id="18cea-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="18cea-207">Het is niet hersteld.</span><span class="sxs-lookup"><span data-stu-id="18cea-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="18cea-208">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="18cea-208">Other resources</span></span>

- <span data-ttu-id="18cea-209">Zie voor een overzicht van de Sleutelkluis voorlopig verwijderen functie [overzicht van Azure Sleutelkluis voorlopig verwijderen](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="18cea-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="18cea-210">Zie voor een algemeen overzicht van Azure Sleutelkluis gebruik [aan de slag met Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="18cea-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

