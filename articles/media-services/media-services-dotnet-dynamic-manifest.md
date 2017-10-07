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
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="041a7-104">Filters maken met Azure Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="041a7-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="041a7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="041a7-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="041a7-106">REST</span><span class="sxs-lookup"><span data-stu-id="041a7-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="041a7-107">Vanaf versie 2.11, kunt u Media Services toodefine filters voor de activa.</span><span class="sxs-lookup"><span data-stu-id="041a7-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="041a7-108">Deze filters zijn server side regels waarmee uw klanten toochoose toodo zaken als: afspelen alleen een gedeelte van een video (in plaats van afgespeeld Hallo hele video), of geef alleen een subset van audio en video vertoningen dat uw klant apparaat kan omgaan met () in plaats van alle Hallo vertoningen die zijn gekoppeld aan Hallo asset).</span><span class="sxs-lookup"><span data-stu-id="041a7-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="041a7-109">Dit filteren van uw assets wordt bereikt door **dynamische Manifest**s die een video van uw klant aanvraag toostream zijn gemaakt op basis van opgegeven filter.</span><span class="sxs-lookup"><span data-stu-id="041a7-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="041a7-110">Zie voor meer gedetailleerde informatie gerelateerde toofilters en dynamische Manifest [dynamische manifesten overzicht](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="041a7-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="041a7-111">Dit onderwerp wordt beschreven hoe toocreate toouse Media Services .NET SDK, bijwerken en verwijderen van de filters.</span><span class="sxs-lookup"><span data-stu-id="041a7-111">This topic shows how toouse Media Services .NET SDK toocreate, update, and delete filters.</span></span> 

<span data-ttu-id="041a7-112">Houd er rekening mee dat als u een filter bijwerkt, het streaming-eindpunt toorefresh Hallo regels too2 minuten kan duren.</span><span class="sxs-lookup"><span data-stu-id="041a7-112">Note if you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="041a7-113">Als Hallo inhoud is uitgevoerd met dit filter (en in het cachegeheugen van proxy's en CDN caches), kan het bijwerken van dit filter leiden tot player fouten.</span><span class="sxs-lookup"><span data-stu-id="041a7-113">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="041a7-114">Is het beste tooclear Hallo cache na het bijwerken van Hallo filter.</span><span class="sxs-lookup"><span data-stu-id="041a7-114">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="041a7-115">Als deze optie niet mogelijk is, kunt u overwegen een ander filter.</span><span class="sxs-lookup"><span data-stu-id="041a7-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="041a7-116">Typen toocreate filters gebruikt</span><span class="sxs-lookup"><span data-stu-id="041a7-116">Types used toocreate filters</span></span>
<span data-ttu-id="041a7-117">Hallo worden volgende typen gebruikt wanneer u filters maken:</span><span class="sxs-lookup"><span data-stu-id="041a7-117">hello following types are used when creating filters:</span></span> 

* <span data-ttu-id="041a7-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="041a7-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="041a7-119">Dit type is gebaseerd op Hallo REST-API te volgen [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="041a7-119">This type is based on hello following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="041a7-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="041a7-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="041a7-121">Dit type is gebaseerd op Hallo REST-API te volgen [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="041a7-121">This type is based on hello following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="041a7-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="041a7-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="041a7-123">Dit type is gebaseerd op Hallo REST-API te volgen [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="041a7-123">This type is based on hello following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="041a7-124">**FilterTrackSelectStatement** en **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="041a7-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="041a7-125">Deze typen zijn gebaseerd op Hallo REST-API's te volgen [FilterTrackSelect en FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="041a7-125">These types are based on hello following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="041a7-126">Globale filters maken, bijwerken, lezen/verwijderen</span><span class="sxs-lookup"><span data-stu-id="041a7-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="041a7-127">Hallo volgende code toont hoe toouse .NET toocreate, bijwerken, lezen en verwijderen van asset-filters.</span><span class="sxs-lookup"><span data-stu-id="041a7-127">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

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


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="041a7-128">Filters asset maken, bijwerken, lezen/verwijderen</span><span class="sxs-lookup"><span data-stu-id="041a7-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="041a7-129">Hallo volgende code toont hoe toouse .NET toocreate, bijwerken, lezen en verwijderen van asset-filters.</span><span class="sxs-lookup"><span data-stu-id="041a7-129">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

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




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="041a7-130">Streaming-URL's die gebruikmaken van filters maken</span><span class="sxs-lookup"><span data-stu-id="041a7-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="041a7-131">Voor informatie over hoe toopublish en leveren uw assets zien [leveren van inhoud tooCustomers overzicht](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="041a7-131">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="041a7-132">Hallo volgende voorbeelden laten zien hoe tooadd tooyour streaming-URL's filtert.</span><span class="sxs-lookup"><span data-stu-id="041a7-132">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="041a7-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="041a7-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="041a7-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="041a7-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="041a7-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="041a7-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="041a7-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="041a7-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="041a7-137">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="041a7-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="041a7-138">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="041a7-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="041a7-139">Zie ook</span><span class="sxs-lookup"><span data-stu-id="041a7-139">See Also</span></span>
[<span data-ttu-id="041a7-140">Overzicht van dynamische manifesten</span><span class="sxs-lookup"><span data-stu-id="041a7-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

