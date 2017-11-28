---
title: aaaGet gestart met blob-opslag- en Visual Studio verbonden services (cloudservices) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure Blob-opslag in een cloud service-project in Visual Studio nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="8a6f3-103">Aan de slag met Azure Blob Storage en Visual Studio verbonden services (cloud services-projecten)</span><span class="sxs-lookup"><span data-stu-id="8a6f3-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="8a6f3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8a6f3-104">Overview</span></span>
<span data-ttu-id="8a6f3-105">Dit artikel wordt beschreven hoe de tooget slag met Azure Blob Storage nadat u hebt gemaakt of een Azure Storage-account waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster in een Visual Studio-cloud services-project.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="8a6f3-106">Leert u hoe tooaccess blob-containers en hoe tooperform algemene taken, zoals uploaden, weergeven en downloaden van blobs en maken.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="8a6f3-107">Hallo-voorbeelden zijn geschreven in C\# en gebruik Hallo [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a6f3-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="8a6f3-108">Azure Blob Storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="8a6f3-109">Één blob kan elke grootte zijn.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-109">A single blob can be any size.</span></span> <span data-ttu-id="8a6f3-110">BLOBs kunnen worden items zoals afbeeldingen, audio en video-bestanden, onbewerkte gegevens en bestanden.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="8a6f3-111">Net als bestanden bevinden zich in mappen, live storage-blobs in containers.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="8a6f3-112">Nadat u een opslagruimte hebt gemaakt, kunt u een of meer containers maken in Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="8a6f3-113">Bijvoorbeeld in een opslag 'Plakboek' genoemd, kunt u containers maken in de opslag van Hallo aangeroepen 'afbeeldingen' toostore afbeeldingen en andere 'audio' toostore aangeroepen audio-bestanden.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="8a6f3-114">Nadat u Hallo containers maken, kunt u afzonderlijke blob bestanden toothem uploaden.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="8a6f3-115">Zie voor meer informatie over het bewerken van programmatisch blobs [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8a6f3-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="8a6f3-116">Raadpleeg voor algemene informatie over Azure Storage [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="8a6f3-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="8a6f3-117">Raadpleeg voor algemene informatie over Azure Cloud Services [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="8a6f3-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="8a6f3-118">Zie voor meer informatie over het programmeren van ASP.NET-toepassingen [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="8a6f3-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="8a6f3-119">Toegang tot blob-containers in code</span><span class="sxs-lookup"><span data-stu-id="8a6f3-119">Access blob containers in code</span></span>
<span data-ttu-id="8a6f3-120">tooprogrammatically toegang tot blobs in cloudserviceprojecten, moet u tooadd Hallo items, te volgen als ze nog niet aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="8a6f3-121">Hallo na code naamruimte declaraties toohello boven aan elk C#-bestand waarin u tooprogrammatically toegang tot Azure Storage wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="8a6f3-122">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8a6f3-123">Gebruik Hallo na code tooget Hallo uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="8a6f3-124">Ophalen van een **CloudBlobClient** object tooreference een bestaande container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="8a6f3-125">Ophalen van een **CloudBlobContainer** object tooreference een specifieke blob-container.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="8a6f3-126">Alle weergegeven in de vorige procedure Hallo voor Hallo-code die wordt weergegeven in de volgende secties Hallo Hallo-code gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="8a6f3-127">Een container in code maken</span><span class="sxs-lookup"><span data-stu-id="8a6f3-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="8a6f3-128">Sommige API's die het uitvoeren van aanroepen uit tooAzure opslag in ASP.NET zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="8a6f3-129">Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="8a6f3-130">Hallo-code in Hallo volgende voorbeeld wordt ervan uitgegaan dat u van programming async-methoden gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="8a6f3-131">een container in uw opslagaccount toocreate, hoeft u toodo is Voeg een aanroep toe te**CreateIfNotExistsAsync** zoals Hallo na de code in:</span><span class="sxs-lookup"><span data-stu-id="8a6f3-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="8a6f3-132">toomake hello bestanden binnen hello container beschikbaar tooeveryone, u kunt instellen Hallo container toobe openbare met behulp van de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="8a6f3-133">Iedereen op Internet Hallo blobs in een openbare container kunt zien, maar u kunt wijzigen of ze alleen verwijderen als u de juiste toegangssleutel Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="8a6f3-134">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="8a6f3-134">Upload a blob into a container</span></span>
<span data-ttu-id="8a6f3-135">Azure Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="8a6f3-136">In Hallo meeste gevallen is het blok-blob Hallo type toouse aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="8a6f3-137">een bestand tooa blok-blob tooupload een containerverwijzing ophalen en deze tooget een blok-blobverwijzing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="8a6f3-138">Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom tooit gegevens uploaden door de aanroepende Hallo **UploadFromStream** methode.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="8a6f3-139">Deze bewerking wordt Hallo blob gemaakt als deze niet eerder bestond, of deze wordt overschreven als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="8a6f3-140">Hallo volgende voorbeeld wordt getoond hoe tooupload een blob naar een container en wordt ervan uitgegaan dat Hallo-container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="8a6f3-141">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="8a6f3-141">List hello blobs in a container</span></span>
<span data-ttu-id="8a6f3-142">toolist hello blobs in een container, eerst ophalen een containerverwijzing.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="8a6f3-143">Vervolgens kunt u Hallo-container **ListBlobs** methode tooretrieve Hallo blobs en/of mappen hierin.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="8a6f3-144">tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **IListBlobItem**, u dit casten tooa **CloudBlockBlob**, **CloudPageBlob**, of  **CloudBlobDirectory** object.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="8a6f3-145">Als Hallo type onbekend is, kunt u een type selectievakje toodetermine welke toocast naar.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="8a6f3-146">Hallo volgende code laat zien hoe tooretrieve en uitvoer URI van elk item in Hallo Hallo **foto's** container:</span><span class="sxs-lookup"><span data-stu-id="8a6f3-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

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

<span data-ttu-id="8a6f3-147">Zoals u in het vorige codevoorbeeld hello, heeft Hallo blob-service Hallo concept van mappen in containers, evenals.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="8a6f3-148">Dit is zodat u kunt uw blobs in een map achtige structuur indelen.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="8a6f3-149">Denk bijvoorbeeld de volgende set blok-blobs in een container met de naam Hallo **foto's**:</span><span class="sxs-lookup"><span data-stu-id="8a6f3-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="8a6f3-150">Als u aanroept **ListBlobs** op Hallo-container (zoals in het vorige voorbeeld Hallo), Hallo verzameling geretourneerd bevat **CloudBlobDirectory** en **CloudBlockBlob** objecten Hallo mappen en blobs die zijn opgenomen op het hoogste niveau Hallo die.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="8a6f3-151">Dit is de resulterende uitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="8a6f3-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="8a6f3-152">Desgewenst kunt u instellen Hallo **UseFlatBlobListing** parameter van Hallo **ListBlobs** methode **true**.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="8a6f3-153">Dit resulteert in elke blob wordt geretourneerd als een **CloudBlockBlob**, ongeacht van de directory.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="8a6f3-154">Hier is Hallo aanroep te**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="8a6f3-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="8a6f3-155">en hier vindt u Hallo resultaten:</span><span class="sxs-lookup"><span data-stu-id="8a6f3-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="8a6f3-156">Zie voor meer informatie [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a6f3-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="8a6f3-157">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="8a6f3-157">Download blobs</span></span>
<span data-ttu-id="8a6f3-158">toodownload blobs, eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo **DownloadToStream** methode.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="8a6f3-159">Hallo volgende voorbeeld wordt Hallo **DownloadToStream** methode tootransfer Hallo blob inhoud tooa stroomobject dat u vervolgens blijven tooa lokaal bestand behouden kunt.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="8a6f3-160">U kunt ook Hallo **DownloadToStream** methode toodownload Hallo inhoud van een blob als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="8a6f3-161">Blobs verwijderen</span><span class="sxs-lookup"><span data-stu-id="8a6f3-161">Delete blobs</span></span>
<span data-ttu-id="8a6f3-162">een blob toodelete eerst een blobverwijzing ophalen en roept u vervolgens de **verwijderen** methode.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="8a6f3-163">Blobs asynchroon op pagina's weergeven</span><span class="sxs-lookup"><span data-stu-id="8a6f3-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="8a6f3-164">Als u een groot aantal blobs aanbiedt of u toocontrol Hallo aantal u in één aanbieding bewerking retourneren resultaten wilt, kunt u op pagina's met resultaten kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="8a6f3-165">Dit voorbeeld toont tooreturn hoe resultaten op pagina's asynchroon, zodat de uitvoering niet wordt geblokkeerd tijdens het wachten op tooreturn een groot aantal resultaten.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="8a6f3-166">Dit voorbeeld ziet u een platte blob weergeven, maar u kunt ook een hiërarchische lijst uitvoeren door de instelling Hallo **useFlatBlobListing** parameter Hallo **ListBlobsSegmentedAsync** methode te **ONWAAR**.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="8a6f3-167">Omdat Hallo voorbeeldmethode een asynchrone methode wordt aangeroepen, moet deze worden voorafgegaan door hello **asynchrone** sleutelwoord en deze moet retourneren een **taak** object.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="8a6f3-168">Hallo await trefwoord opgegeven voor Hallo **ListBlobsSegmentedAsync** methode onderbreekt de uitvoering van Hallo voorbeeldmethode totdat de taak in de lijst Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8a6f3-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="8a6f3-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a6f3-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

