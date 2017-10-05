---
title: Aan de slag met blob storage en Visual Studio verbonden services (ASP.NET Core) | Microsoft Docs
description: Hoe u aan de slag met Azure Blob-opslag in een project voor Visual Studio ASP.NET Core nadat u een opslagaccount met behulp van Visual Studio verbonden services hebt gemaakt
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2e8060b44c395ad7c24e7778c0ef65148a3a45de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="021ee-103">Aan de slag met Azure Blob storage en Visual Studio verbonden services (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="021ee-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="021ee-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="021ee-104">Overview</span></span>
<span data-ttu-id="021ee-105">Dit artikel wordt beschreven hoe u aan de slag met Azure Blob storage in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een ASP.NET Core-project waarnaar wordt verwezen in het dialoogvenster Visual Studio verbonden Services toevoegen.</span><span class="sxs-lookup"><span data-stu-id="021ee-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="021ee-106">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens die toegankelijk zijn vanuit overal ter wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="021ee-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="021ee-107">Één blob kan elke grootte zijn.</span><span class="sxs-lookup"><span data-stu-id="021ee-107">A single blob can be any size.</span></span> <span data-ttu-id="021ee-108">BLOBs kunnen worden items zoals afbeeldingen, audio en video-bestanden, onbewerkte gegevens en bestanden.</span><span class="sxs-lookup"><span data-stu-id="021ee-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="021ee-109">Dit artikel wordt beschreven hoe u aan de slag met blob storage nadat u een Azure storage-account hebt gemaakt met behulp van de Visual Studio **verbonden Services toevoegen** dialoogvenster in een project ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="021ee-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="021ee-110">Net als bestanden bevinden zich in mappen, live storage-blobs in containers.</span><span class="sxs-lookup"><span data-stu-id="021ee-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="021ee-111">Nadat u een opslagruimte hebt gemaakt, kunt u een of meer containers maken in de opslag.</span><span class="sxs-lookup"><span data-stu-id="021ee-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="021ee-112">Bijvoorbeeld in een opslag 'Plakboek' genoemd, kunt u containers maken in de opslag, naam 'images' voor het opslaan van afbeeldingen en andere aangeroepen 'audio' audio-bestanden op te slaan.</span><span class="sxs-lookup"><span data-stu-id="021ee-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="021ee-113">Nadat u de containers hebt gemaakt, kunt u afzonderlijke blob bestanden om ze te uploaden.</span><span class="sxs-lookup"><span data-stu-id="021ee-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="021ee-114">Zie [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) voor meer informatie over het bewerken van programmatisch blobs.</span><span class="sxs-lookup"><span data-stu-id="021ee-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="021ee-115">Toegang tot blob-containers in code</span><span class="sxs-lookup"><span data-stu-id="021ee-115">Access blob containers in code</span></span>
<span data-ttu-id="021ee-116">Om programmatisch toegang biedt tot de blobs in ASP.NET Core projecten, moet u de volgende items toevoegen als ze nog niet aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="021ee-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="021ee-117">De volgende code naamruimtedeclaraties toevoegen aan het begin van een C#-bestand waarin u wilt programmatisch toegang biedt tot Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="021ee-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="021ee-118">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="021ee-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="021ee-119">Gebruik de volgende code naar uw verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van de Azure-service.</span><span class="sxs-lookup"><span data-stu-id="021ee-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="021ee-120">**Opmerking:** alle bovenstaande code voor de code in de volgende secties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="021ee-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="021ee-121">Gebruik een **CloudBlobClient** object ophalen van een **CloudBlobContainer** verwijzing naar een bestaande container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="021ee-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="021ee-122">Een container in code maken</span><span class="sxs-lookup"><span data-stu-id="021ee-122">Create a container in code</span></span>
<span data-ttu-id="021ee-123">U kunt ook de **CloudBlobClient** een container maken in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="021ee-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="021ee-124">U hoeft te doen is het toevoegen van een aanroep van **CreateIfNotExistsAsync** zoals in de volgende code:</span><span class="sxs-lookup"><span data-stu-id="021ee-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="021ee-125">**Opmerking:** de API's die het uitvoeren van aanroepen naar Azure storage in ASP.NET Core zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="021ee-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="021ee-126">Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="021ee-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="021ee-127">De volgende code wordt ervan uitgegaan programming async-methoden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="021ee-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="021ee-128">Als u de bestanden in de container beschikbaar wilt maken voor iedereen, kunt u de container als public met behulp van de volgende code instellen.</span><span class="sxs-lookup"><span data-stu-id="021ee-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="021ee-129">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="021ee-129">Upload a blob into a container</span></span>
<span data-ttu-id="021ee-130">Als u wilt een blob-bestand uploaden naar een container, een containerverwijzing ophalen en deze gebruiken een blobverwijzing ophalen.</span><span class="sxs-lookup"><span data-stu-id="021ee-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="021ee-131">Nadat u een blobverwijzing hebt, kunt u een stream met gegevens uploaden naar het door het aanroepen van de **UploadFromStreamAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="021ee-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="021ee-132">Deze bewerking wordt de blob gemaakt als deze nog niet is gebeurd, of deze wordt overschreven als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="021ee-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="021ee-133">Het volgende voorbeeld laat zien hoe u een blob uploadt naar een container. Hierbij wordt ervan uitgegaan dat de container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="021ee-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="021ee-134">De blobs in een container in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="021ee-134">List the blobs in a container</span></span>
<span data-ttu-id="021ee-135">Als u een lijst van de blobs in een container wilt weergeven, moet u eerst een containerverwijzing ophalen.</span><span class="sxs-lookup"><span data-stu-id="021ee-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="021ee-136">Vervolgens kunt u de container aanroepen **ListBlobsSegmentedAsync** methode voor het ophalen van de blobs en/of de mappen hierin.</span><span class="sxs-lookup"><span data-stu-id="021ee-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="021ee-137">Voor toegang tot de uitgebreide set eigenschappen en methoden voor een geretourneerde **IListBlobItem** moet u dit casten naar een object van het type **CloudBlockBlob**, **CloudPageBlob** of **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="021ee-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="021ee-138">Als u het blobtype niet weet, kunt u typecontrole gebruiken om te bepalen welke dit casten naar.</span><span class="sxs-lookup"><span data-stu-id="021ee-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="021ee-139">De volgende code laat zien hoe ophalen en de uitvoer van de URI van elk item in een container.</span><span class="sxs-lookup"><span data-stu-id="021ee-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

<span data-ttu-id="021ee-140">Er zijn andere manieren om de inhoud van een blob-container.</span><span class="sxs-lookup"><span data-stu-id="021ee-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="021ee-141">Zie [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="021ee-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="021ee-142">Een blob downloaden</span><span class="sxs-lookup"><span data-stu-id="021ee-142">Download a blob</span></span>
<span data-ttu-id="021ee-143">Voor het downloaden van een blob, eerst een verwijzing naar de blob ophalen en roept u vervolgens de **DownloadToStreamAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="021ee-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="021ee-144">Het volgende voorbeeld wordt de **DownloadToStreamAsync** methode voor het overdragen van de blobinhoud naar een stroomobject dat u kunt vervolgens opslaan als een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="021ee-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="021ee-145">Er zijn andere manieren om het opslaan van blobs als bestanden.</span><span class="sxs-lookup"><span data-stu-id="021ee-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="021ee-146">Zie [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="021ee-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="021ee-147">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="021ee-147">Delete a blob</span></span>
<span data-ttu-id="021ee-148">Als u wilt verwijderen van een blob, eerst een verwijzing naar de blob ophalen en roept u vervolgens de **DeleteAsync** methode erop.</span><span class="sxs-lookup"><span data-stu-id="021ee-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="021ee-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="021ee-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

