---
title: Aan de slag met het leveren van inhoud on demand met .NET | Microsoft Docs
description: In deze zelfstudie leert u een eenvoudige toepassing voor de levering van on demand inhoud te implementeren met Azure Media Services door gebruik te maken van .NET.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f0be787ba1ccee067fb1d7e6a6554be32f886089
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="d4e20-103">Aan de slag met het leveren van inhoud on demand met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d4e20-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="d4e20-104">In deze zelfstudie wordt u begeleid bij het implementeren van een basisservice voor levering van VoD-inhoud (Video-on-Demand) met de AMS-toepassing (Azure Media Services) via de Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d4e20-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4e20-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d4e20-105">Prerequisites</span></span>

<span data-ttu-id="d4e20-106">Hieronder wordt aangegeven wat de vereisten zijn om de zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="d4e20-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="d4e20-107">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="d4e20-107">An Azure account.</span></span> <span data-ttu-id="d4e20-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d4e20-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d4e20-109">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d4e20-109">A Media Services account.</span></span> <span data-ttu-id="d4e20-110">Zie [Een Media Services-account maken](media-services-portal-create-account.md) voor meer informatie over het maken van een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d4e20-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d4e20-111">.NET framework 4.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d4e20-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="d4e20-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4e20-112">Visual Studio.</span></span>

<span data-ttu-id="d4e20-113">Deze zelfstudie bevat de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="d4e20-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="d4e20-114">Streaming-eindpunt starten (vanuit Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="d4e20-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="d4e20-115">Een Visual Studio-project maken en configureren.</span><span class="sxs-lookup"><span data-stu-id="d4e20-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="d4e20-116">Verbinding maken met het Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="d4e20-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="d4e20-117">Een videobestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="d4e20-117">Upload a video file.</span></span>
3. <span data-ttu-id="d4e20-118">Het bronbestand coderen in een set Adaptive Bitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="d4e20-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="d4e20-119">De asset publiceren en URL's voor streamen en progressief downloaden ophalen.</span><span class="sxs-lookup"><span data-stu-id="d4e20-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="d4e20-120">Uw inhoud afspelen.</span><span class="sxs-lookup"><span data-stu-id="d4e20-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="d4e20-121">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d4e20-121">Overview</span></span>
<span data-ttu-id="d4e20-122">In deze zelfstudie leert u een eenvoudige toepassing voor de levering van VoD-inhoud (Video-on-Demand) te implementeren met Azure Media Services door gebruik te maken van de Azure Media Services (AMS) SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="d4e20-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="d4e20-123">In deze zelfstudie maakt u kennis met de algemene werkstroom voor Media Services en de meest algemene programmeerobjecten en -taken die zijn vereist voor het ontwikkelen van Media Services.</span><span class="sxs-lookup"><span data-stu-id="d4e20-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="d4e20-124">Wanneer u de zelfstudie hebt voltooid, kunt u een voorbeeldmediabestand streamen of progressief downloaden dat u hebt eerder hebt geüpload, gecodeerd of gedownload.</span><span class="sxs-lookup"><span data-stu-id="d4e20-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="d4e20-125">AMS-model</span><span class="sxs-lookup"><span data-stu-id="d4e20-125">AMS model</span></span>

<span data-ttu-id="d4e20-126">In de volgende afbeelding ziet u een aantal van de meest gebruikte objecten bij het ontwikkelen van VoD-toepassingen in het Media Services OData-model.</span><span class="sxs-lookup"><span data-stu-id="d4e20-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="d4e20-127">Klik op de afbeelding om deze in volledig formaat weer te geven.</span><span class="sxs-lookup"><span data-stu-id="d4e20-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="d4e20-128">U kunt [hier](https://media.windows.net/API/$metadata?api-version=2.15) het hele model bekijken.</span><span class="sxs-lookup"><span data-stu-id="d4e20-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="d4e20-129">Streaming-eindpunten starten met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d4e20-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="d4e20-130">Bij het werken met Azure Media Services wordt video meestal via Adaptive Bitrate Streaming geleverd.</span><span class="sxs-lookup"><span data-stu-id="d4e20-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="d4e20-131">Media Services biedt dynamische pakketten waarmee u uw Adaptive Bitrate MP4-inhoud 'just in time' kunt leveren in de streaming-indelingen die door Media Services worden ondersteund (MPEG DASH, HLS, Smooth Streaming), zonder dat u vooraf verpakte versies van elk van deze streaming-indelingen hoeft op te slaan.</span><span class="sxs-lookup"><span data-stu-id="d4e20-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="d4e20-132">Wanneer uw AMS-account is gemaakt, wordt er een **standaardstreaming-eindpunt** met de status **Gestopt** toegevoegd aan uw account.</span><span class="sxs-lookup"><span data-stu-id="d4e20-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="d4e20-133">Als u inhoud wilt streamen en gebruik wilt maken van dynamische pakketten en dynamische versleuteling, moet het streaming-eindpunt van waar u inhoud wilt streamen, de status **Wordt uitgevoerd** hebben.</span><span class="sxs-lookup"><span data-stu-id="d4e20-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="d4e20-134">U start het streaming-eindpunt als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4e20-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="d4e20-135">Meld u aan bij de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d4e20-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d4e20-136">Klik in het venster Instellingen op Streaming-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="d4e20-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="d4e20-137">Klik op het standaardstreaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d4e20-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="d4e20-138">Het venster DETAILS VAN STANDAARDSTREAMING-EINDPUNT wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d4e20-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="d4e20-139">Klik op het pictogram Start.</span><span class="sxs-lookup"><span data-stu-id="d4e20-139">Click the Start icon.</span></span>
5. <span data-ttu-id="d4e20-140">Klik op de knop Opslaan om uw wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="d4e20-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d4e20-141">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="d4e20-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d4e20-142">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d4e20-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d4e20-143">Maak een nieuwe map (deze kan overal op uw lokaal station zijn opgeslagen) en kopieer een MP4-bestand dat u wilt coderen en streamen of progressief wilt downloaden.</span><span class="sxs-lookup"><span data-stu-id="d4e20-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="d4e20-144">In dit voorbeeld wordt het pad C:\VideoFiles gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d4e20-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="d4e20-145">Verbinding met het Azure Media Services-account maken</span><span class="sxs-lookup"><span data-stu-id="d4e20-145">Connect to the Media Services account</span></span>

<span data-ttu-id="d4e20-146">Als u Media Services gebruikt met .NET, moet u voor de meeste Media Services-programmeertaken de klasse **CloudMediaContext** gebruiken: verbinding maken met het Media Services-account; maken, bijwerken, gebruiken en verwijderen van de volgende objecten: assets, assetbestanden, taken, toegangsbeleid, locators enzovoort.</span><span class="sxs-lookup"><span data-stu-id="d4e20-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="d4e20-147">Overschrijf de standaardklasse Program met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="d4e20-147">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="d4e20-148">De code laat zien u hoe de verbindingswaarden in het bestand App.config kunt lezen en hoe u het object **CloudMediaContext** maakt om verbinding met Media Services te maken.</span><span class="sxs-lookup"><span data-stu-id="d4e20-148">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="d4e20-149">Zie [Verbinding maken met de Media Services-API](media-services-use-aad-auth-to-access-ams-api.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d4e20-149">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="d4e20-150">Zorg ervoor dat de bestandsnaam en het pad waar u het media-bestand hebt opgeslagen, zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d4e20-150">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="d4e20-151">Met de functie **Main** worden methoden aangeroepen die later in deze sectie verder worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d4e20-151">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="d4e20-152">Er worden compilatiefouten geretourneerd totdat u definities hebt toegevoegd voor alle functies.</span><span class="sxs-lookup"><span data-stu-id="d4e20-152">You will be getting compilation errors until you add definitions for all the functions.</span></span>

    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="d4e20-153">Een nieuwe asset maken en een videobestand uploaden</span><span class="sxs-lookup"><span data-stu-id="d4e20-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="d4e20-154">In Media Services moet u uw digitale bestanden uploaden naar (of opnemen in) een asset.</span><span class="sxs-lookup"><span data-stu-id="d4e20-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="d4e20-155">De entiteit **Asset** kan video, audio, afbeeldingen, verzamelingen miniaturen, tekstsporen en ondertitelingsbestanden (en de metagegevens over deze bestanden) bevatten.  Zodra de bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in de cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="d4e20-155">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="d4e20-156">De bestanden in de asset worden **assetbestanden** genoemd.</span><span class="sxs-lookup"><span data-stu-id="d4e20-156">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="d4e20-157">Met de methode **UploadFile**, zoals hieronder gedefinieerd, wordt **CreateFromFile** (gedefinieerd in .NET SDK Extensions) aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d4e20-157">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="d4e20-158">Met **CreateFromFile** wordt een nieuwe asset gemaakt waarnaar het opgegeven bestand wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="d4e20-158">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="d4e20-159">De methode **CreateFromFile** maakt gebruik van **AssetCreationOptions**, waarmee u een van de volgende opties voor het maken van assets kunt opgeven:</span><span class="sxs-lookup"><span data-stu-id="d4e20-159">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="d4e20-160">**Geen**: er wordt geen versleuteling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d4e20-160">**None** - No encryption is used.</span></span> <span data-ttu-id="d4e20-161">Dit is de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="d4e20-161">This is the default value.</span></span> <span data-ttu-id="d4e20-162">Houd er rekening mee dat bij gebruik van deze optie de inhoud tijdens de overdracht of in de opslag niet is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="d4e20-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="d4e20-163">Als u een MP4-bestand wilt leveren via progressief downloaden, gebruikt u deze optie.</span><span class="sxs-lookup"><span data-stu-id="d4e20-163">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="d4e20-164">**StorageEncrypted**: gebruik deze optie om uw niet-versleutelde inhoud lokaal te versleutelen met Advanced Encryption Standard (AES) 256-bitsversleuteling, waarna de inhoud wordt geüpload naar en versleuteld wordt bewaard in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d4e20-164">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="d4e20-165">De versleuteling van assets die zijn beveiligd met Storage Encryption, wordt automatisch ongedaan gemaakt en de assets worden automatisch in een versleuteld bestandssysteem geplaatst voordat ze worden gecodeerd. Eventueel kunnen ze opnieuw worden versleuteld voordat ze opnieuw worden geüpload als een nieuwe uitvoerasset.</span><span class="sxs-lookup"><span data-stu-id="d4e20-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="d4e20-166">Storage Encryption wordt voornamelijk gebruikt om uw invoerbestanden met media van hoge kwaliteit die zijn opgeslagen op de schijf, te beveiligen met een sterke versleuteling.</span><span class="sxs-lookup"><span data-stu-id="d4e20-166">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="d4e20-167">**CommonEncryptionProtected**: gebruik deze optie als u inhoud uploadt die al is versleuteld en beveiligd met Common Encryption of PlayReady DRM (bijvoorbeeld Smooth Streaming beveiligd met PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="d4e20-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="d4e20-168">**EnvelopeEncryptionProtected**: gebruik deze optie als u een HLS-stream uploadt die is versleuteld met AES.</span><span class="sxs-lookup"><span data-stu-id="d4e20-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="d4e20-169">Houd er rekening mee dat de bestanden moeten zijn gecodeerd en versleuteld door Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="d4e20-169">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="d4e20-170">Met de methode **CreateFromFile** kunt u ook een retouraanroep opgeven om de uploadvoortgang van het bestand te rapporteren.</span><span class="sxs-lookup"><span data-stu-id="d4e20-170">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="d4e20-171">In het volgende voorbeeld is voor de assetopties de waarde **Geen** opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d4e20-171">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="d4e20-172">Voeg de volgende methode toe aan de klasse Program.</span><span class="sxs-lookup"><span data-stu-id="d4e20-172">Add the following method to the Program class.</span></span>

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


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="d4e20-173">Het bronbestand coderen in een set Adaptive Bitrate MP4-bestanden</span><span class="sxs-lookup"><span data-stu-id="d4e20-173">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="d4e20-174">Nadat assets zijn opgenomen in Media Services, kan de media worden gecodeerd, transmuxed, van een watermerk worden voorzien enzovoort, voordat deze aan clients wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="d4e20-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="d4e20-175">Deze activiteiten worden gepland en uitgevoerd op meerdere achtergrondrolinstanties om hoge prestaties en een hoge beschikbaarheid te garanderen.</span><span class="sxs-lookup"><span data-stu-id="d4e20-175">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="d4e20-176">Deze activiteiten worden taken genoemd. Elke taak bestaat uit atomische taken die daadwerkelijk werken op het assetbestand.</span><span class="sxs-lookup"><span data-stu-id="d4e20-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="d4e20-177">Zoals eerder al is aangegeven, wordt bij het werken met Azure Media Services meestal Adaptive Bitrate Streaming aan de clients geleverd.</span><span class="sxs-lookup"><span data-stu-id="d4e20-177">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="d4e20-178">Met Media Services kunt u een dynamisch pakket met een van de volgende indelingen van MP4-bestanden met een adaptieve bitsnelheid maken: HTTP Live Streaming (HLS), Smooth Streaming en MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="d4e20-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="d4e20-179">Als u gebruik wilt maken van dynamische pakketten, moet u uw tussentijds (bron)bestand (trans)coderen naar een set MP4-bestanden met een adaptieve bitsnelheid of naar Smooth Streaming-bestanden met een adaptieve bitsnelheid.</span><span class="sxs-lookup"><span data-stu-id="d4e20-179">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="d4e20-180">De volgende code toont u hoe u een codeertaak verzendt.</span><span class="sxs-lookup"><span data-stu-id="d4e20-180">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="d4e20-181">De taak bevat één taak die aangeeft dat het tussentijdse bestand met **Media Encoder Standard** moet worden getranscodeerd in een set MP4-bestanden met een adaptieve bitsnelheid.</span><span class="sxs-lookup"><span data-stu-id="d4e20-181">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="d4e20-182">De code verzendt de taak en wacht totdat de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d4e20-182">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="d4e20-183">Zodra de taak is voltooid, kunt u uw asset streamen of MP4-bestanden die zijn gemaakt naar aanleiding van een transcodering progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="d4e20-183">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="d4e20-184">Voeg de volgende methode toe aan de klasse Program.</span><span class="sxs-lookup"><span data-stu-id="d4e20-184">Add the following method to the Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="d4e20-185">De asset publiceren en URL's ophalen voor streamen en progressief downloaden</span><span class="sxs-lookup"><span data-stu-id="d4e20-185">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="d4e20-186">Als u een asset wilt streamen of downloaden, moet u deze eerste publiceren door een locator te maken.</span><span class="sxs-lookup"><span data-stu-id="d4e20-186">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="d4e20-187">Locators bieden toegang tot bestanden in de asset.</span><span class="sxs-lookup"><span data-stu-id="d4e20-187">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="d4e20-188">Media Services ondersteunt twee typen locators: OnDemandOrigin-locators, voor het streamen van media (bijvoorbeeld MPEG DASH, HLS, of Smooth Streaming), en SAS-locators (Shared Access Signature), voor het downloaden van mediabestanden. (Ga naar [dit](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog voor meer informatie over SAS-locators.)</span><span class="sxs-lookup"><span data-stu-id="d4e20-188">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="d4e20-189">Details over URL-indelingen</span><span class="sxs-lookup"><span data-stu-id="d4e20-189">Some details about URL formats</span></span>

<span data-ttu-id="d4e20-190">Nadat u de locators hebt gemaakt, kunt u de URL's maken die worden gebruikt om uw bestanden te streamen of te downloaden.</span><span class="sxs-lookup"><span data-stu-id="d4e20-190">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="d4e20-191">In het voorbeeld in deze zelfstudie worden URL's geretourneerd die u in de juiste browsers kunt plakken.</span><span class="sxs-lookup"><span data-stu-id="d4e20-191">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="d4e20-192">Deze sectie bevat korte voorbeelden van hoe verschillende indelingen er uitzien.</span><span class="sxs-lookup"><span data-stu-id="d4e20-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="d4e20-193">Een streaming-URL voor MPEG DASH heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="d4e20-193">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="d4e20-194">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="d4e20-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="d4e20-195">Een streaming-URL voor HLS heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="d4e20-195">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="d4e20-196">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="d4e20-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="d4e20-197">Een streaming-URL voor Smooth Streaming heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="d4e20-197">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="d4e20-198">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="d4e20-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="d4e20-199">Een SAS-URL die wordt gebruikt om bestanden te downloaden, heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="d4e20-199">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="d4e20-200">{blobcontainernaam}/{assetname}/{bestandsnaam}/{SAS-handtekening}</span><span class="sxs-lookup"><span data-stu-id="d4e20-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="d4e20-201">Media Services .NET SDK Extensions bieden handige Help-methoden die ingedeelde URL's voor de gepubliceerde asset retourneren.</span><span class="sxs-lookup"><span data-stu-id="d4e20-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="d4e20-202">De volgende code gebruikt .NET SDK Extensions om locators te maken en URL's op te halen die u kunt gebruiken om te streamen of progressief te downloaden.</span><span class="sxs-lookup"><span data-stu-id="d4e20-202">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="d4e20-203">De code toont u ook hoe u bestanden downloadt naar een lokale map.</span><span class="sxs-lookup"><span data-stu-id="d4e20-203">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="d4e20-204">Voeg de volgende methode toe aan de klasse Program.</span><span class="sxs-lookup"><span data-stu-id="d4e20-204">Add the following method to the Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="d4e20-205">Testen door uw inhoud af te spelen</span><span class="sxs-lookup"><span data-stu-id="d4e20-205">Test by playing your content</span></span>

<span data-ttu-id="d4e20-206">Zodra u het programma uitvoert dat in de vorige sectie is gedefinieerd, worden er URL's in het consolevenster weergegeven die vergelijkbaar zijn met de volgende URL's.</span><span class="sxs-lookup"><span data-stu-id="d4e20-206">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="d4e20-207">URL's voor adaptief streamen:</span><span class="sxs-lookup"><span data-stu-id="d4e20-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="d4e20-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="d4e20-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="d4e20-209">HLS</span><span class="sxs-lookup"><span data-stu-id="d4e20-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="d4e20-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="d4e20-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="d4e20-211">URL's voor progressief downloaden (audio en video).</span><span class="sxs-lookup"><span data-stu-id="d4e20-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="d4e20-212">Plak de URL in het URL-tekstvak in de [Azure Media Services-speler](http://amsplayer.azurewebsites.net/azuremediaplayer.html) om de video te streamen.</span><span class="sxs-lookup"><span data-stu-id="d4e20-212">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="d4e20-213">Als u het progressief downloaden wilt testen, plakt u een URL in een browser (bijvoorbeeld Internet Explorer, Chrome of Safari).</span><span class="sxs-lookup"><span data-stu-id="d4e20-213">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="d4e20-214">Zie de volgende onderwerpen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="d4e20-214">For more information, see the following topics:</span></span>

- [<span data-ttu-id="d4e20-215">Uw inhoud afspelen op bestaande spelers</span><span class="sxs-lookup"><span data-stu-id="d4e20-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="d4e20-216">Videospelertoepassingen ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="d4e20-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="d4e20-217">Een adaptieve MPEG-DASH-videostream insluiten in een HTML5-toepassing met DASH.js</span><span class="sxs-lookup"><span data-stu-id="d4e20-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="d4e20-218">Voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="d4e20-218">Download sample</span></span>
<span data-ttu-id="d4e20-219">Het volgende voorbeeld bevat de code die u hebt gemaakt in deze zelfstudie: [voorbeeld](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="d4e20-219">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4e20-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d4e20-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d4e20-221">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="d4e20-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
