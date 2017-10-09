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
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="3df7a-103">Aan de slag met Azure Blob Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="3df7a-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="3df7a-104">Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat.</span><span class="sxs-lookup"><span data-stu-id="3df7a-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="3df7a-105">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3df7a-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="3df7a-106">BLOB-opslag is ook bedoeld tooas vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="3df7a-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="3df7a-107">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="3df7a-107">About this tutorial</span></span>
<span data-ttu-id="3df7a-108">Deze zelfstudie laat zien hoe toowrite .NET code van enkele algemene scenario's met behulp van Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="3df7a-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="3df7a-109">Scenario's die aan bod komen, zijn onder meer het uploaden, in een lijst weergeven, downloaden en verwijderen van blobs.</span><span class="sxs-lookup"><span data-stu-id="3df7a-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="3df7a-110">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="3df7a-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="3df7a-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3df7a-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="3df7a-112">Azure Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="3df7a-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="3df7a-113">Azure Configuration Manager voor .NET</span><span class="sxs-lookup"><span data-stu-id="3df7a-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="3df7a-114">Een [Azure Storage-account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="3df7a-114">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="3df7a-115">Meer voorbeelden</span><span class="sxs-lookup"><span data-stu-id="3df7a-115">More samples</span></span>
<span data-ttu-id="3df7a-116">Zie [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Aan de slag met Azure Blob Storage in .NET) voor meer voorbeelden van het gebruik van Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3df7a-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="3df7a-117">Hallo-voorbeeldtoepassing downloaden en uitvoeren, of blader Hallo-code op GitHub.</span><span class="sxs-lookup"><span data-stu-id="3df7a-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="3df7a-118">Using-instructies toevoegen</span><span class="sxs-lookup"><span data-stu-id="3df7a-118">Add using directives</span></span>
<span data-ttu-id="3df7a-119">Voeg de volgende Hallo **met** richtlijnen toohello bovenaan Hallo `Program.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="3df7a-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="3df7a-120">Hallo-verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="3df7a-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="3df7a-121">Hallo Blob-serviceclient maken</span><span class="sxs-lookup"><span data-stu-id="3df7a-121">Create hello Blob service client</span></span>
<span data-ttu-id="3df7a-122">Hallo **CloudBlobClient** klasse kunt u tooretrieve containers en blobs die zijn opgeslagen in Blob storage.</span><span class="sxs-lookup"><span data-stu-id="3df7a-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="3df7a-123">Hier volgt een eenrichtingssessie toocreate Hallo-client-service:</span><span class="sxs-lookup"><span data-stu-id="3df7a-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="3df7a-124">U bent nu klaar toowrite-code die gegevens leest uit en schrijft tooBlob gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="3df7a-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="3df7a-125">Een container maken</span><span class="sxs-lookup"><span data-stu-id="3df7a-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="3df7a-126">Dit voorbeeld ziet u hoe toocreate een container als deze niet al bestaat:</span><span class="sxs-lookup"><span data-stu-id="3df7a-126">This example shows how toocreate a container if it does not already exist:</span></span>

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

<span data-ttu-id="3df7a-127">Standaard is de Hallo nieuwe container privé, wat betekent dat u uw opslag toegang tot belangrijke toodownload blobs uit deze container moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="3df7a-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="3df7a-128">Als u toomake Hallo bestanden binnen hello container beschikbaar tooeveryone wilt, kunt u Hallo container toobe openbare met behulp van de volgende code Hallo instellen:</span><span class="sxs-lookup"><span data-stu-id="3df7a-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="3df7a-129">Iedereen op Internet Hallo kunt blobs in een openbare container zien.</span><span class="sxs-lookup"><span data-stu-id="3df7a-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="3df7a-130">U kunt echter wijzigen of ze alleen verwijderen als er Hallo juiste accounttoegangssleutel of een shared access signature.</span><span class="sxs-lookup"><span data-stu-id="3df7a-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="3df7a-131">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="3df7a-131">Upload a blob into a container</span></span>
<span data-ttu-id="3df7a-132">Azure Blob Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="3df7a-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="3df7a-133">In de meeste gevallen is de blok-blob Hallo type toouse aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="3df7a-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="3df7a-134">een bestand tooa blok-blob tooupload een containerverwijzing ophalen en deze tooget een blok-blobverwijzing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3df7a-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="3df7a-135">Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom tooit gegevens uploaden door de aanroepende Hallo **UploadFromStream** methode.</span><span class="sxs-lookup"><span data-stu-id="3df7a-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="3df7a-136">Deze bewerking wordt Hallo blob gemaakt als deze niet eerder bestond, of deze wordt overschreven als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="3df7a-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="3df7a-137">Hallo volgende voorbeeld wordt getoond hoe tooupload een blob naar een container en wordt ervan uitgegaan dat Hallo-container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3df7a-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

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

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="3df7a-138">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="3df7a-138">List hello blobs in a container</span></span>
<span data-ttu-id="3df7a-139">toolist hello blobs in een container, eerst ophalen een containerverwijzing.</span><span class="sxs-lookup"><span data-stu-id="3df7a-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="3df7a-140">Vervolgens kunt u Hallo-container **ListBlobs** methode tooretrieve Hallo blobs en/of mappen hierin.</span><span class="sxs-lookup"><span data-stu-id="3df7a-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="3df7a-141">tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **IListBlobItem**, u dit casten tooa **CloudBlockBlob**, **CloudPageBlob**, of  **CloudBlobDirectory** object.</span><span class="sxs-lookup"><span data-stu-id="3df7a-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="3df7a-142">Als Hallo type onbekend is, kunt u een type selectievakje toodetermine welke toocast naar.</span><span class="sxs-lookup"><span data-stu-id="3df7a-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="3df7a-143">Hallo volgende code laat zien hoe tooretrieve en uitvoer URI van elk item in Hallo Hallo _foto's_ container:</span><span class="sxs-lookup"><span data-stu-id="3df7a-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

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

<span data-ttu-id="3df7a-144">Door padgegevens in blobnamen op te nemen, kunt u een virtuele mapstructuur maken die u kunt ordenen en doorlopen als een traditioneel bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="3df7a-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="3df7a-145">Hallo-mapstructuur virtueel is alleen--Hallo alleen beschikbare resources in Blob storage containers en blobs zijn.</span><span class="sxs-lookup"><span data-stu-id="3df7a-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="3df7a-146">Hallo opslagclientbibliotheek biedt echter een **CloudBlobDirectory** object toorefer tooa virtuele map en Hallo vereenvoudigen van het werken met blobs die op deze manier zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="3df7a-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="3df7a-147">Denk bijvoorbeeld de volgende set blok-blobs in een container met de naam Hallo *foto's*:</span><span class="sxs-lookup"><span data-stu-id="3df7a-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

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

<span data-ttu-id="3df7a-148">Als u aanroept **ListBlobs** op Hallo *foto's* container (zoals in Hallo voorgaande codefragment), een hiërarchische opsomming geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3df7a-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="3df7a-149">Deze bevat zowel **CloudBlobDirectory** en **CloudBlockBlob** objecten, Hallo mappen en blobs in de container hello, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="3df7a-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="3df7a-150">Hallo resulterende uitvoer ziet eruit als:</span><span class="sxs-lookup"><span data-stu-id="3df7a-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="3df7a-151">Desgewenst kunt u instellen Hallo **UseFlatBlobListing** parameter Hallo **ListBlobs** methode **true**.</span><span class="sxs-lookup"><span data-stu-id="3df7a-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="3df7a-152">In dit geval wordt elke blob in Hallo container geretourneerd als een **CloudBlockBlob** object.</span><span class="sxs-lookup"><span data-stu-id="3df7a-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="3df7a-153">Hallo aanroep te**ListBlobs** tooreturn een platte lijst ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="3df7a-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="3df7a-154">en Hallo resultaten zien er als volgt:</span><span class="sxs-lookup"><span data-stu-id="3df7a-154">and hello results look like this:</span></span>

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

## <a name="download-blobs"></a><span data-ttu-id="3df7a-155">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="3df7a-155">Download blobs</span></span>
<span data-ttu-id="3df7a-156">toodownload blobs, eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo **DownloadToStream** methode.</span><span class="sxs-lookup"><span data-stu-id="3df7a-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="3df7a-157">Hallo volgende voorbeeld wordt Hallo **DownloadToStream** methode tootransfer Hallo blob inhoud tooa stroomobject dat u vervolgens blijven tooa lokaal bestand behouden kunt.</span><span class="sxs-lookup"><span data-stu-id="3df7a-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

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

<span data-ttu-id="3df7a-158">U kunt ook Hallo **DownloadToStream** methode toodownload Hallo inhoud van een blob als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="3df7a-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

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

## <a name="delete-blobs"></a><span data-ttu-id="3df7a-159">Blobs verwijderen</span><span class="sxs-lookup"><span data-stu-id="3df7a-159">Delete blobs</span></span>
<span data-ttu-id="3df7a-160">een blob toodelete eerst een blobverwijzing ophalen en roept u vervolgens de **verwijderen** methode erop.</span><span class="sxs-lookup"><span data-stu-id="3df7a-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

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

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="3df7a-161">Blobs asynchroon op pagina's weergeven</span><span class="sxs-lookup"><span data-stu-id="3df7a-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="3df7a-162">Als u een groot aantal blobs aanbiedt of u toocontrol Hallo aantal u in één aanbieding bewerking retourneren resultaten wilt, kunt u op pagina's met resultaten kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="3df7a-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="3df7a-163">Dit voorbeeld toont tooreturn hoe resultaten op pagina's asynchroon, zodat de uitvoering niet wordt geblokkeerd tijdens het wachten op tooreturn een groot aantal resultaten.</span><span class="sxs-lookup"><span data-stu-id="3df7a-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="3df7a-164">Dit voorbeeld ziet u een platte blob weergeven, maar u kunt ook een hiërarchische lijst uitvoeren door de instelling Hallo _useFlatBlobListing_ parameter Hallo **ListBlobsSegmentedAsync** too_false_ methode.</span><span class="sxs-lookup"><span data-stu-id="3df7a-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="3df7a-165">Omdat Hallo voorbeeldmethode een asynchrone methode wordt aangeroepen, moet deze worden voorafgegaan door hello _asynchrone_ sleutelwoord en deze moet retourneren een **taak** object.</span><span class="sxs-lookup"><span data-stu-id="3df7a-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="3df7a-166">Hallo await trefwoord opgegeven voor Hallo **ListBlobsSegmentedAsync** methode onderbreekt de uitvoering van Hallo voorbeeldmethode totdat de taak in de lijst Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3df7a-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

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

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="3df7a-167">Schrijven tooan toevoeg-blob</span><span class="sxs-lookup"><span data-stu-id="3df7a-167">Writing tooan append blob</span></span>
<span data-ttu-id="3df7a-168">Een toevoeg-blob is geoptimaliseerd voor toevoegbewerkingen, zoals logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="3df7a-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="3df7a-169">Zoals een blok-blob bestaat een toevoeg-blob uit blokken, maar wanneer u een nieuw blok tooan toevoeg-blob toevoegt, wordt het altijd toegevoegde toohello einde van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="3df7a-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="3df7a-170">U kunt een bestaand blok in een toevoeg-blob niet bijwerken of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3df7a-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="3df7a-171">Hallo blok-id's voor een toevoeg-blob worden niet weergegeven zoals ze zijn voor een blok-blob.</span><span class="sxs-lookup"><span data-stu-id="3df7a-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="3df7a-172">Elk blok in een toevoeg-blob kan een andere grootte, up tooa maximaal 4 MB en een toevoeg-blob kan maximaal 50.000 blokken bevatten.</span><span class="sxs-lookup"><span data-stu-id="3df7a-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="3df7a-173">Hallo maximale grootte van een toevoeg-blob is daarom iets meer dan 195 GB (4 MB X 50.000 blokken).</span><span class="sxs-lookup"><span data-stu-id="3df7a-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="3df7a-174">Hallo in het volgende voorbeeld maakt u een nieuwe toevoeg-blob en voegt sommige gegevens tooit, een bewerking voor eenvoudige logboekregistratie simuleren.</span><span class="sxs-lookup"><span data-stu-id="3df7a-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

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

<span data-ttu-id="3df7a-175">Zie [blok-Blobs, pagina-Blobs en toevoeg-Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) voor meer informatie over Hallo verschillen tussen Hallo drie typen blobs.</span><span class="sxs-lookup"><span data-stu-id="3df7a-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="3df7a-176">Beveiliging beheren voor blobs</span><span class="sxs-lookup"><span data-stu-id="3df7a-176">Managing security for blobs</span></span>
<span data-ttu-id="3df7a-177">Standaard beveiligt Azure Storage uw gegevens door te beperken van toegang toohello accounteigenaar, die in bezit is van de toegangssleutels Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="3df7a-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="3df7a-178">Wanneer u tooshare blob-gegevens in uw storage-account nodig hebt, is het belangrijk toodo geval Hallo beveiliging van de toegangssleutels van uw account in gevaar.</span><span class="sxs-lookup"><span data-stu-id="3df7a-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="3df7a-179">U kunt bovendien versleutelen tooensure van de blob-gegevens die deze worden beveiligd via de kabel hello en in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3df7a-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="3df7a-180">Toegang tot tooblob gegevens beheren</span><span class="sxs-lookup"><span data-stu-id="3df7a-180">Controlling access tooblob data</span></span>
<span data-ttu-id="3df7a-181">Hallo blobgegevens in uw storage-account is standaard toegankelijk alleen toostorage accounteigenaar.</span><span class="sxs-lookup"><span data-stu-id="3df7a-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="3df7a-182">Verificatie-aanvragen op basis van de Blob-opslag is toegangssleutel Hallo standaard vereist.</span><span class="sxs-lookup"><span data-stu-id="3df7a-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="3df7a-183">Echter, kunt u toomake bepaalde blob-gegevens beschikbaar tooother gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3df7a-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="3df7a-184">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="3df7a-184">You have two options:</span></span>

* <span data-ttu-id="3df7a-185">**Anonieme toegang:** u kunt een container of de blobs erin openbaar beschikbaar maken voor anonieme toegang.</span><span class="sxs-lookup"><span data-stu-id="3df7a-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="3df7a-186">Zie [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3df7a-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="3df7a-187">**Shared access signatures:** u kunt clients voorzien een shared access signature (SAS), waarmee gedelegeerde toegang tooa bron in uw storage-account met machtigingen die u opgeeft en via een interval dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="3df7a-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="3df7a-188">Zie [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Shared Access Signatures (SAS) gebruiken) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3df7a-188">See [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="3df7a-189">Blobgegevens versleutelen</span><span class="sxs-lookup"><span data-stu-id="3df7a-189">Encrypting blob data</span></span>
<span data-ttu-id="3df7a-190">Azure Storage ondersteunt de versleuteling van blobgegevens op Hallo-client en server Hallo:</span><span class="sxs-lookup"><span data-stu-id="3df7a-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="3df7a-191">**Versleuteling aan clientzijde:** Hallo Storage-clientbibliotheek voor .NET biedt ondersteuning voor versleuteling van gegevens binnen clienttoepassingen voordat tooAzure opslag uploaden en ontsleutelen van gegevens tijdens het downloaden van toohello client.</span><span class="sxs-lookup"><span data-stu-id="3df7a-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="3df7a-192">Hallo-bibliotheek ondersteunt ook integratie met Azure Key Vault voor sleutelbeheer storage-account.</span><span class="sxs-lookup"><span data-stu-id="3df7a-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="3df7a-193">Zie [Versleuteling aan clientzijde met .NET voor Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3df7a-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span> <span data-ttu-id="3df7a-194">Zie ook [Zelfstudie: blobs versleutelen en ontsleutelen in Microsoft Azure Storage met Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="3df7a-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="3df7a-195">**Versleuteling aan serverzijde**: Azure Storage ondersteunt nu ook versleuteling aan serverzijde.</span><span class="sxs-lookup"><span data-stu-id="3df7a-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="3df7a-196">Zie [Azure Storage-service: versleuteling van data-at-rest (preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3df7a-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3df7a-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3df7a-197">Next steps</span></span>
<span data-ttu-id="3df7a-198">Nu u Hallo basisprincipes van Blob storage hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="3df7a-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="3df7a-199">Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="3df7a-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="3df7a-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="3df7a-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="3df7a-201">Voorbeelden van Blob Storage</span><span class="sxs-lookup"><span data-stu-id="3df7a-201">Blob storage samples</span></span>
* [<span data-ttu-id="3df7a-202">Aan de slag met Azure Blob Storage in .NET</span><span class="sxs-lookup"><span data-stu-id="3df7a-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="3df7a-203">Naslaginformatie over Blob Storage</span><span class="sxs-lookup"><span data-stu-id="3df7a-203">Blob storage reference</span></span>
* [<span data-ttu-id="3df7a-204">Naslaginformatie over de Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="3df7a-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="3df7a-205">Naslaginformatie over REST API</span><span class="sxs-lookup"><span data-stu-id="3df7a-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="3df7a-206">Conceptuele handleidingen</span><span class="sxs-lookup"><span data-stu-id="3df7a-206">Conceptual guides</span></span>
* [<span data-ttu-id="3df7a-207">Gegevensoverdracht met Hallo AzCopy-opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="3df7a-207">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="3df7a-208">Aan de slag met File Storage voor .NET</span><span class="sxs-lookup"><span data-stu-id="3df7a-208">Get started with File storage for .NET</span></span>](../files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="3df7a-209">Hoe toouse Azure blob-opslag met Hallo WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="3df7a-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
