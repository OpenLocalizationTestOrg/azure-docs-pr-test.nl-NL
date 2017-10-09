---
title: aaaPublish Azure Media Services-inhoud met .NET | Microsoft Docs
description: Meer informatie over hoe toocreate een locator die gebruikte toobuild een streaming-URL. Codevoorbeelden zijn geschreven in C# en gebruiken van Hallo Media Services SDK voor .NET.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="742f0-104">Azure Media Services-inhoud met .NET publiceren</span><span class="sxs-lookup"><span data-stu-id="742f0-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="742f0-105">REST</span><span class="sxs-lookup"><span data-stu-id="742f0-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="742f0-106">.NET</span><span class="sxs-lookup"><span data-stu-id="742f0-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="742f0-107">Portal</span><span class="sxs-lookup"><span data-stu-id="742f0-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="742f0-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="742f0-108">Overview</span></span>
<span data-ttu-id="742f0-109">Een adaptive bitrate MP4-set door een OnDemand-locator voor streaming maken en het bouwen van een streaming-URL kan worden gestreamd.</span><span class="sxs-lookup"><span data-stu-id="742f0-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="742f0-110">Hallo [een asset coderen](media-services-encode-asset.md) onderwerp ziet u hoe tooencode in een adaptive bitrate MP4 instellen.</span><span class="sxs-lookup"><span data-stu-id="742f0-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="742f0-111">Als uw inhoud is versleuteld, leveringsbeleid voor Assets configureren (zoals beschreven in [dit](media-services-dotnet-configure-asset-delivery-policy.md) onderwerp) voordat u een locator maakt.</span><span class="sxs-lookup"><span data-stu-id="742f0-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="742f0-112">U kunt ook een OnDemand streaming-locator toobuild URL's die punt tooMP4-bestanden die geleidelijk kunnen worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="742f0-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="742f0-113">Dit onderwerp wordt beschreven hoe een streaming-locator toopublish uw asset en bouwen van een Smooth MPEG DASH en streaming-URL voor HLS OnDemand toocreate.</span><span class="sxs-lookup"><span data-stu-id="742f0-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="742f0-114">U ziet ook hot toobuild progressieve download-URL's.</span><span class="sxs-lookup"><span data-stu-id="742f0-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="742f0-115">Een OnDemand-streaminglocator maken</span><span class="sxs-lookup"><span data-stu-id="742f0-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="742f0-116">toocreate Hallo OnDemand-streaminglocator en URL's ophalen, moet u toodo Hallo dingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="742f0-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="742f0-117">Als het Hallo-inhoud is versleuteld, een toegangsbeleid definiëren.</span><span class="sxs-lookup"><span data-stu-id="742f0-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="742f0-118">Een OnDemand-streaminglocator maken.</span><span class="sxs-lookup"><span data-stu-id="742f0-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="742f0-119">Als u van plan toostream bent, krijgt u Hallo manifestbestand (ISM) in Hallo asset streamen.</span><span class="sxs-lookup"><span data-stu-id="742f0-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="742f0-120">Als u van plan tooprogressively downloaden bent, moet u de namen van de Hallo MP4-bestanden in Hallo-activum ophalen.</span><span class="sxs-lookup"><span data-stu-id="742f0-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="742f0-121">URL's toohello manifestbestand of MP4-bestanden maken.</span><span class="sxs-lookup"><span data-stu-id="742f0-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="742f0-122">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="742f0-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="742f0-123">Gebruik dezelfde Hallo beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen.</span><span class="sxs-lookup"><span data-stu-id="742f0-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="742f0-124">Beleid voor locators die zijn bedoeld bijvoorbeeld tooremain erin gedurende een lange periode (niet-upload policies).</span><span class="sxs-lookup"><span data-stu-id="742f0-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="742f0-125">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="742f0-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="742f0-126">Mediaservices .NET SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="742f0-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="742f0-127">Streaming-URL's samenstellen</span><span class="sxs-lookup"><span data-stu-id="742f0-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="742f0-128">Hallo-uitvoer:</span><span class="sxs-lookup"><span data-stu-id="742f0-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="742f0-129">U kunt ook de inhoud streamen via een SSL-verbinding.</span><span class="sxs-lookup"><span data-stu-id="742f0-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="742f0-130">toodo dit benadert, zorg ervoor dat uw streaming URL's starten met HTTPS.</span><span class="sxs-lookup"><span data-stu-id="742f0-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="742f0-131">Op dit moment ondersteuning AMS geen voor SSL met aangepaste domeinen.</span><span class="sxs-lookup"><span data-stu-id="742f0-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="742f0-132">Progressieve download-URL's samenstellen</span><span class="sxs-lookup"><span data-stu-id="742f0-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="742f0-133">Hallo-uitvoer:</span><span class="sxs-lookup"><span data-stu-id="742f0-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="742f0-134">Media Services .NET SDK Extensions gebruiken</span><span class="sxs-lookup"><span data-stu-id="742f0-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="742f0-135">Hallo volgende code .NET SDK extensions methoden aangeroepen die een locator te maken en het genereren van Hallo Smooth Streaming, HLS en MPEG-DASH-URL's voor adaptief streamen.</span><span class="sxs-lookup"><span data-stu-id="742f0-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="742f0-136">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="742f0-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="742f0-137">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="742f0-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="742f0-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="742f0-138">Next steps</span></span>
* [<span data-ttu-id="742f0-139">Activa downloaden</span><span class="sxs-lookup"><span data-stu-id="742f0-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="742f0-140">Leveringsbeleid voor Assets configureren</span><span class="sxs-lookup"><span data-stu-id="742f0-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

