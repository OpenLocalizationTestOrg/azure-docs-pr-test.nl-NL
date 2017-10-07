---
ms.assetid: 
title: aaaAzure Sleutelkluis toegangscodes voor opslag
description: Toegangscodes voor opslag bieden een seemless integratie tussen Azure Sleutelkluis en de toegang tot de sleutel op basis tooAzure Storage-Account.
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="1c717-103">De Opslagaccountsleutels voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="1c717-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="1c717-104">Voordat u Azure Key Vault Opslagaccountsleutels, ontwikkelaars had toomanage hun eigen sleutels Azure Storage-Account (ASA) en deze handmatig of via een externe automatisering draaien.</span><span class="sxs-lookup"><span data-stu-id="1c717-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="1c717-105">Nu Sleutelkluis Opslagaccountsleutels worden geïmplementeerd als [Sleutelkluis geheimen](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) voor verificatie met een Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="1c717-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="1c717-106">belangrijke functie van Hallo ASA geheime rotatie voor u beheert en Hallo behoefte aan uw rechtstreeks contact met een sleutel ASA verwijdert door het aanbieden van Shared Access Signatures (SAS) als een methode.</span><span class="sxs-lookup"><span data-stu-id="1c717-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="1c717-107">Zie voor meer algemene informatie over Azure Storage-Accounts [over Azure storage-accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1c717-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="1c717-108">Interfaces ondersteunen</span><span class="sxs-lookup"><span data-stu-id="1c717-108">Supporting interfaces</span></span>

<span data-ttu-id="1c717-109">Hallo functie van de sleutels Azure Storage-Account is in eerste instantie beschikbaar via Hallo REST, .NET / C# en PowerShell-interfaces.</span><span class="sxs-lookup"><span data-stu-id="1c717-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="1c717-110">Zie voor meer informatie [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="1c717-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="1c717-111">Storage-account sleutels gedrag</span><span class="sxs-lookup"><span data-stu-id="1c717-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="1c717-112">Wat Sleutelkluis beheert</span><span class="sxs-lookup"><span data-stu-id="1c717-112">What Key Vault manages</span></span>

<span data-ttu-id="1c717-113">Wanneer u toegangscodes voor opslag gebruikt, voert Sleutelkluis verschillende interne beheerfuncties namens jou.</span><span class="sxs-lookup"><span data-stu-id="1c717-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="1c717-114">Azure Sleutelkluis beheert sleutels van een Azure Storage-Account (ASA).</span><span class="sxs-lookup"><span data-stu-id="1c717-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="1c717-115">Intern, kunt u Azure Sleutelkluis sleutels (sync) met een Azure Storage-Account weergeven.</span><span class="sxs-lookup"><span data-stu-id="1c717-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="1c717-116">Genereert Azure Key Vault (draait) Hallo periodiek-codes.</span><span class="sxs-lookup"><span data-stu-id="1c717-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="1c717-117">Sleutelwaarden worden nooit geretourneerd in antwoord toocaller.</span><span class="sxs-lookup"><span data-stu-id="1c717-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="1c717-118">Azure Sleutelkluis beheert sleutels van zowel de Storage-Accounts en de klassieke Opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="1c717-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="1c717-119">Azure Sleutelkluis kunt u, Hallo kluis/objecteigenaar, toocreate SAS (account of service-SAS) definities.</span><span class="sxs-lookup"><span data-stu-id="1c717-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="1c717-120">Hallo SAS-waarde is gemaakt met behulp van SAS-definitie geretourneerd als een geheim via Hallo REST-URI-pad.</span><span class="sxs-lookup"><span data-stu-id="1c717-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="1c717-121">Zie voor meer informatie [-account voor Azure Sleutelkluis opslagbewerkingen](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="1c717-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="1c717-122">Richtlijnen voor de naamgeving</span><span class="sxs-lookup"><span data-stu-id="1c717-122">Naming guidance</span></span>

<span data-ttu-id="1c717-123">Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="1c717-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="1c717-124">Een SAS-definitie-naam moet 1 102 tekens met alleen 0-9, a-z, A-Z.</span><span class="sxs-lookup"><span data-stu-id="1c717-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="1c717-125">Functionaliteit voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="1c717-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="1c717-126">Voordat u Azure Sleutelkluis Opslagsleutels</span><span class="sxs-lookup"><span data-stu-id="1c717-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="1c717-127">Ontwikkelaars tooneed toodo hello te volgen met een opslag-account key tooget toegang tooAzure opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1c717-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="1c717-128">Na Opslagsleutels voor Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="1c717-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="1c717-129">Aanbevolen procedures voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="1c717-129">Developer best practices</span></span> 

- <span data-ttu-id="1c717-130">Kan Sleutelkluis toomanage alleen de ASA-sleutels.</span><span class="sxs-lookup"><span data-stu-id="1c717-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="1c717-131">Probeer niet toomanage ze zelf u verstoort processen van de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1c717-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="1c717-132">ASA sleutels toobe beheerd door meer dan één Sleutelkluis-object is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="1c717-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="1c717-133">Als u moet toomanually opnieuw genereren van uw sleutels ASA, is het raadzaam dat u ze via Sleutelkluis genereren.</span><span class="sxs-lookup"><span data-stu-id="1c717-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="1c717-134">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="1c717-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="1c717-135">Instellingen voor op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC)</span><span class="sxs-lookup"><span data-stu-id="1c717-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="1c717-136">Sleutelkluis moet de machtigingen te*lijst* en *genereren* sleutels voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1c717-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="1c717-137">Stelt u deze machtigingen met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c717-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="1c717-138">Object-id van Sleutelkluis ophalen:</span><span class="sxs-lookup"><span data-stu-id="1c717-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="1c717-139">Toewijzen van opslag sleutel Operator rol tooAzure Sleutelkluis identiteit:</span><span class="sxs-lookup"><span data-stu-id="1c717-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="1c717-140">Voor een klassieke accounttype ingesteld parameter Hallo-rol te*'Klassieke Storage Account sleutel Operator Service rol'*.</span><span class="sxs-lookup"><span data-stu-id="1c717-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="1c717-141">Storage-account voorbereiden</span><span class="sxs-lookup"><span data-stu-id="1c717-141">Storage account onboarding</span></span> 

<span data-ttu-id="1c717-142">Voorbeeld: Als de eigenaar van een Sleutelkluis-object toevoegen van een storage account object tooyour Azure Key Vault tooonboard een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1c717-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="1c717-143">Tijdens de voorbereiding, moet de Sleutelkluis tooverify dat Hallo identiteit van Hallo onboarding account machtigingen te heeft*lijst* en te*genereren* opslagsleutels.</span><span class="sxs-lookup"><span data-stu-id="1c717-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="1c717-144">In volgorde tooverify deze machtigingen, Sleutelkluis krijgt een OBO (op andere gebruikers van) token van de verificatieservice hello, doelgroep ingesteld tooAzure Resource Manager en maakt een *lijst* sleutel aanroep toohello Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="1c717-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="1c717-145">Als hello *lijst* aanroepen mislukt, Hallo Sleutelkluis maken van het object is mislukt met HTTP-statuscode *verboden*.</span><span class="sxs-lookup"><span data-stu-id="1c717-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="1c717-146">Hallo-sleutels op deze manier worden vermeld in de cache opgeslagen met de opslag van uw sleutelkluis entiteit.</span><span class="sxs-lookup"><span data-stu-id="1c717-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="1c717-147">Sleutelkluis moet verifiëren dat Hallo identiteit heeft *genereren* machtigingen voordat deze kan eigenaar van uw sleutels opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="1c717-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="1c717-148">tooverify die Hallo identiteit via OBO-token, evenals Hallo Sleutelkluis eerste partij identiteit beschikt over deze machtigingen:</span><span class="sxs-lookup"><span data-stu-id="1c717-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="1c717-149">Sleutelkluis bevat RBAC-machtigingen voor Hallo storage account bron.</span><span class="sxs-lookup"><span data-stu-id="1c717-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="1c717-150">Sleutelkluis valideert Hallo antwoord via reguliere expressie die overeenkomt met van acties en niet-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="1c717-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="1c717-151">Ondersteunende voorbeelden op vinden [Sleutelkluis - Storage-Account sleutels voorbeelden beheerd](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="1c717-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="1c717-152">Als Hallo identiteit geen heeft *genereren* machtigingen of als het eerste partij identiteit van de Sleutelkluis geen *lijst* of *genereren* machtiging vervolgens Hallo voorbereiden aanvraag is mislukt voor het retourneren van een juiste foutcode en het bericht.</span><span class="sxs-lookup"><span data-stu-id="1c717-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="1c717-153">Hallo OBO token werkt alleen wanneer u directe, native clienttoepassingen van PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="1c717-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="1c717-154">Andere toepassingen</span><span class="sxs-lookup"><span data-stu-id="1c717-154">Other applications</span></span>

- <span data-ttu-id="1c717-155">SAS-tokens opgesteld met Sleutelkluis sleutels van opslagaccount, bieden nog meer beperkte toegang tooan Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="1c717-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="1c717-156">Zie voor meer informatie [gedeelde handtekeningen voor toegang](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="1c717-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="1c717-157">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1c717-157">See also</span></span>

- [<span data-ttu-id="1c717-158">Informatie over sleutels, geheimen en certificaten</span><span class="sxs-lookup"><span data-stu-id="1c717-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="1c717-159">Sleutelkluis-teamblog</span><span class="sxs-lookup"><span data-stu-id="1c717-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
