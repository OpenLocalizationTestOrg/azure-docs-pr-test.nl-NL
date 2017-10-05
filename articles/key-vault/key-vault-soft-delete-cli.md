---
ms.assetid: 
title: Azure Sleutelkluis - voorlopig verwijderen gebruiken met CLI
description: Case voorbeelden van voorlopig verwijderen gebruiken met CLI codefragmenten
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 3ee2c5dfb99d734cde25894174466b8e49823c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-cli"></a><span data-ttu-id="43016-103">Sleutelkluis voorlopig verwijderen gebruiken met CLI</span><span class="sxs-lookup"><span data-stu-id="43016-103">How to use Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="43016-104">Azure Key Vault van voorlopige verwijderingen functie kunt herstellen van verwijderde kluizen en objecten van de kluis.</span><span class="sxs-lookup"><span data-stu-id="43016-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="43016-105">In het bijzonder voorlopig verwijderen adressen van de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="43016-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="43016-106">Ondersteuning voor herstelbare verwijdering van een sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="43016-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="43016-107">Ondersteuning voor verwijdering van de herstelbare objecten van de sleutelkluis. sleutels, geheimen, en certificaten</span><span class="sxs-lookup"><span data-stu-id="43016-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43016-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="43016-108">Prerequisites</span></span>

- <span data-ttu-id="43016-109">Azure CLI 2.0 - als u deze instelling niet voor uw omgeving hebt, Zie [Key Vault beheren met CLI 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="43016-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="43016-110">Zie voor Sleutelkluis specifieke informatie voor CLI [Azure CLI 2.0 Sleutelkluis verwijzing](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="43016-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="43016-111">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="43016-111">Required permissions</span></span>

<span data-ttu-id="43016-112">Sleutelkluis worden afzonderlijk beheerd via op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC) als volgt:</span><span class="sxs-lookup"><span data-stu-id="43016-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="43016-113">Bewerking</span><span class="sxs-lookup"><span data-stu-id="43016-113">Operation</span></span> | <span data-ttu-id="43016-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="43016-114">Description</span></span> | <span data-ttu-id="43016-115">Machtigingen van gebruiker</span><span class="sxs-lookup"><span data-stu-id="43016-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="43016-116">Lijst</span><span class="sxs-lookup"><span data-stu-id="43016-116">List</span></span>|<span data-ttu-id="43016-117">Een lijst met sleutelkluizen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="43016-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="43016-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="43016-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="43016-119">Herstellen</span><span class="sxs-lookup"><span data-stu-id="43016-119">Recover</span></span>|<span data-ttu-id="43016-120">Hiermee herstelt u een verwijderde sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="43016-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="43016-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="43016-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="43016-122">Opschonen</span><span class="sxs-lookup"><span data-stu-id="43016-122">Purge</span></span>|<span data-ttu-id="43016-123">Een verwijderde sleutelkluis en alle bijbehorende inhoud verwijderd permanent.</span><span class="sxs-lookup"><span data-stu-id="43016-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="43016-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="43016-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="43016-125">Zie voor meer informatie over de machtigingen en toegangsbeheer [beveiligen van uw sleutelkluis](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="43016-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="43016-126">Inschakelen van voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="43016-126">Enabling soft-delete</span></span>

<span data-ttu-id="43016-127">Als u een verwijderde sleutelkluis of objecten die zijn opgeslagen in een sleutelkluis herstellen, moet u eerst de soft-het verwijderen van die sleutelkluis inschakelen.</span><span class="sxs-lookup"><span data-stu-id="43016-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="43016-128">Bestaande sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="43016-128">Existing key vault</span></span>

<span data-ttu-id="43016-129">Voor een bestaande sleutelkluis ContosoVault met de naam, moet u voorlopig verwijderen als volgt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="43016-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="43016-130">Op dit moment moet u met Azure Resource Manager resource manipulatie rechtstreeks schrijft de *enableSoftDelete* eigenschap aan de Sleutelkluis-resource.</span><span class="sxs-lookup"><span data-stu-id="43016-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="43016-131">Nieuwe sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="43016-131">New key vault</span></span>

<span data-ttu-id="43016-132">Voorlopig verwijderen voor een nieuwe sleutelkluis inschakelen tijdens het maken wordt gedaan door toe te voegen de vlag voorlopig verwijderen inschakelen voor uw opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="43016-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="43016-133">Controleren inschakelen voor voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="43016-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="43016-134">Om te controleren of er een sleutelkluis voorlopig verwijderen ingeschakeld is, voer de *weergeven* opdracht en zoekt u de 'voorlopig verwijderen Enabled?'</span><span class="sxs-lookup"><span data-stu-id="43016-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="43016-135">kenmerk en de instelling true of false.</span><span class="sxs-lookup"><span data-stu-id="43016-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="43016-136">Verwijderen van een sleutelkluis beveiligd door voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="43016-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="43016-137">De opdracht uit om een sleutelkluis verwijderen (of verwijderen) hetzelfde is gebleven, maar het gedrag verandert, afhankelijk van of u voorlopig verwijderen of niet hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="43016-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="43016-138">Als u de vorige opdracht voor een sleutelkluis die geen voorlopig verwijderen ingeschakeld uitvoert, wordt u deze sleutelkluis en alle bijbehorende inhoud zonder opties voor herstel permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="43016-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="43016-139">Hoe voorlopig verwijderen beschermt uw sleutelkluizen</span><span class="sxs-lookup"><span data-stu-id="43016-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="43016-140">Ingeschakeld met voorlopig verwijderen:</span><span class="sxs-lookup"><span data-stu-id="43016-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="43016-141">Wanneer een sleutelkluis wordt verwijderd, is deze verwijderd uit de resourcegroep en geplaatst in een gereserveerde naamruimte die alleen wordt gekoppeld aan de locatie waar ze werden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="43016-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="43016-142">Objecten in een verwijderde sleutel kluis, zoals sleutels, geheimen en certificaten, zijn niet toegankelijk en blijven ook terwijl hun insluitende sleutelkluis de status verwijderd heeft wordt.</span><span class="sxs-lookup"><span data-stu-id="43016-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="43016-143">De DNS-naam voor een sleutelkluis in een verwijderde status is nog steeds gereserveerd, zodat een nieuwe sleutelkluis met dezelfde naam kan niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="43016-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="43016-144">U kunt verwijderde status sleutelkluizen, dat wordt gekoppeld aan uw abonnement weergeven met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="43016-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="43016-145">De *Resource-ID* verwijst in de uitvoer naar de oorspronkelijke bron-ID van deze kluis.</span><span class="sxs-lookup"><span data-stu-id="43016-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="43016-146">Aangezien deze sleutelkluis nu in een verwijderde staat bevindt is, bestaat er is geen resource met die resource-ID.</span><span class="sxs-lookup"><span data-stu-id="43016-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="43016-147">De *Id* veld kan worden gebruikt voor het identificeren van de resource als herstellen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="43016-147">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="43016-148">De *opschonen datum gepland* veld geeft aan wanneer de kluis wordt definitief verwijderd (verwijderd) als er geen actie voor deze verwijderde kluis ondernomen.</span><span class="sxs-lookup"><span data-stu-id="43016-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="43016-149">De bewaartermijn gebruikt voor het berekenen van de *opschonen datum gepland*, is 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="43016-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="43016-150">Een sleutelkluis herstellen</span><span class="sxs-lookup"><span data-stu-id="43016-150">Recovering a key vault</span></span>

<span data-ttu-id="43016-151">Om te herstellen een sleutelkluis, moet u de naam van de sleutelkluis, resourcegroep en locatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="43016-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="43016-152">Noteer de locatie en de resourcegroep van de verwijderde sleutelkluis als u deze voor het herstelproces van een sleutelkluis nodig.</span><span class="sxs-lookup"><span data-stu-id="43016-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="43016-153">Wanneer een sleutelkluis is hersteld, is het resultaat een nieuwe resource met de sleutelkluis oorspronkelijke bron-ID.</span><span class="sxs-lookup"><span data-stu-id="43016-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="43016-154">Als de resourcegroep waar de sleutelkluis bestond is verwijderd, moet een nieuwe resourcegroep met dezelfde naam worden gemaakt voordat de sleutelkluis kan worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="43016-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="43016-155">Sleutelkluis-objecten en voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="43016-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="43016-156">Voor een sleutel 'ContosoFirstKey' in een sleutelkluis met de naam 'ContosoVault' met voorlopig verwijderen ingeschakeld, hier van wilt hoe u verwijderen die sleutel.</span><span class="sxs-lookup"><span data-stu-id="43016-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="43016-157">Aan de sleutelkluis is ingeschakeld voor voorlopig verwijderen, weergegeven een verwijderde sleutel nog steeds zoals deze wordt verwijderd, behalve, wanneer u expliciet aanbiedt of verwijderde sleutels ophalen.</span><span class="sxs-lookup"><span data-stu-id="43016-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="43016-158">De meeste bewerkingen voor een sleutel in de status verwijderd heeft mislukt met uitzondering van de aanbieding een verwijderde sleutel, herstellen of leegmaakt.</span><span class="sxs-lookup"><span data-stu-id="43016-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="43016-159">Bijvoorbeeld, om aan te vragen tot sleutels van de lijst verwijderd in een sleutelkluis, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="43016-159">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="43016-160">Transitiestatus</span><span class="sxs-lookup"><span data-stu-id="43016-160">Transition state</span></span> 

<span data-ttu-id="43016-161">Wanneer u een sleutel in een sleutelkluis met de soft-delete is ingeschakeld verwijderen, wordt het duurt een paar seconden voor de overgang te voltooien.</span><span class="sxs-lookup"><span data-stu-id="43016-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="43016-162">Tijdens deze transitiestatus zal verschijnen de sleutel is niet in de actieve status of de status verwijderd heeft.</span><span class="sxs-lookup"><span data-stu-id="43016-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="43016-163">Met deze opdracht wordt een lijst alle verwijderde sleutels in de sleutelkluis met de naam 'ContosoVault'.</span><span class="sxs-lookup"><span data-stu-id="43016-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="43016-164">Voorlopig verwijderen gebruiken met sleutelkluis-objecten</span><span class="sxs-lookup"><span data-stu-id="43016-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="43016-165">Net zoals sleutelkluizen, een verwijderde sleutel geheim of certificaat blijft in verwijderde staat bevindt voor maximaal 90 dagen tenzij u deze herstellen of het opschonen.</span><span class="sxs-lookup"><span data-stu-id="43016-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="43016-166">Sleutels</span><span class="sxs-lookup"><span data-stu-id="43016-166">Keys</span></span>

<span data-ttu-id="43016-167">Een verwijderde sleutel herstellen:</span><span class="sxs-lookup"><span data-stu-id="43016-167">To recover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="43016-168">Een sleutel permanent verwijderen:</span><span class="sxs-lookup"><span data-stu-id="43016-168">To permanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="43016-169">Bezig met het verwijderen van een sleutel wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="43016-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="43016-170">De **herstellen** en **opschonen** acties hebben hun eigen machtigingen die zijn gekoppeld in een sleutelkluis-beleid.</span><span class="sxs-lookup"><span data-stu-id="43016-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="43016-171">Voor een gebruiker of service-principal te kunnen uitvoeren een **herstellen** of **opschonen** actie ze gemachtigd bent de respectieve voor dat object (sleutel of geheim) in het toegangsbeleid van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="43016-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="43016-172">Standaard de **opschonen** machtiging is niet toegevoegd aan een sleutelkluis toegangsbeleid wanneer de snelkoppeling 'all' wordt gebruikt voor alle machtigingen verlenen aan een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="43016-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="43016-173">U moet expliciet verlenen **opschonen** machtiging.</span><span class="sxs-lookup"><span data-stu-id="43016-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="43016-174">De volgende opdracht bijvoorbeeld verleent user@contoso.com toestemming voor het uitvoeren van verschillende bewerkingen voor sleutels in *ContosoVault* inclusief **opschonen**.</span><span class="sxs-lookup"><span data-stu-id="43016-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="43016-175">Beleid voor sleutelkluis toegang instellen</span><span class="sxs-lookup"><span data-stu-id="43016-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="43016-176">Als u een bestaande sleutelkluis die ingeschakeld voor voorlopig verwijderen NET heeft hebt, hebt u geen **herstellen** en **opschonen** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="43016-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="43016-177">Geheimen</span><span class="sxs-lookup"><span data-stu-id="43016-177">Secrets</span></span>

<span data-ttu-id="43016-178">Zoals sleutels, worden geheimen in een sleutelkluis met hun eigen opdrachten beheerd op.</span><span class="sxs-lookup"><span data-stu-id="43016-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="43016-179">Te volgen, zijn de opdrachten voor het verwijderen van, aanbieden, herstellen en geheimen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="43016-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="43016-180">Een geheim dat met de naam SQLPassword verwijderen:</span><span class="sxs-lookup"><span data-stu-id="43016-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="43016-181">Lijst van alle verwijderde geheimen in een sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="43016-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="43016-182">Een geheim in de status verwijderd heeft herstellen:</span><span class="sxs-lookup"><span data-stu-id="43016-182">Recover a secret in the deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="43016-183">Opschonen van een geheim in verwijderde staat bevindt:</span><span class="sxs-lookup"><span data-stu-id="43016-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="43016-184">Bezig met het verwijderen van een geheim wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="43016-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="43016-185">Hiervoor en sleutel kluizen</span><span class="sxs-lookup"><span data-stu-id="43016-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="43016-186">Sleutelkluis-objecten</span><span class="sxs-lookup"><span data-stu-id="43016-186">Key vault objects</span></span>

<span data-ttu-id="43016-187">Opruimen van een sleutel wordt geheim of certificaat permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="43016-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="43016-188">De sleutelkluis die deel uitmaakt van het verwijderde object echter blijven behouden als alle andere objecten in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="43016-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="43016-189">Sleutel-kluizen als containers</span><span class="sxs-lookup"><span data-stu-id="43016-189">Key vaults as containers</span></span>
<span data-ttu-id="43016-190">Wanneer een sleutelkluis is opgeschoond, worden alle inhoud, met inbegrip van sleutels, geheimen en certificaten, permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="43016-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="43016-191">Als u wilt een sleutelkluis verwijderen, gebruikt u de `az keyvault purge` opdracht.</span><span class="sxs-lookup"><span data-stu-id="43016-191">To purge a key vault, use the `az keyvault purge` command.</span></span> <span data-ttu-id="43016-192">U kunt zoeken naar de locatie van uw abonnement verwijderd sleutelkluizen met de opdracht `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="43016-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="43016-193">Bezig met het verwijderen van een sleutelkluis wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="43016-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="43016-194">Opschonen van de vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="43016-194">Purge permissions required</span></span>
- <span data-ttu-id="43016-195">Als u wilt verwijderen een verwijderde sleutelkluis, zodat de kluis en alle bijbehorende inhoud permanent worden verwijderd, moet de gebruiker RBAC-machtiging voor het uitvoeren van een *Microsoft.KeyVault/locations/deletedVaults/purge/action* bewerking.</span><span class="sxs-lookup"><span data-stu-id="43016-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="43016-196">Als de verwijderde sleutel wilt weergeven, de kluis van een gebruiker RBAC heeft toestemming nodig om uit te voeren *Microsoft.KeyVault/deletedVaults/read* machtiging.</span><span class="sxs-lookup"><span data-stu-id="43016-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="43016-197">Alleen de abonnementsbeheerder van een heeft standaard deze machtigingen.</span><span class="sxs-lookup"><span data-stu-id="43016-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="43016-198">Geplande opschonen</span><span class="sxs-lookup"><span data-stu-id="43016-198">Scheduled purge</span></span>

<span data-ttu-id="43016-199">Uw sleutelkluis verwijderde objecten weergeven geeft aan wanneer ze schedled worden opgeschoond door Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="43016-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="43016-200">De *opschonen datum gepland* veld geeft aan wanneer een object van de sleutelkluis, worden definitief verwijderd, als er geen actie ondernomen.</span><span class="sxs-lookup"><span data-stu-id="43016-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="43016-201">De bewaarperiode voor een verwijderde sleutelkluis-object is standaard 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="43016-201">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="43016-202">Een object opgeschoonde kluis, geactiveerd door de *opschonen datum gepland* veld, wordt definitief verwijderd.</span><span class="sxs-lookup"><span data-stu-id="43016-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="43016-203">Het is niet hersteld.</span><span class="sxs-lookup"><span data-stu-id="43016-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="43016-204">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="43016-204">Other resources</span></span>

- <span data-ttu-id="43016-205">Zie voor een overzicht van de Sleutelkluis voorlopig verwijderen functie [overzicht van Azure Sleutelkluis voorlopig verwijderen](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="43016-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="43016-206">Zie voor een algemeen overzicht van Azure Sleutelkluis gebruik [aan de slag met Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="43016-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

