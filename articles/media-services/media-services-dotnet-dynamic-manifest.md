---
title: aaaCreating Filters met Azure Media Services .NET SDK
description: Dit onderwerp wordt beschreven hoe toocreate gefilterd zodat de client deze toostream specifieke secties in een stream kunt gebruiken. Media Services dynamische manifesten tooachieve deze selectief streaming wordt gemaakt.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Filters maken met Azure Media Services .NET SDK
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

Vanaf versie 2.11, kunt u Media Services toodefine filters voor de activa. Deze filters zijn server side regels waarmee uw klanten toochoose toodo zaken als: afspelen alleen een gedeelte van een video (in plaats van afgespeeld Hallo hele video), of geef alleen een subset van audio en video vertoningen dat uw klant apparaat kan omgaan met () in plaats van alle Hallo vertoningen die zijn gekoppeld aan Hallo asset). Dit filteren van uw assets wordt bereikt door **dynamische Manifest**s die een video van uw klant aanvraag toostream zijn gemaakt op basis van opgegeven filter.

Zie voor meer gedetailleerde informatie gerelateerde toofilters en dynamische Manifest [dynamische manifesten overzicht](media-services-dynamic-manifest-overview.md).

Dit onderwerp wordt beschreven hoe toocreate toouse Media Services .NET SDK, bijwerken en verwijderen van de filters. 

Houd er rekening mee dat als u een filter bijwerkt, het streaming-eindpunt toorefresh Hallo regels too2 minuten kan duren. Als Hallo inhoud is uitgevoerd met dit filter (en in het cachegeheugen van proxy's en CDN caches), kan het bijwerken van dit filter leiden tot player fouten. Is het beste tooclear Hallo cache na het bijwerken van Hallo filter. Als deze optie niet mogelijk is, kunt u overwegen een ander filter. 

## <a name="types-used-toocreate-filters"></a>Typen toocreate filters gebruikt
Hallo worden volgende typen gebruikt wanneer u filters maken: 

* **IStreamingFilter**.  Dit type is gebaseerd op Hallo REST-API te volgen [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Dit type is gebaseerd op Hallo REST-API te volgen [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Dit type is gebaseerd op Hallo REST-API te volgen [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** en **IFilterTrackPropertyCondition**. Deze typen zijn gebaseerd op Hallo REST-API's te volgen [FilterTrackSelect en FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Globale filters maken, bijwerken, lezen/verwijderen
Hallo volgende code toont hoe toouse .NET toocreate, bijwerken, lezen en verwijderen van asset-filters.

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a>Filters asset maken, bijwerken, lezen/verwijderen
Hallo volgende code toont hoe toouse .NET toocreate, bijwerken, lezen en verwijderen van asset-filters.

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a>Streaming-URL's die gebruikmaken van filters maken
Voor informatie over hoe toopublish en leveren uw assets zien [leveren van inhoud tooCustomers overzicht](media-services-deliver-content-overview.md).

Hallo volgende voorbeelden laten zien hoe tooadd tooyour streaming-URL's filtert.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[Overzicht van dynamische manifesten](media-services-dynamic-manifest-overview.md)

