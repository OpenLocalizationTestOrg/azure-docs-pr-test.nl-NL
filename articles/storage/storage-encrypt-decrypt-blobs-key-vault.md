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
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="c338d-103">Zelfstudie: Blobs versleutelen en ontsleutelen in Microsoft Azure Storage met Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="c338d-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="c338d-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="c338d-104">Introduction</span></span>
<span data-ttu-id="c338d-105">Deze zelfstudie bevat informatie over hoe toomake gebruiken van client-side opslagversleuteling met Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c338d-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="c338d-106">Dit laat zien hoe u tooencrypt en ontsleutelen van een blob in een consoletoepassing met behulp van deze technologieën.</span><span class="sxs-lookup"><span data-stu-id="c338d-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="c338d-107">**Geschatte tijd toocomplete:** 20 minuten</span><span class="sxs-lookup"><span data-stu-id="c338d-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="c338d-108">Zie voor informatie over Azure Sleutelkluis [wat is Azure Sleutelkluis?](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c338d-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="c338d-109">Zie voor informatie over client-side '-versleuteling voor Azure Storage, [Client-Side-versleuteling en Azure Key Vault voor Microsoft Azure Storage](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="c338d-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c338d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c338d-110">Prerequisites</span></span>
<span data-ttu-id="c338d-111">toocomplete in deze zelfstudie hebt u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c338d-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c338d-112">Een Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="c338d-112">An Azure Storage account</span></span>
* <span data-ttu-id="c338d-113">Visual Studio 2013 of hoger</span><span class="sxs-lookup"><span data-stu-id="c338d-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="c338d-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c338d-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="c338d-115">Overzicht van client-side '-versleuteling</span><span class="sxs-lookup"><span data-stu-id="c338d-115">Overview of client-side encryption</span></span>
<span data-ttu-id="c338d-116">Zie voor een overzicht van client-side '-versleuteling voor Azure Storage [Client-Side-versleuteling en Azure Key Vault voor Microsoft Azure Storage](storage-client-side-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="c338d-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md)</span></span>

<span data-ttu-id="c338d-117">Hier volgt een korte beschrijving van de werking van versleuteling aan de clientzijde:</span><span class="sxs-lookup"><span data-stu-id="c338d-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="c338d-118">Hello Azure Storage client SDK genereert een inhoud versleutelingssleutel (CEK), die een symmetrische sleutel met een eenmalig gebruik is.</span><span class="sxs-lookup"><span data-stu-id="c338d-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="c338d-119">Gegevens van de klant is versleuteld met behulp van deze CEK.</span><span class="sxs-lookup"><span data-stu-id="c338d-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="c338d-120">Hallo wordt CEK vervolgens verpakt (versleuteld) met de belangrijkste versleutelingssleutel hello (KEK-sleutel).</span><span class="sxs-lookup"><span data-stu-id="c338d-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="c338d-121">Hallo KEK wordt aangeduid met een sleutel-id en een asymmetrisch sleutelpaar of een symmetrische sleutel en kan worden beheerd lokaal of opgeslagen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c338d-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="c338d-122">Hallo opslag client zichzelf heeft nooit toegang toohello KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c338d-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="c338d-123">Het aanroept zojuist Hallo sleutel wrapping algoritme die wordt geleverd door Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c338d-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="c338d-124">Klanten kunnen aangepaste providers voor de sleutel als ze willen wrapping/uitpakken toouse kiezen.</span><span class="sxs-lookup"><span data-stu-id="c338d-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="c338d-125">Hallo versleutelde gegevens is vervolgens toohello Azure Storage-service geüpload.</span><span class="sxs-lookup"><span data-stu-id="c338d-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="c338d-126">Instellen van uw Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="c338d-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="c338d-127">In de volgorde tooproceed in deze zelfstudie, moet u toodo Hallo stappen hebt uitgevoerd, die worden beschreven in de zelfstudie Hallo [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="c338d-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="c338d-128">Een sleutelkluis maken.</span><span class="sxs-lookup"><span data-stu-id="c338d-128">Create a key vault.</span></span>
* <span data-ttu-id="c338d-129">Een sleutel of geheim toohello sleutelkluis toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c338d-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="c338d-130">Registreert een toepassing met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c338d-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="c338d-131">Autoriseren hello toepassing toouse Hallo sleutel of geheim.</span><span class="sxs-lookup"><span data-stu-id="c338d-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="c338d-132">Controleer de opmerking Hallo ClientID en ClientSecret die zijn gegenereerd tijdens het registreren van een toepassing met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c338d-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="c338d-133">Beide sleutels in de sleutelkluis Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="c338d-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="c338d-134">We gaan ervanuit voor Hallo rest van de zelfstudie Hallo dat u de volgende namen Hallo hebt gebruikt: ContosoKeyVault en TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="c338d-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="c338d-135">Maak een consoletoepassing met pakketten en AppSettings</span><span class="sxs-lookup"><span data-stu-id="c338d-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="c338d-136">Maak een nieuwe consoletoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c338d-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="c338d-137">Benodigde nuget-pakketten in Hallo Package Manager-Console toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c338d-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="c338d-138">AppSettings toohello App.Config toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c338d-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="c338d-139">Voeg de volgende Hallo `using` -instructies en zorg ervoor dat tooadd een verwijzing tooSystem.Configuration toohello project.</span><span class="sxs-lookup"><span data-stu-id="c338d-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="c338d-140">Een methode tooget een consoletoepassing token tooyour toevoegen</span><span class="sxs-lookup"><span data-stu-id="c338d-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="c338d-141">Hallo wordt volgende methode gebruikt door de Sleutelkluis-klassen die tooauthenticate nodig voor toegang tot tooyour sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c338d-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

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

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="c338d-142">Toegang tot opslag en Sleutelkluis in uw programma</span><span class="sxs-lookup"><span data-stu-id="c338d-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="c338d-143">In de functie Main Hallo, toevoegen Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="c338d-143">In hello Main function, add hello following code.</span></span>

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
> <span data-ttu-id="c338d-144">Netwerkobjectmodellen voor Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="c338d-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="c338d-145">Het is belangrijk dat er daadwerkelijk twee Sleutelkluis-object zijn toounderstand toobe op de hoogte van modellen: een is gebaseerd op Hallo REST-API (KeyVault-naamruimte) en Hallo andere is een uitbreiding voor client-side '-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="c338d-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="c338d-146">Hallo Sleutelkluis Client communiceert met de Hallo REST-API en JSON Web sleutels en geheimen voor Hallo twee soorten bewerkingen die zijn opgenomen in de Sleutelkluis begrijpt.</span><span class="sxs-lookup"><span data-stu-id="c338d-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="c338d-147">Hallo Sleutelkluis extensies zijn klassen die lijken speciaal voor client-side '-versleuteling in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c338d-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="c338d-148">Ze bevatten een interface voor sleutels (IKey) en klassen die zijn gebaseerd op Hallo concept van een sleutel-Resolver.</span><span class="sxs-lookup"><span data-stu-id="c338d-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="c338d-149">Er zijn twee implementaties van dat u nodig hebt tooknow IKey: RSAKey en SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="c338d-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="c338d-150">Nu ze toocoincide Hallo dingen die zijn opgenomen in een Sleutelkluis gebeuren op dit moment zijn echter onafhankelijke klassen (zodat Hallo sleutel en geheime opgehaald door Hallo Sleutelkluis Client niet IKey implementeert).</span><span class="sxs-lookup"><span data-stu-id="c338d-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="c338d-151">BLOBs versleutelen en uploaden</span><span class="sxs-lookup"><span data-stu-id="c338d-151">Encrypt blob and upload</span></span>
<span data-ttu-id="c338d-152">Hallo volgende code tooencrypt een blob en upload het tooyour Azure storage-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c338d-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="c338d-153">Hallo **ResolveKeyAsync** retourneert een IKey methode die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c338d-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

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

<span data-ttu-id="c338d-154">Hieronder volgt een schermafbeelding van Hallo [klassieke Azure-Portal](https://manage.windowsazure.com) voor een blob die zijn versleuteld met behulp van versleuteling aan clientzijde met een sleutel die wordt opgeslagen in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c338d-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="c338d-155">Hallo **KeyId** eigenschap Hallo URI voor de sleutel in de Sleutelkluis die fungeert als KEK Hallo Hallo is.</span><span class="sxs-lookup"><span data-stu-id="c338d-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="c338d-156">Hallo **EncryptedKey** eigenschap Hallo versleutelde versie van Hallo CEK bevat.</span><span class="sxs-lookup"><span data-stu-id="c338d-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Schermopname van de metagegevens van de Blob die versleutelingsmetagegevens bevat](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="c338d-158">Als u Hallo BlobEncryptionPolicy constructor bekijkt, ziet u dat deze een sleutel-en/of een resolver kan accepteren.</span><span class="sxs-lookup"><span data-stu-id="c338d-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="c338d-159">Let die op dit moment kunt u een conflictoplosser voor versleuteling heeft momenteel geen ondersteuning bieden voor een standaardsleutel.</span><span class="sxs-lookup"><span data-stu-id="c338d-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="c338d-160">Blob ontsleutelen en te downloaden</span><span class="sxs-lookup"><span data-stu-id="c338d-160">Decrypt blob and download</span></span>
<span data-ttu-id="c338d-161">Ontsleuteling is in feite wanneer met behulp van Hallo Resolver zinvol zijn klassen.</span><span class="sxs-lookup"><span data-stu-id="c338d-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="c338d-162">Hallo-ID van Hallo-sleutel gebruikt voor versleuteling wordt gekoppeld aan blob in de metagegevens Hallo zodat er geen reden voor u tooretrieve Hallo sleutel is en onthouden Hallo koppeling tussen de sleutel en de blob.</span><span class="sxs-lookup"><span data-stu-id="c338d-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="c338d-163">U hebt zojuist toomake zeker van te zijn dat deze sleutel Hallo blijft in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c338d-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="c338d-164">Hallo persoonlijke sleutel van een RSA-sleutel blijft in de Sleutelkluis, dus voor ontsleuteling toooccur, Hallo versleutelde sleutel van Hallo blobmetagegevens met Hallo CEK tooKey kluis voor ontsleuteling wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="c338d-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="c338d-165">Voeg Hallo na toodecrypt Hallo blob die u zojuist hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="c338d-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="c338d-166">Er zijn een aantal andere soorten resolvers toomake Sleutelbeheer eenvoudiger, met inbegrip van: AggregateKeyResolver en CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="c338d-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="c338d-167">Gebruik Sleutelkluis geheimen</span><span class="sxs-lookup"><span data-stu-id="c338d-167">Use Key Vault secrets</span></span>
<span data-ttu-id="c338d-168">Hallo manier toouse een geheim met versleuteling aan clientzijde is via Hallo SymmetricKey klasse omdat een geheim in wezen een symmetrische sleutel is.</span><span class="sxs-lookup"><span data-stu-id="c338d-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="c338d-169">Maar zoals eerder vermeld, een geheim in de Sleutelkluis exact tooa SymmetricKey komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="c338d-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="c338d-170">Er zijn een paar dingen toounderstand:</span><span class="sxs-lookup"><span data-stu-id="c338d-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="c338d-171">Hallo-sleutel in een SymmetricKey toobe heeft een vaste lengte: 128, 192, 256, 384 of 512 bits.</span><span class="sxs-lookup"><span data-stu-id="c338d-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="c338d-172">Hallo-sleutel in een SymmetricKey moet Base64-gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="c338d-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="c338d-173">Een Sleutelkluis geheim dat wordt gebruikt als een SymmetricKey moet toohave een inhoudstype van 'application/octet-stream' in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c338d-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="c338d-174">Hier volgt een voorbeeld in PowerShell voor het maken van een geheim in de Sleutelkluis die kunnen worden gebruikt als een SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="c338d-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="c338d-175">Houd er rekening mee dat Hallo harde code vastgelegd, $key, alleen daartoe demonstratie is.</span><span class="sxs-lookup"><span data-stu-id="c338d-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="c338d-176">In uw eigen code moet u toogenerate deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="c338d-176">In your own code you'll want toogenerate this key.</span></span>

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

<span data-ttu-id="c338d-177">U kunt Hallo dezelfde aanroep vóór tooretrieve dit geheim als een SymmetricKey gebruiken in uw consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="c338d-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="c338d-178">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="c338d-178">That's it.</span></span> <span data-ttu-id="c338d-179">Veel plezier!</span><span class="sxs-lookup"><span data-stu-id="c338d-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="c338d-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c338d-180">Next steps</span></span>
<span data-ttu-id="c338d-181">Zie voor meer informatie over het gebruik van Microsoft Azure Storage met C# [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="c338d-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="c338d-182">Zie voor meer informatie over Hallo Blob REST-API, [REST-API van Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="c338d-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="c338d-183">Ga voor Hallo meest recente informatie over Microsoft Azure Storage, toohello [Blog van Microsoft Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="c338d-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
