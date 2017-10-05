---
ms.assetid: 
title: De Opslagaccountsleutels voor Azure Sleutelkluis
description: Een seemless integratie tussen Azure Key Vault en toegang tot de sleutel op basis bieden toegangscodes voor opslag voor Azure Storage-Account.
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: 3148088c88236c64e089fd25c98eb8ac7cdcbfea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="bb255-103">De Opslagaccountsleutels voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bb255-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="bb255-104">Voordat u Azure Key Vault Opslagaccountsleutels moest ontwikkelaars hun eigen sleutels Azure Storage-Account (ASA) beheren en deze handmatig of via een externe automatisering draaien.</span><span class="sxs-lookup"><span data-stu-id="bb255-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="bb255-105">Nu Sleutelkluis Opslagaccountsleutels worden geïmplementeerd als [Sleutelkluis geheimen](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) voor verificatie met een Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="bb255-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="bb255-106">De ASA belangrijke functie geheime rotatie voor u beheert en verwijdert de behoefte aan uw rechtstreeks contact met een sleutel ASA door het aanbieden van Shared Access Signatures (SAS) als een methode.</span><span class="sxs-lookup"><span data-stu-id="bb255-106">The ASA key feature manages secret rotation for you and removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="bb255-107">Zie voor meer algemene informatie over Azure Storage-Accounts [over Azure storage-accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="bb255-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="bb255-108">Interfaces ondersteunen</span><span class="sxs-lookup"><span data-stu-id="bb255-108">Supporting interfaces</span></span>

<span data-ttu-id="bb255-109">De functie van de sleutels Azure Storage-Account is in eerste instantie beschikbaar via de REST, .NET / C# en PowerShell-interfaces.</span><span class="sxs-lookup"><span data-stu-id="bb255-109">The Azure Storage Account keys feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="bb255-110">Zie voor meer informatie [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="bb255-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="bb255-111">Storage-account sleutels gedrag</span><span class="sxs-lookup"><span data-stu-id="bb255-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="bb255-112">Wat Sleutelkluis beheert</span><span class="sxs-lookup"><span data-stu-id="bb255-112">What Key Vault manages</span></span>

<span data-ttu-id="bb255-113">Wanneer u toegangscodes voor opslag gebruikt, voert Sleutelkluis verschillende interne beheerfuncties namens jou.</span><span class="sxs-lookup"><span data-stu-id="bb255-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="bb255-114">Azure Sleutelkluis beheert sleutels van een Azure Storage-Account (ASA).</span><span class="sxs-lookup"><span data-stu-id="bb255-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="bb255-115">Intern, kunt u Azure Sleutelkluis sleutels (sync) met een Azure Storage-Account weergeven.</span><span class="sxs-lookup"><span data-stu-id="bb255-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="bb255-116">Genereert Azure Key Vault (draait) periodiek de sleutels.</span><span class="sxs-lookup"><span data-stu-id="bb255-116">Azure Key Vault regenerates (rotates) the keys periodically.</span></span> 
    - <span data-ttu-id="bb255-117">Sleutelwaarden worden nooit geretourneerd in antwoord op de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="bb255-117">Key values are never returned in response to caller.</span></span> 
    - <span data-ttu-id="bb255-118">Azure Sleutelkluis beheert sleutels van zowel de Storage-Accounts en de klassieke Opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="bb255-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="bb255-119">Azure Sleutelkluis kunt u de kluis/objecteigenaar, SAS (account of service-SAS)-definities maken.</span><span class="sxs-lookup"><span data-stu-id="bb255-119">Azure Key Vault allows you, the vault/object owner, to create SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="bb255-120">De SAS-waarde, gemaakt met behulp van SAS-definitie geretourneerd als een geheim via de REST-URI-pad.</span><span class="sxs-lookup"><span data-stu-id="bb255-120">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="bb255-121">Zie voor meer informatie [-account voor Azure Sleutelkluis opslagbewerkingen](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="bb255-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="bb255-122">Richtlijnen voor de naamgeving</span><span class="sxs-lookup"><span data-stu-id="bb255-122">Naming guidance</span></span>

<span data-ttu-id="bb255-123">Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="bb255-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="bb255-124">Een SAS-definitie-naam moet 1 102 tekens met alleen 0-9, a-z, A-Z.</span><span class="sxs-lookup"><span data-stu-id="bb255-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="bb255-125">Functionaliteit voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="bb255-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="bb255-126">Voordat u Azure Sleutelkluis Opslagsleutels</span><span class="sxs-lookup"><span data-stu-id="bb255-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="bb255-127">Ontwikkelaars hoeven te maken van de volgende procedures met de sleutel van een opslagaccount wordt gebruikt voor toegang tot Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="bb255-127">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="bb255-128">Na Opslagsleutels voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bb255-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure to set storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command to get Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and the Blob storage endpoint to create a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about to expire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="bb255-129">Aanbevolen procedures voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="bb255-129">Developer best practices</span></span> 

- <span data-ttu-id="bb255-130">Kan alleen Sleutelkluis voor het beheren van uw sleutels ASA.</span><span class="sxs-lookup"><span data-stu-id="bb255-130">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="bb255-131">Probeer niet zelf beheren, wordt u processen van de Sleutelkluis verstoren.</span><span class="sxs-lookup"><span data-stu-id="bb255-131">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="bb255-132">ASA sleutels die worden beheerd door meer dan één Sleutelkluis-object is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bb255-132">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="bb255-133">Als u moet handmatig opnieuw genereren van uw sleutels ASA, raden wij u ze via Sleutelkluis genereren.</span><span class="sxs-lookup"><span data-stu-id="bb255-133">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="bb255-134">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="bb255-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="bb255-135">Instellingen voor op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC)</span><span class="sxs-lookup"><span data-stu-id="bb255-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="bb255-136">Sleutelkluis moet machtigingen voor *lijst* en *genereren* sleutels voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="bb255-136">Key Vault needs permissions to *list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="bb255-137">Stelt u deze machtigingen met behulp van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bb255-137">Set up these permissions using the following steps:</span></span>

- <span data-ttu-id="bb255-138">Object-id van Sleutelkluis ophalen:</span><span class="sxs-lookup"><span data-stu-id="bb255-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="bb255-139">Opslag sleutel Operator rol toewijzen aan Azure Key Vault Identity:</span><span class="sxs-lookup"><span data-stu-id="bb255-139">Assign Storage Key Operator role to Azure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="bb255-140">Voor een klassieke accounttype, stelt u de rolparameter te *'Klassieke Storage Account sleutel Operator Service rol'*.</span><span class="sxs-lookup"><span data-stu-id="bb255-140">For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="bb255-141">Storage-account voorbereiden</span><span class="sxs-lookup"><span data-stu-id="bb255-141">Storage account onboarding</span></span> 

<span data-ttu-id="bb255-142">Voorbeeld: als een object Sleutelkluis eigenaar die u een opslagobject van het account aan uw Azure Sleutelkluis vrijgeven een opslagaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bb255-142">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="bb255-143">Tijdens de voorbereiding, Sleutelkluis moet controleren of de identiteit van de voorbereiding-serviceaccount is gemachtigd om *lijst* en *genereren* opslagsleutels.</span><span class="sxs-lookup"><span data-stu-id="bb255-143">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="bb255-144">Om te controleren of deze machtigingen, Sleutelkluis krijgt een OBO (op andere gebruikers van)-token van de verificatieservice, doelgroep instellen in Azure Resource Manager en maakt een *lijst* sleutel aanroep naar de Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="bb255-144">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="bb255-145">Als de *lijst* aanroep is mislukt, de Sleutelkluis maken van het object is mislukt met HTTP-statuscode *verboden*.</span><span class="sxs-lookup"><span data-stu-id="bb255-145">If the *list* call fails, the Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="bb255-146">De sleutels op deze manier worden vermeld in de cache opgeslagen met de opslag van uw sleutelkluis entiteit.</span><span class="sxs-lookup"><span data-stu-id="bb255-146">The keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="bb255-147">Sleutelkluis moet verifiëren dat de identiteit heeft *genereren* machtigingen voordat deze kan eigenaar van uw sleutels opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="bb255-147">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="bb255-148">Om te controleren dat de identiteit, via OBO-token, evenals de Sleutelkluis identiteit eigen beschikt over deze machtigingen:</span><span class="sxs-lookup"><span data-stu-id="bb255-148">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="bb255-149">Sleutelkluis worden RBAC-machtigingen op de bron voor storage-account.</span><span class="sxs-lookup"><span data-stu-id="bb255-149">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="bb255-150">Sleutelkluis valideert het antwoord via reguliere expressie die overeenkomt met van acties en niet-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bb255-150">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="bb255-151">Ondersteunende voorbeelden op vinden [Sleutelkluis - Storage-Account sleutels voorbeelden beheerd](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="bb255-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="bb255-152">Als de identiteit geen heeft *genereren* machtigingen of als het eerste partij identiteit van de Sleutelkluis geen *lijst* of *genereren* machtiging en vervolgens het voorbereidingsproces aanvragen mislukt retourneren van een juiste foutcode en het bericht.</span><span class="sxs-lookup"><span data-stu-id="bb255-152">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="bb255-153">Het token OBO werkt alleen wanneer u directe, native clienttoepassingen van PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="bb255-153">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="bb255-154">Andere toepassingen</span><span class="sxs-lookup"><span data-stu-id="bb255-154">Other applications</span></span>

- <span data-ttu-id="bb255-155">SAS-tokens opgesteld met Sleutelkluis sleutels van opslagaccount, bieden nog meer beheerde toegang tot Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="bb255-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="bb255-156">Zie voor meer informatie [gedeelde handtekeningen voor toegang](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="bb255-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="bb255-157">Zie ook</span><span class="sxs-lookup"><span data-stu-id="bb255-157">See also</span></span>

- [<span data-ttu-id="bb255-158">Informatie over sleutels, geheimen en certificaten</span><span class="sxs-lookup"><span data-stu-id="bb255-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="bb255-159">Sleutelkluis-teamblog</span><span class="sxs-lookup"><span data-stu-id="bb255-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
