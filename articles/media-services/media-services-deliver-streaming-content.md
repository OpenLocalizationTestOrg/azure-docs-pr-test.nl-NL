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
# <a name="publish-azure-media-services-content-using-net"></a>Azure Media Services-inhoud met .NET publiceren
> [!div class="op_single_selector"]
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [Portal](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a>Overzicht
Een adaptive bitrate MP4-set door een OnDemand-locator voor streaming maken en het bouwen van een streaming-URL kan worden gestreamd. Hallo [een asset coderen](media-services-encode-asset.md) onderwerp ziet u hoe tooencode in een adaptive bitrate MP4 instellen. 

> [!NOTE]
> Als uw inhoud is versleuteld, leveringsbeleid voor Assets configureren (zoals beschreven in [dit](media-services-dotnet-configure-asset-delivery-policy.md) onderwerp) voordat u een locator maakt. 
> 
> 

U kunt ook een OnDemand streaming-locator toobuild URL's die punt tooMP4-bestanden die geleidelijk kunnen worden gedownload.  

Dit onderwerp wordt beschreven hoe een streaming-locator toopublish uw asset en bouwen van een Smooth MPEG DASH en streaming-URL voor HLS OnDemand toocreate. U ziet ook hot toobuild progressieve download-URL's. 

## <a name="create-an-ondemand-streaming-locator"></a>Een OnDemand-streaminglocator maken
toocreate Hallo OnDemand-streaminglocator en URL's ophalen, moet u toodo Hallo dingen te volgen:

1. Als het Hallo-inhoud is versleuteld, een toegangsbeleid definiëren.
2. Een OnDemand-streaminglocator maken.
3. Als u van plan toostream bent, krijgt u Hallo manifestbestand (ISM) in Hallo asset streamen. 
   
   Als u van plan tooprogressively downloaden bent, moet u de namen van de Hallo MP4-bestanden in Hallo-activum ophalen.  
4. URL's toohello manifestbestand of MP4-bestanden maken. 


>[!NOTE]
>Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Gebruik dezelfde Hallo beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen. Beleid voor locators die zijn bedoeld bijvoorbeeld tooremain erin gedurende een lange periode (niet-upload policies). Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.

### <a name="use-media-services-net-sdk"></a>Mediaservices .NET SDK gebruiken
Streaming-URL's samenstellen 

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

Hallo-uitvoer:

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> U kunt ook de inhoud streamen via een SSL-verbinding. toodo dit benadert, zorg ervoor dat uw streaming URL's starten met HTTPS. Op dit moment ondersteuning AMS geen voor SSL met aangepaste domeinen.
> 
> 

Progressieve download-URL's samenstellen 

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

Hallo-uitvoer:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a>Media Services .NET SDK Extensions gebruiken
Hallo volgende code .NET SDK extensions methoden aangeroepen die een locator te maken en het genereren van Hallo Smooth Streaming, HLS en MPEG-DASH-URL's voor adaptief streamen.

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


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Volgende stappen
* [Activa downloaden](media-services-deliver-asset-download.md)
* [Leveringsbeleid voor Assets configureren](media-services-dotnet-configure-asset-delivery-policy.md)

