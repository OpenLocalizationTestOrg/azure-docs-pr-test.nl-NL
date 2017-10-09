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
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="8cff2-103">Hoe toouse Sleutelkluis voorlopig verwijderen met CLI</span><span class="sxs-lookup"><span data-stu-id="8cff2-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="8cff2-104">Azure Key Vault van voorlopige verwijderingen functie kunt herstellen van verwijderde kluizen en objecten van de kluis.</span><span class="sxs-lookup"><span data-stu-id="8cff2-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="8cff2-105">In het bijzonder voorlopig verwijderen adressen Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="8cff2-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="8cff2-106">Ondersteuning voor herstelbare verwijdering van een sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="8cff2-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="8cff2-107">Ondersteuning voor verwijdering van de herstelbare objecten van de sleutelkluis. sleutels, geheimen, en certificaten</span><span class="sxs-lookup"><span data-stu-id="8cff2-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cff2-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8cff2-108">Prerequisites</span></span>

- <span data-ttu-id="8cff2-109">Azure CLI 2.0 - als u deze instelling niet voor uw omgeving hebt, Zie [Key Vault beheren met CLI 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="8cff2-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="8cff2-110">Zie voor Sleutelkluis specifieke informatie voor CLI [Azure CLI 2.0 Sleutelkluis verwijzing](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="8cff2-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="8cff2-111">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="8cff2-111">Required permissions</span></span>

<span data-ttu-id="8cff2-112">Sleutelkluis worden afzonderlijk beheerd via op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC) als volgt:</span><span class="sxs-lookup"><span data-stu-id="8cff2-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="8cff2-113">Bewerking</span><span class="sxs-lookup"><span data-stu-id="8cff2-113">Operation</span></span> | <span data-ttu-id="8cff2-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8cff2-114">Description</span></span> | <span data-ttu-id="8cff2-115">Machtigingen van gebruiker</span><span class="sxs-lookup"><span data-stu-id="8cff2-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="8cff2-116">Lijst</span><span class="sxs-lookup"><span data-stu-id="8cff2-116">List</span></span>|<span data-ttu-id="8cff2-117">Een lijst met sleutelkluizen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8cff2-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="8cff2-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="8cff2-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="8cff2-119">Herstellen</span><span class="sxs-lookup"><span data-stu-id="8cff2-119">Recover</span></span>|<span data-ttu-id="8cff2-120">Hiermee herstelt u een verwijderde sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="8cff2-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="8cff2-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="8cff2-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="8cff2-122">Opschonen</span><span class="sxs-lookup"><span data-stu-id="8cff2-122">Purge</span></span>|<span data-ttu-id="8cff2-123">Een verwijderde sleutelkluis en alle bijbehorende inhoud verwijderd permanent.</span><span class="sxs-lookup"><span data-stu-id="8cff2-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="8cff2-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="8cff2-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="8cff2-125">Zie voor meer informatie over de machtigingen en toegangsbeheer [beveiligen van uw sleutelkluis](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="8cff2-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="8cff2-126">Inschakelen van voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="8cff2-126">Enabling soft-delete</span></span>

<span data-ttu-id="8cff2-127">toobe kunnen toorecover een verwijderde sleutelkluis of objecten die zijn opgeslagen in een sleutel-kluis, moet u eerst soft-het verwijderen van die sleutelkluis inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="8cff2-128">Bestaande sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="8cff2-128">Existing key vault</span></span>

<span data-ttu-id="8cff2-129">Voor een bestaande sleutelkluis ContosoVault met de naam, moet u voorlopig verwijderen als volgt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="8cff2-130">Op dit moment moet u toouse Azure Resource Manager resource manipulatie toodirectly schrijven Hallo *enableSoftDelete* eigenschap toohello Sleutelkluis-resource.</span><span class="sxs-lookup"><span data-stu-id="8cff2-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="8cff2-131">Nieuwe sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="8cff2-131">New key vault</span></span>

<span data-ttu-id="8cff2-132">Voorlopig verwijderen voor een nieuwe sleutelkluis inschakelen wordt uitgevoerd tijdens het maken door toe te voegen Hallo voorlopig verwijderen inschakelen vlag tooyour opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="8cff2-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="8cff2-133">Controleren inschakelen voor voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="8cff2-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="8cff2-134">tooverify die een sleutelkluis ingeschakeld is, zachte verwijderen uitvoeren Hallo *weergeven* opdracht en zoek naar 'Voorlopig verwijderen Enabled?' Hallo</span><span class="sxs-lookup"><span data-stu-id="8cff2-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="8cff2-135">kenmerk en de instelling true of false.</span><span class="sxs-lookup"><span data-stu-id="8cff2-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="8cff2-136">Verwijderen van een sleutelkluis beveiligd door voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="8cff2-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="8cff2-137">Hallo opdracht toodelete (of verwijderen) blijft een sleutelkluis Hallo dezelfde, maar de gedragswijzigingen afhankelijk van of u hebt ingeschakeld voorlopig verwijderen of niet.</span><span class="sxs-lookup"><span data-stu-id="8cff2-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="8cff2-138">Als u de vorige opdracht Hallo voor een sleutelkluis die geen voorlopig verwijderen ingeschakeld uitvoert, wordt u deze sleutelkluis en alle bijbehorende inhoud zonder opties voor herstel permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8cff2-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="8cff2-139">Hoe voorlopig verwijderen beschermt uw sleutelkluizen</span><span class="sxs-lookup"><span data-stu-id="8cff2-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="8cff2-140">Ingeschakeld met voorlopig verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8cff2-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="8cff2-141">Wanneer een sleutelkluis wordt verwijderd, is deze verwijderd uit de resourcegroep en geplaatst in een gereserveerde naamruimte die alleen wordt gekoppeld aan het Hallo-locatie waar ze werden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8cff2-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="8cff2-142">Objecten in een verwijderde sleutel kluis, zoals sleutels, geheimen en certificaten, zijn niet toegankelijk en blijven ook wanneer hun insluitende sleutelkluis Hallo verwijderde status heeft.</span><span class="sxs-lookup"><span data-stu-id="8cff2-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="8cff2-143">Hallo DNS-naam voor een sleutelkluis in een verwijderde status is nog steeds gereserveerd, zodat een nieuwe sleutelkluis met dezelfde naam kan niet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8cff2-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="8cff2-144">U kunt verwijderde status sleutelkluizen, dat wordt gekoppeld aan uw abonnement bekijken met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8cff2-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="8cff2-145">Hallo *Resource-ID* in Hallo uitvoer toohello oorspronkelijke bron-ID van deze kluis verwijst.</span><span class="sxs-lookup"><span data-stu-id="8cff2-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="8cff2-146">Aangezien deze sleutelkluis nu in een verwijderde staat bevindt is, bestaat er is geen resource met die resource-ID.</span><span class="sxs-lookup"><span data-stu-id="8cff2-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="8cff2-147">Hallo *Id* het veld mag gebruikte tooidentify Hallo resource als herstellen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="8cff2-148">Hallo *opschonen datum gepland* veld geeft aan wanneer Hallo kluis wordt definitief verwijderd (verwijderd) als er geen actie voor deze verwijderde kluis ondernomen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="8cff2-149">Hallo standaard bewaren periode, gebruikte toocalculate hello *opschonen datum gepland*, is 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="8cff2-150">Een sleutelkluis herstellen</span><span class="sxs-lookup"><span data-stu-id="8cff2-150">Recovering a key vault</span></span>

<span data-ttu-id="8cff2-151">een sleutelkluis toorecover, moet u toospecify hello sleutelkluisnaam, de resourcegroep en locatie.</span><span class="sxs-lookup"><span data-stu-id="8cff2-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="8cff2-152">Houd er rekening mee Hallo locatie en de resourcegroep Hallo van sleutelkluis Hallo verwijderd als u deze voor het herstelproces van een sleutelkluis nodig.</span><span class="sxs-lookup"><span data-stu-id="8cff2-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="8cff2-153">Een sleutelkluis is hersteld, Hallo resultaat is een nieuwe resource met Hallo sleutelkluis de oorspronkelijke bron-ID.</span><span class="sxs-lookup"><span data-stu-id="8cff2-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="8cff2-154">Als de resourcegroep Hallo waar Hallo sleutelkluis bestond is verwijderd, moet een nieuwe resourcegroep met dezelfde naam worden gemaakt voordat de sleutelkluis Hallo kan worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="8cff2-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="8cff2-155">Sleutelkluis-objecten en voorlopig verwijderen</span><span class="sxs-lookup"><span data-stu-id="8cff2-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="8cff2-156">Voor een sleutel 'ContosoFirstKey' in een sleutelkluis met de naam 'ContosoVault' met voorlopig verwijderen ingeschakeld, hier van wilt hoe u verwijderen die sleutel.</span><span class="sxs-lookup"><span data-stu-id="8cff2-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="8cff2-157">Aan de sleutelkluis is ingeschakeld voor voorlopig verwijderen, weergegeven een verwijderde sleutel nog steeds zoals deze wordt verwijderd, behalve, wanneer u expliciet aanbiedt of verwijderde sleutels ophalen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="8cff2-158">De meeste bewerkingen voor een sleutel in Hallo verwijderd status mislukt met uitzondering van de aanbieding een verwijderde sleutel, herstellen of leegmaakt.</span><span class="sxs-lookup"><span data-stu-id="8cff2-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="8cff2-159">Bijvoorbeeld: toorequest toolist verwijderd sleutels in een sleutelkluis Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8cff2-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="8cff2-160">Transitiestatus</span><span class="sxs-lookup"><span data-stu-id="8cff2-160">Transition state</span></span> 

<span data-ttu-id="8cff2-161">Wanneer u een sleutel in een sleutelkluis met de soft-delete is ingeschakeld verwijderen, wordt het duurt een paar seconden Hallo overgang toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8cff2-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="8cff2-162">Tijdens deze transitiestatus deze kan worden weergegeven die Hallo-sleutel niet in Hallo active of Hallo verwijderde staat.</span><span class="sxs-lookup"><span data-stu-id="8cff2-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="8cff2-163">Met deze opdracht wordt een lijst alle verwijderde sleutels in de sleutelkluis met de naam 'ContosoVault'.</span><span class="sxs-lookup"><span data-stu-id="8cff2-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="8cff2-164">Voorlopig verwijderen gebruiken met sleutelkluis-objecten</span><span class="sxs-lookup"><span data-stu-id="8cff2-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="8cff2-165">Net zoals sleutelkluizen, een verwijderde sleutel geheim of certificaat blijft in verwijderde staat bevindt voor too90 dagen tenzij u deze herstellen of het opschonen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="8cff2-166">Sleutels</span><span class="sxs-lookup"><span data-stu-id="8cff2-166">Keys</span></span>

<span data-ttu-id="8cff2-167">een verwijderde sleutel toorecover:</span><span class="sxs-lookup"><span data-stu-id="8cff2-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="8cff2-168">toopermanently een sleutel verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8cff2-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="8cff2-169">Bezig met het verwijderen van een sleutel wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="8cff2-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="8cff2-170">Hallo **herstellen** en **opschonen** acties hebben hun eigen machtigingen die zijn gekoppeld in een sleutelkluis-beleid.</span><span class="sxs-lookup"><span data-stu-id="8cff2-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="8cff2-171">Voor een gebruiker of service principal toobe kunnen tooexecute een **herstellen** of **opschonen** ze gemachtigd Hallo respectieve voor dat object (sleutel of geheim) in Hallo sleutelkluis-beleid in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="8cff2-172">Standaard Hallo **opschonen** machtiging tooa key vault-beleid niet is toegevoegd als Hallo 'all' snelkoppeling gebruikte toogrant tooa alle machtigingen van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8cff2-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="8cff2-173">U moet expliciet verlenen **opschonen** machtiging.</span><span class="sxs-lookup"><span data-stu-id="8cff2-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="8cff2-174">Bijvoorbeeld, Hallo opdracht verleent na user@contoso.com machtiging tooperform verschillende bewerkingen voor sleutels in *ContosoVault* inclusief **opschonen**.</span><span class="sxs-lookup"><span data-stu-id="8cff2-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="8cff2-175">Beleid voor sleutelkluis toegang instellen</span><span class="sxs-lookup"><span data-stu-id="8cff2-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="8cff2-176">Als u een bestaande sleutelkluis die ingeschakeld voor voorlopig verwijderen NET heeft hebt, hebt u geen **herstellen** en **opschonen** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="8cff2-177">Geheimen</span><span class="sxs-lookup"><span data-stu-id="8cff2-177">Secrets</span></span>

<span data-ttu-id="8cff2-178">Zoals sleutels, worden geheimen in een sleutelkluis met hun eigen opdrachten beheerd op.</span><span class="sxs-lookup"><span data-stu-id="8cff2-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="8cff2-179">Te volgen, zijn Hallo-opdrachten voor het verwijderen van, aanbieden, herstellen en geheimen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="8cff2-180">Een geheim dat met de naam SQLPassword verwijderen:</span><span class="sxs-lookup"><span data-stu-id="8cff2-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="8cff2-181">Lijst van alle verwijderde geheimen in een sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="8cff2-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="8cff2-182">Een geheim Hallo verwijderd status herstellen:</span><span class="sxs-lookup"><span data-stu-id="8cff2-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="8cff2-183">Opschonen van een geheim in verwijderde staat bevindt:</span><span class="sxs-lookup"><span data-stu-id="8cff2-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="8cff2-184">Bezig met het verwijderen van een geheim wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="8cff2-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="8cff2-185">Hiervoor en sleutel kluizen</span><span class="sxs-lookup"><span data-stu-id="8cff2-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="8cff2-186">Sleutelkluis-objecten</span><span class="sxs-lookup"><span data-stu-id="8cff2-186">Key vault objects</span></span>

<span data-ttu-id="8cff2-187">Opruimen van een sleutel wordt geheim of certificaat permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="8cff2-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="8cff2-188">Hallo-sleutelkluis die Hallo verwijderd object bevat echter blijven behouden als alle andere objecten in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="8cff2-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="8cff2-189">Sleutel-kluizen als containers</span><span class="sxs-lookup"><span data-stu-id="8cff2-189">Key vaults as containers</span></span>
<span data-ttu-id="8cff2-190">Wanneer een sleutelkluis is opgeschoond, worden alle inhoud, met inbegrip van sleutels, geheimen en certificaten, permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8cff2-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="8cff2-191">een sleutelkluis toopurge gebruiken Hallo `az keyvault purge` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8cff2-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="8cff2-192">U kunt zoeken naar Hallo locatie van uw abonnement verwijderd sleutelkluizen met Hallo opdracht `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="8cff2-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="8cff2-193">Bezig met het verwijderen van een sleutelkluis wordt permanent verwijderd, wat betekent dat deze kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="8cff2-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="8cff2-194">Opschonen van de vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="8cff2-194">Purge permissions required</span></span>
- <span data-ttu-id="8cff2-195">een verwijderde sleutelkluis toopurge, zodat het Hallo-kluis en alle bijbehorende inhoud permanent worden verwijderd, Hallo gebruiker RBAC-machtiging tooperform moet een *Microsoft.KeyVault/locations/deletedVaults/purge/action* bewerking.</span><span class="sxs-lookup"><span data-stu-id="8cff2-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="8cff2-196">toolist hello verwijderd sleutel Hallo kluis een gebruiker moet RBAC-machtiging tooperform *Microsoft.KeyVault/deletedVaults/read* machtiging.</span><span class="sxs-lookup"><span data-stu-id="8cff2-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="8cff2-197">Alleen de abonnementsbeheerder van een heeft standaard deze machtigingen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="8cff2-198">Geplande opschonen</span><span class="sxs-lookup"><span data-stu-id="8cff2-198">Scheduled purge</span></span>

<span data-ttu-id="8cff2-199">Uw sleutelkluis verwijderde objecten weergeven geeft aan wanneer ze schedled toobe Sleutelkluis opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="8cff2-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="8cff2-200">Hallo *opschonen datum gepland* veld geeft aan wanneer een object van de sleutelkluis, worden definitief verwijderd, als er geen actie ondernomen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="8cff2-201">Hallo bewaarperiode voor een object verwijderde sleutelkluis is standaard 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="8cff2-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="8cff2-202">Een object opgeschoonde kluis, geactiveerd door de *opschonen datum gepland* veld, wordt definitief verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8cff2-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="8cff2-203">Het is niet hersteld.</span><span class="sxs-lookup"><span data-stu-id="8cff2-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="8cff2-204">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="8cff2-204">Other resources</span></span>

- <span data-ttu-id="8cff2-205">Zie voor een overzicht van de Sleutelkluis voorlopig verwijderen functie [overzicht van Azure Sleutelkluis voorlopig verwijderen](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="8cff2-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="8cff2-206">Zie voor een algemeen overzicht van Azure Sleutelkluis gebruik [aan de slag met Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8cff2-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

