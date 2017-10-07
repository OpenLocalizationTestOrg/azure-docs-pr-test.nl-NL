---
title: 'Zelfstudie: Blobs versleutelen en ontsleutelen in Azure Storage met Azure Sleutelkluis | Microsoft Docs'
description: Hoe tooencrypt en ontsleutelen van een blob met client-side '-codering voor Microsoft Azure Storage met Azure Sleutelkluis.
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Zelfstudie: Blobs versleutelen en ontsleutelen in Microsoft Azure Storage met Azure Sleutelkluis
## <a name="introduction"></a>Inleiding
Deze zelfstudie bevat informatie over hoe toomake gebruiken van client-side opslagversleuteling met Azure Sleutelkluis. Dit laat zien hoe u tooencrypt en ontsleutelen van een blob in een consoletoepassing met behulp van deze technologieën.

**Geschatte tijd toocomplete:** 20 minuten

Zie voor informatie over Azure Sleutelkluis [wat is Azure Sleutelkluis?](../key-vault/key-vault-whatis.md).

Zie voor informatie over client-side '-versleuteling voor Azure Storage, [Client-Side-versleuteling en Azure Key Vault voor Microsoft Azure Storage](storage-client-side-encryption.md).

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie hebt u hello te volgen:

* Een Azure Storage-account
* Visual Studio 2013 of hoger
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>Overzicht van client-side '-versleuteling
Zie voor een overzicht van client-side '-versleuteling voor Azure Storage [Client-Side-versleuteling en Azure Key Vault voor Microsoft Azure Storage](storage-client-side-encryption.md)

Hier volgt een korte beschrijving van de werking van versleuteling aan de clientzijde:

1. Hello Azure Storage client SDK genereert een inhoud versleutelingssleutel (CEK), die een symmetrische sleutel met een eenmalig gebruik is.
2. Gegevens van de klant is versleuteld met behulp van deze CEK.
3. Hallo wordt CEK vervolgens verpakt (versleuteld) met de belangrijkste versleutelingssleutel hello (KEK-sleutel). Hallo KEK wordt aangeduid met een sleutel-id en een asymmetrisch sleutelpaar of een symmetrische sleutel en kan worden beheerd lokaal of opgeslagen in Azure Sleutelkluis. Hallo opslag client zichzelf heeft nooit toegang toohello KEK-sleutel. Het aanroept zojuist Hallo sleutel wrapping algoritme die wordt geleverd door Sleutelkluis. Klanten kunnen aangepaste providers voor de sleutel als ze willen wrapping/uitpakken toouse kiezen.
4. Hallo versleutelde gegevens is vervolgens toohello Azure Storage-service geüpload.

## <a name="set-up-your-azure-key-vault"></a>Instellen van uw Azure Sleutelkluis
In de volgorde tooproceed in deze zelfstudie, moet u toodo Hallo stappen hebt uitgevoerd, die worden beschreven in de zelfstudie Hallo [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md):

* Een sleutelkluis maken.
* Een sleutel of geheim toohello sleutelkluis toevoegen.
* Registreert een toepassing met Azure Active Directory.
* Autoriseren hello toepassing toouse Hallo sleutel of geheim.

Controleer de opmerking Hallo ClientID en ClientSecret die zijn gegenereerd tijdens het registreren van een toepassing met Azure Active Directory.

Beide sleutels in de sleutelkluis Hallo maken. We gaan ervanuit voor Hallo rest van de zelfstudie Hallo dat u de volgende namen Hallo hebt gebruikt: ContosoKeyVault en TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Maak een consoletoepassing met pakketten en AppSettings
Maak een nieuwe consoletoepassing in Visual Studio.

Benodigde nuget-pakketten in Hallo Package Manager-Console toevoegen.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

AppSettings toohello App.Config toevoegen.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Voeg de volgende Hallo `using` -instructies en zorg ervoor dat tooadd een verwijzing tooSystem.Configuration toohello project.

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Een methode tooget een consoletoepassing token tooyour toevoegen
Hallo wordt volgende methode gebruikt door de Sleutelkluis-klassen die tooauthenticate nodig voor toegang tot tooyour sleutelkluis.

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a>Toegang tot opslag en Sleutelkluis in uw programma
In de functie Main Hallo, toevoegen Hallo code te volgen.

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> Netwerkobjectmodellen voor Sleutelkluis
> 
> Het is belangrijk dat er daadwerkelijk twee Sleutelkluis-object zijn toounderstand toobe op de hoogte van modellen: een is gebaseerd op Hallo REST-API (KeyVault-naamruimte) en Hallo andere is een uitbreiding voor client-side '-versleuteling.
> 
> Hallo Sleutelkluis Client communiceert met de Hallo REST-API en JSON Web sleutels en geheimen voor Hallo twee soorten bewerkingen die zijn opgenomen in de Sleutelkluis begrijpt.
> 
> Hallo Sleutelkluis extensies zijn klassen die lijken speciaal voor client-side '-versleuteling in Azure Storage. Ze bevatten een interface voor sleutels (IKey) en klassen die zijn gebaseerd op Hallo concept van een sleutel-Resolver. Er zijn twee implementaties van dat u nodig hebt tooknow IKey: RSAKey en SymmetricKey. Nu ze toocoincide Hallo dingen die zijn opgenomen in een Sleutelkluis gebeuren op dit moment zijn echter onafhankelijke klassen (zodat Hallo sleutel en geheime opgehaald door Hallo Sleutelkluis Client niet IKey implementeert).
> 
> 

## <a name="encrypt-blob-and-upload"></a>BLOBs versleutelen en uploaden
Hallo volgende code tooencrypt een blob en upload het tooyour Azure storage-account toevoegen. Hallo **ResolveKeyAsync** retourneert een IKey methode die wordt gebruikt.

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

Hieronder volgt een schermafbeelding van Hallo [klassieke Azure-Portal](https://manage.windowsazure.com) voor een blob die zijn versleuteld met behulp van versleuteling aan clientzijde met een sleutel die wordt opgeslagen in de Sleutelkluis. Hallo **KeyId** eigenschap Hallo URI voor de sleutel in de Sleutelkluis die fungeert als KEK Hallo Hallo is. Hallo **EncryptedKey** eigenschap Hallo versleutelde versie van Hallo CEK bevat.

![Schermopname van de metagegevens van de Blob die versleutelingsmetagegevens bevat](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Als u Hallo BlobEncryptionPolicy constructor bekijkt, ziet u dat deze een sleutel-en/of een resolver kan accepteren. Let die op dit moment kunt u een conflictoplosser voor versleuteling heeft momenteel geen ondersteuning bieden voor een standaardsleutel.
> 
> 

## <a name="decrypt-blob-and-download"></a>Blob ontsleutelen en te downloaden
Ontsleuteling is in feite wanneer met behulp van Hallo Resolver zinvol zijn klassen. Hallo-ID van Hallo-sleutel gebruikt voor versleuteling wordt gekoppeld aan blob in de metagegevens Hallo zodat er geen reden voor u tooretrieve Hallo sleutel is en onthouden Hallo koppeling tussen de sleutel en de blob. U hebt zojuist toomake zeker van te zijn dat deze sleutel Hallo blijft in de Sleutelkluis.   

Hallo persoonlijke sleutel van een RSA-sleutel blijft in de Sleutelkluis, dus voor ontsleuteling toooccur, Hallo versleutelde sleutel van Hallo blobmetagegevens met Hallo CEK tooKey kluis voor ontsleuteling wordt verzonden.

Voeg Hallo na toodecrypt Hallo blob die u zojuist hebt geüpload.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Er zijn een aantal andere soorten resolvers toomake Sleutelbeheer eenvoudiger, met inbegrip van: AggregateKeyResolver en CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Gebruik Sleutelkluis geheimen
Hallo manier toouse een geheim met versleuteling aan clientzijde is via Hallo SymmetricKey klasse omdat een geheim in wezen een symmetrische sleutel is. Maar zoals eerder vermeld, een geheim in de Sleutelkluis exact tooa SymmetricKey komt niet overeen. Er zijn een paar dingen toounderstand:

* Hallo-sleutel in een SymmetricKey toobe heeft een vaste lengte: 128, 192, 256, 384 of 512 bits.
* Hallo-sleutel in een SymmetricKey moet Base64-gecodeerd.
* Een Sleutelkluis geheim dat wordt gebruikt als een SymmetricKey moet toohave een inhoudstype van 'application/octet-stream' in de Sleutelkluis.

Hier volgt een voorbeeld in PowerShell voor het maken van een geheim in de Sleutelkluis die kunnen worden gebruikt als een SymmetricKey.
Houd er rekening mee dat Hallo harde code vastgelegd, $key, alleen daartoe demonstratie is. In uw eigen code moet u toogenerate deze sleutel.

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

U kunt Hallo dezelfde aanroep vóór tooretrieve dit geheim als een SymmetricKey gebruiken in uw consoletoepassing.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
Dat is alles. Veel plezier!

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het gebruik van Microsoft Azure Storage met C# [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Zie voor meer informatie over Hallo Blob REST-API, [REST-API van Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Ga voor Hallo meest recente informatie over Microsoft Azure Storage, toohello [Blog van Microsoft Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/).
