---
title: Configureren van het coderingsprogramma FMLE voor het verzenden van een single-bitrate live stream | Microsoft Docs
description: Dit onderwerp leest hoe u configureert het coderingsprogramma Flash Media Live coderingsprogramma (FMLE) voor het verzenden van een single-bitrate stream AMS-kanalen die zijn ingeschakeld voor live codering.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="7d1c2-103">Het coderingsprogramma FMLE gebruiken voor het verzenden van een single-bitrate live stream</span><span class="sxs-lookup"><span data-stu-id="7d1c2-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d1c2-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="7d1c2-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="7d1c2-105">Live elemental</span><span class="sxs-lookup"><span data-stu-id="7d1c2-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="7d1c2-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="7d1c2-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="7d1c2-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="7d1c2-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="7d1c2-108">Dit onderwerp wordt beschreven hoe u configureert de [Media Flash Live coderingsprogramma](http://www.adobe.com/products/flash-media-encoder.html) (FMLE)-codering verzenden een single-bitrate stream naar AMS kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="7d1c2-109">Zie [Werken met kanalen waarmee Live Encoding kan worden uitgevoerd met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="7d1c2-110">Deze zelfstudie laat zien hoe Azure Media Services (AMS) beheren met Azure Media Services Explorer (AMSE)-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="7d1c2-111">Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="7d1c2-112">Als u op Mac- of Linux, gebruikt u de Azure portal maken [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="7d1c2-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="7d1c2-113">Houd er rekening mee dat deze zelfstudie wordt beschreven hoe AAC.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="7d1c2-114">FMLE ondersteunt niet echter AAC standaard.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="7d1c2-115">U moet aanschaffen van een invoegtoepassing voor AAC codering bijvoorbeeld van MainConcept: [AAC-invoegtoepassing](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="7d1c2-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d1c2-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7d1c2-116">Prerequisites</span></span>
* [<span data-ttu-id="7d1c2-117">Een Azure Media Services-account maken</span><span class="sxs-lookup"><span data-stu-id="7d1c2-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="7d1c2-118">Zorg dat er een Streaming-eindpunt is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="7d1c2-119">Zie voor meer informatie [Streaming-eindpunten beheren in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="7d1c2-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="7d1c2-120">Installeer de nieuwste versie van de [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="7d1c2-121">Het hulpprogramma voor starten en verbinding maken met uw AMS-account.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="7d1c2-122">Tips</span><span class="sxs-lookup"><span data-stu-id="7d1c2-122">Tips</span></span>
* <span data-ttu-id="7d1c2-123">Gebruik indien mogelijk een internetverbinding ' hardwired '.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="7d1c2-124">Een goede vuistregel bij het bepalen van de vereiste bandbreedte is voor de streaming bitsnelheden verdubbelen.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="7d1c2-125">Hoewel dit niet verplicht is, wordt deze verminderen de impact van opstoppingen in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="7d1c2-126">Wanneer met behulp van software gebaseerd coderingsprogramma's, sluit u alle onnodige programma's.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="7d1c2-127">Een kanaal maken</span><span class="sxs-lookup"><span data-stu-id="7d1c2-127">Create a channel</span></span>
1. <span data-ttu-id="7d1c2-128">Navigeer in het AMSE-hulpprogramma naar het **Live** tabblad en klik met de rechtermuisknop in het gebied van kanaal.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="7d1c2-129">Selecteer **kanaal maken...**</span><span class="sxs-lookup"><span data-stu-id="7d1c2-129">Select **Create channel…**</span></span> <span data-ttu-id="7d1c2-130">in het menu.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="7d1c2-132">Geef een kanaalnaam het beschrijvingsveld is optioneel.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="7d1c2-133">Selecteer onder instellingen voor kanaal **standaard** voor de optie Live Encoding met het invoer-Protocol die is ingesteld op **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="7d1c2-134">U kunt alle andere instellingen zoals is laten.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="7d1c2-135">Zorg ervoor dat de **nu starten van het nieuwe kanaal** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="7d1c2-136">Klik op **kanaal maken**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="7d1c2-138">Het kanaal kan zo lang starten 20 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="7d1c2-139">Terwijl het kanaal wordt gestart. u kunt [configureren van het coderingsprogramma](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="7d1c2-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d1c2-140">Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="7d1c2-141">Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="7d1c2-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="7d1c2-142"><a id=configure_fmle_rtmp></a>Het coderingsprogramma FMLE configureren</span><span class="sxs-lookup"><span data-stu-id="7d1c2-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="7d1c2-143">In deze zelfstudie worden de volgende uitvoerinstellingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="7d1c2-144">De rest van deze sectie beschrijft de configuratiestappen in meer detail.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="7d1c2-145">**Video**:</span><span class="sxs-lookup"><span data-stu-id="7d1c2-145">**Video**:</span></span>

* <span data-ttu-id="7d1c2-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="7d1c2-146">Codec: H.264</span></span>
* <span data-ttu-id="7d1c2-147">Profiel: Hoge (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="7d1c2-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="7d1c2-148">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="7d1c2-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="7d1c2-149">Sleutelframe: 2 seconden (60 seconden)</span><span class="sxs-lookup"><span data-stu-id="7d1c2-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="7d1c2-150">Frequentie frame: 30</span><span class="sxs-lookup"><span data-stu-id="7d1c2-150">Frame Rate: 30</span></span>

<span data-ttu-id="7d1c2-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="7d1c2-151">**Audio**:</span></span>

* <span data-ttu-id="7d1c2-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="7d1c2-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="7d1c2-153">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="7d1c2-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="7d1c2-154">Samplefrequentie: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="7d1c2-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="7d1c2-155">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="7d1c2-155">Configuration steps</span></span>
1. <span data-ttu-id="7d1c2-156">Navigeer naar het Flash Media Live coderingsprogramma van (FMLE) interface op de computer die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="7d1c2-157">De interface is één hoofdpagina van instellingen.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-157">The interface is one main page of settings.</span></span> <span data-ttu-id="7d1c2-158">Let op de volgende instellingen om te beginnen met het streamen FMLE met aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="7d1c2-159">Indeling: H.264 framesnelheid: 30,00</span><span class="sxs-lookup"><span data-stu-id="7d1c2-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="7d1c2-160">De grootte van de invoer: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="7d1c2-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="7d1c2-161">Bitsnelheid: 5000 Kbps (kan worden aangepast op basis van de beperkingen op het netwerk)</span><span class="sxs-lookup"><span data-stu-id="7d1c2-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="7d1c2-163">Bronnen met behulp van interlaced, neemt u de optie 'Zonder interliniëring' vinkje</span><span class="sxs-lookup"><span data-stu-id="7d1c2-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="7d1c2-164">Selecteer de moersleutelpictogram naast indeling, moeten deze extra instellingen:</span><span class="sxs-lookup"><span data-stu-id="7d1c2-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="7d1c2-165">Profiel: Main</span><span class="sxs-lookup"><span data-stu-id="7d1c2-165">Profile: Main</span></span>
   * <span data-ttu-id="7d1c2-166">Niveau: 4.0</span><span class="sxs-lookup"><span data-stu-id="7d1c2-166">Level: 4.0</span></span>
   * <span data-ttu-id="7d1c2-167">Keyframe frequentie: 2 seconden</span><span class="sxs-lookup"><span data-stu-id="7d1c2-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="7d1c2-169">Stel de volgende belangrijke audio-instelling:</span><span class="sxs-lookup"><span data-stu-id="7d1c2-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="7d1c2-170">Indeling: AAC</span><span class="sxs-lookup"><span data-stu-id="7d1c2-170">Format: AAC</span></span>
   * <span data-ttu-id="7d1c2-171">Samplefrequentie: 44100 Hz</span><span class="sxs-lookup"><span data-stu-id="7d1c2-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="7d1c2-172">Bitrate: 192 Kbps</span><span class="sxs-lookup"><span data-stu-id="7d1c2-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="7d1c2-174">Get het kanaal de invoer-URL om te kunnen toewijzen aan de FMLE **RTMP eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="7d1c2-175">Ga terug naar het AMSE-hulpprogramma, en controleren van de voltooiingsstatus van kanaal.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="7d1c2-176">Zodra de status is gewijzigd van **starten** naar **met**, krijgt u de invoer-URL.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="7d1c2-177">Wanneer het kanaal wordt uitgevoerd, klikt u met de rechtermuisknop op naam van het kanaal, navigeer naar aanwijzen via **invoer-URL kopiëren naar Klembord** en selecteer vervolgens **primaire invoer-URL**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="7d1c2-179">Plak deze informatie in de **FMS URL** veld van de sectie uitvoer, en wijst u de naam van een gegevensstroom.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="7d1c2-181">Herhaal deze stappen aan de secundaire invoer-URL voor extra redundantie.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="7d1c2-182">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d1c2-183">Voordat u op **Connect**, u **moet** ervoor te zorgen dat het kanaal gereed is.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="7d1c2-184">Zorg ervoor dat u niet het kanaal in een status ready heeft verlaten zonder een invoer bijdrage feed langer dan 15 minuten >.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="7d1c2-185">Test afspelen</span><span class="sxs-lookup"><span data-stu-id="7d1c2-185">Test playback</span></span>

<span data-ttu-id="7d1c2-186">Navigeer naar het AMSE-hulpprogramma en klikt u met de rechtermuisknop op het kanaal moet worden getest.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="7d1c2-187">In het menu Beweeg de muisaanwijzer over **afspelen van de Preview** en selecteer **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="7d1c2-188">Als de stroom wordt weergegeven in de speler, is klikt u vervolgens het coderingsprogramma juist geconfigureerd voor verbinding met AMS.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="7d1c2-189">Als een fout wordt ontvangen, wordt het kanaal moet opnieuw worden ingesteld en instellingen voor codering aangepast.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="7d1c2-190">Zie de [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="7d1c2-191">Een programma maken</span><span class="sxs-lookup"><span data-stu-id="7d1c2-191">Create a program</span></span>
1. <span data-ttu-id="7d1c2-192">Nadat het kanaal afspelen is bevestigd, maak een programma.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="7d1c2-193">Onder de **Live** tabblad in het AMSE-hulpprogramma, klik met de rechtermuisknop in het gebied van het programma en selecteer **nieuw programma maken**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="7d1c2-195">Naam van het programma en wijzig indien nodig de **lengte van een archiefvenster** (die standaard 4 uur).</span><span class="sxs-lookup"><span data-stu-id="7d1c2-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="7d1c2-196">U kunt ook opgeven van een opslaglocatie of laat de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="7d1c2-197">Controleer de **Start het programma nu** vak.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="7d1c2-198">Klik op **programma maken**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="7d1c2-199">Maken van het programma kost minder tijd dan het maken van kanaal.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="7d1c2-200">Zodra het programma wordt uitgevoerd, bevestigt u afspelen door te klikken met de rechtermuisknop op het programma en te navigeren naar **afspelen van de programma's** en selecteren **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="7d1c2-201">Zodra bevestigd, klik met de rechtermuisknop het programma opnieuw en selecteer **Kopieer de URL van de uitvoer naar Klembord** (of het ophalen van deze informatie van de **programma gegevens en instellingen** optie in het menu).</span><span class="sxs-lookup"><span data-stu-id="7d1c2-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="7d1c2-202">De stroom is nu gereed om te worden ingesloten in een speler of gedistribueerd naar een doelgroep voor live weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="7d1c2-203">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7d1c2-203">Troubleshooting</span></span>
<span data-ttu-id="7d1c2-204">Zie de [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="7d1c2-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7d1c2-205">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="7d1c2-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7d1c2-206">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="7d1c2-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
