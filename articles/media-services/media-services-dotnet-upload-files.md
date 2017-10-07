---
title: aaaUpload bestanden naar een Media Services-account met .NET | Microsoft Docs
description: Meer informatie over hoe tooget media van inhoud in Media Services door het maken en uploaden van activa.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="ca8ae-103">Bestanden uploaden naar een Media Services-account met .NET</span><span class="sxs-lookup"><span data-stu-id="ca8ae-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca8ae-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ca8ae-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="ca8ae-105">REST</span><span class="sxs-lookup"><span data-stu-id="ca8ae-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="ca8ae-106">Portal</span><span class="sxs-lookup"><span data-stu-id="ca8ae-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="ca8ae-107">In Media Services moet u uw digitale bestanden uploaden naar (of opnemen in) een asset.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="ca8ae-108">Hallo **Asset** entiteit kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.)  Zodra het Hallo-bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="ca8ae-109">Hallo-bestanden in Hallo asset heten **Assetbestanden**.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="ca8ae-110">Hallo **AssetFile** exemplaar en de werkelijke mediabestand Hallo zijn twee verschillende objecten.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="ca8ae-111">Hallo AssetFile exemplaar bevat metagegevens over mediabestand hello, terwijl het mediabestand Hallo Hallo echte media-inhoud bevat.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="ca8ae-112">Hallo overwegingen volgende van toepassing:</span><span class="sxs-lookup"><span data-stu-id="ca8ae-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="ca8ae-113">Media Services gebruikt Hallo-waarde van Hallo IAssetFile.Name eigenschap tijdens het bouwen van URL's voor Hallo streaming-inhoud (bijvoorbeeld http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Om deze reden is procent codering niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="ca8ae-114">waarde van Hallo Hallo **naam** eigenschap kan niet een van de volgende Hallo hebben [procent-encoding-gereserveerde tekens](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] '.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="ca8ae-115">Bovendien kunnen alleen er een '.' hello bestandsnaamextensie.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="ca8ae-116">Hallo-lengte van Hallo-naam mag niet groter zijn dan 260 tekens zijn.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="ca8ae-117">Er is een limiet toohello maximale bestandsgrootte voor de verwerking van Media Services wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="ca8ae-118">Zie [dit](media-services-quotas-and-limitations.md) onderwerp voor meer informatie over Hallo beperking voor de bestandsgrootte.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="ca8ae-119">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="ca8ae-120">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="ca8ae-121">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="ca8ae-122">Wanneer u activa maakt, kunt u Hallo versleutelingsopties te volgen.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="ca8ae-123">**Geen**: er wordt geen versleuteling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-123">**None** - No encryption is used.</span></span> <span data-ttu-id="ca8ae-124">Dit is de standaardwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-124">This is hello default value.</span></span> <span data-ttu-id="ca8ae-125">Houd er rekening mee dat wanneer u deze optie uw inhoud wordt niet beveiligd tijdens de overdracht of in rust in de opslag.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="ca8ae-126">Als u van plan toodeliver een MP4 via progressief downloaden bent, moet u deze optie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="ca8ae-127">**CommonEncryption** -Gebruik deze optie als u inhoud uploadt die al is versleuteld en beveiligd met Common Encryption of PlayReady DRM (bijvoorbeeld Smooth Streaming beveiligd met PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="ca8ae-128">**EnvelopeEncrypted** – Gebruik deze optie als u HLS versleuteld met AES uploaden wilt.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="ca8ae-129">Houd er rekening mee dat Hallo bestanden moeten zijn gecodeerd en versleuteld door Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="ca8ae-130">**StorageEncrypted** - versleutelde inhoud lokaal met AES-256-bitsversleuteling versleuteld en geüpload en tooAzure opslag wordt bewaard in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="ca8ae-131">Automatisch worden beveiligd met Storage Encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="ca8ae-132">Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is dat u wilt toosecure uw invoer mediabestanden van hoge kwaliteit met sterke versleuteling-op schijf rest.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="ca8ae-133">Media Services biedt versleuteling van opslag op schijf voor de activa, niet over-the-wire zoals Manager van digitale rechten (DRM).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="ca8ae-134">Als uw asset opslag versleuteld is, moet u het leveringsbeleid voor Assets configureren.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="ca8ae-135">Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="ca8ae-136">Als u opgeeft voor uw asset toobe versleuteld met een **CommonEncrypted** optie, of een **EnvelopeEncypted** optie, moet u tooassociate uw asset met een **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="ca8ae-137">Zie voor meer informatie [hoe toocreate een ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="ca8ae-138">Als u opgeeft voor uw asset toobe versleuteld met een **StorageEncrypted** optie, Hallo Media Services SDK voor .NET maakt een **StorateEncrypted** **ContentKey** voor uw Asset.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="ca8ae-139">Dit onderwerp wordt beschreven hoe toouse Media Services .NET SDK, evenals de Media Services .NET SDK extensions tooupload bestanden naar een Media Services-asset.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="ca8ae-140">Uploaden van één bestand met Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ca8ae-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="ca8ae-141">Hallo voorbeeldcode hieronder gebruikt .NET SDK tooupload één bestand.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="ca8ae-142">Hallo AccessPolicy en Locator worden gemaakt en vernietigd door Hallo uploaden functie.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="ca8ae-143">Uploaden van meerdere bestanden met Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ca8ae-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="ca8ae-144">Hallo van de volgende code wordt getoond hoe toocreate een asset en meerdere bestanden te uploaden.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="ca8ae-145">Hallo-code Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca8ae-145">hello code does hello following:</span></span>

* <span data-ttu-id="ca8ae-146">Maakt een lege asset Hallo CreateEmptyAsset methode die is gedefinieerd in de vorige stap hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="ca8ae-147">Maakt een **AccessPolicy** -exemplaar dat Hallo machtigingen en de duur van toegang toohello asset definieert.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="ca8ae-148">Maakt een **Locator** exemplaar waarmee toegang toohello asset.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="ca8ae-149">Maakt een **BlobTransferClient** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="ca8ae-150">Dit type vertegenwoordigt een client die wordt toegepast op Hallo die Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="ca8ae-151">In dit voorbeeld gebruiken we Hallo client toomonitor Hallo-uploadvoortgang.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="ca8ae-152">Via de bestanden in de opgegeven map Hallo inventariseren en maakt een **AssetFile** exemplaar voor elk bestand.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="ca8ae-153">Uploaden van bestanden in Media Services met behulp van Hallo Hallo **UploadAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="ca8ae-154">Hallo UploadAsync methode tooensure die Hallo aanroepen niet worden geblokkeerd en Hallo bestanden zijn geüpload parallel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="ca8ae-155">Overweeg de volgende Hallo tijdens het uploaden van een groot aantal activa.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="ca8ae-156">Maak een nieuwe **CloudMediaContext** object per thread.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="ca8ae-157">Hallo **CloudMediaContext** klasse is niet thread-veilig.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="ca8ae-158">NumberOfConcurrentTransfers van Hallo standaardwaarde van 2 tooa hogere waarde zoals 5 verhogen.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="ca8ae-159">Als u deze eigenschap is van invloed op alle exemplaren van **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="ca8ae-160">Houd ParallelTransferThreadCount Hallo standaardwaarde van 10.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="ca8ae-161"><a id="ingest_in_bulk"></a>Het opnemen van de activa in Bulk met Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ca8ae-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="ca8ae-162">Grote assetbestanden uploaden, kan een knelpunt zijn tijdens het maken van asset.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="ca8ae-163">Omvat het opnemen van activa in Bulk of 'Opnemen van grote hoeveelheden' asset maken via het uploadproces Hallo ontkoppeling.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="ca8ae-164">toouse een ingesting benadering bulksgewijs maken een manifest (IngestManifest) die worden beschreven Hallo asset en de bijbehorende bestanden.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="ca8ae-165">Gebruik vervolgens Hallo Uploadmethode van uw keuze tooupload Hallo gekoppelde bestanden toohello manifest van blob-container.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="ca8ae-166">Microsoft Azure Media Services bewaakt Hallo blob-container die is gekoppeld aan Hallo manifest.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="ca8ae-167">Als een bestand geüpload toohello blob-container is, is Microsoft Azure Media Services voltooid Hallo asset maken op basis van de configuratie Hallo van Hallo actief in het Hallo-manifest (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="ca8ae-168">een nieuwe IngestManifest toocreate Hallo maken methode die worden weergegeven door Hallo IngestManifests verzameling op Hallo CloudMediaContext aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="ca8ae-169">Deze methode maakt een nieuwe IngestManifest met Hallo manifest die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="ca8ae-170">Hallo-assets die gekoppeld aan Hallo bulksgewijs IngestManifest zijn maken.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="ca8ae-171">Opties voor Hallo gewenst versleuteling op Hallo actief voor het opnemen van grote hoeveelheden configureren.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="ca8ae-172">Een Asset koppelt een IngestManifestAsset aan een bulksgewijs IngestManifest voor het opnemen van grote hoeveelheden.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="ca8ae-173">Ook wordt gekoppeld Hallo AssetFiles waaruit alle activa.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="ca8ae-174">de methode Create Hallo toocreate een IngestManifestAsset gebruiken op Hallo servercontext.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="ca8ae-175">Hallo volgende voorbeeld bevat toe te voegen twee nieuwe IngestManifestAssets die Hallo twee activa eerder gemaakte toohello bulksgewijs koppelt manifest opnemen.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="ca8ae-176">Elke IngestManifestAsset koppelt ook een set van bestanden die worden geüpload voor elk actief tijdens het opnemen van grote hoeveelheden.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="ca8ae-177">U kunt een clienttoepassing hoge snelheid kunnen uploaden Hallo asset bestanden toohello blob storage-container URI dat is opgegeven door Hallo **IIngestManifest.BlobStorageUriForUpload** eigenschap Hallo IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="ca8ae-178">Een opmerkelijke hoge snelheid uploaden service [Aspera On Demand voor Azure-toepassing](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="ca8ae-179">U kunt ook programmacode schrijven tooupload Hallo activa bestanden zoals weergegeven in het volgende codevoorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

<span data-ttu-id="ca8ae-180">Hallo-code voor het uploaden van bestanden van de Hallo asset voor Hallo-voorbeeld gebruikt in dit onderwerp wordt weergegeven in het volgende codevoorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="ca8ae-181">U kunt bepalen Hallo voortgang van Hallo bulksgewijs opnemen voor alle activa die zijn gekoppeld aan een **IngestManifest** door Hallo statistieken eigenschap Hallo **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="ca8ae-182">In de volgorde tooupdate voortgangsinformatie, moet u een nieuwe **CloudMediaContext** telkens wanneer u Hallo statistieken eigenschap opvragen.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="ca8ae-183">Hallo volgende voorbeeld toont een IngestManifest door polling de **Id**.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="ca8ae-184">Uploaden van bestanden met behulp van de .NET SDK Extensions</span><span class="sxs-lookup"><span data-stu-id="ca8ae-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="ca8ae-185">Hallo voorbeeld hieronder ziet u hoe tooupload een bestand met behulp van de .NET SDK Extensions.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="ca8ae-186">In dit geval Hallo **CreateFromFile** methode wordt gebruikt, maar de asynchrone versie Hallo is ook beschikbaar (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="ca8ae-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="ca8ae-187">Hallo **CreateFromFile** methode kunt u opgeven Hallo-bestandsnaam, versleutelingsoptie en een retouraanroep in volgorde tooreport Hallo voortgang van Hallo-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

<span data-ttu-id="ca8ae-188">Hallo volgende voorbeeld UploadFile functie aanroept en versleuteling van opslag geeft als Hallo-optie voor het maken van asset.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="ca8ae-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ca8ae-189">Next steps</span></span>

<span data-ttu-id="ca8ae-190">U kunt nu de geüploade assets coderen.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="ca8ae-191">Zie [Assets coderen](media-services-portal-encode.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="ca8ae-192">U kunt ook Azure Functions tootrigger een codeertaak op basis van een bestand in container Hallo geconfigureerd die binnenkomen.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="ca8ae-193">Zie [dit voorbeeld](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ca8ae-194">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="ca8ae-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ca8ae-195">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="ca8ae-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="ca8ae-196">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="ca8ae-196">Next step</span></span>
<span data-ttu-id="ca8ae-197">Nu dat u hebt een actief geüpload tooMedia Services, gaat u toohello [hoe tooGet een Processor Media] [ How tooGet a Media Processor] onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ca8ae-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

