---
title: Azure Media Services aaaMicrosoft scenario's en beschikbaarheid van functies in datacenters | Microsoft Docs
description: In dit onderwerp vindt u informatie over Microsoft Azure Media Services-scenario's en over de beschikbaarheid van functies en services in datacenters.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a><span data-ttu-id="3b006-103">Scenario's en de beschikbaarheid van Media Services-functies in datacenters</span><span class="sxs-lookup"><span data-stu-id="3b006-103">Scenarios and availability of Media Services features across datacenters</span></span>

<span data-ttu-id="3b006-104">Microsoft Azure Media Services (AMS) kunt u toosecurely uploaden, opslaan, coderen en video of audio-inhoud van het pakket voor zowel op aanvraag en live streaming levering toovarious clients (bijvoorbeeld TV, PC en mobiele apparaten).</span><span class="sxs-lookup"><span data-stu-id="3b006-104">Microsoft Azure Media Services (AMS) enables you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="3b006-105">AMS draait in meerdere datacenters Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="3b006-105">AMS operates in multiple data centers around hello world.</span></span> <span data-ttu-id="3b006-106">Deze datacenters worden gegroepeerd in toogeographic regio's, waardoor u flexibiliteit bij het kiezen waar toobuild uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3b006-106">These data centers are grouped in toogeographic regions, giving you flexibility in choosing where toobuild your applications.</span></span> <span data-ttu-id="3b006-107">U kunt bekijken Hallo [lijst met regio's en de locaties](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="3b006-107">You can review hello [list of regions and their locations](https://azure.microsoft.com/regions/).</span></span> 

<span data-ttu-id="3b006-108">Dit onderwerp bevat algemene scenario's voor het leveren van uw inhoud: [live](#live_scenarios) of [on-demand](#vod_scenarios).</span><span class="sxs-lookup"><span data-stu-id="3b006-108">This topic shows common scenarios for delivering your content [live](#live_scenarios) or [on-demand](#vod_scenarios).</span></span> <span data-ttu-id="3b006-109">Hallo onderwerp bevat ook informatie over de beschikbaarheid van mediafuncties en services via datacenters.</span><span class="sxs-lookup"><span data-stu-id="3b006-109">hello topic also provides details about availability of media features and services across data centers.</span></span>

## <a name="overview"></a><span data-ttu-id="3b006-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3b006-110">Overview</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3b006-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3b006-111">Prerequisites</span></span>

<span data-ttu-id="3b006-112">toostart met Azure Media Services, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="3b006-112">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="3b006-113">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3b006-113">An Azure account.</span></span> <span data-ttu-id="3b006-114">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="3b006-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3b006-115">Zie [Gratis proefversie van Azure](https://azure.microsoft.com) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-115">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="3b006-116">Een Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="3b006-116">An Azure Media Services account.</span></span> <span data-ttu-id="3b006-117">Zie [Een account maken](media-services-portal-create-account.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-117">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="3b006-118">Hallo streaming-eindpunt van waaruit u wilt dat toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="3b006-118">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

    <span data-ttu-id="3b006-119">Wanneer uw AMS-account is gemaakt, een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="3b006-119">When your AMS account is created, a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="3b006-120">toostart streaming van uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling, Hallo streaming-eindpunt heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="3b006-120">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint has toobe in hello **Running** state.</span></span>

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a><span data-ttu-id="3b006-121">Veelgebruikte objecten bij het ontwikkelen van tegen Hallo AMS OData-model</span><span class="sxs-lookup"><span data-stu-id="3b006-121">Commonly used objects when developing against hello AMS OData model</span></span>

<span data-ttu-id="3b006-122">Hallo volgende afbeelding ziet u enkele van de meest gebruikte Hallo-objecten bij het ontwikkelen van toepassingen met Media Services OData-model Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b006-122">hello following image shows some of hello most commonly used objects when developing against hello Media Services OData model.</span></span>

<span data-ttu-id="3b006-123">Klik op Hallo installatiekopie tooview het maximale grootte.</span><span class="sxs-lookup"><span data-stu-id="3b006-123">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="3b006-124">U kunt hele model Hallo weergeven [hier](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="3b006-124">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a><span data-ttu-id="3b006-125">Inhoud in de opslag beveiligen en Hallo streamingmedia leveren wissen (niet-versleutelde)</span><span class="sxs-lookup"><span data-stu-id="3b006-125">Protect content in storage and deliver streaming media in hello clear (non-encrypted)</span></span>

![VoD-werkstroom](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. <span data-ttu-id="3b006-127">Upload een mediabestand van hoge kwaliteit naar een asset.</span><span class="sxs-lookup"><span data-stu-id="3b006-127">Upload a high-quality media file into an asset.</span></span>

    <span data-ttu-id="3b006-128">Het verdient aanbeveling tooapply opslag versleuteling optie tooyour asset in volgorde tooprotect uw inhoud tijdens het uploaden en terwijl in rust in de opslag.</span><span class="sxs-lookup"><span data-stu-id="3b006-128">It is recommended tooapply storage encryption option tooyour asset in order tooprotect your content during upload and while at rest in storage.</span></span>
2. <span data-ttu-id="3b006-129">Codeer tooa set adaptive bitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="3b006-129">Encode tooa set of adaptive bitrate MP4 files.</span></span>

    <span data-ttu-id="3b006-130">Het is raadzaam om uw inhoud in rust voor uitvoer asset in volgorde tooprotect tooapply opslag versleuteling optie toohello.</span><span class="sxs-lookup"><span data-stu-id="3b006-130">It is recommended tooapply storage encryption option toohello output asset in order tooprotect your content at rest.</span></span>
3. <span data-ttu-id="3b006-131">Configureer het beleid voor de levering van assets (gebruikt voor dynamische pakketten).</span><span class="sxs-lookup"><span data-stu-id="3b006-131">Configure asset delivery policy (used by dynamic packaging).</span></span>

    <span data-ttu-id="3b006-132">Als de opslag van uw asset is versleuteld, **moet** u een beleid voor assetlevering configureren.</span><span class="sxs-lookup"><span data-stu-id="3b006-132">If your asset is storage encrypted, you **must** configure asset delivery policy.</span></span>
4. <span data-ttu-id="3b006-133">Hallo asset publiceren door een OnDemand-locator te maken.</span><span class="sxs-lookup"><span data-stu-id="3b006-133">Publish hello asset by creating an OnDemand locator.</span></span>
5. <span data-ttu-id="3b006-134">Stream de gepubliceerde inhoud.</span><span class="sxs-lookup"><span data-stu-id="3b006-134">Stream published content.</span></span>

<span data-ttu-id="3b006-135">Zie voor informatie over de beschikbaarheid van datacenters Hallo [beschikbaarheid](#availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="3b006-135">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a><span data-ttu-id="3b006-136">De inhoud in de opslag beveiligen, dynamisch versleutelde streamingmedia leveren</span><span class="sxs-lookup"><span data-stu-id="3b006-136">Protect content in storage, deliver dynamically encrypted streaming media</span></span>

![Beveiligen met PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. <span data-ttu-id="3b006-138">Upload een mediabestand van hoge kwaliteit naar een asset.</span><span class="sxs-lookup"><span data-stu-id="3b006-138">Upload a high-quality media file into an asset.</span></span> <span data-ttu-id="3b006-139">Storage encryption optie toohello asset toepassen.</span><span class="sxs-lookup"><span data-stu-id="3b006-139">Apply storage encryption option toohello asset.</span></span>
2. <span data-ttu-id="3b006-140">Codeer tooa set adaptive bitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="3b006-140">Encode tooa set of adaptive bitrate MP4 files.</span></span> <span data-ttu-id="3b006-141">Storage encryption optie toohello uitvoerasset toepassen.</span><span class="sxs-lookup"><span data-stu-id="3b006-141">Apply storage encryption option toohello output asset.</span></span>
3. <span data-ttu-id="3b006-142">Inhoud coderingssleutel voor Hallo asset die u toobe dynamisch worden versleuteld tijdens het afspelen wilt maken.</span><span class="sxs-lookup"><span data-stu-id="3b006-142">Create encryption content key for hello asset you want toobe dynamically encrypted during playback.</span></span>
4. <span data-ttu-id="3b006-143">Configureer het autorisatiebeleid voor de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="3b006-143">Configure content key authorization policy.</span></span>
5. <span data-ttu-id="3b006-144">Configureer het beleid voor de levering van assets (gebruikt door dynamische pakketten en dynamische versleuteling).</span><span class="sxs-lookup"><span data-stu-id="3b006-144">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
6. <span data-ttu-id="3b006-145">Hallo asset publiceren door een OnDemand-locator te maken.</span><span class="sxs-lookup"><span data-stu-id="3b006-145">Publish hello asset by creating an OnDemand locator.</span></span>
7. <span data-ttu-id="3b006-146">Stream de gepubliceerde inhoud.</span><span class="sxs-lookup"><span data-stu-id="3b006-146">Stream published content.</span></span>

<span data-ttu-id="3b006-147">Zie voor informatie over de beschikbaarheid van datacenters Hallo [beschikbaarheid](#availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="3b006-147">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a><span data-ttu-id="3b006-148">Media Analytics tooderive bruikbare inzicht in uw video's gebruiken</span><span class="sxs-lookup"><span data-stu-id="3b006-148">Use Media Analytics tooderive actionable insights from your videos</span></span>

<span data-ttu-id="3b006-149">Media Analytics is een verzameling spraakonderdelen en visuele onderdelen waarmee het eenvoudiger voor organisaties en bedrijven tooderive bruikbare inzichten aan hun video's.</span><span class="sxs-lookup"><span data-stu-id="3b006-149">Media Analytics is a collection of speech and vision components that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="3b006-150">Zie [Overzicht van Azure Media Services Analytics](media-services-analytics-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-150">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

1. <span data-ttu-id="3b006-151">Upload een mediabestand van hoge kwaliteit naar een asset.</span><span class="sxs-lookup"><span data-stu-id="3b006-151">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="3b006-152">Uw video's verwerken met een Hallo Media Analytics-services die worden beschreven in Hallo [Media Analytics overzicht](media-services-analytics-overview.md) sectie.</span><span class="sxs-lookup"><span data-stu-id="3b006-152">Process your videos with one of hello Media Analytics services described in hello [Media Analytics overview](media-services-analytics-overview.md) section.</span></span>
3. <span data-ttu-id="3b006-153">Media Analytics-mediaprocessoren produceren MP4- of JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="3b006-153">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="3b006-154">Als een Mediaprocessor een MP4-bestand, kunt u Hallo bestand progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="3b006-154">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="3b006-155">Als een Mediaprocessor een JSON-bestand, kunt u Hallo-bestand downloaden van hello Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="3b006-155">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span>

<span data-ttu-id="3b006-156">Zie voor informatie over de beschikbaarheid van datacenters Hallo [beschikbaarheid](#availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="3b006-156">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="deliver-progressive-download"></a><span data-ttu-id="3b006-157">Een progressieve download leveren</span><span class="sxs-lookup"><span data-stu-id="3b006-157">Deliver progressive download</span></span>

1. <span data-ttu-id="3b006-158">Upload een mediabestand van hoge kwaliteit naar een asset.</span><span class="sxs-lookup"><span data-stu-id="3b006-158">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="3b006-159">Codeer tooa één MP4-bestand.</span><span class="sxs-lookup"><span data-stu-id="3b006-159">Encode tooa single MP4 file.</span></span>
3. <span data-ttu-id="3b006-160">Hallo asset publiceren door een OnDemand- of SAS-locator te maken.</span><span class="sxs-lookup"><span data-stu-id="3b006-160">Publish hello asset by creating an OnDemand or SAS locator.</span></span>

    <span data-ttu-id="3b006-161">Als u SAS-locator gebruikt, worden Hallo inhoud wordt gedownload van hello Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="3b006-161">If using SAS locator, hello content is downloaded from hello Azure blob storage.</span></span> <span data-ttu-id="3b006-162">In dit geval hoeft niet toohave streaming-eindpunten in gestarte staat verkeert.</span><span class="sxs-lookup"><span data-stu-id="3b006-162">In this case, you do not need toohave streaming endpoints in started state.</span></span>
4. <span data-ttu-id="3b006-163">Download de inhoud op progressieve wijze.</span><span class="sxs-lookup"><span data-stu-id="3b006-163">Progressively download content.</span></span>

## <span data-ttu-id="3b006-164"><a id="live_scenarios"></a>Evenementen live streamen</span><span class="sxs-lookup"><span data-stu-id="3b006-164"><a id="live_scenarios"></a>Delivering live-streaming events</span></span> 

1. <span data-ttu-id="3b006-165">Live-inhoud met verschillende protocollen voor live streamen opnemen (bijvoorbeeld RTMP of Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="3b006-165">Ingest live content using various live streaming protocols (for example RTMP or Smooth Streaming).</span></span>
2. <span data-ttu-id="3b006-166">(Optioneel) Uw stream coderen in een stream met een adaptieve bitsnelheid.</span><span class="sxs-lookup"><span data-stu-id="3b006-166">(optionally) Encode your stream into adaptive bitrate stream.</span></span>
3. <span data-ttu-id="3b006-167">Een voorbeeld van uw livestream bekijken.</span><span class="sxs-lookup"><span data-stu-id="3b006-167">Preview your live stream.</span></span>
4. <span data-ttu-id="3b006-168">Hallo leveren via algemene streaming protocollen (bijvoorbeeld MPEG DASH, Smooth, HLS) rechtstreeks tooyour klanten of tooa inhoud Delivery Network (CDN) voor verdere distributie.</span><span class="sxs-lookup"><span data-stu-id="3b006-168">Deliver hello content through common streaming protocols (for example, MPEG DASH, Smooth, HLS) directly tooyour customers, or tooa Content Delivery Network (CDN) for further distribution.</span></span>

    <span data-ttu-id="3b006-169">-of-</span><span class="sxs-lookup"><span data-stu-id="3b006-169">-or-</span></span>

    <span data-ttu-id="3b006-170">Record- en store Hallo ingenomen inhoud in de volgorde toobe gestreamd later (Video-on-Demand).</span><span class="sxs-lookup"><span data-stu-id="3b006-170">Record and store hello ingested content in order toobe streamed later (Video-on-Demand).</span></span>

<span data-ttu-id="3b006-171">Bij het uitvoeren van live streamen, kunt u een van de volgende Hallo van routes:</span><span class="sxs-lookup"><span data-stu-id="3b006-171">When doing live streaming, you can choose one of hello following routes:</span></span>

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a><span data-ttu-id="3b006-172">Werken met kanalen die een multi-bitrate livestream van on-premises encoders ontvangen (pass-through)</span><span class="sxs-lookup"><span data-stu-id="3b006-172">Working with channels that receive multi-bitrate live stream from on-premises encoders (pass-through)</span></span>

<span data-ttu-id="3b006-173">Hallo volgende diagram toont Hallo belangrijke onderdelen van Hallo AMS-platform die betrokken zijn bij Hallo **pass-through** werkstroom.</span><span class="sxs-lookup"><span data-stu-id="3b006-173">hello following diagram shows hello major parts of hello AMS platform that are involved in hello **pass-through** workflow.</span></span>

![Live-werkstroom](./media/scenarios-and-availability/media-services-live-streaming-current.png)

<span data-ttu-id="3b006-175">Zie [Werken met kanalen die een multi-bitrate livestream van on-premises coderingsprogramma’s ontvangen](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-175">For more information, see [Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders](media-services-live-streaming-with-onprem-encoders.md).</span></span>

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a><span data-ttu-id="3b006-176">Werken met kanalen die zijn ingeschakeld tooperform live codering met Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="3b006-176">Working with channels that are enabled tooperform live encoding with Azure Media Services</span></span>

<span data-ttu-id="3b006-177">Hallo volgende diagram toont Hallo belangrijke onderdelen van Hallo AMS-platform die betrokken zijn bij Live Streaming-werkstroom waarbij een kanaal is ingeschakeld tooperform live codering met Media Services.</span><span class="sxs-lookup"><span data-stu-id="3b006-177">hello following diagram shows hello major parts of hello AMS platform that are involved in Live Streaming workflow where a Channel is enabled tooperform live encoding with Media Services.</span></span>

![Live-werkstroom](./media/scenarios-and-availability/media-services-live-streaming-new.png)

<span data-ttu-id="3b006-179">Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="3b006-179">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="3b006-180">Zie voor informatie over de beschikbaarheid van datacenters Hallo [beschikbaarheid](#availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="3b006-180">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="consuming-content"></a><span data-ttu-id="3b006-181">Inhoud gebruiken</span><span class="sxs-lookup"><span data-stu-id="3b006-181">Consuming content</span></span>

<span data-ttu-id="3b006-182">Azure Media Services biedt u hulpprogramma's voor Hallo moet toocreate rijke, dynamische clientspelertoepassingen voor de meeste platforms, waaronder: iOS-apparaten, Android-apparaten, Windows, Windows Phone, Xbox en Set-top vakken.</span><span class="sxs-lookup"><span data-stu-id="3b006-182">Azure Media Services provides hello tools you need toocreate rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="3b006-183">Volgend onderwerp Hallo biedt koppelingen tooSDKs en Frameworks voor spelers die u kunt gebruiken toodevelop uw eigen clienttoepassingen die streamingmedia van Media Services kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3b006-183">hello following topic provides links tooSDKs and Player Frameworks that you can use toodevelop your own client applications that can consume streaming media from Media Services.</span></span> <span data-ttu-id="3b006-184">Zie [Toepassingen voor het afspelen van video ontwikkelen](media-services-develop-video-players.md) voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="3b006-184">For more information, see [Developing video payer applications](media-services-develop-video-players.md)</span></span>

## <a name="enabling-azure-cdn"></a><span data-ttu-id="3b006-185">Azure CDN inschakelen</span><span class="sxs-lookup"><span data-stu-id="3b006-185">Enabling Azure CDN</span></span>

<span data-ttu-id="3b006-186">Media Services ondersteunt de integratie met Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="3b006-186">Media Services supports integration with Azure CDN.</span></span> <span data-ttu-id="3b006-187">Voor meer informatie over Azure CDN tooenable Zie [hoe tooManage Streaming-eindpunten in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="3b006-187">For information on how tooenable Azure CDN, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>

## <span data-ttu-id="3b006-188"><a id="scaling"></a>Een Media Services-account schalen</span><span class="sxs-lookup"><span data-stu-id="3b006-188"><a id="scaling"></a>Scaling a Media Services account</span></span>

<span data-ttu-id="3b006-189">AMS-klanten kunnen streaming-eindpunten, de mediaverwerking en de opslag in hun AMS-accounts schalen.</span><span class="sxs-lookup"><span data-stu-id="3b006-189">AMS customers can scale streaming endpoints, media processing, and storage in their AMS accounts.</span></span>

* <span data-ttu-id="3b006-190">Media Services-klanten kunnen een **Standard**-streaming-eindpunt of een Premium-**streaming**-eindpunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="3b006-190">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="3b006-191">**Standard**-streaming-eindpunten zijn geschikt voor de meeste streaming-workloads.</span><span class="sxs-lookup"><span data-stu-id="3b006-191">A **Standard** streaming endpoint is suitable for most streaming workloads.</span></span> <span data-ttu-id="3b006-192">Het Hallo dezelfde functies als bevat een **Premium** automatisch streaming-eindpunten en kan worden geschaald uitgaande bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="3b006-192">It includes hello same features as a **Premium** streaming endpoints and scales outbound bandwidth automatically.</span></span> 

    <span data-ttu-id="3b006-193">**Premium**-streaming-eindpunten zijn geschikt voor geavanceerde workloads omdat er gebruik wordt gemaakt van toegewezen, schaalbare bandbreedtecapaciteit.</span><span class="sxs-lookup"><span data-stu-id="3b006-193">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="3b006-194">Klanten met een **Premium**-streaming-eindpunt krijgen standaard één streaming-eenheid (SU).</span><span class="sxs-lookup"><span data-stu-id="3b006-194">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="3b006-195">Hallo streaming-eindpunt kan worden uitgebreid door SUs toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3b006-195">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="3b006-196">Elke SU biedt extra bandbreedte capaciteit toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="3b006-196">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="3b006-197">Voor meer informatie over het schalen van **Premium** Hallo streaming-eindpunten, Zie [streaming-eindpunten schalen](media-services-portal-scale-streaming-endpoints.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3b006-197">For more information about scaling **Premium** streaming endpoints, see hello [Scaling streaming endpoints](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

* <span data-ttu-id="3b006-198">Een Media Services-account is gekoppeld aan een gereserveerde eenheidstype, waarmee wordt bepaald Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3b006-198">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="3b006-199">U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: **S1**, **S2**, of **S3**.</span><span class="sxs-lookup"><span data-stu-id="3b006-199">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="3b006-200">Bijvoorbeeld, Hallo dezelfde coderingstaak sneller wordt uitgevoerd wanneer u Hallo **S2** gereserveerde eenheidstype vergelijken toohello **S1** type.</span><span class="sxs-lookup"><span data-stu-id="3b006-200">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

    <span data-ttu-id="3b006-201">Bovendien toospecifying Hallo eenheidstype gereserveerd, kunt u tooprovision uw account met opgeven **gereserveerde eenheden** (RUs).</span><span class="sxs-lookup"><span data-stu-id="3b006-201">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="3b006-202">het aantal ingerichte RUs Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account.</span><span class="sxs-lookup"><span data-stu-id="3b006-202">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3b006-203">RU's werken voor het parallel verwerken van alle media, waaronder indexeringstaken via Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="3b006-203">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="3b006-204">Indexeringstaken worden echter niet sneller verwerkt met snellere gereserveerde eenheden, terwijl dit bij coderen wel het geval is.</span><span class="sxs-lookup"><span data-stu-id="3b006-204">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

    <span data-ttu-id="3b006-205">Zie [Mediaverwerking schalen](media-services-portal-scale-media-processing.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-205">For more information see, [Scale media processing](media-services-portal-scale-media-processing.md).</span></span>
* <span data-ttu-id="3b006-206">U kunt ook uw Media Services-account schalen door storage accounts tooit toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3b006-206">You can also scale your Media Services account by adding storage accounts tooit.</span></span> <span data-ttu-id="3b006-207">Elk opslagaccount is beperkt too500 TB.</span><span class="sxs-lookup"><span data-stu-id="3b006-207">Each storage account is limited too500 TB.</span></span> <span data-ttu-id="3b006-208">tooexpand uw opslag buiten de standaardbeperkingen hello, kunt u tooattach meerdere storage accounts tooa enkel Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="3b006-208">tooexpand your storage beyond hello default limitations, you can choose tooattach multiple storage accounts tooa single Media Services account.</span></span> <span data-ttu-id="3b006-209">Zie [Opslagaccounts beheren](meda-services-managing-multiple-storage-accounts.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-209">For more information, see [Manage storage accounts](meda-services-managing-multiple-storage-accounts.md).</span></span>

##<span data-ttu-id="3b006-210"><a id="availability"></a> De beschikbaarheid van Media Services-functies in datacenters</span><span class="sxs-lookup"><span data-stu-id="3b006-210"><a id="availability"></a> Availability of Media Services features across datacenters</span></span>

<span data-ttu-id="3b006-211">Deze sectie bevat informatie over de beschikbaarheid van Media Services-functies in datacenters.</span><span class="sxs-lookup"><span data-stu-id="3b006-211">This section provides details about availability of Media Services features across datacenters.</span></span>

### <a name="ams-accounts"></a><span data-ttu-id="3b006-212">AMS-accounts</span><span class="sxs-lookup"><span data-stu-id="3b006-212">AMS accounts</span></span>

#### <a name="availability"></a><span data-ttu-id="3b006-213">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-213">Availability</span></span>

<span data-ttu-id="3b006-214">U kunt Media Services accounts maken in Hallo gebieden te volgen: Noord-Europa, West-Europa, VS-West, VS-Oost, Zuidoost-Azië, Oost-Azië, Japan-West, Japan-Oost, Brazilië-Zuid, India-West, Zuid-India en India, midden.</span><span class="sxs-lookup"><span data-stu-id="3b006-214">You can create Media Services accounts in hello following regions: North Europe, West Europe, West US, East US, Southeast Asia, East Asia, Japan West, Japan East, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="streaming-endpoints"></a><span data-ttu-id="3b006-215">Streaming-eindpunten</span><span class="sxs-lookup"><span data-stu-id="3b006-215">Streaming endpoints</span></span> 

<span data-ttu-id="3b006-216">Media Services-klanten kunnen een **Standard**-streaming-eindpunt of een Premium-**streaming**-eindpunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="3b006-216">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="3b006-217">Zie voor meer informatie, Hallo [schalen](#scaling) sectie.</span><span class="sxs-lookup"><span data-stu-id="3b006-217">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="3b006-218">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-218">Availability</span></span>

|<span data-ttu-id="3b006-219">Naam</span><span class="sxs-lookup"><span data-stu-id="3b006-219">Name</span></span>|<span data-ttu-id="3b006-220">Status</span><span class="sxs-lookup"><span data-stu-id="3b006-220">Status</span></span>|<span data-ttu-id="3b006-221">Datacenters</span><span class="sxs-lookup"><span data-stu-id="3b006-221">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="3b006-222">Standard</span><span class="sxs-lookup"><span data-stu-id="3b006-222">Standard</span></span>|<span data-ttu-id="3b006-223">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-223">GA</span></span>|<span data-ttu-id="3b006-224">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-224">All</span></span>|
|<span data-ttu-id="3b006-225">Premium</span><span class="sxs-lookup"><span data-stu-id="3b006-225">Premium</span></span>|<span data-ttu-id="3b006-226">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-226">GA</span></span>|<span data-ttu-id="3b006-227">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-227">All</span></span>|

### <a name="live-encoding"></a><span data-ttu-id="3b006-228">Live Encoding</span><span class="sxs-lookup"><span data-stu-id="3b006-228">Live encoding</span></span>

#### <a name="availability"></a><span data-ttu-id="3b006-229">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-229">Availability</span></span>

<span data-ttu-id="3b006-230">Beschikbaar in alle datacenters, behalve in: Duitsland, Zuid-Brazilië, West-India, Zuid-India en Centraal-India.</span><span class="sxs-lookup"><span data-stu-id="3b006-230">Available in all datacenters except: Germany, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="encoding-media-processors"></a><span data-ttu-id="3b006-231">Mediaprocessors coderen</span><span class="sxs-lookup"><span data-stu-id="3b006-231">Encoding media processors</span></span>

<span data-ttu-id="3b006-232">AMS biedt twee coderingsprogramma's die op basis van behoefte kunnen worden gebruikt: **Media Encoder Standard** en **Media Encoder Premium Workflow**.</span><span class="sxs-lookup"><span data-stu-id="3b006-232">AMS offers two on-demand encoders **Media Encoder Standard** and **Media Encoder Premium Workflow**.</span></span> <span data-ttu-id="3b006-233">Zie [Overzicht en een vergelijking van Azure-mediacoderingsprogramma's die op basis van behoefte kunnen worden gebruikt](media-services-encode-asset.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-233">For more information, see [Overview and comparison of Azure on-demand media encoders](media-services-encode-asset.md).</span></span> 

#### <a name="availability"></a><span data-ttu-id="3b006-234">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-234">Availability</span></span>

|<span data-ttu-id="3b006-235">Naam van mediaprocessor</span><span class="sxs-lookup"><span data-stu-id="3b006-235">Media processor name</span></span>|<span data-ttu-id="3b006-236">Status</span><span class="sxs-lookup"><span data-stu-id="3b006-236">Status</span></span>|<span data-ttu-id="3b006-237">Datacenters</span><span class="sxs-lookup"><span data-stu-id="3b006-237">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="3b006-238">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="3b006-238">Media Encoder Standard</span></span>|<span data-ttu-id="3b006-239">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-239">GA</span></span>|<span data-ttu-id="3b006-240">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-240">All</span></span>|
|<span data-ttu-id="3b006-241">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="3b006-241">Media Encoder Premium Workflow</span></span>|<span data-ttu-id="3b006-242">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-242">GA</span></span>|<span data-ttu-id="3b006-243">Overal behalve China</span><span class="sxs-lookup"><span data-stu-id="3b006-243">All except China</span></span>|

### <a name="analytics-media-processors"></a><span data-ttu-id="3b006-244">Mediaprocessors voor analyse</span><span class="sxs-lookup"><span data-stu-id="3b006-244">Analytics media processors</span></span>

<span data-ttu-id="3b006-245">Media Analytics is een verzameling spraakonderdelen en visuele onderdelen waarmee eenvoudiger voor organisaties en bedrijven tooderive bruikbare inzichten aan hun video's.</span><span class="sxs-lookup"><span data-stu-id="3b006-245">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="3b006-246">Zie [Overzicht van Azure Media Services Analytics](media-services-analytics-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-246">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="3b006-247">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-247">Availability</span></span>

|<span data-ttu-id="3b006-248">Naam van mediaprocessor</span><span class="sxs-lookup"><span data-stu-id="3b006-248">Media processor name</span></span>|<span data-ttu-id="3b006-249">Status</span><span class="sxs-lookup"><span data-stu-id="3b006-249">Status</span></span>|<span data-ttu-id="3b006-250">Datacenters</span><span class="sxs-lookup"><span data-stu-id="3b006-250">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="3b006-251">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="3b006-251">Azure Media Face Detector</span></span>|<span data-ttu-id="3b006-252">Preview</span><span class="sxs-lookup"><span data-stu-id="3b006-252">Preview</span></span>|<span data-ttu-id="3b006-253">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-253">All</span></span>|
|<span data-ttu-id="3b006-254">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="3b006-254">Azure Media Hyperlapse</span></span>|<span data-ttu-id="3b006-255">Preview</span><span class="sxs-lookup"><span data-stu-id="3b006-255">Preview</span></span>|<span data-ttu-id="3b006-256">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-256">All</span></span>|
|<span data-ttu-id="3b006-257">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="3b006-257">Azure Media Indexer</span></span>|<span data-ttu-id="3b006-258">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-258">GA</span></span>|<span data-ttu-id="3b006-259">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-259">All</span></span>|
|<span data-ttu-id="3b006-260">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="3b006-260">Azure Media Motion Detector</span></span>|<span data-ttu-id="3b006-261">Preview</span><span class="sxs-lookup"><span data-stu-id="3b006-261">Preview</span></span>|<span data-ttu-id="3b006-262">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-262">All</span></span>|
|<span data-ttu-id="3b006-263">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="3b006-263">Azure Media OCR</span></span>|<span data-ttu-id="3b006-264">Preview</span><span class="sxs-lookup"><span data-stu-id="3b006-264">Preview</span></span>|<span data-ttu-id="3b006-265">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-265">All</span></span>|
|<span data-ttu-id="3b006-266">Azure Media Redactor</span><span class="sxs-lookup"><span data-stu-id="3b006-266">Azure Media Redactor</span></span>|<span data-ttu-id="3b006-267">Preview</span><span class="sxs-lookup"><span data-stu-id="3b006-267">Preview</span></span>|<span data-ttu-id="3b006-268">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-268">All</span></span>|
|<span data-ttu-id="3b006-269">Azure Media Stabilizer</span><span class="sxs-lookup"><span data-stu-id="3b006-269">Azure Media Stabilizer</span></span>|<span data-ttu-id="3b006-270">Preview</span><span class="sxs-lookup"><span data-stu-id="3b006-270">Preview</span></span>|<span data-ttu-id="3b006-271">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-271">All</span></span>|
|<span data-ttu-id="3b006-272">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="3b006-272">Azure Media Video Thumbnails</span></span>|<span data-ttu-id="3b006-273">Preview</span><span class="sxs-lookup"><span data-stu-id="3b006-273">Preview</span></span>|<span data-ttu-id="3b006-274">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-274">All</span></span>|
|<span data-ttu-id="3b006-275">Azure Media Indexer 2</span><span class="sxs-lookup"><span data-stu-id="3b006-275">Azure Media Indexer 2</span></span>|<span data-ttu-id="3b006-276">Preview</span><span class="sxs-lookup"><span data-stu-id="3b006-276">Preview</span></span>|<span data-ttu-id="3b006-277">Overal behalve China en regio federale overheid</span><span class="sxs-lookup"><span data-stu-id="3b006-277">All except China and Federal Government region</span></span>|

### <a name="protection"></a><span data-ttu-id="3b006-278">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="3b006-278">Protection</span></span>

<span data-ttu-id="3b006-279">Microsoft Azure Media Services kunt u toosecure uw media Hallo tijd vanaf uw computer via de opslag, verwerking en levering.</span><span class="sxs-lookup"><span data-stu-id="3b006-279">Microsoft Azure Media Services enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="3b006-280">Zie [AMS-inhoud beveiligen](media-services-content-protection-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b006-280">For more information, see [Protecting AMS content](media-services-content-protection-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="3b006-281">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-281">Availability</span></span>

|<span data-ttu-id="3b006-282">Versleuteling</span><span class="sxs-lookup"><span data-stu-id="3b006-282">Encryption</span></span>|<span data-ttu-id="3b006-283">Status</span><span class="sxs-lookup"><span data-stu-id="3b006-283">Status</span></span>|<span data-ttu-id="3b006-284">Datacenters</span><span class="sxs-lookup"><span data-stu-id="3b006-284">Datacenters</span></span>|
|---|---|---| 
|<span data-ttu-id="3b006-285">Storage</span><span class="sxs-lookup"><span data-stu-id="3b006-285">Storage</span></span>|<span data-ttu-id="3b006-286">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-286">GA</span></span>|<span data-ttu-id="3b006-287">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-287">All</span></span>|
|<span data-ttu-id="3b006-288">AES-128-sleutels</span><span class="sxs-lookup"><span data-stu-id="3b006-288">AES-128 keys</span></span>|<span data-ttu-id="3b006-289">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-289">GA</span></span>|<span data-ttu-id="3b006-290">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-290">All</span></span>|
|<span data-ttu-id="3b006-291">FairPlay</span><span class="sxs-lookup"><span data-stu-id="3b006-291">Fairplay</span></span>|<span data-ttu-id="3b006-292">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-292">GA</span></span>|<span data-ttu-id="3b006-293">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-293">All</span></span>|
|<span data-ttu-id="3b006-294">PlayReady</span><span class="sxs-lookup"><span data-stu-id="3b006-294">PlayReady</span></span>|<span data-ttu-id="3b006-295">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-295">GA</span></span>|<span data-ttu-id="3b006-296">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-296">All</span></span>|
|<span data-ttu-id="3b006-297">Widevine</span><span class="sxs-lookup"><span data-stu-id="3b006-297">Widevine</span></span>|<span data-ttu-id="3b006-298">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-298">GA</span></span>|<span data-ttu-id="3b006-299">Overal behalve in Duitsland, bij overheden en in China.</span><span class="sxs-lookup"><span data-stu-id="3b006-299">All except Germany, Federal Government and China.</span></span>

### <a name="reserved-units-rus"></a><span data-ttu-id="3b006-300">Gereserveerde eenheden (RU's)</span><span class="sxs-lookup"><span data-stu-id="3b006-300">Reserved units (RUs)</span></span>

<span data-ttu-id="3b006-301">het aantal ingerichte gereserveerde eenheden Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account.</span><span class="sxs-lookup"><span data-stu-id="3b006-301">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> 

<span data-ttu-id="3b006-302">Zie voor meer informatie, Hallo [schalen](#scaling) sectie.</span><span class="sxs-lookup"><span data-stu-id="3b006-302">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="3b006-303">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-303">Availability</span></span>

<span data-ttu-id="3b006-304">Beschikbaar in alle datacenters.</span><span class="sxs-lookup"><span data-stu-id="3b006-304">Available in all datacenters.</span></span>

### <a name="reserved-unit-ru-type"></a><span data-ttu-id="3b006-305">Gereserveerde-eenheidstype (RU)</span><span class="sxs-lookup"><span data-stu-id="3b006-305">Reserved unit (RU) type</span></span>

<span data-ttu-id="3b006-306">Een Media Services-account is gekoppeld aan een gereserveerde eenheidstype, waarmee wordt bepaald Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3b006-306">A Media Services account is associated with a Reserved unit type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="3b006-307">U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: S1, S2 of S3.</span><span class="sxs-lookup"><span data-stu-id="3b006-307">You can pick between hello following reserved unit types: S1, S2, or S3.</span></span>

<span data-ttu-id="3b006-308">Zie voor meer informatie, Hallo [schalen](#scaling) sectie.</span><span class="sxs-lookup"><span data-stu-id="3b006-308">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="3b006-309">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-309">Availability</span></span>

|<span data-ttu-id="3b006-310">RU-typenaam</span><span class="sxs-lookup"><span data-stu-id="3b006-310">RU type name</span></span>|<span data-ttu-id="3b006-311">Status</span><span class="sxs-lookup"><span data-stu-id="3b006-311">Status</span></span>|<span data-ttu-id="3b006-312">Datacenters</span><span class="sxs-lookup"><span data-stu-id="3b006-312">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="3b006-313">S1</span><span class="sxs-lookup"><span data-stu-id="3b006-313">S1</span></span>|<span data-ttu-id="3b006-314">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-314">GA</span></span>|<span data-ttu-id="3b006-315">Alle</span><span class="sxs-lookup"><span data-stu-id="3b006-315">All</span></span>|
|<span data-ttu-id="3b006-316">S2</span><span class="sxs-lookup"><span data-stu-id="3b006-316">S2</span></span>|<span data-ttu-id="3b006-317">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-317">GA</span></span>|<span data-ttu-id="3b006-318">Overal behalve in Zuid-Brazilië en West-India</span><span class="sxs-lookup"><span data-stu-id="3b006-318">All except Brazil South, and India West</span></span>|
|<span data-ttu-id="3b006-319">S3</span><span class="sxs-lookup"><span data-stu-id="3b006-319">S3</span></span>|<span data-ttu-id="3b006-320">Algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="3b006-320">GA</span></span>|<span data-ttu-id="3b006-321">Overal behalve in West-India</span><span class="sxs-lookup"><span data-stu-id="3b006-321">All except India West</span></span>|

## <a name="next-steps"></a><span data-ttu-id="3b006-322">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b006-322">Next steps</span></span>

<span data-ttu-id="3b006-323">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="3b006-323">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3b006-324">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="3b006-324">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

