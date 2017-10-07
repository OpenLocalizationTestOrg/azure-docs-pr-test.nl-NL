---
title: aaaLive stream met lokale coderingsprogramma's met behulp van hello Azure-portal | Microsoft Docs
description: Deze zelfstudie wordt u begeleid Hallo stappen voor het maken van een kanaal dat is geconfigureerd voor een doorvoerlevering.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="14580-103">Hoe live streamen van tooperform met lokale coderingsprogramma's via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="14580-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14580-104">Portal</span><span class="sxs-lookup"><span data-stu-id="14580-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="14580-105">.NET</span><span class="sxs-lookup"><span data-stu-id="14580-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="14580-106">REST</span><span class="sxs-lookup"><span data-stu-id="14580-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="14580-107">Deze zelfstudie leert u Hallo van het gebruik van Azure portal toocreate Hallo een **kanaal** die is geconfigureerd voor een doorvoerlevering.</span><span class="sxs-lookup"><span data-stu-id="14580-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="14580-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="14580-108">Prerequisites</span></span>
<span data-ttu-id="14580-109">Hallo volgen vereist toocomplete Hallo-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="14580-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="14580-110">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="14580-110">An Azure account.</span></span> <span data-ttu-id="14580-111">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14580-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="14580-112">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="14580-112">A Media Services account.</span></span> <span data-ttu-id="14580-113">een Media Services-account toocreate Zie [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="14580-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="14580-114">Een webcam.</span><span class="sxs-lookup"><span data-stu-id="14580-114">A webcam.</span></span> <span data-ttu-id="14580-115">Bijvoorbeeld [Telestream Wirecast-coderingsprogramma](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="14580-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="14580-116">Het is raadzaam tooreview Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="14580-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="14580-117">Azure Media Services RTMP-ondersteuning en live coderingsprogramma's</span><span class="sxs-lookup"><span data-stu-id="14580-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="14580-118">Overzicht van live streamen met Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="14580-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="14580-119">Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken</span><span class="sxs-lookup"><span data-stu-id="14580-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="14580-120"><a id="scenario"></a>Algemeen scenario voor live streamen</span><span class="sxs-lookup"><span data-stu-id="14580-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="14580-121">Hallo beschrijven volgende stappen taken voor het maken van algemene toepassingen voor live streamen die kanalen gebruiken die zijn geconfigureerd voor doorvoerlevering.</span><span class="sxs-lookup"><span data-stu-id="14580-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="14580-122">Deze zelfstudie laat zien hoe toocreate een doorvoerkanaal en live gebeurtenissen en beheren.</span><span class="sxs-lookup"><span data-stu-id="14580-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="14580-123">Zorg ervoor dat Hallo streaming-eindpunt van waaruit u wilt dat toostream inhoud wordt Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="14580-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="14580-124">Sluit een videocamera tooa-computer.</span><span class="sxs-lookup"><span data-stu-id="14580-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="14580-125">Start en configureer een on-premises live coderingsprogramma waarmee een multi-bitrate RTMP- of Fragmented MP4-stream wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="14580-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="14580-126">Zie [Azure Media Services RTMP-ondersteuning en live coderingsprogramma's](http://go.microsoft.com/fwlink/?LinkId=532824) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14580-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="14580-127">Deze stap kan ook worden uitgevoerd nadat u uw kanaal hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14580-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="14580-128">Maak en start een doorvoerkanaal.</span><span class="sxs-lookup"><span data-stu-id="14580-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="14580-129">URL voor opnemen ophalen Hallo kanaal.</span><span class="sxs-lookup"><span data-stu-id="14580-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="14580-130">Hallo URL voor opnemen wordt gebruikt door Hallo live coderingsprogramma toosend Hallo stroom toohello kanaal.</span><span class="sxs-lookup"><span data-stu-id="14580-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="14580-131">Hallo kanaal preview URL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="14580-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="14580-132">Gebruik deze URL tooverify dat Hallo livestream goed door het kanaal wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="14580-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="14580-133">Maak een live gebeurtenis/programma.</span><span class="sxs-lookup"><span data-stu-id="14580-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="14580-134">Wanneer met behulp van hello Azure-portal, het maken van een live gebeurtenis ook een asset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14580-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="14580-135">Start Hallo gebeurtenis/het programma wanneer u bent klaar toostart streamen en te archiveren.</span><span class="sxs-lookup"><span data-stu-id="14580-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="14580-136">Hallo live coderingsprogramma kan desgewenst gesignaleerde toostart een advertentie zijn.</span><span class="sxs-lookup"><span data-stu-id="14580-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="14580-137">Hallo advertentie wordt ingevoegd in de uitvoerstroom Hallo.</span><span class="sxs-lookup"><span data-stu-id="14580-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="14580-138">Stop Hallo gebeurtenis/het programma als u wilt dat toostop streaming en Hallo-gebeurtenis wilt archiveren.</span><span class="sxs-lookup"><span data-stu-id="14580-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="14580-139">Verwijder Hallo gebeurtenis/het programma (en verwijder desgewenst Hallo asset).</span><span class="sxs-lookup"><span data-stu-id="14580-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="14580-140">Raadpleeg [Live streamen met on-premises-coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) toolearn over de concepten en overwegingen gerelateerde toolive streamen met on-premises coderingsprogramma's en doorvoerkanalen.</span><span class="sxs-lookup"><span data-stu-id="14580-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="14580-141">tooview meldingen en fouten</span><span class="sxs-lookup"><span data-stu-id="14580-141">tooview notifications and errors</span></span>
<span data-ttu-id="14580-142">Als u wilt dat tooview meldingen en fouten die wordt geproduceerd door hello Azure-portal, klik op het pictogram in systeemvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="14580-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Meldingen](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="14580-144">Doorvoerkanalen en gebeurtenissen maken en starten</span><span class="sxs-lookup"><span data-stu-id="14580-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="14580-145">Een kanaal is gekoppeld aan gebeurtenissen/programma's waarmee u toocontrol Hallo publiceren en opslaan van segmenten in een live stream.</span><span class="sxs-lookup"><span data-stu-id="14580-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="14580-146">Kanalen beheren gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="14580-146">Channels manage events.</span></span> 

<span data-ttu-id="14580-147">Kunt u het aantal uren waarop u tooretain Hallo opgenomen inhoud voor Hallo programma door de instelling Hallo Hallo **archiefvenster** lengte.</span><span class="sxs-lookup"><span data-stu-id="14580-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="14580-148">Deze waarde kan worden ingesteld van minimaal 5 minuten tooa maximaal 25 uur.</span><span class="sxs-lookup"><span data-stu-id="14580-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="14580-149">Lengte van een archiefvenster bepaalt ook de maximale hoeveelheid tijd die clients terug in tijd vanaf de huidige live positie Hallo zoeken kunnen Hallo.</span><span class="sxs-lookup"><span data-stu-id="14580-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="14580-150">Gebeurtenissen in de opgegeven tijdsduur Hallo kunnen uitvoeren, maar de inhoud die achter de lengte van Hallo venster valt, wordt altijd verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14580-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="14580-151">De waarde van deze eigenschap bepaalt ook hoe lang Hallo client manifesten kunnen groeien.</span><span class="sxs-lookup"><span data-stu-id="14580-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="14580-152">Elke gebeurtenis is gekoppeld aan een asset.</span><span class="sxs-lookup"><span data-stu-id="14580-152">Each event is associated with an asset.</span></span> <span data-ttu-id="14580-153">toopublish hello gebeurtenis, moet u een OnDemand-locator voor Hallo gekoppeld asset maken.</span><span class="sxs-lookup"><span data-stu-id="14580-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="14580-154">Met deze locator kunt u een streaming-URL die u kunt tooyour clients leveren toobuild.</span><span class="sxs-lookup"><span data-stu-id="14580-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="14580-155">Een kanaal biedt ondersteuning voor maximaal toothree gebeurtenissen gelijktijdig uitvoeren zodat u kunt meerdere archieven van Hallo maken dezelfde binnenkomende stream.</span><span class="sxs-lookup"><span data-stu-id="14580-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="14580-156">Hiermee kunt u toopublish en te archiveren verschillende onderdelen van een gebeurtenis naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="14580-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="14580-157">De vereiste van uw bedrijf is bijvoorbeeld tooarchive zes uur van een programma, maar toobroadcast alleen de laatste tien minuten.</span><span class="sxs-lookup"><span data-stu-id="14580-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="14580-158">tooaccomplish, moet u twee gelijktijdig actieve programma's toocreate.</span><span class="sxs-lookup"><span data-stu-id="14580-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="14580-159">Een programma wordt ingesteld tooarchive zes uur van de gebeurtenis Hallo maar Hallo programma wordt niet gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="14580-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="14580-160">Hallo andere programma is set tooarchive voor 10 minuten en dit programma is gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="14580-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="14580-161">Gebruik de bestaande live gebeurtenissen niet opnieuw.</span><span class="sxs-lookup"><span data-stu-id="14580-161">You should not reuse existing live events.</span></span> <span data-ttu-id="14580-162">In plaats daarvan maakt en start u een nieuwe gebeurtenis voor elke gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="14580-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="14580-163">Start Hallo gebeurtenis wanneer u bent klaar toostart streamen en te archiveren.</span><span class="sxs-lookup"><span data-stu-id="14580-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="14580-164">Stop Hallo programma als u wilt dat toostop streaming en Hallo-gebeurtenis wilt archiveren.</span><span class="sxs-lookup"><span data-stu-id="14580-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="14580-165">toodelete gearchiveerde inhoud, stoppen en Hallo gebeurtenis verwijderen en verwijder vervolgens de gekoppelde asset Hallo.</span><span class="sxs-lookup"><span data-stu-id="14580-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="14580-166">Een asset kan niet worden verwijderd als deze wordt gebruikt door een gebeurtenis; Hallo-gebeurtenis moet eerst worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14580-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="14580-167">Zelfs na het stoppen en verwijderen van de gebeurtenis Hallo Hallo gebruikers kunnen toostream uw gearchiveerde inhoud als video op aanvraag voor niet zolang u Hallo asset niet hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14580-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="14580-168">Als u tooretain Hallo gearchiveerde inhoud wilt, maar niet langer voor streaming beschikbaar, verwijdert u Hallo streaming-locator.</span><span class="sxs-lookup"><span data-stu-id="14580-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="14580-169">toouse hello portal toocreate een kanaal</span><span class="sxs-lookup"><span data-stu-id="14580-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="14580-170">Deze sectie wordt beschreven hoe toouse hello **snelle invoer** optie toocreate een doorvoerkanaal.</span><span class="sxs-lookup"><span data-stu-id="14580-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="14580-171">Zie [Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie over doorvoerkanalen.</span><span class="sxs-lookup"><span data-stu-id="14580-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="14580-172">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="14580-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="14580-173">In Hallo **instellingen** venster, klikt u op **Live streamen**.</span><span class="sxs-lookup"><span data-stu-id="14580-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![Aan de slag](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="14580-175">Hallo **Live streamen** venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="14580-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="14580-176">Klik op **snelle invoer** toocreate een doorvoerkanaal Hello RTMP-opnameprotocol.</span><span class="sxs-lookup"><span data-stu-id="14580-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="14580-177">Hallo **een nieuw kanaal maken** venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="14580-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="14580-178">Hallo nieuw kanaal een naam geven en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="14580-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="14580-179">Hiermee maakt u een doorvoerkanaal Hello RTMP-opnameprotocol.</span><span class="sxs-lookup"><span data-stu-id="14580-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="14580-180">Gebeurtenissen maken</span><span class="sxs-lookup"><span data-stu-id="14580-180">Create events</span></span>
1. <span data-ttu-id="14580-181">Selecteer een kanaal toowhich gewenste tooadd een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="14580-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="14580-182">Klik op de knop **Live gebeurtenis**.</span><span class="sxs-lookup"><span data-stu-id="14580-182">Press **Live Event** button.</span></span>

![Gebeurtenis](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="14580-184">URL’s voor opnemen ophalen</span><span class="sxs-lookup"><span data-stu-id="14580-184">Get ingest URLs</span></span>
<span data-ttu-id="14580-185">Wanneer het Hallo-kanaal is gemaakt, kunt u URL's die u toohello live codering voor opnemen.</span><span class="sxs-lookup"><span data-stu-id="14580-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="14580-186">Hallo coderingsprogramma gebruikt deze URL's tooinput een live stream.</span><span class="sxs-lookup"><span data-stu-id="14580-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Gemaakt](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="14580-188">Hallo controlegebeurtenis</span><span class="sxs-lookup"><span data-stu-id="14580-188">Watch hello event</span></span>
<span data-ttu-id="14580-189">toowatch hello gebeurtenis, klikt u op **controle** in hello Azure portal of een kopie van Hallo streaming-URL en gebruikt u een speler van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="14580-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Gemaakt](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="14580-191">Live gebeurtenis ophalen automatisch inhoud geconverteerde tooon aanvraag wanneer gestopt.</span><span class="sxs-lookup"><span data-stu-id="14580-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="14580-192">Opruimen</span><span class="sxs-lookup"><span data-stu-id="14580-192">Clean up</span></span>
<span data-ttu-id="14580-193">Zie [Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie over doorvoerkanalen.</span><span class="sxs-lookup"><span data-stu-id="14580-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="14580-194">Een kanaal kan worden gestopt, alleen wanneer alle gebeurtenissen/programma's op Hallo kanaal zijn gestopt.</span><span class="sxs-lookup"><span data-stu-id="14580-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="14580-195">Zodra het Hallo-kanaal is gestopt, wordt deze niet worden geen kosten berekend.</span><span class="sxs-lookup"><span data-stu-id="14580-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="14580-196">Wanneer u toostart moet deze opnieuw, is er hello dezelfde URL voor opnemen zodat u geen tooreconfigure het coderingsprogramma hoeft.</span><span class="sxs-lookup"><span data-stu-id="14580-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="14580-197">Een kanaal kan alleen worden verwijderd als alle live gebeurtenissen op Hallo kanaal zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14580-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="14580-198">Gearchiveerde inhoud weergeven</span><span class="sxs-lookup"><span data-stu-id="14580-198">View archived content</span></span>
<span data-ttu-id="14580-199">Zelfs na het stoppen en verwijderen van de gebeurtenis Hallo Hallo gebruikers kunnen toostream uw gearchiveerde inhoud als video op aanvraag voor niet zolang u Hallo asset niet hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14580-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="14580-200">Een asset kan niet worden verwijderd als deze wordt gebruikt door een gebeurtenis; Hallo-gebeurtenis moet eerst worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14580-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="14580-201">uw assets selecteert u toomanage **instelling** en klik op **activa**.</span><span class="sxs-lookup"><span data-stu-id="14580-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Assets](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="14580-203">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="14580-203">Next step</span></span>
<span data-ttu-id="14580-204">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="14580-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="14580-205">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="14580-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

