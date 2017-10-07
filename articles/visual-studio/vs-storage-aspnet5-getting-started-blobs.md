---
title: aaaGet gestart met blob-opslag- en Visual Studio verbonden services (ASP.NET Core) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure Blob-opslag in een project voor Visual Studio ASP.NET Core nadat u een opslagaccount met Visual Studio hebt gemaakt, verbonden services
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
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="d1f19-103">Aan de slag met Azure Blob storage en Visual Studio verbonden services (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="d1f19-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d1f19-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d1f19-104">Overview</span></span>
<span data-ttu-id="d1f19-105">Dit artikel wordt beschreven hoe het gebruik van Azure Blob-opslag in Visual Studio, nadat u hebt gemaakt of een Azure storage-account in een ASP.NET Core-project waarnaar wordt verwezen met behulp van Visual Studio verbonden Services toevoegen-dialoogvenster Hallo van tooget wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d1f19-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="d1f19-106">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d1f19-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="d1f19-107">Één blob kan elke grootte zijn.</span><span class="sxs-lookup"><span data-stu-id="d1f19-107">A single blob can be any size.</span></span> <span data-ttu-id="d1f19-108">BLOBs kunnen worden items zoals afbeeldingen, audio en video-bestanden, onbewerkte gegevens en bestanden.</span><span class="sxs-lookup"><span data-stu-id="d1f19-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="d1f19-109">Dit artikel wordt beschreven hoe tooget gestart met blob storage nadat u een Azure storage-account hebt gemaakt met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster in een project ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d1f19-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="d1f19-110">Net als bestanden bevinden zich in mappen, live storage-blobs in containers.</span><span class="sxs-lookup"><span data-stu-id="d1f19-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="d1f19-111">Nadat u een opslagruimte hebt gemaakt, kunt u een of meer containers maken in Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="d1f19-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="d1f19-112">Bijvoorbeeld in een opslag 'Plakboek' genoemd, kunt u containers maken in de opslag van Hallo aangeroepen 'afbeeldingen' toostore afbeeldingen en andere 'audio' toostore aangeroepen audio-bestanden.</span><span class="sxs-lookup"><span data-stu-id="d1f19-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="d1f19-113">Nadat u Hallo containers maken, kunt u afzonderlijke blob bestanden toothem uploaden.</span><span class="sxs-lookup"><span data-stu-id="d1f19-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="d1f19-114">Zie [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) voor meer informatie over het bewerken van programmatisch blobs.</span><span class="sxs-lookup"><span data-stu-id="d1f19-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="d1f19-115">Toegang tot blob-containers in code</span><span class="sxs-lookup"><span data-stu-id="d1f19-115">Access blob containers in code</span></span>
<span data-ttu-id="d1f19-116">tooprogrammatically toegang tot blobs in ASP.NET Core projecten, moet u tooadd Hallo volgende items, als ze nog niet aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="d1f19-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="d1f19-117">Hallo na code naamruimte declaraties toohello boven aan elk C#-bestand waarin u tooprogrammatically toegang tot Azure-opslag wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d1f19-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="d1f19-118">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="d1f19-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d1f19-119">Gebruik Hallo code tooget na uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="d1f19-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="d1f19-120">**Opmerking:** alle Hallo bovenstaande code voor Hallo code gebruiken in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d1f19-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="d1f19-121">Gebruik een **CloudBlobClient** object tooget een **CloudBlobContainer** verwijzing tooan bestaande container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d1f19-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="d1f19-122">Een container in code maken</span><span class="sxs-lookup"><span data-stu-id="d1f19-122">Create a container in code</span></span>
<span data-ttu-id="d1f19-123">U kunt ook Hallo **CloudBlobClient** toocreate een container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d1f19-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="d1f19-124">Alles wat u nodig hebt toodo is een aanroep van tooadd te**CreateIfNotExistsAsync** zoals Hallo na de code in:</span><span class="sxs-lookup"><span data-stu-id="d1f19-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="d1f19-125">**Opmerking:** Hallo API's die aanroepen tooAzure opslag in ASP.NET Core uitvoeren zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="d1f19-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="d1f19-126">Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d1f19-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="d1f19-127">Hallo-code hieronder wordt ervan uitgegaan programming async-methoden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d1f19-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="d1f19-128">toomake hello bestanden binnen hello container beschikbaar tooeveryone, u kunt instellen Hallo container toobe openbare met behulp van de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1f19-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d1f19-129">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="d1f19-129">Upload a blob into a container</span></span>
<span data-ttu-id="d1f19-130">tooupload een blob-bestand naar een container een containerverwijzing ophalen en deze tooget een blobverwijzing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d1f19-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="d1f19-131">Nadat u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom tooit gegevens uploaden door de aanroepende Hallo **UploadFromStreamAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="d1f19-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="d1f19-132">Deze bewerking wordt Hallo blob gemaakt als deze nog niet is gebeurd, of deze wordt overschreven als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="d1f19-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="d1f19-133">Hallo volgende voorbeeld wordt getoond hoe tooupload een blob naar een container en wordt ervan uitgegaan dat Hallo-container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d1f19-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="d1f19-134">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="d1f19-134">List hello blobs in a container</span></span>
<span data-ttu-id="d1f19-135">toolist hello blobs in een container, eerst ophalen een containerverwijzing.</span><span class="sxs-lookup"><span data-stu-id="d1f19-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="d1f19-136">Vervolgens kunt u Hallo-container aanroepen **ListBlobsSegmentedAsync** methode tooretrieve Hallo blobs en/of mappen hierin.</span><span class="sxs-lookup"><span data-stu-id="d1f19-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="d1f19-137">tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **IListBlobItem**, u dit casten tooa **CloudBlockBlob**, **CloudPageBlob**, of  **CloudBlobDirectory** object.</span><span class="sxs-lookup"><span data-stu-id="d1f19-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="d1f19-138">Als u Hallo blob, typt u niet weet, kunt u een type selectievakje toodetermine welke toocast naar.</span><span class="sxs-lookup"><span data-stu-id="d1f19-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="d1f19-139">Hallo volgende code laat zien hoe tooretrieve en uitvoer Hallo URI van elk item in een container.</span><span class="sxs-lookup"><span data-stu-id="d1f19-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

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

<span data-ttu-id="d1f19-140">Er zijn andere manieren toolist Hallo inhoud van een blob-container.</span><span class="sxs-lookup"><span data-stu-id="d1f19-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="d1f19-141">Zie [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d1f19-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="d1f19-142">Een blob downloaden</span><span class="sxs-lookup"><span data-stu-id="d1f19-142">Download a blob</span></span>
<span data-ttu-id="d1f19-143">toodownload een blob eerst een verwijzing toohello blob ophalen en deze vervolgens aanroepen Hallo **DownloadToStreamAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="d1f19-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="d1f19-144">Hallo volgende voorbeeld wordt Hallo **DownloadToStreamAsync** methode tootransfer Hallo blob inhoud tooa stroomobject dat u kunt vervolgens opslaan als een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="d1f19-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="d1f19-145">Er zijn andere manieren toosave blobs als bestanden.</span><span class="sxs-lookup"><span data-stu-id="d1f19-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="d1f19-146">Zie [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d1f19-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="d1f19-147">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="d1f19-147">Delete a blob</span></span>
<span data-ttu-id="d1f19-148">toodelete een blob eerst een verwijzing toohello blob ophalen en deze vervolgens aanroepen Hallo **DeleteAsync** methode erop.</span><span class="sxs-lookup"><span data-stu-id="d1f19-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="d1f19-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1f19-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

