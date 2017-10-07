---
title: aaaGet gestart met het leveren van inhoud on demand met .NET | Microsoft Docs
description: Deze zelfstudie leert u Hallo van een on demand leveren van inhoud toepassing implementeren met Azure Media Services met .NET.
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
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="bfa66-103">Aan de slag met het leveren van inhoud on demand met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="bfa66-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="bfa66-104">Deze zelfstudie leert u Hallo van een eenvoudige Video-on-Demand (VoD) leveren van inhoud service implementeren met Azure Media Services (AMS)-toepassing hello Azure Media Services .NET SDK gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfa66-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfa66-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bfa66-105">Prerequisites</span></span>

<span data-ttu-id="bfa66-106">Hallo volgen vereist toocomplete Hallo-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="bfa66-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="bfa66-107">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="bfa66-107">An Azure account.</span></span> <span data-ttu-id="bfa66-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bfa66-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bfa66-109">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="bfa66-109">A Media Services account.</span></span> <span data-ttu-id="bfa66-110">een Media Services-account toocreate Zie [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="bfa66-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="bfa66-111">.NET framework 4.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="bfa66-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="bfa66-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfa66-112">Visual Studio.</span></span>

<span data-ttu-id="bfa66-113">Deze zelfstudie bevat Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="bfa66-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="bfa66-114">Start de streaming-eindpunt (met behulp van hello Azure-portal).</span><span class="sxs-lookup"><span data-stu-id="bfa66-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="bfa66-115">Een Visual Studio-project maken en configureren.</span><span class="sxs-lookup"><span data-stu-id="bfa66-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="bfa66-116">Toohello Media Services-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="bfa66-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="bfa66-117">Een videobestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="bfa66-117">Upload a video file.</span></span>
3. <span data-ttu-id="bfa66-118">Hallo-bronbestand coderen in een set adaptive bitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="bfa66-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="bfa66-119">Hallo asset publiceren en get streamen en progressief downloaden van URL's.</span><span class="sxs-lookup"><span data-stu-id="bfa66-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="bfa66-120">Uw inhoud afspelen.</span><span class="sxs-lookup"><span data-stu-id="bfa66-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="bfa66-121">Overzicht</span><span class="sxs-lookup"><span data-stu-id="bfa66-121">Overview</span></span>
<span data-ttu-id="bfa66-122">In deze zelfstudie wordt u begeleid Hallo stappen voor het implementeren van een eenvoudige (VoD) leveren van inhoud toepassing met Azure Media Services (AMS) SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="bfa66-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="bfa66-123">Hallo-zelfstudie introduceert Hallo basiswerkstroom Media Services en de meest algemene programmeerobjecten Hallo en taken die zijn vereist voor het ontwikkelen van Media Services.</span><span class="sxs-lookup"><span data-stu-id="bfa66-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="bfa66-124">Bij voltooiing Hallo Hallo zelfstudie, wordt u kunnen toostream of progressief downloaden van media met een voorbeeldbestand die geüpload, gecodeerd en gedownload.</span><span class="sxs-lookup"><span data-stu-id="bfa66-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="bfa66-125">AMS-model</span><span class="sxs-lookup"><span data-stu-id="bfa66-125">AMS model</span></span>

<span data-ttu-id="bfa66-126">Hello volgende afbeelding ziet u enkele van de meest gebruikte Hallo objecten wanneer VoD toepassingen ontwikkelt voor Hallo Media Services OData-model.</span><span class="sxs-lookup"><span data-stu-id="bfa66-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="bfa66-127">Klik op Hallo installatiekopie tooview het maximale grootte.</span><span class="sxs-lookup"><span data-stu-id="bfa66-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="bfa66-128">U kunt hele model Hallo weergeven [hier](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="bfa66-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="bfa66-129">Start de streaming-eindpunten met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="bfa66-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="bfa66-130">Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo leveren van video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="bfa66-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="bfa66-131">Media Services biedt dynamische pakketten zodat u toodeliver uw adaptive bitrate MP4-inhoud in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, zonder dat u vooraf verpakte toostore hoeft versies van elk van deze streaming-indelingen.</span><span class="sxs-lookup"><span data-stu-id="bfa66-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="bfa66-132">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="bfa66-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="bfa66-133">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="bfa66-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="bfa66-134">toostart Hallo streaming-eindpunt, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="bfa66-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="bfa66-135">Aanmelden op Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bfa66-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bfa66-136">Klik in het venster Instellingen Hallo, Streaming-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="bfa66-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="bfa66-137">Klik op Hallo standaardstreaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="bfa66-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="bfa66-138">Hallo DEFAULT STREAMING ENDPOINT DETAILS venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bfa66-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="bfa66-139">Klik op Hallo Start pictogram.</span><span class="sxs-lookup"><span data-stu-id="bfa66-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="bfa66-140">Klik op Hallo opslaan knop toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="bfa66-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="bfa66-141">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="bfa66-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="bfa66-142">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bfa66-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="bfa66-143">Maak een nieuwe map (map kan zich ergens op uw lokale schijf) en kopieer een MP4-bestand dat u tooencode en streamen wilt of progressief te downloaden.</span><span class="sxs-lookup"><span data-stu-id="bfa66-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="bfa66-144">In dit voorbeeld wordt Hallo 'C:\VideoFiles' pad gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfa66-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="bfa66-145">Verbinding maken met toohello Media Services-account</span><span class="sxs-lookup"><span data-stu-id="bfa66-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="bfa66-146">Wanneer u Media Services met .NET, moet u Hallo **CloudMediaContext** klasse voor de meeste Media Services-programmeertaken: verbinding maken met tooMedia Services-account; maken, bijwerken, gebruiken en verwijderen van de volgende Hallo objecten: assets, assetbestanden, taken, toegangsbeleid, locators, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="bfa66-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="bfa66-147">Hallo standaardklasse Program met Hallo volgende code worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="bfa66-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="bfa66-148">Hallo code laat zien hoe tooread hello uit Hallo App.config-bestand verbindingswaarden en hoe toocreate hello **CloudMediaContext** Services-object in de volgorde tooconnect tooMedia.</span><span class="sxs-lookup"><span data-stu-id="bfa66-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="bfa66-149">Zie voor meer informatie [toohello Media Services-API verbinden](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="bfa66-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="bfa66-150">Zorg ervoor dat tooupdate Hallo bestand naam en pad toowhere die u hebt uw mediabestand.</span><span class="sxs-lookup"><span data-stu-id="bfa66-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="bfa66-151">Hallo **Main** functie methoden aangeroepen die worden gedefinieerd in deze sectie verder.</span><span class="sxs-lookup"><span data-stu-id="bfa66-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="bfa66-152">U wordt worden ophalen compilatiefouten totdat u de definities voor alle Hallo functies toevoegt.</span><span class="sxs-lookup"><span data-stu-id="bfa66-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

    class Program
    {
        // Read values from hello App.config file.
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

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="bfa66-153">Een nieuwe asset maken en een videobestand uploaden</span><span class="sxs-lookup"><span data-stu-id="bfa66-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="bfa66-154">In Media Services moet u uw digitale bestanden uploaden naar (of opnemen in) een asset.</span><span class="sxs-lookup"><span data-stu-id="bfa66-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="bfa66-155">Hallo **Asset** entiteit kan bevatten, video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden (en Hallo metagegevens over deze bestanden.)  Zodra het Hallo-bestanden zijn geüpload, wordt uw inhoud veilig opgeslagen in Hallo cloud voor verdere verwerking en streaming.</span><span class="sxs-lookup"><span data-stu-id="bfa66-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="bfa66-156">Hallo-bestanden in Hallo asset heten **Assetbestanden**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="bfa66-157">Hallo **UploadFile** methode die is gedefinieerd onder aanroepen **CreateFromFile** (gedefinieerd in .NET SDK Extensions).</span><span class="sxs-lookup"><span data-stu-id="bfa66-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="bfa66-158">**CreateFromFile** maakt een nieuwe asset in welke Hallo opgegeven bestand is geüpload.</span><span class="sxs-lookup"><span data-stu-id="bfa66-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="bfa66-159">Hallo **CreateFromFile** methode vergt **AssetCreationOptions** waarmee u kunt een van de volgende opties voor het maken van asset Hallo opgeven:</span><span class="sxs-lookup"><span data-stu-id="bfa66-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="bfa66-160">**Geen**: er wordt geen versleuteling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfa66-160">**None** - No encryption is used.</span></span> <span data-ttu-id="bfa66-161">Dit is de standaardwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="bfa66-161">This is hello default value.</span></span> <span data-ttu-id="bfa66-162">Houd er rekening mee dat bij gebruik van deze optie de inhoud tijdens de overdracht of in de opslag niet is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="bfa66-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="bfa66-163">Als u van plan toodeliver een MP4 via progressief downloaden bent, moet u deze optie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfa66-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="bfa66-164">**StorageEncrypted** -Gebruik deze optie tooencrypt versleutelde inhoud lokaal met Advanced Encryption Standard (AES) 256-bitsversleuteling, die geüpload en tooAzure opslag wordt bewaard in rust versleuteld.</span><span class="sxs-lookup"><span data-stu-id="bfa66-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="bfa66-165">Automatisch worden beveiligd met Storage Encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset.</span><span class="sxs-lookup"><span data-stu-id="bfa66-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="bfa66-166">Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is wanneer u dat deze toosecure invoer van hoge kwaliteit mediabestanden met een sterke codering in rust op schijf.</span><span class="sxs-lookup"><span data-stu-id="bfa66-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="bfa66-167">**CommonEncryptionProtected**: gebruik deze optie als u inhoud uploadt die al is versleuteld en beveiligd met Common Encryption of PlayReady DRM (bijvoorbeeld Smooth Streaming beveiligd met PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="bfa66-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="bfa66-168">**EnvelopeEncryptionProtected**: gebruik deze optie als u een HLS-stream uploadt die is versleuteld met AES.</span><span class="sxs-lookup"><span data-stu-id="bfa66-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="bfa66-169">Houd er rekening mee dat Hallo bestanden moeten zijn gecodeerd en versleuteld door Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="bfa66-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="bfa66-170">Hallo **CreateFromFile** methode kunt u een retouraanroep opgeven in de volgorde tooreport hello uploadvoortgang van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="bfa66-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="bfa66-171">In Hallo voorbeeld te volgen, geven we **geen** voor Hallo assetopties.</span><span class="sxs-lookup"><span data-stu-id="bfa66-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="bfa66-172">Hallo na methode toohello programma klasse toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bfa66-172">Add hello following method toohello Program class.</span></span>

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="bfa66-173">Hallo-bronbestand coderen in een set adaptive bitrate MP4-bestanden</span><span class="sxs-lookup"><span data-stu-id="bfa66-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="bfa66-174">Nadat assets in Media Services, kan de media worden gecodeerd, transmuxed, een watermerk, enzovoort, voordat deze tooclients wordt afgeleverd.</span><span class="sxs-lookup"><span data-stu-id="bfa66-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="bfa66-175">Deze activiteiten worden gepland en uitgevoerd op meerdere achtergrond rol exemplaren tooensure hoge prestaties en beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="bfa66-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="bfa66-176">Deze activiteiten worden taken genoemd, en elke taak bestaat uit atomische taken die daadwerkelijk werken op Hallo assetbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="bfa66-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="bfa66-177">Zoals is eerder vermeld, als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo adaptive bitrate streaming-tooyour clients leveren.</span><span class="sxs-lookup"><span data-stu-id="bfa66-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="bfa66-178">Media Services kunt u een dynamisch pakket een set adaptive bitrate MP4-bestanden in een van de volgende indelingen Hallo: HTTP Live Streaming (HLS), Smooth Streaming- en MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="bfa66-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="bfa66-179">tootake profiteren van dynamische pakketten hoeft u tooencode of transcodeer uw tussentijds (bron) bestand in een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden.</span><span class="sxs-lookup"><span data-stu-id="bfa66-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="bfa66-180">Hallo volgende code toont hoe een codering toosubmit taak.</span><span class="sxs-lookup"><span data-stu-id="bfa66-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="bfa66-181">Hallo taak bevat één taak die aangeeft dat tootranscode Hallo tussentijds bestand in een set adaptive bitrate MP4s met behulp van **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="bfa66-182">Hallo code verzendt Hallo taak en wacht totdat deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bfa66-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="bfa66-183">Als het Hallo-taak is voltooid, zou u kunnen toostream worden uw asset of MP4-bestanden die zijn gemaakt als gevolg van een transcodering progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="bfa66-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="bfa66-184">Hallo na methode toohello programma klasse toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bfa66-184">Add hello following method toohello Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
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

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="bfa66-185">Hallo asset publiceren en URL's voor streamen en progressief downloaden ophalen</span><span class="sxs-lookup"><span data-stu-id="bfa66-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="bfa66-186">toostream of download een asset, u eerst moet te 'publiceren' door een locator te maken.</span><span class="sxs-lookup"><span data-stu-id="bfa66-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="bfa66-187">Locators bieden toegang toofiles opgenomen in Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="bfa66-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="bfa66-188">Media Services ondersteunt twee typen locators: OnDemandOrigin-locators, gebruikte toostream media (bijvoorbeeld MPEG DASH, HLS of Smooth Streaming) en Access Signature (SAS)-locators, gebruikt media-bestanden (voor meer informatie over SAS-locators Zie toodownload[dit](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="bfa66-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="bfa66-189">Details over URL-indelingen</span><span class="sxs-lookup"><span data-stu-id="bfa66-189">Some details about URL formats</span></span>

<span data-ttu-id="bfa66-190">Nadat u Hallo locators hebt gemaakt, kunt u Hallo-URL's die zouden worden gebruikte toostream of uw bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="bfa66-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="bfa66-191">Hallo voorbeeld in deze zelfstudie wordt de URL's die u in de juiste browsers plakken kunt uitvoer.</span><span class="sxs-lookup"><span data-stu-id="bfa66-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="bfa66-192">Deze sectie bevat korte voorbeelden van hoe verschillende indelingen er uitzien.</span><span class="sxs-lookup"><span data-stu-id="bfa66-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="bfa66-193">Een streaming-URL voor MPEG DASH heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="bfa66-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="bfa66-194">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="bfa66-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="bfa66-195">Een streaming-URL voor HLS heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="bfa66-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="bfa66-196">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="bfa66-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="bfa66-197">Een streaming-URL voor Smooth Streaming heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="bfa66-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="bfa66-198">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="bfa66-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="bfa66-199">Een SAS-URL gebruikt toodownload bestanden heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="bfa66-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="bfa66-200">{blobcontainernaam}/{assetname}/{bestandsnaam}/{SAS-handtekening}</span><span class="sxs-lookup"><span data-stu-id="bfa66-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="bfa66-201">Media Services .NET SDK extensions bieden handige Help-methoden dat return URL's voor Hallo indeling gepubliceerde asset.</span><span class="sxs-lookup"><span data-stu-id="bfa66-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="bfa66-202">Hallo volgende code gebruikt .NET SDK Extensions toocreate locators en tooget streamen en progressief downloaden van URL's.</span><span class="sxs-lookup"><span data-stu-id="bfa66-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="bfa66-203">Hallo code toont u ook hoe toodownload bestanden tooa lokale map.</span><span class="sxs-lookup"><span data-stu-id="bfa66-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="bfa66-204">Hallo na methode toohello programma klasse toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bfa66-204">Add hello following method toohello Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
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

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="bfa66-205">Testen door uw inhoud af te spelen</span><span class="sxs-lookup"><span data-stu-id="bfa66-205">Test by playing your content</span></span>

<span data-ttu-id="bfa66-206">Zodra u gedefinieerd in de vorige sectie Hallo Hallo-programma uitvoert, Hallo vergelijkbare toohello volgende wordt weergegeven in het consolevenster Hallo URL's.</span><span class="sxs-lookup"><span data-stu-id="bfa66-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="bfa66-207">URL's voor adaptief streamen:</span><span class="sxs-lookup"><span data-stu-id="bfa66-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="bfa66-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="bfa66-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="bfa66-209">HLS</span><span class="sxs-lookup"><span data-stu-id="bfa66-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="bfa66-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="bfa66-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="bfa66-211">URL's voor progressief downloaden (audio en video).</span><span class="sxs-lookup"><span data-stu-id="bfa66-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="bfa66-212">toostream uw video plak de URL in Hallo URL textbox in Hallo [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="bfa66-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="bfa66-213">tootest progressief downloaden, plakt u een URL in een browser (bijvoorbeeld Internet Explorer, Chrome of Safari).</span><span class="sxs-lookup"><span data-stu-id="bfa66-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="bfa66-214">Zie de volgende onderwerpen Hallo voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="bfa66-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="bfa66-215">Uw inhoud afspelen op bestaande spelers</span><span class="sxs-lookup"><span data-stu-id="bfa66-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="bfa66-216">Videospelertoepassingen ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="bfa66-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="bfa66-217">Een adaptieve MPEG-DASH-videostream insluiten in een HTML5-toepassing met DASH.js</span><span class="sxs-lookup"><span data-stu-id="bfa66-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="bfa66-218">Voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="bfa66-218">Download sample</span></span>
<span data-ttu-id="bfa66-219">Hallo codevoorbeeld Hallo-code bevat die u hebt gemaakt in deze zelfstudie: [voorbeeld](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="bfa66-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfa66-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfa66-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bfa66-221">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="bfa66-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
