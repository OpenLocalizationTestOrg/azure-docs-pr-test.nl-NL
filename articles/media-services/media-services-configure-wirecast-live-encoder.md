---
title: aaaConfigure hello Telestream Wirecast-coderingsprogramma toosend een single-bitrate live stream | Microsoft Docs
description: 'Dit onderwerp leest hoe tooconfigure hello Wirecast live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering. '
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="6beb5-103">Hallo Wirecast-coderingsprogramma toosend een single-bitrate live stream gebruiken</span><span class="sxs-lookup"><span data-stu-id="6beb5-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6beb5-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="6beb5-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="6beb5-105">Live elemental</span><span class="sxs-lookup"><span data-stu-id="6beb5-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="6beb5-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="6beb5-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="6beb5-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="6beb5-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="6beb5-108">Dit onderwerp wordt beschreven hoe tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="6beb5-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="6beb5-109">Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="6beb5-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="6beb5-110">Deze zelfstudie laat zien hoe toomanage Azure Media Services (AMS) met Azure Media Services Explorer (AMSE)-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="6beb5-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="6beb5-111">Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC.</span><span class="sxs-lookup"><span data-stu-id="6beb5-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="6beb5-112">Als u op Mac- of Linux, gebruikt u Azure portal toocreate hello [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="6beb5-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6beb5-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6beb5-113">Prerequisites</span></span>
* [<span data-ttu-id="6beb5-114">Een Azure Media Services-account maken</span><span class="sxs-lookup"><span data-stu-id="6beb5-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="6beb5-115">Zorg dat er een Streaming-eindpunt is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6beb5-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="6beb5-116">Zie voor meer informatie [Streaming-eindpunten beheren in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="6beb5-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="6beb5-117">Installeer de meest recente versie Hallo Hallo [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="6beb5-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="6beb5-118">Hallo hulpprogramma start en tooyour AMS-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="6beb5-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="6beb5-119">Tips</span><span class="sxs-lookup"><span data-stu-id="6beb5-119">Tips</span></span>
* <span data-ttu-id="6beb5-120">Gebruik indien mogelijk een internetverbinding ' hardwired '.</span><span class="sxs-lookup"><span data-stu-id="6beb5-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="6beb5-121">Een goede vuistregel bij het bepalen van de vereiste bandbreedte is toodouble Hallo bitsnelheden streaming.</span><span class="sxs-lookup"><span data-stu-id="6beb5-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="6beb5-122">Hoewel dit niet verplicht is, wordt deze verminderen Hallo impact van opstoppingen in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="6beb5-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="6beb5-123">Wanneer met behulp van software gebaseerd coderingsprogramma's, sluit u alle onnodige programma's.</span><span class="sxs-lookup"><span data-stu-id="6beb5-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="6beb5-124">Een kanaal maken</span><span class="sxs-lookup"><span data-stu-id="6beb5-124">Create a channel</span></span>
1. <span data-ttu-id="6beb5-125">Navigeer in Hallo AMSE-hulpprogramma, toohello **Live** tabblad en klik met de rechtermuisknop in Hallo kanaal gebied.</span><span class="sxs-lookup"><span data-stu-id="6beb5-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="6beb5-126">Selecteer **kanaal maken...**</span><span class="sxs-lookup"><span data-stu-id="6beb5-126">Select **Create channel…**</span></span> <span data-ttu-id="6beb5-127">Hallo upmenu.</span><span class="sxs-lookup"><span data-stu-id="6beb5-127">from hello menu.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="6beb5-129">Geef een kanaalnaam Hallo beschrijvingsveld is optioneel.</span><span class="sxs-lookup"><span data-stu-id="6beb5-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="6beb5-130">Selecteer onder instellingen voor kanaal **standaard** voor Hallo optie Live Encoding, hello invoer Protocol ingesteld te**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="6beb5-131">U kunt alle andere instellingen zoals is laten.</span><span class="sxs-lookup"><span data-stu-id="6beb5-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="6beb5-132">Zorg ervoor dat Hallo **Start Hallo nieuw kanaal nu** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="6beb5-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="6beb5-133">Klik op **kanaal maken**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-133">Click **Create Channel**.</span></span>

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="6beb5-135">Hallo kanaal kan 20 minuten toostart zo lang duren.</span><span class="sxs-lookup"><span data-stu-id="6beb5-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="6beb5-136">Tijdens het Hallo-kanaal wordt gestart. u kunt [Hallo-codering configureren](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="6beb5-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6beb5-137">Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed.</span><span class="sxs-lookup"><span data-stu-id="6beb5-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="6beb5-138">Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="6beb5-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="6beb5-139"><a id=configure_wirecast_rtmp></a>Hallo Telestream Wirecast-coderingsprogramma configureren</span><span class="sxs-lookup"><span data-stu-id="6beb5-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="6beb5-140">In deze zelfstudie Hallo volgende uitvoerinstellingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6beb5-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="6beb5-141">Hallo rest van deze sectie beschrijft de configuratiestappen in meer detail.</span><span class="sxs-lookup"><span data-stu-id="6beb5-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="6beb5-142">**Video**:</span><span class="sxs-lookup"><span data-stu-id="6beb5-142">**Video**:</span></span>

* <span data-ttu-id="6beb5-143">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="6beb5-143">Codec: H.264</span></span>
* <span data-ttu-id="6beb5-144">Profiel: Hoge (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="6beb5-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="6beb5-145">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="6beb5-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="6beb5-146">Sleutelframe: 2 seconden (60 seconden)</span><span class="sxs-lookup"><span data-stu-id="6beb5-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="6beb5-147">Frequentie frame: 30</span><span class="sxs-lookup"><span data-stu-id="6beb5-147">Frame Rate: 30</span></span>

<span data-ttu-id="6beb5-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="6beb5-148">**Audio**:</span></span>

* <span data-ttu-id="6beb5-149">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="6beb5-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="6beb5-150">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="6beb5-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="6beb5-151">Samplefrequentie: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="6beb5-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="6beb5-152">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="6beb5-152">Configuration steps</span></span>
1. <span data-ttu-id="6beb5-153">Open Hallo Telestream Wirecast-toepassing op het Hallo-machine wordt gebruikt, en voor het streamen van RTMP ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6beb5-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="6beb5-154">Hallo-uitvoer configureren door te navigeren toohello **uitvoer** tabblad en het selecteren van **uitvoerinstellingen...** .</span><span class="sxs-lookup"><span data-stu-id="6beb5-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="6beb5-155">Zorg ervoor dat Hallo **bestemming voor de uitvoer** te is ingesteld,**RTMP Server**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="6beb5-156">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-156">Click **OK**.</span></span>
4. <span data-ttu-id="6beb5-157">Ingesteld op de instellingenpagina Hallo Hallo **bestemming** veld toobe **Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="6beb5-158">Hallo codering profiel is vooraf ingeschakeld te**Azure H.264 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="6beb5-159">toocustomize deze instellingen, selecteer Hallo tandwielpictogram pictogram toohello rechts van Hallo vervolgkeuzelijst en kies vervolgens **nieuwe voorinstelling**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="6beb5-161">Standaardinstellingen voor codering configureren.</span><span class="sxs-lookup"><span data-stu-id="6beb5-161">Configure encoder presets.</span></span>

    <span data-ttu-id="6beb5-162">Naam Hallo voorinstelling en te controleren op Hallo volgende aanbevolen instellingen:</span><span class="sxs-lookup"><span data-stu-id="6beb5-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="6beb5-163">**Video**</span><span class="sxs-lookup"><span data-stu-id="6beb5-163">**Video**</span></span>

   * <span data-ttu-id="6beb5-164">Codering: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="6beb5-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="6beb5-165">Frames per seconde: 30</span><span class="sxs-lookup"><span data-stu-id="6beb5-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="6beb5-166">Gemiddelde bitsnelheid: 5000 kbits per seconde (kan worden aangepast op basis van de beperkingen op het netwerk)</span><span class="sxs-lookup"><span data-stu-id="6beb5-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="6beb5-167">Profiel: Main</span><span class="sxs-lookup"><span data-stu-id="6beb5-167">Profile: Main</span></span>
   * <span data-ttu-id="6beb5-168">Sleutelframe elke: 60 frames</span><span class="sxs-lookup"><span data-stu-id="6beb5-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="6beb5-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="6beb5-169">**Audio**</span></span>

   * <span data-ttu-id="6beb5-170">Doelbitsnelheid: 192 kbits per seconde</span><span class="sxs-lookup"><span data-stu-id="6beb5-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="6beb5-171">Samplefrequentie: 44,100 kHz</span><span class="sxs-lookup"><span data-stu-id="6beb5-171">Sample Rate: 44.100 kHz</span></span>

     ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="6beb5-173">Druk op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-173">Press **Save**.</span></span>

    <span data-ttu-id="6beb5-174">het veld Encoding Hallo is nu Hallo nieuw gemaakt profiel beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="6beb5-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="6beb5-175">Zorg ervoor dat nieuwe Hallo-profiel is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="6beb5-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="6beb5-176">Hallo-kanaal invoer-URL ophalen in volgorde tooassign het toohello Wirecast **RTMP eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="6beb5-177">Navigeer terug toohello AMSE-hulpprogramma, en controleren op Hallo kanaal voltooiingsstatus weer.</span><span class="sxs-lookup"><span data-stu-id="6beb5-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="6beb5-178">Zodra het Hallo-status is gewijzigd van **starten** te**met**, krijgt u Hallo invoer-URL.</span><span class="sxs-lookup"><span data-stu-id="6beb5-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="6beb5-179">Wanneer Hallo kanaal wordt uitgevoerd, klik met de rechtermuisknop op Hallo kanaalnaam, omlaag toohover gaan via **invoer-URL kopiëren tooclipboard** en selecteer vervolgens **primaire invoer-URL**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="6beb5-181">In Hallo Wirecast **uitvoerinstellingen** venster plakt u deze informatie in Hallo **adres** veld sectie Hallo-uitvoer, en wijst u de naam van een gegevensstroom.</span><span class="sxs-lookup"><span data-stu-id="6beb5-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="6beb5-183">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-183">Select **OK**.</span></span>
2. <span data-ttu-id="6beb5-184">Op de belangrijkste Hallo **Wirecast** scherm, invoerbronnen bevestigen voor video en audio gereed zijn en klik vervolgens op **stroom** in Hallo bovenste linkerkant hoek.</span><span class="sxs-lookup"><span data-stu-id="6beb5-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="6beb5-186">Voordat u op **stroom**, u **moet** ervoor te zorgen dat het Hallo-kanaal klaar is.</span><span class="sxs-lookup"><span data-stu-id="6beb5-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="6beb5-187">Zorg er ook geen tooleave Hallo kanaal in een status gereed zonder een bijdrage invoer feed langer dan 15 minuten >.</span><span class="sxs-lookup"><span data-stu-id="6beb5-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="6beb5-188">Test afspelen</span><span class="sxs-lookup"><span data-stu-id="6beb5-188">Test playback</span></span>

<span data-ttu-id="6beb5-189">Navigeer toohello AMSE-hulpprogramma en Hallo kanaal toobe getest met de rechtermuisknop op.</span><span class="sxs-lookup"><span data-stu-id="6beb5-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="6beb5-190">Hallo menu Beweeg de muisaanwijzer over **afspelen Hallo Preview** en selecteer **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="6beb5-191">Als Hallo stroom wordt weergegeven in Hallo-speler, heeft Hallo encoder correct geconfigureerde tooconnect tooAMS zijn.</span><span class="sxs-lookup"><span data-stu-id="6beb5-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="6beb5-192">Als een fout wordt ontvangen, moet Hallo kanaal toobe opnieuw instellen en coderingsprogramma instellingen aangepast.</span><span class="sxs-lookup"><span data-stu-id="6beb5-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="6beb5-193">Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="6beb5-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="6beb5-194">Een programma maken</span><span class="sxs-lookup"><span data-stu-id="6beb5-194">Create a program</span></span>
1. <span data-ttu-id="6beb5-195">Nadat het kanaal afspelen is bevestigd, maak een programma.</span><span class="sxs-lookup"><span data-stu-id="6beb5-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="6beb5-196">Onder Hallo **Live** tabblad Hallo AMSE-hulpprogramma, klik met de rechtermuisknop in Hallo programma gebied en selecteer **nieuw programma maken**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="6beb5-198">Hallo-programma een naam en wijzig indien nodig, Hallo **lengte van een archiefvenster** (welke standaardwaarden too4 uur).</span><span class="sxs-lookup"><span data-stu-id="6beb5-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="6beb5-199">U kunt ook opgeven van een opslaglocatie of laat als Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="6beb5-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="6beb5-200">Controleer de Hallo **Start Hallo programma nu** vak.</span><span class="sxs-lookup"><span data-stu-id="6beb5-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="6beb5-201">Klik op **programma maken**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="6beb5-202">Maken van het programma kost minder tijd dan het maken van kanaal.</span><span class="sxs-lookup"><span data-stu-id="6beb5-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="6beb5-203">Zodra het Hallo-programma wordt uitgevoerd, bevestigt u afspelen met de rechtermuisknop te klikken op het Hallo-programma en te navigeren**afspelen Hallo-programma's** en selecteren **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="6beb5-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="6beb5-204">Zodra bevestigd, klik met de rechtermuisknop Hallo programma opnieuw en selecteer **kopiëren Hallo uitvoer URL tooClipboard** (of deze informatie ophalen van Hallo **programma gegevens en instellingen** optie uit Hallo menu).</span><span class="sxs-lookup"><span data-stu-id="6beb5-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="6beb5-205">Hallo-stroom is nu gereed toobe ingesloten in een speler of gedistribueerde tooan doelgroep voor live weergeven.</span><span class="sxs-lookup"><span data-stu-id="6beb5-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="6beb5-206">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="6beb5-206">Troubleshooting</span></span>
<span data-ttu-id="6beb5-207">Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="6beb5-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6beb5-208">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="6beb5-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6beb5-209">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="6beb5-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
