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
# <a name="azure-key-vault-storage-account-keys"></a>De Opslagaccountsleutels voor Azure Sleutelkluis

Voordat u Azure Key Vault Opslagaccountsleutels, ontwikkelaars had toomanage hun eigen sleutels Azure Storage-Account (ASA) en deze handmatig of via een externe automatisering draaien. Nu Sleutelkluis Opslagaccountsleutels worden geïmplementeerd als [Sleutelkluis geheimen](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) voor verificatie met een Azure Storage-Account. 

belangrijke functie van Hallo ASA geheime rotatie voor u beheert en Hallo behoefte aan uw rechtstreeks contact met een sleutel ASA verwijdert door het aanbieden van Shared Access Signatures (SAS) als een methode. 

Zie voor meer algemene informatie over Azure Storage-Accounts [over Azure storage-accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Interfaces ondersteunen

Hallo functie van de sleutels Azure Storage-Account is in eerste instantie beschikbaar via Hallo REST, .NET / C# en PowerShell-interfaces. Zie voor meer informatie [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Storage-account sleutels gedrag

### <a name="what-key-vault-manages"></a>Wat Sleutelkluis beheert

Wanneer u toegangscodes voor opslag gebruikt, voert Sleutelkluis verschillende interne beheerfuncties namens jou.

1. Azure Sleutelkluis beheert sleutels van een Azure Storage-Account (ASA). 
    - Intern, kunt u Azure Sleutelkluis sleutels (sync) met een Azure Storage-Account weergeven.  
    - Genereert Azure Key Vault (draait) Hallo periodiek-codes. 
    - Sleutelwaarden worden nooit geretourneerd in antwoord toocaller. 
    - Azure Sleutelkluis beheert sleutels van zowel de Storage-Accounts en de klassieke Opslagaccounts. 
2. Azure Sleutelkluis kunt u, Hallo kluis/objecteigenaar, toocreate SAS (account of service-SAS) definities. 
    - Hallo SAS-waarde is gemaakt met behulp van SAS-definitie geretourneerd als een geheim via Hallo REST-URI-pad. Zie voor meer informatie [-account voor Azure Sleutelkluis opslagbewerkingen](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).

### <a name="naming-guidance"></a>Richtlijnen voor de naamgeving

Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.  
 
Een SAS-definitie-naam moet 1 102 tekens met alleen 0-9, a-z, A-Z.

## <a name="developer-experience"></a>Functionaliteit voor ontwikkelaars 

### <a name="before-azure-key-vault-storage-keys"></a>Voordat u Azure Sleutelkluis Opslagsleutels 

Ontwikkelaars tooneed toodo hello te volgen met een opslag-account key tooget toegang tooAzure opslag gebruikt. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Na Opslagsleutels voor Azure Sleutelkluis 

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
 
 ### <a name="developer-best-practices"></a>Aanbevolen procedures voor ontwikkelaars 

- Kan Sleutelkluis toomanage alleen de ASA-sleutels. Probeer niet toomanage ze zelf u verstoort processen van de Sleutelkluis. 
- ASA sleutels toobe beheerd door meer dan één Sleutelkluis-object is niet toegestaan. 
- Als u moet toomanually opnieuw genereren van uw sleutels ASA, is het raadzaam dat u ze via Sleutelkluis genereren. 

## <a name="getting-started"></a>Aan de slag

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Instellingen voor op rollen gebaseerde machtigingen voor toegangsbeheer (RBAC)

Sleutelkluis moet de machtigingen te*lijst* en *genereren* sleutels voor een opslagaccount. Stelt u deze machtigingen met Hallo stappen te volgen:

- Object-id van Sleutelkluis ophalen: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Toewijzen van opslag sleutel Operator rol tooAzure Sleutelkluis identiteit: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Voor een klassieke accounttype ingesteld parameter Hallo-rol te*'Klassieke Storage Account sleutel Operator Service rol'*.

### <a name="storage-account-onboarding"></a>Storage-account voorbereiden 

Voorbeeld: Als de eigenaar van een Sleutelkluis-object toevoegen van een storage account object tooyour Azure Key Vault tooonboard een opslagaccount.

Tijdens de voorbereiding, moet de Sleutelkluis tooverify dat Hallo identiteit van Hallo onboarding account machtigingen te heeft*lijst* en te*genereren* opslagsleutels. In volgorde tooverify deze machtigingen, Sleutelkluis krijgt een OBO (op andere gebruikers van) token van de verificatieservice hello, doelgroep ingesteld tooAzure Resource Manager en maakt een *lijst* sleutel aanroep toohello Azure Storage-service. Als hello *lijst* aanroepen mislukt, Hallo Sleutelkluis maken van het object is mislukt met HTTP-statuscode *verboden*. Hallo-sleutels op deze manier worden vermeld in de cache opgeslagen met de opslag van uw sleutelkluis entiteit. 

Sleutelkluis moet verifiëren dat Hallo identiteit heeft *genereren* machtigingen voordat deze kan eigenaar van uw sleutels opnieuw genereren. tooverify die Hallo identiteit via OBO-token, evenals Hallo Sleutelkluis eerste partij identiteit beschikt over deze machtigingen:

- Sleutelkluis bevat RBAC-machtigingen voor Hallo storage account bron.
- Sleutelkluis valideert Hallo antwoord via reguliere expressie die overeenkomt met van acties en niet-bewerkingen. 

Ondersteunende voorbeelden op vinden [Sleutelkluis - Storage-Account sleutels voorbeelden beheerd](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).

Als Hallo identiteit geen heeft *genereren* machtigingen of als het eerste partij identiteit van de Sleutelkluis geen *lijst* of *genereren* machtiging vervolgens Hallo voorbereiden aanvraag is mislukt voor het retourneren van een juiste foutcode en het bericht. 

Hallo OBO token werkt alleen wanneer u directe, native clienttoepassingen van PowerShell of CLI.

## <a name="other-applications"></a>Andere toepassingen

- SAS-tokens opgesteld met Sleutelkluis sleutels van opslagaccount, bieden nog meer beperkte toegang tooan Azure storage-account. Zie voor meer informatie [gedeelde handtekeningen voor toegang](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>Zie ook

- [Informatie over sleutels, geheimen en certificaten](https://docs.microsoft.com/rest/api/keyvault/)
- [Sleutelkluis-teamblog](https://blogs.technet.microsoft.com/kv/)
