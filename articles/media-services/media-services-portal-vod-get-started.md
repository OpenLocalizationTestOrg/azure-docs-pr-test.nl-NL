---
title: aaaGet gestart met het leveren van VoD hello Azure-portal met | Microsoft Docs
description: Deze zelfstudie leert u Hallo van een basic Video-on-Demand (VoD) leveren van inhoud service implementeren met Azure Media Services (AMS)-toepassing hello Azure-portal gebruiken.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="a415b-103">Aan de slag met het leveren van inhoud on demand met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a415b-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="a415b-104">Deze zelfstudie leert u Hallo van een basic Video-on-Demand (VoD) leveren van inhoud service implementeren met Azure Media Services (AMS)-toepassing hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a415b-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a415b-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a415b-105">Prerequisites</span></span>
<span data-ttu-id="a415b-106">Hallo volgen vereist toocomplete Hallo-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="a415b-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="a415b-107">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a415b-107">An Azure account.</span></span> <span data-ttu-id="a415b-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a415b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="a415b-109">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="a415b-109">A Media Services account.</span></span> <span data-ttu-id="a415b-110">een Media Services-account toocreate Zie [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a415b-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="a415b-111">Deze zelfstudie bevat Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="a415b-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="a415b-112">Streaming-eindpunt starten.</span><span class="sxs-lookup"><span data-stu-id="a415b-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="a415b-113">Een videobestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="a415b-113">Upload a video file.</span></span>
3. <span data-ttu-id="a415b-114">Hallo-bronbestand coderen in een set adaptive bitrate MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="a415b-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="a415b-115">Hallo asset publiceren en get streamen en progressief downloaden van URL's.</span><span class="sxs-lookup"><span data-stu-id="a415b-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="a415b-116">Uw inhoud afspelen.</span><span class="sxs-lookup"><span data-stu-id="a415b-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="a415b-117">Streaming-eindpunten starten</span><span class="sxs-lookup"><span data-stu-id="a415b-117">Start streaming endpoints</span></span> 

<span data-ttu-id="a415b-118">Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo leveren van video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="a415b-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="a415b-119">Media Services biedt dynamische pakketten zodat u toodeliver uw adaptive bitrate MP4-inhoud in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, zonder dat u vooraf verpakte toostore hoeft versies van elk van deze streaming-indelingen.</span><span class="sxs-lookup"><span data-stu-id="a415b-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="a415b-120">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="a415b-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="a415b-121">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="a415b-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="a415b-122">toostart Hallo streaming-eindpunt, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="a415b-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="a415b-123">Aanmelden op Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a415b-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a415b-124">Klik in het venster Instellingen Hallo, Streaming-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="a415b-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="a415b-125">Klik op Hallo standaardstreaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a415b-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="a415b-126">Hallo DEFAULT STREAMING ENDPOINT DETAILS venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a415b-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="a415b-127">Klik op Hallo Start pictogram.</span><span class="sxs-lookup"><span data-stu-id="a415b-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="a415b-128">Klik op Hallo opslaan knop toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="a415b-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="a415b-129">Bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="a415b-129">Upload files</span></span>
<span data-ttu-id="a415b-130">toostream video's met Azure Media Services, moet u tooupload Hallo bron video's, ze coderen in meerdere bitsnelheden en Hallo resultaat publiceren.</span><span class="sxs-lookup"><span data-stu-id="a415b-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="a415b-131">Hallo eerste stap wordt in deze sectie beschreven.</span><span class="sxs-lookup"><span data-stu-id="a415b-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="a415b-132">In Hallo **instelling** venster, klikt u op **activa**.</span><span class="sxs-lookup"><span data-stu-id="a415b-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![Bestanden uploaden](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="a415b-134">Klik op Hallo **uploaden** knop.</span><span class="sxs-lookup"><span data-stu-id="a415b-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="a415b-135">Hallo **videoasset uploaden** venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a415b-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a415b-136">Er geldt geen beperking voor de bestandsgrootte.</span><span class="sxs-lookup"><span data-stu-id="a415b-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="a415b-137">Blader toohello gewenste video op uw computer, selecteert u deze en klik op OK.</span><span class="sxs-lookup"><span data-stu-id="a415b-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="a415b-138">Hallo uploaden wordt gestart en u kunt de voortgang Hallo onder Hallo bestandsnaam bekijken.</span><span class="sxs-lookup"><span data-stu-id="a415b-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="a415b-139">Nadat het Hallo uploaden is voltooid, ziet u Hallo nieuwe asset weergegeven in Hallo **activa** venster.</span><span class="sxs-lookup"><span data-stu-id="a415b-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="a415b-140">Assets coderen</span><span class="sxs-lookup"><span data-stu-id="a415b-140">Encode assets</span></span>

<span data-ttu-id="a415b-141">Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo adaptive bitrate streaming tooyour clients leveren.</span><span class="sxs-lookup"><span data-stu-id="a415b-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="a415b-142">Media Services ondersteunt de volgende adaptive bitrate streaming-technologieën Hallo: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="a415b-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="a415b-143">tooprepare uw video's voor adaptive bitrate streaming, moet u tooencode de bron-video in multi-bitrate-bestanden.</span><span class="sxs-lookup"><span data-stu-id="a415b-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="a415b-144">Moet u Hallo **Media Encoder Standard** encoder tooencode uw video's.</span><span class="sxs-lookup"><span data-stu-id="a415b-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="a415b-145">Media Services biedt ook dynamische pakketten zodat u toodeliver uw multi-bitrate MP4s in de volgende streaming-indelingen Hallo: MPEG DASH, HLS, Smooth Streaming, zonder dat u toorepackage in een van deze streaming-indelingen hoeft.</span><span class="sxs-lookup"><span data-stu-id="a415b-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="a415b-146">Met dynamische pakketten hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services bouwt en Hallo juiste reactie op basis van aanvragen van een client fungeert.</span><span class="sxs-lookup"><span data-stu-id="a415b-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="a415b-147">tootake profiteren van dynamische pakketten hoeft u tooencode uw bronbestand in een set multi-bitrate MP4-bestanden (Hallo coderingsstappen worden uitgelegd later in deze sectie).</span><span class="sxs-lookup"><span data-stu-id="a415b-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="a415b-148">toouse hello portal tooencode</span><span class="sxs-lookup"><span data-stu-id="a415b-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="a415b-149">Deze sectie beschrijft Hallo mogelijke stappen tooencode uw inhoud met Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="a415b-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="a415b-150">In Hallo **instellingen** Selecteer **activa**.</span><span class="sxs-lookup"><span data-stu-id="a415b-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="a415b-151">In Hallo **activa** venster, selecteer Hallo asset dat u tooencode wilt.</span><span class="sxs-lookup"><span data-stu-id="a415b-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="a415b-152">Druk op Hallo **coderen** knop.</span><span class="sxs-lookup"><span data-stu-id="a415b-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="a415b-153">In Hallo **een asset coderen** venster, selecteer Hallo 'Media Encoder Standard' processor en een standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="a415b-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="a415b-154">Zie [automatisch een bitrate ladder genereren](media-services-autogen-bitrate-ladder-with-mes.md) en [Standaardinstellingen voor taken in MES](media-services-mes-presets-overview.md) voor informatie over standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="a415b-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="a415b-155">Als u van plan toocontrol welke codering definitie wordt gebruikt bent, houd hiermee rekening: het is belangrijk tooselect Hallo voorinstelling die het meest geschikt is voor uw invoervideo.</span><span class="sxs-lookup"><span data-stu-id="a415b-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="a415b-156">Bijvoorbeeld, als u weet dat uw invoervideo een resolutie van 1920 x 1080 pixels heeft, kan u Hallo ' standaardinstelling H264 Multiple Bitrate 1080p ' vooraf ingestelde.</span><span class="sxs-lookup"><span data-stu-id="a415b-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="a415b-157">Als u een video met een lage resolutie (640 x 360) hebt, gebruikt u niet de standaardinstelling H264 Multiple Bitrate 1080p.</span><span class="sxs-lookup"><span data-stu-id="a415b-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="a415b-158">Voor eenvoudiger beheer hebt u een optie bewerken Hallo-naam van de uitvoerasset hello en Hallo-naam van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="a415b-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Assets coderen](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="a415b-160">Kies **Maken**.</span><span class="sxs-lookup"><span data-stu-id="a415b-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="a415b-161">De voortgang van het codering van de taak bewaken</span><span class="sxs-lookup"><span data-stu-id="a415b-161">Monitor encoding job progress</span></span>
<span data-ttu-id="a415b-162">toomonitor hello voortgang van Hallo codering van de taak, klikt u op **instellingen** (bovenaan Hallo Hallo pagina) en selecteer vervolgens **taken**.</span><span class="sxs-lookup"><span data-stu-id="a415b-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![Taken](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="a415b-164">Inhoud publiceren</span><span class="sxs-lookup"><span data-stu-id="a415b-164">Publish content</span></span>
<span data-ttu-id="a415b-165">tooprovide uw gebruikers met een URL die kan worden gebruikt toostream of uw inhoud downloaden, u eerst hoeft te 'publiceren' uw asset door een locator te maken.</span><span class="sxs-lookup"><span data-stu-id="a415b-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="a415b-166">Locators bieden toegang toofiles opgenomen in Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="a415b-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="a415b-167">Media Services ondersteunt twee typen locators:</span><span class="sxs-lookup"><span data-stu-id="a415b-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="a415b-168">Streaming-locators (OnDemandOrigin), die wordt gebruikt voor adaptief streamen (bijvoorbeeld toostream MPEG DASH, HLS of Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="a415b-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="a415b-169">een streaming-locator toocreate uw asset een ISM-bestand moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="a415b-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="a415b-170">Progressieve locators (SAS) die worden gebruikt voor het leveren van video via progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="a415b-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="a415b-171">Een streaming-URL Hallo na indeling heeft en u tooplay Smooth Streaming-assets kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a415b-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="a415b-172">toobuild een streaming-URL voor HLS toevoegen (format = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="a415b-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="a415b-173">toobuild een streaming-URL voor MPEG DASH toevoegen (format = mpd-time-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="a415b-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="a415b-174">Een SAS-URL heeft Hallo indeling te volgen.</span><span class="sxs-lookup"><span data-stu-id="a415b-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="a415b-175">Als u Hallo portal toocreate locators vóór maart 2015 gebruikt, zijn locators met een vervaldatum van twee jaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a415b-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="a415b-176">tooupdate een vervaldatum op een locator, gebruik [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) of [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API's.</span><span class="sxs-lookup"><span data-stu-id="a415b-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="a415b-177">Wanneer u de vervaldatum Hallo van een SAS-locator bijwerkt, wordt Hallo URL gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a415b-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="a415b-178">toouse hello portal toopublish een asset</span><span class="sxs-lookup"><span data-stu-id="a415b-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="a415b-179">toouse hello portal toopublish een asset Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="a415b-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="a415b-180">Selecteer **Instellingen** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="a415b-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="a415b-181">Selecteer Hallo asset die u toopublish wilt.</span><span class="sxs-lookup"><span data-stu-id="a415b-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="a415b-182">Klik op Hallo **publiceren** knop.</span><span class="sxs-lookup"><span data-stu-id="a415b-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="a415b-183">Selecteer Hallo locator type.</span><span class="sxs-lookup"><span data-stu-id="a415b-183">Select hello locator type.</span></span>
5. <span data-ttu-id="a415b-184">Klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a415b-184">Press **Add**.</span></span>
   
    ![Publiceren](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="a415b-186">Hallo-URL toegevoegd toohello lijst met **gepubliceerde URL's**.</span><span class="sxs-lookup"><span data-stu-id="a415b-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="a415b-187">Inhoud afspelen vanuit Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="a415b-187">Play content from hello portal</span></span>
<span data-ttu-id="a415b-188">Hello Azure portal biedt een speler inhoud die u tootest uw video gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="a415b-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="a415b-189">Klik op Hallo gewenste video en klik vervolgens op Hallo **afspelen** knop.</span><span class="sxs-lookup"><span data-stu-id="a415b-189">Click hello desired video and then click hello **Play** button.</span></span>

![Publiceren](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="a415b-191">Hierbij geldt het volgende:</span><span class="sxs-lookup"><span data-stu-id="a415b-191">Some considerations apply:</span></span>

* <span data-ttu-id="a415b-192">toobegin streaming starten actieve Hallo **standaard** streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a415b-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="a415b-193">Zorg ervoor dat Hallo video is gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="a415b-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="a415b-194">Dit **mediaspeler** speelt af vanaf Hallo standaard streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a415b-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="a415b-195">Als u wilt dat tooplay van een niet-standaard streaming-eindpunt, klikt u op toocopy Hallo URL en gebruikt een andere speler.</span><span class="sxs-lookup"><span data-stu-id="a415b-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="a415b-196">Bijvoorbeeld [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="a415b-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a415b-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a415b-197">Next steps</span></span>
<span data-ttu-id="a415b-198">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="a415b-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a415b-199">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="a415b-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

