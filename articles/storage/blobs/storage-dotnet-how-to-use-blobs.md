---
title: aaaGet de slag met Azure Blob storage (objectopslag) met .NET | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 3df0cf14b69d85cdc2f62cc3c8b901be102fa026
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a>Aan de slag met Azure Blob Storage met .NET

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat. In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen. BLOB-opslag is ook bedoeld tooas vorm van objectopslag.

### <a name="about-this-tutorial"></a>Over deze zelfstudie
Deze zelfstudie laat zien hoe toowrite .NET code van enkele algemene scenario's met behulp van Azure Blob-opslag. Scenario's die aan bod komen, zijn onder meer het uploaden, in een lijst weergeven, downloaden en verwijderen van blobs.

**Vereisten:**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Azure Configuration Manager voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Een [Azure Storage-account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Meer voorbeelden
Zie [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Aan de slag met Azure Blob Storage in .NET) voor meer voorbeelden van het gebruik van Blob Storage. Hallo-voorbeeldtoepassing downloaden en uitvoeren, of blader Hallo-code op GitHub.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Using-instructies toevoegen
Voeg de volgende Hallo **met** richtlijnen toohello bovenaan Hallo `Program.cs` bestand:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Hallo-verbindingsreeks parseren
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Hallo Blob-serviceclient maken
Hallo **CloudBlobClient** klasse kunt u tooretrieve containers en blobs die zijn opgeslagen in Blob storage. Hier volgt een eenrichtingssessie toocreate Hallo-client-service:

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
U bent nu klaar toowrite-code die gegevens leest uit en schrijft tooBlob gegevensopslag.

## <a name="create-a-container"></a>Een container maken
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Dit voorbeeld ziet u hoe toocreate een container als deze niet al bestaat:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

Standaard is de Hallo nieuwe container privé, wat betekent dat u uw opslag toegang tot belangrijke toodownload blobs uit deze container moet opgeven. Als u toomake Hallo bestanden binnen hello container beschikbaar tooeveryone wilt, kunt u Hallo container toobe openbare met behulp van de volgende code Hallo instellen:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Iedereen op Internet Hallo kunt blobs in een openbare container zien. U kunt echter wijzigen of ze alleen verwijderen als er Hallo juiste accounttoegangssleutel of een shared access signature.

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
Azure Blob Storage ondersteunt blok-blobs en pagina-blobs.  In de meeste gevallen is de blok-blob Hallo type toouse aanbevolen.

een bestand tooa blok-blob tooupload een containerverwijzing ophalen en deze tooget een blok-blobverwijzing gebruiken. Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom tooit gegevens uploaden door de aanroepende Hallo **UploadFromStream** methode. Deze bewerking wordt Hallo blob gemaakt als deze niet eerder bestond, of deze wordt overschreven als deze bestaat.

Hallo volgende voorbeeld wordt getoond hoe tooupload een blob naar een container en wordt ervan uitgegaan dat Hallo-container al is gemaakt.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
toolist hello blobs in een container, eerst ophalen een containerverwijzing. Vervolgens kunt u Hallo-container **ListBlobs** methode tooretrieve Hallo blobs en/of mappen hierin. tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **IListBlobItem**, u dit casten tooa **CloudBlockBlob**, **CloudPageBlob**, of  **CloudBlobDirectory** object. Als Hallo type onbekend is, kunt u een type selectievakje toodetermine welke toocast naar. Hallo volgende code laat zien hoe tooretrieve en uitvoer URI van elk item in Hallo Hallo _foto's_ container:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

Door padgegevens in blobnamen op te nemen, kunt u een virtuele mapstructuur maken die u kunt ordenen en doorlopen als een traditioneel bestandssysteem. Hallo-mapstructuur virtueel is alleen--Hallo alleen beschikbare resources in Blob storage containers en blobs zijn. Hallo opslagclientbibliotheek biedt echter een **CloudBlobDirectory** object toorefer tooa virtuele map en Hallo vereenvoudigen van het werken met blobs die op deze manier zijn ingedeeld.

Denk bijvoorbeeld de volgende set blok-blobs in een container met de naam Hallo *foto's*:

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

Als u aanroept **ListBlobs** op Hallo *foto's* container (zoals in Hallo voorgaande codefragment), een hiërarchische opsomming geretourneerd. Deze bevat zowel **CloudBlobDirectory** en **CloudBlockBlob** objecten, Hallo mappen en blobs in de container hello, respectievelijk. Hallo resulterende uitvoer ziet eruit als:

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Desgewenst kunt u instellen Hallo **UseFlatBlobListing** parameter Hallo **ListBlobs** methode **true**. In dit geval wordt elke blob in Hallo container geretourneerd als een **CloudBlockBlob** object. Hallo aanroep te**ListBlobs** tooreturn een platte lijst ziet er als volgt:

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

en Hallo resultaten zien er als volgt:

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Blobs downloaden
toodownload blobs, eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo **DownloadToStream** methode. Hallo volgende voorbeeld wordt Hallo **DownloadToStream** methode tootransfer Hallo blob inhoud tooa stroomobject dat u vervolgens blijven tooa lokaal bestand behouden kunt.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

U kunt ook Hallo **DownloadToStream** methode toodownload Hallo inhoud van een blob als een tekenreeks.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a>Blobs verwijderen
een blob toodelete eerst een blobverwijzing ophalen en roept u vervolgens de **verwijderen** methode erop.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a>Blobs asynchroon op pagina's weergeven
Als u een groot aantal blobs aanbiedt of u toocontrol Hallo aantal u in één aanbieding bewerking retourneren resultaten wilt, kunt u op pagina's met resultaten kunt weergeven. Dit voorbeeld toont tooreturn hoe resultaten op pagina's asynchroon, zodat de uitvoering niet wordt geblokkeerd tijdens het wachten op tooreturn een groot aantal resultaten.

Dit voorbeeld ziet u een platte blob weergeven, maar u kunt ook een hiërarchische lijst uitvoeren door de instelling Hallo _useFlatBlobListing_ parameter Hallo **ListBlobsSegmentedAsync** too_false_ methode.

Omdat Hallo voorbeeldmethode een asynchrone methode wordt aangeroepen, moet deze worden voorafgegaan door hello _asynchrone_ sleutelwoord en deze moet retourneren een **taak** object. Hallo await trefwoord opgegeven voor Hallo **ListBlobsSegmentedAsync** methode onderbreekt de uitvoering van Hallo voorbeeldmethode totdat de taak in de lijst Hallo is voltooid.

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a>Schrijven tooan toevoeg-blob
Een toevoeg-blob is geoptimaliseerd voor toevoegbewerkingen, zoals logboekregistratie. Zoals een blok-blob bestaat een toevoeg-blob uit blokken, maar wanneer u een nieuw blok tooan toevoeg-blob toevoegt, wordt het altijd toegevoegde toohello einde van Hallo blob. U kunt een bestaand blok in een toevoeg-blob niet bijwerken of verwijderen. Hallo blok-id's voor een toevoeg-blob worden niet weergegeven zoals ze zijn voor een blok-blob.

Elk blok in een toevoeg-blob kan een andere grootte, up tooa maximaal 4 MB en een toevoeg-blob kan maximaal 50.000 blokken bevatten. Hallo maximale grootte van een toevoeg-blob is daarom iets meer dan 195 GB (4 MB X 50.000 blokken).

Hallo in het volgende voorbeeld maakt u een nieuwe toevoeg-blob en voegt sommige gegevens tooit, een bewerking voor eenvoudige logboekregistratie simuleren.

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

Zie [blok-Blobs, pagina-Blobs en toevoeg-Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) voor meer informatie over Hallo verschillen tussen Hallo drie typen blobs.

## <a name="managing-security-for-blobs"></a>Beveiliging beheren voor blobs
Standaard beveiligt Azure Storage uw gegevens door te beperken van toegang toohello accounteigenaar, die in bezit is van de toegangssleutels Hallo-account. Wanneer u tooshare blob-gegevens in uw storage-account nodig hebt, is het belangrijk toodo geval Hallo beveiliging van de toegangssleutels van uw account in gevaar. U kunt bovendien versleutelen tooensure van de blob-gegevens die deze worden beveiligd via de kabel hello en in Azure Storage.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Toegang tot tooblob gegevens beheren
Hallo blobgegevens in uw storage-account is standaard toegankelijk alleen toostorage accounteigenaar. Verificatie-aanvragen op basis van de Blob-opslag is toegangssleutel Hallo standaard vereist. Echter, kunt u toomake bepaalde blob-gegevens beschikbaar tooother gebruikers. U hebt hiervoor twee opties:

* **Anonieme toegang:** u kunt een container of de blobs erin openbaar beschikbaar maken voor anonieme toegang. Zie [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md) voor meer informatie.
* **Shared access signatures:** u kunt clients voorzien een shared access signature (SAS), waarmee gedelegeerde toegang tooa bron in uw storage-account met machtigingen die u opgeeft en via een interval dat u opgeeft. Zie [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Shared Access Signatures (SAS) gebruiken) voor meer informatie.

### <a name="encrypting-blob-data"></a>Blobgegevens versleutelen
Azure Storage ondersteunt de versleuteling van blobgegevens op Hallo-client en server Hallo:

* **Versleuteling aan clientzijde:** Hallo Storage-clientbibliotheek voor .NET biedt ondersteuning voor versleuteling van gegevens binnen clienttoepassingen voordat tooAzure opslag uploaden en ontsleutelen van gegevens tijdens het downloaden van toohello client. Hallo-bibliotheek ondersteunt ook integratie met Azure Key Vault voor sleutelbeheer storage-account. Zie [Versleuteling aan clientzijde met .NET voor Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) voor meer informatie. Zie ook [Zelfstudie: blobs versleutelen en ontsleutelen in Microsoft Azure Storage met Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).
* **Versleuteling aan serverzijde**: Azure Storage ondersteunt nu ook versleuteling aan serverzijde. Zie [Azure Storage-service: versleuteling van data-at-rest (preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Blob storage hebt geleerd, volgt u deze koppelingen toolearn meer.

### <a name="microsoft-azure-storage-explorer"></a>Microsoft Azure Storage Explorer
* [Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.

### <a name="blob-storage-samples"></a>Voorbeelden van Blob Storage
* [Aan de slag met Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Naslaginformatie over Blob Storage
* [Naslaginformatie over de Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Naslaginformatie over REST API](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Conceptuele handleidingen
* [Gegevensoverdracht met Hallo AzCopy-opdrachtregelprogramma](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Aan de slag met File Storage voor .NET](../files/storage-dotnet-how-to-use-files.md)
* [Hoe toouse Azure blob-opslag met Hallo WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
