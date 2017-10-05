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
# <a name="azure-key-vault-storage-account-keys"></a>De Opslagaccountsleutels voor Azure Sleutelkluis

Voordat u Azure Key Vault Opslagaccountsleutels moest ontwikkelaars hun eigen sleutels Azure Storage-Account (ASA) beheren en deze handmatig of via een externe automatisering draaien. Nu Sleutelkluis Opslagaccountsleutels worden geïmplementeerd als [Sleutelkluis geheimen](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) voor verificatie met een Azure Storage-Account. 

De ASA belangrijke functie geheime rotatie voor u beheert en verwijdert de behoefte aan uw rechtstreeks contact met een sleutel ASA door het aanbieden van Shared Access Signatures (SAS) als een methode. 

Zie voor meer algemene informatie over Azure Storage-Accounts [over Azure storage-accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Interfaces ondersteunen

De functie van de sleutels Azure Storage-Account is in eerste instantie beschikbaar via de REST, .NET / C# en PowerShell-interfaces. Zie voor meer informatie [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Storage-account sleutels gedrag

### <a name="what-key-vault-manages"></a>Wat Sleutelkluis beheert

Wanneer u toegangscodes voor opslag gebruikt, voert Sleutelkluis verschillende interne beheerfuncties namens jou.

1. Azure Sleutelkluis beheert sleutels van een Azure Storage-Account (ASA). 
    - Intern, kunt u Azure Sleutelkluis sleutels (sync) met een Azure Storage-Account weergeven.  
    - Genereert Azure Key Vault (draait) periodiek de sleutels. 
    - Sleutelwaarden worden nooit geretourneerd in antwoord op de aanroeper. 
    - Azure Sleutelkluis beheert sleutels van zowel de Storage-Accounts en de klassieke Opslagaccounts. 
2. Azure Sleutelkluis kunt u de kluis/objecteigenaar, SAS (account of service-SAS)-definities maken. 
    - De SAS-waarde, gemaakt met behulp van SAS-definitie geretourneerd als een geheim via de REST-URI-pad. Zie voor meer informatie [-account voor Azure Sleutelkluis opslagbewerkingen](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).

### <a name="naming-guidance"></a>Richtlijnen voor de naamgeving

Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.  
 
Een SAS-definitie-naam moet 1 102 tekens met alleen 0-9, a-z, A-Z.

## <a name="developer-experience"></a>Functionaliteit voor ontwikkelaars 

### <a name="before-azure-key-vault-storage-keys"></a>Voordat u Azure Sleutelkluis Opslagsleutels 

Ontwikkelaars hoeven te maken van de volgende procedures met de sleutel van een opslagaccount wordt gebruikt voor toegang tot Azure-opslag. 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Na Opslagsleutels voor Azure Sleutelkluis 

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
 
 ### <a name="developer-best-practices"></a>Aanbevolen procedures voor ontwikkelaars 

- Kan alleen Sleutelkluis voor het beheren van uw sleutels ASA. Probeer niet zelf beheren, wordt u processen van de Sleutelkluis verstoren. 
- ASA sleutels die worden beheerd door meer dan één Sleutelkluis-object is niet toegestaan. 
- Als u moet handmatig opnieuw genereren van uw sleutels ASA, raden wij u ze via Sleutelkluis genereren. 

## <a name="getting-started"></a>Aan de slag

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Instellingen voor op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC)

Sleutelkluis moet machtigingen voor *lijst* en *genereren* sleutels voor een opslagaccount. Stelt u deze machtigingen met behulp van de volgende stappen uit:

- Object-id van Sleutelkluis ophalen: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Opslag sleutel Operator rol toewijzen aan Azure Key Vault Identity: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Voor een klassieke accounttype, stelt u de rolparameter te *'Klassieke Storage Account sleutel Operator Service rol'*.

### <a name="storage-account-onboarding"></a>Storage-account voorbereiden 

Voorbeeld: als een object Sleutelkluis eigenaar die u een opslagobject van het account aan uw Azure Sleutelkluis vrijgeven een opslagaccount toevoegen.

Tijdens de voorbereiding, Sleutelkluis moet controleren of de identiteit van de voorbereiding-serviceaccount is gemachtigd om *lijst* en *genereren* opslagsleutels. Om te controleren of deze machtigingen, Sleutelkluis krijgt een OBO (op andere gebruikers van)-token van de verificatieservice, doelgroep instellen in Azure Resource Manager en maakt een *lijst* sleutel aanroep naar de Azure Storage-service. Als de *lijst* aanroep is mislukt, de Sleutelkluis maken van het object is mislukt met HTTP-statuscode *verboden*. De sleutels op deze manier worden vermeld in de cache opgeslagen met de opslag van uw sleutelkluis entiteit. 

Sleutelkluis moet verifiëren dat de identiteit heeft *genereren* machtigingen voordat deze kan eigenaar van uw sleutels opnieuw genereren. Om te controleren dat de identiteit, via OBO-token, evenals de Sleutelkluis identiteit eigen beschikt over deze machtigingen:

- Sleutelkluis worden RBAC-machtigingen op de bron voor storage-account.
- Sleutelkluis valideert het antwoord via reguliere expressie die overeenkomt met van acties en niet-bewerkingen. 

Ondersteunende voorbeelden op vinden [Sleutelkluis - Storage-Account sleutels voorbeelden beheerd](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).

Als de identiteit geen heeft *genereren* machtigingen of als het eerste partij identiteit van de Sleutelkluis geen *lijst* of *genereren* machtiging en vervolgens het voorbereidingsproces aanvragen mislukt retourneren van een juiste foutcode en het bericht. 

Het token OBO werkt alleen wanneer u directe, native clienttoepassingen van PowerShell of CLI.

## <a name="other-applications"></a>Andere toepassingen

- SAS-tokens opgesteld met Sleutelkluis sleutels van opslagaccount, bieden nog meer beheerde toegang tot Azure storage-account. Zie voor meer informatie [gedeelde handtekeningen voor toegang](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>Zie ook

- [Informatie over sleutels, geheimen en certificaten](https://docs.microsoft.com/rest/api/keyvault/)
- [Sleutelkluis-teamblog](https://blogs.technet.microsoft.com/kv/)
