---
title: Configureer het elementaire Live coderingsprogramma voor het verzenden van een single-bitrate live stream | Microsoft Docs
description: Dit onderwerp leest hoe u configureert het elementaire Live coderingsprogramma voor het verzenden van een single-bitrate stream AMS-kanalen die zijn ingeschakeld voor live codering.
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
ms.openlocfilehash: 668a3ab46a70c0ee25fa87031d27c0f4333ec89c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="89b37-103">Het elementaire Live coderingsprogramma gebruiken voor het verzenden van een single-bitrate live stream</span><span class="sxs-lookup"><span data-stu-id="89b37-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89b37-104">Live elemental</span><span class="sxs-lookup"><span data-stu-id="89b37-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="89b37-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="89b37-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="89b37-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="89b37-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="89b37-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="89b37-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="89b37-108">Dit onderwerp wordt beschreven hoe u configureert de [elementair Live](http://www.elementaltechnologies.com/products/elemental-live) codering verzendt een single-bitrate stream naar AMS kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="89b37-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="89b37-109">Zie [Werken met kanalen waarmee Live Encoding kan worden uitgevoerd met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="89b37-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="89b37-110">Deze zelfstudie laat zien hoe Azure Media Services (AMS) beheren met Azure Media Services Explorer (AMSE)-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="89b37-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="89b37-111">Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC.</span><span class="sxs-lookup"><span data-stu-id="89b37-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="89b37-112">Als u op Mac- of Linux, gebruikt u de Azure portal maken [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="89b37-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89b37-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="89b37-113">Prerequisites</span></span>
* <span data-ttu-id="89b37-114">Moet een werkende kennis hebben van elementaire Live web-interface gebruiken voor het maken van live gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="89b37-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* [<span data-ttu-id="89b37-115">Een Azure Media Services-account maken</span><span class="sxs-lookup"><span data-stu-id="89b37-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="89b37-116">Zorg dat er een Streaming-eindpunt is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="89b37-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="89b37-117">Zie voor meer informatie [Streaming-eindpunten beheren in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="89b37-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="89b37-118">Installeer de nieuwste versie van de [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="89b37-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="89b37-119">Het hulpprogramma voor starten en verbinding maken met uw AMS-account.</span><span class="sxs-lookup"><span data-stu-id="89b37-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="89b37-120">Tips</span><span class="sxs-lookup"><span data-stu-id="89b37-120">Tips</span></span>
* <span data-ttu-id="89b37-121">Gebruik indien mogelijk een internetverbinding ' hardwired '.</span><span class="sxs-lookup"><span data-stu-id="89b37-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="89b37-122">Een goede vuistregel bij het bepalen van de vereiste bandbreedte is voor de streaming bitsnelheden verdubbelen.</span><span class="sxs-lookup"><span data-stu-id="89b37-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="89b37-123">Hoewel dit niet verplicht is, wordt deze verminderen de impact van opstoppingen in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="89b37-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="89b37-124">Wanneer met behulp van software gebaseerd coderingsprogramma's, sluit u alle onnodige programma's.</span><span class="sxs-lookup"><span data-stu-id="89b37-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="89b37-125">Elementaire Live met RTP opnemen</span><span class="sxs-lookup"><span data-stu-id="89b37-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="89b37-126">Deze sectie toont hoe u configureert het elementaire Live coderingsprogramma dat een single-bitrate live stream via RTP verzendt.</span><span class="sxs-lookup"><span data-stu-id="89b37-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="89b37-127">Zie voor meer informatie [MPEG-TS-stream via RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="89b37-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="89b37-128">Een kanaal maken</span><span class="sxs-lookup"><span data-stu-id="89b37-128">Create a channel</span></span>

1. <span data-ttu-id="89b37-129">Navigeer in het AMSE-hulpprogramma naar het **Live** tabblad en klik met de rechtermuisknop in het gebied van kanaal.</span><span class="sxs-lookup"><span data-stu-id="89b37-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="89b37-130">Selecteer **kanaal maken...**</span><span class="sxs-lookup"><span data-stu-id="89b37-130">Select **Create channel…**</span></span> <span data-ttu-id="89b37-131">in het menu.</span><span class="sxs-lookup"><span data-stu-id="89b37-131">from the menu.</span></span>

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="89b37-133">Geef een kanaalnaam het beschrijvingsveld is optioneel.</span><span class="sxs-lookup"><span data-stu-id="89b37-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="89b37-134">Selecteer onder instellingen voor kanaal **standaard** voor de optie Live Encoding met het invoer-Protocol die is ingesteld op **RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="89b37-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="89b37-135">U kunt alle andere instellingen zoals is laten.</span><span class="sxs-lookup"><span data-stu-id="89b37-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="89b37-136">Zorg ervoor dat de **nu starten van het nieuwe kanaal** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="89b37-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="89b37-137">Klik op **kanaal maken**.</span><span class="sxs-lookup"><span data-stu-id="89b37-137">Click **Create Channel**.</span></span>

   ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="89b37-139">Het kanaal kan zo lang starten 20 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="89b37-139">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="89b37-140">Terwijl het kanaal wordt gestart. u kunt [configureren van het coderingsprogramma](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="89b37-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89b37-141">Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed.</span><span class="sxs-lookup"><span data-stu-id="89b37-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="89b37-142">Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="89b37-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="89b37-143"><a id=configure_elemental_rtp></a>Het elementaire Live coderingsprogramma configureren</span><span class="sxs-lookup"><span data-stu-id="89b37-143"><a id=configure_elemental_rtp></a>Configure the Elemental Live encoder</span></span>
<span data-ttu-id="89b37-144">In deze zelfstudie worden de volgende uitvoerinstellingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="89b37-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="89b37-145">De rest van deze sectie beschrijft de configuratiestappen in meer detail.</span><span class="sxs-lookup"><span data-stu-id="89b37-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="89b37-146">**Video**:</span><span class="sxs-lookup"><span data-stu-id="89b37-146">**Video**:</span></span>

* <span data-ttu-id="89b37-147">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="89b37-147">Codec: H.264</span></span>
* <span data-ttu-id="89b37-148">Profiel: Hoge (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="89b37-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="89b37-149">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="89b37-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="89b37-150">Sleutelframe: 2 seconden (60 seconden)</span><span class="sxs-lookup"><span data-stu-id="89b37-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="89b37-151">Frequentie frame: 30</span><span class="sxs-lookup"><span data-stu-id="89b37-151">Frame Rate: 30</span></span>

<span data-ttu-id="89b37-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="89b37-152">**Audio**:</span></span>

* <span data-ttu-id="89b37-153">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="89b37-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="89b37-154">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="89b37-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="89b37-155">Samplefrequentie: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="89b37-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="89b37-156">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="89b37-156">Configuration steps</span></span>
1. <span data-ttu-id="89b37-157">Navigeer naar de **elementair Live** webinterface en instellen van het coderingsprogramma voor **UDP/TS** streaming.</span><span class="sxs-lookup"><span data-stu-id="89b37-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="89b37-158">Wanneer een nieuwe gebeurtenis is gemaakt, bladert u omlaag naar de uitvoer-groepen en toevoegen de **UDP/TS** uitvoer groep.</span><span class="sxs-lookup"><span data-stu-id="89b37-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="89b37-159">De uitvoer van een nieuwe maken door te selecteren **nieuwe Stream** en vervolgens te klikken op **uitvoer toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="89b37-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="89b37-161">Het wordt aanbevolen dat de elementair gebeurtenis de tijdcode ingesteld op 'Systeemklok heeft' om u te helpen bij het coderingsprogramma opnieuw verbinding maken in het geval van een storing van de stroom.</span><span class="sxs-lookup"><span data-stu-id="89b37-161">It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="89b37-162">Nu dat de uitvoer is gemaakt, klikt u op **stroom toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="89b37-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="89b37-163">De uitvoerinstellingen kunnen nu worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="89b37-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="89b37-164">Schuif omlaag naar 'Stream 1' die is gemaakt, klikt u op de **Video** tabblad aan de linkerkant en vouw de **Geavanceerd** gedeelte instellingen.</span><span class="sxs-lookup"><span data-stu-id="89b37-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="89b37-166">Terwijl elementair Live een breed scala heeft aan beschikbare aanpassen, worden de volgende instellingen worden aanbevolen voor aan de slag met streaming aan AMS.</span><span class="sxs-lookup"><span data-stu-id="89b37-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="89b37-167">Oplossing: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="89b37-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="89b37-168">Framesnelheid: 30</span><span class="sxs-lookup"><span data-stu-id="89b37-168">Framerate: 30</span></span>
   * <span data-ttu-id="89b37-169">GOP grootte: 60 frames</span><span class="sxs-lookup"><span data-stu-id="89b37-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="89b37-170">Modus interliniëren: progressief</span><span class="sxs-lookup"><span data-stu-id="89b37-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="89b37-171">Bitrate: 5000000 bits/s (dit kan worden aangepast op basis van de beperkingen op het netwerk)</span><span class="sxs-lookup"><span data-stu-id="89b37-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="89b37-173">Ophalen van het kanaal invoer-URL.</span><span class="sxs-lookup"><span data-stu-id="89b37-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="89b37-174">Ga terug naar het AMSE-hulpprogramma, en controleren van de voltooiingsstatus van kanaal.</span><span class="sxs-lookup"><span data-stu-id="89b37-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="89b37-175">Zodra de status is gewijzigd van **starten** naar **met**, krijgt u de invoer-URL.</span><span class="sxs-lookup"><span data-stu-id="89b37-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="89b37-176">Wanneer het kanaal wordt uitgevoerd, klikt u met de rechtermuisknop op naam van het kanaal, navigeer naar aanwijzen via **invoer-URL kopiëren naar Klembord** en selecteer vervolgens **primaire invoer-URL**.</span><span class="sxs-lookup"><span data-stu-id="89b37-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="89b37-178">Plak deze informatie in de **primaire doel** veld van de vorm van het element.</span><span class="sxs-lookup"><span data-stu-id="89b37-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="89b37-179">Alle andere instellingen kunnen blijven de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="89b37-179">All other settings can remain the default.</span></span>

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="89b37-181">Herhaal deze stappen aan de secundaire invoer-URL voor het maken van een afzonderlijke tabblad 'Uitvoer' voor het UDP/TS Streaming voor extra redundantie.</span><span class="sxs-lookup"><span data-stu-id="89b37-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="89b37-182">Klik op **maken** (als een nieuwe gebeurtenis is gemaakt) of **Update** (als een bestaande gebeurtenis bewerken) en ga verder met het starten van de encoder.</span><span class="sxs-lookup"><span data-stu-id="89b37-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89b37-183">Voordat u op **Start** op de webinterface elementair Live u **moet** ervoor te zorgen dat het kanaal gereed is.</span><span class="sxs-lookup"><span data-stu-id="89b37-183">Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="89b37-184">Zorg ervoor dat niet het kanaal in een status gereed zonder een gebeurtenis voor langer dan 15 minuten >.</span><span class="sxs-lookup"><span data-stu-id="89b37-184">Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="89b37-185">Nadat de stroom actief is geweest gedurende 30 seconden, gaat u terug naar het AMSE-hulpprogramma's en test afspelen.</span><span class="sxs-lookup"><span data-stu-id="89b37-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="89b37-186">Test afspelen</span><span class="sxs-lookup"><span data-stu-id="89b37-186">Test playback</span></span>

<span data-ttu-id="89b37-187">Navigeer naar het AMSE-hulpprogramma en klikt u met de rechtermuisknop op het kanaal moet worden getest.</span><span class="sxs-lookup"><span data-stu-id="89b37-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="89b37-188">In het menu Beweeg de muisaanwijzer over **afspelen van de Preview** en selecteer **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="89b37-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="89b37-189">Als de stroom wordt weergegeven in de speler, is klikt u vervolgens het coderingsprogramma juist geconfigureerd voor verbinding met AMS.</span><span class="sxs-lookup"><span data-stu-id="89b37-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="89b37-190">Als een fout wordt ontvangen, wordt het kanaal moet opnieuw worden ingesteld en instellingen voor codering aangepast.</span><span class="sxs-lookup"><span data-stu-id="89b37-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="89b37-191">Zie de [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="89b37-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="89b37-192">Een programma maken</span><span class="sxs-lookup"><span data-stu-id="89b37-192">Create a program</span></span>
1. <span data-ttu-id="89b37-193">Nadat het kanaal afspelen is bevestigd, maak een programma.</span><span class="sxs-lookup"><span data-stu-id="89b37-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="89b37-194">Onder de **Live** tabblad in het AMSE-hulpprogramma, klik met de rechtermuisknop in het gebied van het programma en selecteer **nieuw programma maken**.</span><span class="sxs-lookup"><span data-stu-id="89b37-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="89b37-196">Naam van het programma en wijzig indien nodig de **lengte van een archiefvenster** (die standaard 4 uur).</span><span class="sxs-lookup"><span data-stu-id="89b37-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="89b37-197">U kunt ook opgeven van een opslaglocatie of laat de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="89b37-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="89b37-198">Controleer de **Start het programma nu** vak.</span><span class="sxs-lookup"><span data-stu-id="89b37-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="89b37-199">Klik op **programma maken**.</span><span class="sxs-lookup"><span data-stu-id="89b37-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="89b37-200">Maken van het programma kost minder tijd dan het maken van kanaal.</span><span class="sxs-lookup"><span data-stu-id="89b37-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="89b37-201">Zodra het programma wordt uitgevoerd, bevestigt u afspelen door te klikken met de rechtermuisknop op het programma en te navigeren naar **afspelen van de programma's** en selecteren **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="89b37-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="89b37-202">Zodra bevestigd, klik met de rechtermuisknop het programma opnieuw en selecteer **Kopieer de URL van de uitvoer naar Klembord** (of het ophalen van deze informatie van de **programma gegevens en instellingen** optie in het menu).</span><span class="sxs-lookup"><span data-stu-id="89b37-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="89b37-203">De stroom is nu gereed om te worden ingesloten in een speler of gedistribueerd naar een doelgroep voor live weer te geven.</span><span class="sxs-lookup"><span data-stu-id="89b37-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="89b37-204">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="89b37-204">Troubleshooting</span></span>
<span data-ttu-id="89b37-205">Zie de [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="89b37-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="89b37-206">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="89b37-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="89b37-207">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="89b37-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
