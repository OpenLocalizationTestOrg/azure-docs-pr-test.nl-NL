---
title: aaa"inhoud Hello Azure-portal publiceren | Microsoft Docs'
description: Deze zelfstudie wordt u begeleid Hallo stappen voor het publiceren van uw inhoud Hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="9b695-103">Inhoud Hello Azure-portal publiceren</span><span class="sxs-lookup"><span data-stu-id="9b695-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b695-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9b695-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="9b695-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9b695-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="9b695-106">REST</span><span class="sxs-lookup"><span data-stu-id="9b695-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9b695-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9b695-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="9b695-108">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9b695-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="9b695-109">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9b695-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="9b695-110">tooprovide uw gebruikers met een URL die kan worden gebruikt toostream of uw inhoud downloaden, u eerst hoeft te 'publiceren' uw asset door een locator te maken.</span><span class="sxs-lookup"><span data-stu-id="9b695-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="9b695-111">Locators bieden toegang toofiles opgenomen in Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="9b695-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="9b695-112">Media Services ondersteunt twee typen locators:</span><span class="sxs-lookup"><span data-stu-id="9b695-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="9b695-113">Streaming-locators (OnDemandOrigin), die wordt gebruikt voor adaptief streamen (bijvoorbeeld toostream MPEG DASH, HLS of Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="9b695-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="9b695-114">een streaming-locator toocreate uw asset een ISM-bestand moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="9b695-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="9b695-115">Progressieve locators (SAS) die worden gebruikt voor het leveren van video via progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="9b695-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="9b695-116">Een streaming-URL Hallo na indeling heeft en u tooplay Smooth Streaming-assets kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9b695-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="9b695-117">toobuild een streaming-URL voor HLS toevoegen (format = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9b695-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="9b695-118">toobuild een streaming-URL voor MPEG DASH toevoegen (format = mpd-time-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="9b695-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="9b695-119">Een SAS-URL heeft Hallo indeling te volgen.</span><span class="sxs-lookup"><span data-stu-id="9b695-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="9b695-120">Zie voor meer informatie [leveren van inhoud overzicht](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b695-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9b695-121">Als u Hallo portal toocreate locators vóór maart 2015 gebruikt, zijn locators met een vervaldatum van twee jaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b695-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="9b695-122">tooupdate een vervaldatum op een locator, gebruik [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) of [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API's.</span><span class="sxs-lookup"><span data-stu-id="9b695-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="9b695-123">Houd er rekening mee dat wanneer u de vervaldatum Hallo van een SAS-locator bijwerkt, Hallo URL gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9b695-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="9b695-124">toouse hello portal toopublish een asset</span><span class="sxs-lookup"><span data-stu-id="9b695-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="9b695-125">toouse hello portal toopublish een asset Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b695-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="9b695-126">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="9b695-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="9b695-127">Selecteer **Instellingen** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="9b695-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="9b695-128">Selecteer Hallo asset die u toopublish wilt.</span><span class="sxs-lookup"><span data-stu-id="9b695-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="9b695-129">Klik op Hallo **publiceren** knop.</span><span class="sxs-lookup"><span data-stu-id="9b695-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="9b695-130">Selecteer Hallo locator type.</span><span class="sxs-lookup"><span data-stu-id="9b695-130">Select hello locator type.</span></span>
6. <span data-ttu-id="9b695-131">Klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9b695-131">Press **Add**.</span></span>
   
    ![Publiceren](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="9b695-133">Hallo-URL wordt toegevoegd toohello lijst met **gepubliceerde URL's**.</span><span class="sxs-lookup"><span data-stu-id="9b695-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="9b695-134">Inhoud afspelen vanuit Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="9b695-134">Play content from hello portal</span></span>
<span data-ttu-id="9b695-135">Hello Azure portal biedt een speler inhoud die u tootest uw video gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="9b695-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="9b695-136">Klik op Hallo gewenste video en klik vervolgens op Hallo **afspelen** knop.</span><span class="sxs-lookup"><span data-stu-id="9b695-136">Click hello desired video and then click hello **Play** button.</span></span>

![Publiceren](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="9b695-138">Hierbij geldt het volgende:</span><span class="sxs-lookup"><span data-stu-id="9b695-138">Some considerations apply:</span></span>

* <span data-ttu-id="9b695-139">Zorg ervoor dat Hallo video is gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="9b695-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="9b695-140">Dit **mediaspeler** speelt af vanaf Hallo standaard streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="9b695-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="9b695-141">Als u wilt dat tooplay van een niet-standaard streaming-eindpunt, klikt u op toocopy Hallo URL en gebruikt een andere speler.</span><span class="sxs-lookup"><span data-stu-id="9b695-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="9b695-142">Bijvoorbeeld [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="9b695-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="9b695-143">Hallo streaming-eindpunt van waaruit u streaming moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b695-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="9b695-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b695-144">Next steps</span></span>
<span data-ttu-id="9b695-145">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="9b695-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9b695-146">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="9b695-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

