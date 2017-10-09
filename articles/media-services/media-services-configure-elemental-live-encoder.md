---
title: aaaConfigure Hallo elementair Live coderingsprogramma toosend een single-bitrate live stream | Microsoft Docs
description: Dit onderwerp leest hoe tooconfigure Hallo elementair Live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="ac36f-103">Hallo elementair Live coderingsprogramma toosend een single-bitrate live stream gebruiken</span><span class="sxs-lookup"><span data-stu-id="ac36f-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac36f-104">Live elemental</span><span class="sxs-lookup"><span data-stu-id="ac36f-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="ac36f-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="ac36f-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="ac36f-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="ac36f-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="ac36f-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="ac36f-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="ac36f-108">Dit onderwerp wordt beschreven hoe tooconfigure hello [elementair Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="ac36f-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="ac36f-109">Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="ac36f-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="ac36f-110">Deze zelfstudie laat zien hoe toomanage Azure Media Services (AMS) met Azure Media Services Explorer (AMSE)-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="ac36f-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="ac36f-111">Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC.</span><span class="sxs-lookup"><span data-stu-id="ac36f-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="ac36f-112">Als u op Mac- of Linux, gebruikt u Azure portal toocreate hello [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="ac36f-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac36f-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac36f-113">Prerequisites</span></span>
* <span data-ttu-id="ac36f-114">Moet een praktische kennis van het gebruik van elementaire Live web interface toocreate live gebeurtenissen hebben.</span><span class="sxs-lookup"><span data-stu-id="ac36f-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="ac36f-115">Een Azure Media Services-account maken</span><span class="sxs-lookup"><span data-stu-id="ac36f-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="ac36f-116">Zorg dat er een Streaming-eindpunt is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ac36f-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="ac36f-117">Zie voor meer informatie [Streaming-eindpunten beheren in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="ac36f-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="ac36f-118">Installeer de meest recente versie Hallo Hallo [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="ac36f-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="ac36f-119">Hallo hulpprogramma start en tooyour AMS-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="ac36f-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="ac36f-120">Tips</span><span class="sxs-lookup"><span data-stu-id="ac36f-120">Tips</span></span>
* <span data-ttu-id="ac36f-121">Gebruik indien mogelijk een internetverbinding ' hardwired '.</span><span class="sxs-lookup"><span data-stu-id="ac36f-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="ac36f-122">Een goede vuistregel bij het bepalen van de vereiste bandbreedte is toodouble Hallo bitsnelheden streaming.</span><span class="sxs-lookup"><span data-stu-id="ac36f-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="ac36f-123">Hoewel dit niet verplicht is, wordt deze verminderen Hallo impact van opstoppingen in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="ac36f-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="ac36f-124">Wanneer met behulp van software gebaseerd coderingsprogramma's, sluit u alle onnodige programma's.</span><span class="sxs-lookup"><span data-stu-id="ac36f-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="ac36f-125">Elementaire Live met RTP opnemen</span><span class="sxs-lookup"><span data-stu-id="ac36f-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="ac36f-126">Deze sectie wordt beschreven hoe tooconfigure Hallo elementair Live coderingsprogramma dat verzendt een single bitrate livestream via RTP.</span><span class="sxs-lookup"><span data-stu-id="ac36f-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="ac36f-127">Zie voor meer informatie [MPEG-TS-stream via RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="ac36f-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="ac36f-128">Een kanaal maken</span><span class="sxs-lookup"><span data-stu-id="ac36f-128">Create a channel</span></span>

1. <span data-ttu-id="ac36f-129">Navigeer in Hallo AMSE-hulpprogramma, toohello **Live** tabblad en klik met de rechtermuisknop in Hallo kanaal gebied.</span><span class="sxs-lookup"><span data-stu-id="ac36f-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="ac36f-130">Selecteer **kanaal maken...**</span><span class="sxs-lookup"><span data-stu-id="ac36f-130">Select **Create channel…**</span></span> <span data-ttu-id="ac36f-131">Hallo upmenu.</span><span class="sxs-lookup"><span data-stu-id="ac36f-131">from hello menu.</span></span>

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="ac36f-133">Geef een kanaalnaam Hallo beschrijvingsveld is optioneel.</span><span class="sxs-lookup"><span data-stu-id="ac36f-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="ac36f-134">Selecteer onder instellingen voor kanaal **standaard** voor Hallo optie Live Encoding, hello invoer Protocol ingesteld te**RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="ac36f-135">U kunt alle andere instellingen zoals is laten.</span><span class="sxs-lookup"><span data-stu-id="ac36f-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="ac36f-136">Zorg ervoor dat Hallo **Start Hallo nieuw kanaal nu** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ac36f-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="ac36f-137">Klik op **kanaal maken**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-137">Click **Create Channel**.</span></span>

   ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="ac36f-139">Hallo kanaal kan 20 minuten toostart zo lang duren.</span><span class="sxs-lookup"><span data-stu-id="ac36f-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="ac36f-140">Tijdens het Hallo-kanaal wordt gestart. u kunt [Hallo-codering configureren](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="ac36f-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac36f-141">Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed.</span><span class="sxs-lookup"><span data-stu-id="ac36f-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="ac36f-142">Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="ac36f-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="ac36f-143"><a id=configure_elemental_rtp></a>Hallo elementair Live coderingsprogramma configureren</span><span class="sxs-lookup"><span data-stu-id="ac36f-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="ac36f-144">In deze zelfstudie Hallo volgende uitvoerinstellingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ac36f-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="ac36f-145">Hallo rest van deze sectie beschrijft de configuratiestappen in meer detail.</span><span class="sxs-lookup"><span data-stu-id="ac36f-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="ac36f-146">**Video**:</span><span class="sxs-lookup"><span data-stu-id="ac36f-146">**Video**:</span></span>

* <span data-ttu-id="ac36f-147">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="ac36f-147">Codec: H.264</span></span>
* <span data-ttu-id="ac36f-148">Profiel: Hoge (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="ac36f-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="ac36f-149">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="ac36f-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="ac36f-150">Sleutelframe: 2 seconden (60 seconden)</span><span class="sxs-lookup"><span data-stu-id="ac36f-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="ac36f-151">Frequentie frame: 30</span><span class="sxs-lookup"><span data-stu-id="ac36f-151">Frame Rate: 30</span></span>

<span data-ttu-id="ac36f-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="ac36f-152">**Audio**:</span></span>

* <span data-ttu-id="ac36f-153">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="ac36f-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="ac36f-154">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="ac36f-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="ac36f-155">Samplefrequentie: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="ac36f-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="ac36f-156">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="ac36f-156">Configuration steps</span></span>
1. <span data-ttu-id="ac36f-157">Navigeer toohello **elementair Live** webinterface en stellen Hallo-codering voor **UDP/TS** streaming.</span><span class="sxs-lookup"><span data-stu-id="ac36f-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="ac36f-158">Zodra een nieuwe gebeurtenis is gemaakt, schuif naar beneden toohello uitvoer groepen en Hallo toevoegen **UDP/TS** uitvoer groep.</span><span class="sxs-lookup"><span data-stu-id="ac36f-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="ac36f-159">De uitvoer van een nieuwe maken door te selecteren **nieuwe Stream** en vervolgens te klikken op **uitvoer toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="ac36f-161">Het verdient aanbeveling dat Hallo elementair gebeurtenis heeft Hallo tijdcode instellen te 'Systeemklok' toohelp Hallo encoder opnieuw verbinding maken in geval van een stroom fout Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac36f-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="ac36f-162">Nu hello uitvoer is gemaakt, klikt u op **stroom toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="ac36f-163">Hallo uitvoerinstellingen kunnen nu worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ac36f-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="ac36f-164">Schuif naar beneden toohello 'Stream 1' die is gemaakt, klikt u op Hallo **Video** tabblad op Hallo links en vouw Hallo **Geavanceerd** gedeelte instellingen.</span><span class="sxs-lookup"><span data-stu-id="ac36f-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="ac36f-166">Terwijl elementair Live een breed scala heeft aan beschikbare aanpassen, worden hello volgende instellingen aanbevolen voor aan de slag met tooAMS streaming.</span><span class="sxs-lookup"><span data-stu-id="ac36f-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="ac36f-167">Oplossing: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="ac36f-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="ac36f-168">Framesnelheid: 30</span><span class="sxs-lookup"><span data-stu-id="ac36f-168">Framerate: 30</span></span>
   * <span data-ttu-id="ac36f-169">GOP grootte: 60 frames</span><span class="sxs-lookup"><span data-stu-id="ac36f-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="ac36f-170">Modus interliniëren: progressief</span><span class="sxs-lookup"><span data-stu-id="ac36f-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="ac36f-171">Bitrate: 5000000 bits/s (dit kan worden aangepast op basis van de beperkingen op het netwerk)</span><span class="sxs-lookup"><span data-stu-id="ac36f-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="ac36f-173">Hallo-kanaal invoer-URL ophalen.</span><span class="sxs-lookup"><span data-stu-id="ac36f-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="ac36f-174">Navigeer terug toohello AMSE-hulpprogramma, en controleren op Hallo kanaal voltooiingsstatus weer.</span><span class="sxs-lookup"><span data-stu-id="ac36f-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="ac36f-175">Zodra het Hallo-status is gewijzigd van **starten** te**met**, krijgt u Hallo invoer-URL.</span><span class="sxs-lookup"><span data-stu-id="ac36f-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="ac36f-176">Wanneer Hallo kanaal wordt uitgevoerd, klik met de rechtermuisknop op Hallo kanaalnaam, omlaag toohover gaan via **invoer-URL kopiëren tooclipboard** en selecteer vervolgens **primaire invoer-URL**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="ac36f-178">Deze informatie plakken in Hallo **primaire doel** veld Hallo Elemental.</span><span class="sxs-lookup"><span data-stu-id="ac36f-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="ac36f-179">Alle andere instellingen kunnen Hallo standaard blijven.</span><span class="sxs-lookup"><span data-stu-id="ac36f-179">All other settings can remain hello default.</span></span>

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="ac36f-181">Herhaal deze stappen Hello secundaire invoer-URL voor het maken van een afzonderlijke tabblad 'Uitvoer' voor het UDP/TS Streaming voor extra redundantie.</span><span class="sxs-lookup"><span data-stu-id="ac36f-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="ac36f-182">Klik op **maken** (als een nieuwe gebeurtenis is gemaakt) of **Update** (als een bestaande gebeurtenis bewerken) en ga vervolgens verder toostart Hallo encoder.</span><span class="sxs-lookup"><span data-stu-id="ac36f-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac36f-183">Voordat u op **Start** op Hallo elementair Live webinterface, u **moet** ervoor te zorgen dat het Hallo-kanaal klaar is.</span><span class="sxs-lookup"><span data-stu-id="ac36f-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="ac36f-184">Zorg er ook geen tooleave Hallo kanaal in een status gereed zonder een gebeurtenis voor langer dan 15 minuten >.</span><span class="sxs-lookup"><span data-stu-id="ac36f-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="ac36f-185">Nadat het Hallo stroom actief is geweest gedurende 30 seconden, gaat u terug toohello AMSE hulpprogramma's en test afspelen.</span><span class="sxs-lookup"><span data-stu-id="ac36f-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="ac36f-186">Test afspelen</span><span class="sxs-lookup"><span data-stu-id="ac36f-186">Test playback</span></span>

<span data-ttu-id="ac36f-187">Navigeer toohello AMSE-hulpprogramma en Hallo kanaal toobe getest met de rechtermuisknop op.</span><span class="sxs-lookup"><span data-stu-id="ac36f-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="ac36f-188">Hallo menu Beweeg de muisaanwijzer over **afspelen Hallo Preview** en selecteer **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="ac36f-189">Als Hallo stroom wordt weergegeven in Hallo-speler, heeft Hallo encoder correct geconfigureerde tooconnect tooAMS zijn.</span><span class="sxs-lookup"><span data-stu-id="ac36f-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="ac36f-190">Als een fout wordt ontvangen, moet Hallo kanaal toobe opnieuw instellen en coderingsprogramma instellingen aangepast.</span><span class="sxs-lookup"><span data-stu-id="ac36f-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="ac36f-191">Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="ac36f-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="ac36f-192">Een programma maken</span><span class="sxs-lookup"><span data-stu-id="ac36f-192">Create a program</span></span>
1. <span data-ttu-id="ac36f-193">Nadat het kanaal afspelen is bevestigd, maak een programma.</span><span class="sxs-lookup"><span data-stu-id="ac36f-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="ac36f-194">Onder Hallo **Live** tabblad Hallo AMSE-hulpprogramma, klik met de rechtermuisknop in Hallo programma gebied en selecteer **nieuw programma maken**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="ac36f-196">Hallo-programma een naam en wijzig indien nodig, Hallo **lengte van een archiefvenster** (welke standaardwaarden too4 uur).</span><span class="sxs-lookup"><span data-stu-id="ac36f-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="ac36f-197">U kunt ook opgeven van een opslaglocatie of laat als Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="ac36f-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="ac36f-198">Controleer de Hallo **Start Hallo programma nu** vak.</span><span class="sxs-lookup"><span data-stu-id="ac36f-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="ac36f-199">Klik op **programma maken**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="ac36f-200">Maken van het programma kost minder tijd dan het maken van kanaal.</span><span class="sxs-lookup"><span data-stu-id="ac36f-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="ac36f-201">Zodra het Hallo-programma wordt uitgevoerd, bevestigt u afspelen met de rechtermuisknop te klikken op het Hallo-programma en te navigeren**afspelen Hallo-programma's** en selecteren **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="ac36f-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="ac36f-202">Zodra bevestigd, klik met de rechtermuisknop Hallo programma opnieuw en selecteer **kopiëren Hallo uitvoer URL tooClipboard** (of deze informatie ophalen van Hallo **programma gegevens en instellingen** optie uit Hallo menu).</span><span class="sxs-lookup"><span data-stu-id="ac36f-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="ac36f-203">Hallo-stroom is nu gereed toobe ingesloten in een speler of gedistribueerde tooan doelgroep voor live weergeven.</span><span class="sxs-lookup"><span data-stu-id="ac36f-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="ac36f-204">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ac36f-204">Troubleshooting</span></span>
<span data-ttu-id="ac36f-205">Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="ac36f-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ac36f-206">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="ac36f-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ac36f-207">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="ac36f-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
