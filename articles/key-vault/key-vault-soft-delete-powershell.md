---
ms.assetid: 
title: Azure Sleutelkluis - voorlopig verwijderen gebruiken met PowerShell
description: Case voorbeelden van voorlopig verwijderen gebruiken met PowerShell codefragmenten
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 8cf0674f7eb139e50da4a3c22a8d8376a86b0dcc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="cefd4-103">Sleutelkluis voorlopig verwijderen gebruiken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="cefd4-103">How to use Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="cefd4-104">Azure Key Vault van voorlopige verwijderingen functie kunt herstellen van verwijderde kluizen en objecten van de kluis.</span><span class="sxs-lookup"><span data-stu-id="cefd4-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="cefd4-105">In het bijzonder voorlopig verwijderen adressen van de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="cefd4-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="cefd4-106">Ondersteuning voor herstelbare verwijdering van een sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="cefd4-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="cefd4-107">Ondersteuning voor verwijdering van de herstelbare objecten van de sleutelkluis. sleutels, geheimen, en certificaten</span><span class="sxs-lookup"><span data-stu-id="cefd4-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cefd4-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cefd4-108">Prerequisites</span></span>

- <span data-ttu-id="cefd4-109">Azure PowerShell 4.0.0 of later - als u niet dat al ingesteld hebt, Azure PowerShell installeren en deze aan uw Azure-abonnement koppelen, Zie [installeren en configureren van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cefd4-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="cefd4-110">Er is een verouderde versie van de uitvoer van onze Sleutelkluis PowerShell opmaak bestand dat **kan** in uw omgeving in plaats van de juiste versie worden geladen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span></span> <span data-ttu-id="cefd4-111">We zijn anticiperen op een bijgewerkte versie van PowerShell om te kunnen bevatten de benodigde correcties voor de uitvoer-opmaak en dit onderwerp wordt bijgewerkt op dat moment.</span><span class="sxs-lookup"><span data-stu-id="cefd4-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span></span> <span data-ttu-id="cefd4-112">De huidige oplossing, moet u dit probleem zich voordoet opmaak, is:</span><span class="sxs-lookup"><span data-stu-id="cefd4-112">The current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="cefd4-113">Gebruik de volgende query uit als u merkt dat u niet ziet, de soft-verwijderen in dit onderwerp beschreven van de eigenschap enabled: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="cefd4-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="cefd4-114">Zie voor Sleutelkluis refernece voor specifieke informatie voor PowerShell [Azure Key Vault PowerShell-referentie](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="cefd4-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="cefd4-115">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="cefd4-115">Required permissions</span></span>

<span data-ttu-id="cefd4-116">Sleutelkluis worden afzonderlijk beheerd via op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC) als volgt:</span><span class="sxs-lookup"><span data-stu-id="cefd4-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="cefd4-117">Bewerking</span><span class="sxs-lookup"><span data-stu-id="cefd4-117">Operation</span></span> | <span data-ttu-id="cefd4-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cefd4-118">Description</span></span> | <span data-ttu-id="cefd4-119">Machtigingen van gebruiker</span><span class="sxs-lookup"><span data-stu-id="cefd4-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="cefd4-120">Lijst</span><span class="sxs-lookup"><span data-stu-id="cefd4-120">List</span></span>|<span data-ttu-id="cefd4-121">Een lijst met sleutelkluizen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cefd4-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="cefd4-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="cefd4-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="cefd4-123">Herstellen</span><span class="sxs-lookup"><span data-stu-id="cefd4-123">Recover</span></span>|<span data-ttu-id="cefd4-124">Hiermee herstelt u een verwijderde sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="cefd4-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="cefd4-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="cefd4-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="cefd4-126">Opschonen</span><span class="sxs-lookup"><span data-stu-id="cefd4-126">Purge</span></span>|<span data-ttu-id="cefd4-127">Een verwijderde sleutelkluis en alle bijbehorende inhoud verwijderd permanent.</span><span class="sxs-lookup"><span data-stu-id="cefd4-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="cefd4-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="cefd4-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="cefd4-129">Zie voor meer informatie over de machtigingen en toegangsbeheer [beveiligen van uw sleutelkluis](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="cefd4-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="cefd4-130">Inschakelen van voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="cefd4-130">Enabling soft-delete</span></span>

<span data-ttu-id="cefd4-131">Als u een verwijderde sleutelkluis of objecten die zijn opgeslagen in een sleutelkluis herstellen, moet u eerst de soft-het verwijderen van die sleutelkluis inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="cefd4-132">Bestaande sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="cefd4-132">Existing key vault</span></span>

<span data-ttu-id="cefd4-133">Voor een bestaande sleutelkluis ContosoVault met de naam, moet u voorlopig verwijderen als volgt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="cefd4-134">Op dit moment moet u met Azure Resource Manager resource manipulatie rechtstreeks schrijft de *enableSoftDelete* eigenschap aan de Sleutelkluis-resource.</span><span class="sxs-lookup"><span data-stu-id="cefd4-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="cefd4-135">Nieuwe sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="cefd4-135">New key vault</span></span>

<span data-ttu-id="cefd4-136">Voorlopig verwijderen voor een nieuwe sleutelkluis inschakelen tijdens het maken wordt gedaan door toe te voegen de vlag voorlopig verwijderen inschakelen voor uw opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="cefd4-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="cefd4-137">Controleren inschakelen voor voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="cefd4-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="cefd4-138">Om te controleren of er een sleutelkluis voorlopig verwijderen ingeschakeld is, voer de *ophalen* opdracht en zoekt u de 'voorlopig verwijderen Enabled?'</span><span class="sxs-lookup"><span data-stu-id="cefd4-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="cefd4-139">kenmerk en de instelling true of false.</span><span class="sxs-lookup"><span data-stu-id="cefd4-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="cefd4-140">Verwijderen van een sleutelkluis beveiligd door voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="cefd4-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="cefd4-141">De opdracht uit om een sleutelkluis verwijderen (of verwijderen) hetzelfde is gebleven, maar het gedrag verandert, afhankelijk van of u voorlopig verwijderen of niet hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cefd4-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="cefd4-142">Als u de vorige opdracht voor een sleutelkluis die geen voorlopig verwijderen ingeschakeld uitvoert, wordt u deze sleutelkluis en alle bijbehorende inhoud zonder opties voor herstel permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cefd4-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="cefd4-143">Hoe voorlopig verwijderen beschermt uw sleutelkluizen</span><span class="sxs-lookup"><span data-stu-id="cefd4-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="cefd4-144">Ingeschakeld met voorlopig verwijderen:</span><span class="sxs-lookup"><span data-stu-id="cefd4-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="cefd4-145">Wanneer een sleutelkluis wordt verwijderd, is deze verwijderd uit de resourcegroep en geplaatst in een gereserveerde naamruimte die alleen wordt gekoppeld aan de locatie waar ze werden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cefd4-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="cefd4-146">Objecten in een verwijderde sleutel kluis, zoals sleutels, geheimen en certificaten, zijn niet toegankelijk en blijven ook terwijl hun insluitende sleutelkluis de status verwijderd heeft wordt.</span><span class="sxs-lookup"><span data-stu-id="cefd4-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="cefd4-147">De DNS-naam voor een sleutelkluis in een verwijderde status is nog steeds gereserveerd, zodat een nieuwe sleutelkluis met dezelfde naam kan niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cefd4-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="cefd4-148">U kunt verwijderde status sleutelkluizen, dat wordt gekoppeld aan uw abonnement weergeven met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cefd4-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

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

<span data-ttu-id="cefd4-149">De *Resource-ID* verwijst in de uitvoer naar de oorspronkelijke bron-ID van deze kluis.</span><span class="sxs-lookup"><span data-stu-id="cefd4-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="cefd4-150">Aangezien deze sleutelkluis nu in een verwijderde staat bevindt is, bestaat er is geen resource met die resource-ID.</span><span class="sxs-lookup"><span data-stu-id="cefd4-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="cefd4-151">De *Id* veld kan worden gebruikt voor het identificeren van de resource als herstellen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-151">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="cefd4-152">De *opschonen datum gepland* veld geeft aan wanneer de kluis wordt definitief verwijderd (verwijderd) als er geen actie voor deze verwijderde kluis ondernomen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="cefd4-153">De bewaartermijn gebruikt voor het berekenen van de *opschonen datum gepland*, is 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="cefd4-154">Een sleutelkluis herstellen</span><span class="sxs-lookup"><span data-stu-id="cefd4-154">Recovering a key vault</span></span>

<span data-ttu-id="cefd4-155">Om te herstellen een sleutelkluis, moet u de naam van de sleutelkluis, resourcegroep en locatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="cefd4-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="cefd4-156">Noteer de locatie en de resourcegroep van de verwijderde sleutelkluis als u deze voor het herstelproces van een sleutelkluis nodig.</span><span class="sxs-lookup"><span data-stu-id="cefd4-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="cefd4-157">Wanneer een sleutelkluis is hersteld, is het resultaat een nieuwe resource met de sleutelkluis oorspronkelijke bron-ID.</span><span class="sxs-lookup"><span data-stu-id="cefd4-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="cefd4-158">Als de resourcegroep waar de sleutelkluis bestond is verwijderd, moet een nieuwe resourcegroep met dezelfde naam worden gemaakt voordat de sleutelkluis kan worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="cefd4-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="cefd4-159">Sleutelkluis-objecten en voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="cefd4-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="cefd4-160">Voor een sleutel 'ContosoFirstKey' in een sleutelkluis met de naam 'ContosoVault' met voorlopig verwijderen ingeschakeld, hier van wilt hoe u verwijderen die sleutel.</span><span class="sxs-lookup"><span data-stu-id="cefd4-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="cefd4-161">Aan de sleutelkluis is ingeschakeld voor voorlopig verwijderen, weergegeven een verwijderde sleutel nog steeds zoals deze wordt verwijderd, behalve, wanneer u expliciet aanbiedt of verwijderde sleutels ophalen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="cefd4-162">De meeste bewerkingen voor een sleutel in de status verwijderd heeft mislukt met uitzondering van de aanbieding een verwijderde sleutel, herstellen of leegmaakt.</span><span class="sxs-lookup"><span data-stu-id="cefd4-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="cefd4-163">Bijvoorbeeld, om aan te vragen tot sleutels van de lijst verwijderd in een sleutelkluis, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cefd4-163">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="cefd4-164">Transitiestatus</span><span class="sxs-lookup"><span data-stu-id="cefd4-164">Transition state</span></span> 

<span data-ttu-id="cefd4-165">Wanneer u een sleutel in een sleutelkluis met de soft-delete is ingeschakeld verwijderen, wordt het duurt een paar seconden voor de overgang te voltooien.</span><span class="sxs-lookup"><span data-stu-id="cefd4-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="cefd4-166">Tijdens deze transitiestatus zal verschijnen de sleutel is niet in de actieve status of de status verwijderd heeft.</span><span class="sxs-lookup"><span data-stu-id="cefd4-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="cefd4-167">Met deze opdracht wordt een lijst alle verwijderde sleutels in de sleutelkluis met de naam 'ContosoVault'.</span><span class="sxs-lookup"><span data-stu-id="cefd4-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="cefd4-168">Voorlopig verwijderen gebruiken met sleutelkluis-objecten</span><span class="sxs-lookup"><span data-stu-id="cefd4-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="cefd4-169">Net zoals sleutelkluizen, een verwijderde sleutel geheim of certificaat blijft in verwijderde staat bevindt voor maximaal 90 dagen tenzij u deze herstellen of het opschonen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="cefd4-170">Sleutels</span><span class="sxs-lookup"><span data-stu-id="cefd4-170">Keys</span></span>

<span data-ttu-id="cefd4-171">Een verwijderde sleutel herstellen:</span><span class="sxs-lookup"><span data-stu-id="cefd4-171">To recover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="cefd4-172">Een sleutel permanent verwijderen:</span><span class="sxs-lookup"><span data-stu-id="cefd4-172">To permanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="cefd4-173">Bezig met het verwijderen van een sleutel wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="cefd4-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="cefd4-174">De **herstellen** en **opschonen** acties hebben hun eigen machtigingen die zijn gekoppeld in een sleutelkluis-beleid.</span><span class="sxs-lookup"><span data-stu-id="cefd4-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="cefd4-175">Voor een gebruiker of service-principal te kunnen uitvoeren een **herstellen** of **opschonen** actie ze gemachtigd bent de respectieve voor dat object (sleutel of geheim) in het toegangsbeleid van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="cefd4-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="cefd4-176">Standaard de **opschonen** machtiging is niet toegevoegd aan een sleutelkluis toegangsbeleid wanneer de snelkoppeling 'all' wordt gebruikt voor alle machtigingen verlenen aan een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cefd4-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="cefd4-177">U moet expliciet verlenen **opschonen** machtiging.</span><span class="sxs-lookup"><span data-stu-id="cefd4-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="cefd4-178">De volgende opdracht bijvoorbeeld verleent user@contoso.com toestemming voor het uitvoeren van verschillende bewerkingen voor sleutels in *ContosoVault* inclusief **opschonen**.</span><span class="sxs-lookup"><span data-stu-id="cefd4-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="cefd4-179">Beleid voor sleutelkluis toegang instellen</span><span class="sxs-lookup"><span data-stu-id="cefd4-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="cefd4-180">Als u een bestaande sleutelkluis die ingeschakeld voor voorlopig verwijderen NET heeft hebt, hebt u geen **herstellen** en **opschonen** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="cefd4-181">Geheimen</span><span class="sxs-lookup"><span data-stu-id="cefd4-181">Secrets</span></span>

<span data-ttu-id="cefd4-182">Zoals sleutels, worden geheimen in een sleutelkluis met hun eigen opdrachten beheerd op.</span><span class="sxs-lookup"><span data-stu-id="cefd4-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="cefd4-183">Te volgen, zijn de opdrachten voor het verwijderen van, aanbieden, herstellen en geheimen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="cefd4-184">Een geheim dat met de naam SQLPassword verwijderen:</span><span class="sxs-lookup"><span data-stu-id="cefd4-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="cefd4-185">Lijst van alle verwijderde geheimen in een sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="cefd4-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="cefd4-186">Een geheim in de status verwijderd heeft herstellen:</span><span class="sxs-lookup"><span data-stu-id="cefd4-186">Recover a secret in the deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="cefd4-187">Opschonen van een geheim in verwijderde staat bevindt:</span><span class="sxs-lookup"><span data-stu-id="cefd4-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="cefd4-188">Bezig met het verwijderen van een geheim wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="cefd4-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="cefd4-189">Hiervoor en sleutel kluizen</span><span class="sxs-lookup"><span data-stu-id="cefd4-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="cefd4-190">Sleutelkluis-objecten</span><span class="sxs-lookup"><span data-stu-id="cefd4-190">Key vault objects</span></span>

<span data-ttu-id="cefd4-191">Opruimen van een sleutel wordt geheim of certificaat permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="cefd4-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="cefd4-192">De sleutelkluis die deel uitmaakt van het verwijderde object echter blijven behouden als alle andere objecten in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="cefd4-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="cefd4-193">Sleutel-kluizen als containers</span><span class="sxs-lookup"><span data-stu-id="cefd4-193">Key vaults as containers</span></span>
<span data-ttu-id="cefd4-194">Wanneer een sleutelkluis is opgeschoond, worden alle inhoud, met inbegrip van sleutels, geheimen en certificaten, permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cefd4-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="cefd4-195">Als u wilt een sleutelkluis verwijderen, gebruikt u de `Remove-AzureRmKeyVault` opdracht met de optie `-InRemovedState` en op te geven van de locatie van de verwijderde sleutelkluis met de `-Location location` argument.</span><span class="sxs-lookup"><span data-stu-id="cefd4-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span></span> <span data-ttu-id="cefd4-196">U vindt de locatie van een verwijderde kluis met de opdracht `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="cefd4-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="cefd4-197">Bezig met het verwijderen van een sleutelkluis wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="cefd4-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="cefd4-198">Opschonen van de vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="cefd4-198">Purge permissions required</span></span>
- <span data-ttu-id="cefd4-199">Als u wilt verwijderen een verwijderde sleutelkluis, zodat de kluis en alle bijbehorende inhoud permanent worden verwijderd, moet de gebruiker RBAC-machtiging voor het uitvoeren van een *Microsoft.KeyVault/locations/deletedVaults/purge/action* bewerking.</span><span class="sxs-lookup"><span data-stu-id="cefd4-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="cefd4-200">Als de verwijderde sleutel wilt weergeven, de kluis van een gebruiker RBAC heeft toestemming nodig om uit te voeren *Microsoft.KeyVault/deletedVaults/read* machtiging.</span><span class="sxs-lookup"><span data-stu-id="cefd4-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="cefd4-201">Alleen de abonnementsbeheerder van een heeft standaard deze machtigingen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="cefd4-202">Geplande opschonen</span><span class="sxs-lookup"><span data-stu-id="cefd4-202">Scheduled purge</span></span>

<span data-ttu-id="cefd4-203">Uw sleutelkluis verwijderde objecten weergeven geeft aan wanneer ze schedled worden opgeschoond door Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="cefd4-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="cefd4-204">De *opschonen datum gepland* veld geeft aan wanneer een object van de sleutelkluis, worden definitief verwijderd, als er geen actie ondernomen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="cefd4-205">De bewaarperiode voor een verwijderde sleutelkluis-object is standaard 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="cefd4-205">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="cefd4-206">Een object opgeschoonde kluis, geactiveerd door de *opschonen datum gepland* veld, wordt definitief verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cefd4-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="cefd4-207">Het is niet hersteld.</span><span class="sxs-lookup"><span data-stu-id="cefd4-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="cefd4-208">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="cefd4-208">Other resources</span></span>

- <span data-ttu-id="cefd4-209">Zie voor een overzicht van de Sleutelkluis voorlopig verwijderen functie [overzicht van Azure Sleutelkluis voorlopig verwijderen](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="cefd4-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="cefd4-210">Zie voor een algemeen overzicht van Azure Sleutelkluis gebruik [aan de slag met Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cefd4-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

