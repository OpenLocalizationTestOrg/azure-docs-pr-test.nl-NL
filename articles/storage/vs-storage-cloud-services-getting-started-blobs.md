---
title: Aan de slag met blob storage en Visual Studio verbonden services (cloudservices) | Microsoft Docs
description: Hoe u aan de slag met Azure Blob-opslag in een cloud service-project in Visual Studio nadat u verbinding met een opslagaccount met Visual Studio hebt verbonden services
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
ms.openlocfilehash: e154c81ef3765a3c006b3c27a979be881f14d0ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="79ee5-103">Aan de slag met Azure Blob Storage en Visual Studio verbonden services (cloud services-projecten)</span><span class="sxs-lookup"><span data-stu-id="79ee5-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="79ee5-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="79ee5-104">Overview</span></span>
<span data-ttu-id="79ee5-105">Dit artikel wordt beschreven hoe u aan de slag met Azure Blob Storage nadat u hebt gemaakt of een Azure Storage-account waarnaar wordt verwezen door het gebruik van de Visual Studio **verbonden Services toevoegen** dialoogvenster in een Visual Studio-cloud services-project.</span><span class="sxs-lookup"><span data-stu-id="79ee5-105">This article describes how to get started with Azure Blob Storage after you created or referenced an Azure Storage account by using the Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="79ee5-106">Leert u hoe toegang tot blob-containers maken en hoe u veelvoorkomende taken uitvoeren zoals het uploaden, weergeven en blobs downloaden.</span><span class="sxs-lookup"><span data-stu-id="79ee5-106">We'll show you how to access and create blob containers, and how to perform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="79ee5-107">De voorbeelden zijn geschreven in C\# en gebruik de [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="79ee5-107">The samples are written in C\# and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="79ee5-108">Azure Blob Storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens die toegankelijk zijn vanuit overal ter wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="79ee5-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="79ee5-109">Één blob kan elke grootte zijn.</span><span class="sxs-lookup"><span data-stu-id="79ee5-109">A single blob can be any size.</span></span> <span data-ttu-id="79ee5-110">BLOBs kunnen worden items zoals afbeeldingen, audio en video-bestanden, onbewerkte gegevens en bestanden.</span><span class="sxs-lookup"><span data-stu-id="79ee5-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="79ee5-111">Net als bestanden bevinden zich in mappen, live storage-blobs in containers.</span><span class="sxs-lookup"><span data-stu-id="79ee5-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="79ee5-112">Nadat u een opslagruimte hebt gemaakt, kunt u een of meer containers maken in de opslag.</span><span class="sxs-lookup"><span data-stu-id="79ee5-112">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="79ee5-113">Bijvoorbeeld in een opslag 'Plakboek' genoemd, kunt u containers maken in de opslag, naam 'images' voor het opslaan van afbeeldingen en andere aangeroepen 'audio' audio-bestanden op te slaan.</span><span class="sxs-lookup"><span data-stu-id="79ee5-113">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="79ee5-114">Nadat u de containers hebt gemaakt, kunt u afzonderlijke blob bestanden om ze te uploaden.</span><span class="sxs-lookup"><span data-stu-id="79ee5-114">After you create the containers, you can upload individual blob files to them.</span></span>

* <span data-ttu-id="79ee5-115">Zie voor meer informatie over het bewerken van programmatisch blobs [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="79ee5-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="79ee5-116">Raadpleeg voor algemene informatie over Azure Storage [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="79ee5-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="79ee5-117">Raadpleeg voor algemene informatie over Azure Cloud Services [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="79ee5-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="79ee5-118">Zie voor meer informatie over het programmeren van ASP.NET-toepassingen [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="79ee5-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="79ee5-119">Toegang tot blob-containers in code</span><span class="sxs-lookup"><span data-stu-id="79ee5-119">Access blob containers in code</span></span>
<span data-ttu-id="79ee5-120">Om programmatisch toegang biedt tot de blobs in cloudserviceprojecten, moet u de volgende items toevoegen als ze nog niet aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="79ee5-120">To programmatically access blobs in cloud service projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="79ee5-121">De volgende code naamruimtedeclaraties toevoegen aan het begin van een C#-bestand waarin u wilt programmatisch toegang biedt tot Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="79ee5-121">Add the following code namespace declarations to the top of any C# file in which you wish to programmatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="79ee5-122">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="79ee5-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="79ee5-123">De volgende code gebruiken om op te halen de uw verbindingsreeks voor opslag en opslag accountgegevens van de configuratie van Azure service.</span><span class="sxs-lookup"><span data-stu-id="79ee5-123">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="79ee5-124">Ophalen van een **CloudBlobClient** object om te verwijzen naar een bestaande container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="79ee5-124">Get a **CloudBlobClient** object to reference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="79ee5-125">Ophalen van een **CloudBlobContainer** object om te verwijzen naar een specifieke blob-container.</span><span class="sxs-lookup"><span data-stu-id="79ee5-125">Get a **CloudBlobContainer** object to reference a specific blob container.</span></span>
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="79ee5-126">Alle van de code die wordt weergegeven in de vorige procedure voor de code die wordt weergegeven in de volgende secties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="79ee5-126">Use all of the code shown in the previous procedure in front of the code shown in the following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="79ee5-127">Een container in code maken</span><span class="sxs-lookup"><span data-stu-id="79ee5-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="79ee5-128">Sommige API's die het uitvoeren van aanroepen uit Azure Storage in ASP.NET zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="79ee5-128">Some APIs that perform calls out to Azure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="79ee5-129">Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="79ee5-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="79ee5-130">De code in het volgende voorbeeld wordt ervan uitgegaan dat u van programming async-methoden gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="79ee5-130">The code in the following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="79ee5-131">Als u wilt een container maken in uw opslagaccount, hoeft u is Voeg een aanroep naar **CreateIfNotExistsAsync** zoals in de volgende code:</span><span class="sxs-lookup"><span data-stu-id="79ee5-131">To create a container in your storage account, all you need to do is add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="79ee5-132">Als u de bestanden in de container beschikbaar wilt maken voor iedereen, kunt u de container als public met behulp van de volgende code instellen.</span><span class="sxs-lookup"><span data-stu-id="79ee5-132">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="79ee5-133">Iedereen op Internet kan blobs in een openbare container zien, maar u kunt wijzigen of ze alleen verwijderen als u de juiste sleutel hebt.</span><span class="sxs-lookup"><span data-stu-id="79ee5-133">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="79ee5-134">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="79ee5-134">Upload a blob into a container</span></span>
<span data-ttu-id="79ee5-135">Azure Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="79ee5-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="79ee5-136">In de meeste gevallen is een blok-blob het aangewezen type om te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="79ee5-136">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="79ee5-137">Om een bestand naar een blok-blob te uploaden, haalt u een containerverwijzing op en gebruikt u deze om een blok-blobverwijzing op te halen.</span><span class="sxs-lookup"><span data-stu-id="79ee5-137">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="79ee5-138">Zodra u een blobverwijzing hebt, kunt u er elke gewenste gegevensstroom naar uploaden door de methode **UploadFromStream** aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="79ee5-138">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="79ee5-139">Met deze bewerking wordt de blob gemaakt als deze nog niet bestaat, of overschreven als deze wel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="79ee5-139">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="79ee5-140">Het volgende voorbeeld laat zien hoe u een blob uploadt naar een container. Hierbij wordt ervan uitgegaan dat de container al is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="79ee5-140">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Retrieve a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="79ee5-141">De blobs in een container in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="79ee5-141">List the blobs in a container</span></span>
<span data-ttu-id="79ee5-142">Als u een lijst van de blobs in een container wilt weergeven, moet u eerst een containerverwijzing ophalen.</span><span class="sxs-lookup"><span data-stu-id="79ee5-142">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="79ee5-143">Vervolgens kunt u de methode **ListBlobs** van de container gebruiken voor het ophalen van de blobs en/of de mappen hierin.</span><span class="sxs-lookup"><span data-stu-id="79ee5-143">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="79ee5-144">Voor toegang tot de uitgebreide set eigenschappen en methoden voor een geretourneerde **IListBlobItem**, u dit casten naar een **CloudBlockBlob**, **CloudPageBlob**, of  **CloudBlobDirectory** object.</span><span class="sxs-lookup"><span data-stu-id="79ee5-144">To access the rich set of properties and methods for a  returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="79ee5-145">Als het type onbekend is, kunt u typecontrole gebruiken om te bepalen waarnaar het moet worden gecast.</span><span class="sxs-lookup"><span data-stu-id="79ee5-145">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="79ee5-146">De volgende code toont hoe de URI van elk item in de **photos**-container wordt opgehaald en uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="79ee5-146">The following code demonstrates how to retrieve and output the URI of each item in the **photos** container:</span></span>

    // Loop over items within the container and output the length and URI.
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

<span data-ttu-id="79ee5-147">Zoals u in het vorige codevoorbeeld, heeft de blob-service het concept van mappen in containers, evenals.</span><span class="sxs-lookup"><span data-stu-id="79ee5-147">As shown in the previous code sample, the blob service has the concept of directories within containers, as well.</span></span> <span data-ttu-id="79ee5-148">Dit is zodat u kunt uw blobs in een map achtige structuur indelen.</span><span class="sxs-lookup"><span data-stu-id="79ee5-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="79ee5-149">Bekijk bijvoorbeeld de volgende set blok-blobs in een container met de naam **photos**:</span><span class="sxs-lookup"><span data-stu-id="79ee5-149">For example, consider the following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="79ee5-150">Als u aanroept **ListBlobs** op de container (zoals in het vorige voorbeeld), de verzameling geretourneerd bevat **CloudBlobDirectory** en **CloudBlockBlob** objecten die de mappen en blobs die zijn opgenomen op het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="79ee5-150">When you call **ListBlobs** on the container (as in the previous sample), the collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="79ee5-151">Dit is de resulterende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="79ee5-151">Here is the resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="79ee5-152">U kunt desgewenst de parameter **UseFlatBlobListing** van de methode **ListBlobs** instellen op **true**.</span><span class="sxs-lookup"><span data-stu-id="79ee5-152">Optionally, you can set the **UseFlatBlobListing** parameter of of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="79ee5-153">Dit resulteert in elke blob wordt geretourneerd als een **CloudBlockBlob**, ongeacht van de directory.</span><span class="sxs-lookup"><span data-stu-id="79ee5-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="79ee5-154">Hier wordt de aanroep van **ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="79ee5-154">Here is the call to **ListBlobs**:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="79ee5-155">en hier worden de resultaten:</span><span class="sxs-lookup"><span data-stu-id="79ee5-155">and here are the results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="79ee5-156">Zie voor meer informatie [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="79ee5-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="79ee5-157">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="79ee5-157">Download blobs</span></span>
<span data-ttu-id="79ee5-158">Om blobs te downloaden, moet u eerst een blobverwijzing ophalen en vervolgens de methode **DownloadToStream** aanroepen.</span><span class="sxs-lookup"><span data-stu-id="79ee5-158">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="79ee5-159">In het volgende voorbeeld wordt de methode **DownloadToStream** gebruikt om de blobinhoud over te dragen naar een stroomobject, dat u vervolgens persistent kunt maken in een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="79ee5-159">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents to a file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="79ee5-160">U kunt ook de methode **DownloadToStream** gebruiken om de inhoud van een blob te downloaden als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="79ee5-160">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

    // Get a reference to a blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="79ee5-161">Blobs verwijderen</span><span class="sxs-lookup"><span data-stu-id="79ee5-161">Delete blobs</span></span>
<span data-ttu-id="79ee5-162">U verwijdert een blob door eerst een blobverwijzing ophalen en roept u vervolgens de **verwijderen** methode.</span><span class="sxs-lookup"><span data-stu-id="79ee5-162">To delete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="79ee5-163">Blobs asynchroon op pagina's weergeven</span><span class="sxs-lookup"><span data-stu-id="79ee5-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="79ee5-164">Als u een groot aantal blobs in een lijst weergeeft of als u het aantal resultaten dat per lijst wordt geretourneerd, wilt bepalen, kunt u blobs weergeven op pagina's met resultaten.</span><span class="sxs-lookup"><span data-stu-id="79ee5-164">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="79ee5-165">Dit voorbeeld laat zien hoe resultaten op pagina's asynchroon worden geretourneerd, zodat de uitvoering niet wordt geblokkeerd tijdens het wachten op het retourneren van een groot aantal resultaten.</span><span class="sxs-lookup"><span data-stu-id="79ee5-165">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="79ee5-166">In dit voorbeeld gebruiken we een platte bloblijst, maar u kunt ook een hiërarchische lijst uitvoeren door de parameter **useFlatBlobListing** van de methode **ListBlobsSegmentedAsync** in te stellen op **false**.</span><span class="sxs-lookup"><span data-stu-id="79ee5-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the **useFlatBlobListing** parameter of the **ListBlobsSegmentedAsync** method to **false**.</span></span>

<span data-ttu-id="79ee5-167">Omdat de voorbeeldmethode een asynchrone bewerking aanroept, moet deze worden voorafgegaan door het sleutelwoord **async** en een **Task**-object retourneren.</span><span class="sxs-lookup"><span data-stu-id="79ee5-167">Because the sample method calls an asynchronous method, it must be prefaced with the **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="79ee5-168">Het sleutelwoord 'await' dat is opgegeven voor de methode **ListBlobsSegmentedAsync**, onderbreekt de uitvoering van de voorbeeldmethode totdat de taak in de lijst is voltooid.</span><span class="sxs-lookup"><span data-stu-id="79ee5-168">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs to the console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
        // When the continuation token is null, the last page has been returned and execution can exit the loop.
        do
        {
            // This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get the continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a><span data-ttu-id="79ee5-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79ee5-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

