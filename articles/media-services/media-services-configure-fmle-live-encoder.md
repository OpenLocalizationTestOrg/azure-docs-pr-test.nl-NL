---
title: aaaConfigure hello FMLE encoder toosend een single-bitrate live stream | Microsoft Docs
description: Dit onderwerp leest hoe tooconfigure Hallo Flash Media Live coderingsprogramma (FMLE) encoder toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.
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
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="949c2-103">Hallo FMLE encoder toosend een single-bitrate live stream gebruiken</span><span class="sxs-lookup"><span data-stu-id="949c2-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="949c2-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="949c2-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="949c2-105">Live elemental</span><span class="sxs-lookup"><span data-stu-id="949c2-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="949c2-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="949c2-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="949c2-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="949c2-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="949c2-108">Dit onderwerp wordt beschreven hoe tooconfigure hello [Media Flash Live coderingsprogramma](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="949c2-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="949c2-109">Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="949c2-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="949c2-110">Deze zelfstudie laat zien hoe toomanage Azure Media Services (AMS) met Azure Media Services Explorer (AMSE)-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="949c2-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="949c2-111">Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC.</span><span class="sxs-lookup"><span data-stu-id="949c2-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="949c2-112">Als u op Mac- of Linux, gebruikt u Azure portal toocreate hello [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="949c2-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="949c2-113">Houd er rekening mee dat deze zelfstudie wordt beschreven hoe AAC.</span><span class="sxs-lookup"><span data-stu-id="949c2-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="949c2-114">FMLE ondersteunt niet echter AAC standaard.</span><span class="sxs-lookup"><span data-stu-id="949c2-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="949c2-115">U moet een invoegtoepassing voor het coderen van AAC toopurchase bijvoorbeeld van MainConcept: [AAC-invoegtoepassing](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="949c2-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="949c2-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="949c2-116">Prerequisites</span></span>
* [<span data-ttu-id="949c2-117">Een Azure Media Services-account maken</span><span class="sxs-lookup"><span data-stu-id="949c2-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="949c2-118">Zorg dat er een Streaming-eindpunt is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="949c2-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="949c2-119">Zie voor meer informatie [Streaming-eindpunten beheren in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="949c2-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="949c2-120">Installeer de meest recente versie Hallo Hallo [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="949c2-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="949c2-121">Hallo hulpprogramma start en tooyour AMS-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="949c2-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="949c2-122">Tips</span><span class="sxs-lookup"><span data-stu-id="949c2-122">Tips</span></span>
* <span data-ttu-id="949c2-123">Gebruik indien mogelijk een internetverbinding ' hardwired '.</span><span class="sxs-lookup"><span data-stu-id="949c2-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="949c2-124">Een goede vuistregel bij het bepalen van de vereiste bandbreedte is toodouble Hallo bitsnelheden streaming.</span><span class="sxs-lookup"><span data-stu-id="949c2-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="949c2-125">Hoewel dit niet verplicht is, wordt deze verminderen Hallo impact van opstoppingen in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="949c2-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="949c2-126">Wanneer met behulp van software gebaseerd coderingsprogramma's, sluit u alle onnodige programma's.</span><span class="sxs-lookup"><span data-stu-id="949c2-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="949c2-127">Een kanaal maken</span><span class="sxs-lookup"><span data-stu-id="949c2-127">Create a channel</span></span>
1. <span data-ttu-id="949c2-128">Navigeer in Hallo AMSE-hulpprogramma, toohello **Live** tabblad en klik met de rechtermuisknop in Hallo kanaal gebied.</span><span class="sxs-lookup"><span data-stu-id="949c2-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="949c2-129">Selecteer **kanaal maken...**</span><span class="sxs-lookup"><span data-stu-id="949c2-129">Select **Create channel…**</span></span> <span data-ttu-id="949c2-130">Hallo upmenu.</span><span class="sxs-lookup"><span data-stu-id="949c2-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="949c2-132">Geef een kanaalnaam Hallo beschrijvingsveld is optioneel.</span><span class="sxs-lookup"><span data-stu-id="949c2-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="949c2-133">Selecteer onder instellingen voor kanaal **standaard** voor Hallo optie Live Encoding, hello invoer Protocol ingesteld te**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="949c2-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="949c2-134">U kunt alle andere instellingen zoals is laten.</span><span class="sxs-lookup"><span data-stu-id="949c2-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="949c2-135">Zorg ervoor dat Hallo **Start Hallo nieuw kanaal nu** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="949c2-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="949c2-136">Klik op **kanaal maken**.</span><span class="sxs-lookup"><span data-stu-id="949c2-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="949c2-138">Hallo kanaal kan 20 minuten toostart zo lang duren.</span><span class="sxs-lookup"><span data-stu-id="949c2-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="949c2-139">Tijdens het Hallo-kanaal wordt gestart. u kunt [Hallo-codering configureren](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="949c2-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="949c2-140">Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed.</span><span class="sxs-lookup"><span data-stu-id="949c2-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="949c2-141">Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="949c2-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="949c2-142"><a id=configure_fmle_rtmp></a>Hallo FMLE codering configureren</span><span class="sxs-lookup"><span data-stu-id="949c2-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="949c2-143">In deze zelfstudie Hallo volgende uitvoerinstellingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="949c2-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="949c2-144">Hallo rest van deze sectie beschrijft de configuratiestappen in meer detail.</span><span class="sxs-lookup"><span data-stu-id="949c2-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="949c2-145">**Video**:</span><span class="sxs-lookup"><span data-stu-id="949c2-145">**Video**:</span></span>

* <span data-ttu-id="949c2-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="949c2-146">Codec: H.264</span></span>
* <span data-ttu-id="949c2-147">Profiel: Hoge (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="949c2-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="949c2-148">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="949c2-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="949c2-149">Sleutelframe: 2 seconden (60 seconden)</span><span class="sxs-lookup"><span data-stu-id="949c2-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="949c2-150">Frequentie frame: 30</span><span class="sxs-lookup"><span data-stu-id="949c2-150">Frame Rate: 30</span></span>

<span data-ttu-id="949c2-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="949c2-151">**Audio**:</span></span>

* <span data-ttu-id="949c2-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="949c2-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="949c2-153">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="949c2-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="949c2-154">Samplefrequentie: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="949c2-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="949c2-155">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="949c2-155">Configuration steps</span></span>
1. <span data-ttu-id="949c2-156">Navigeer toohello die Flash Media Live coderingsprogramma van (FMLE) interface op Hallo machine die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="949c2-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="949c2-157">Hallo-interface is één hoofdpagina van instellingen.</span><span class="sxs-lookup"><span data-stu-id="949c2-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="949c2-158">Let op Hallo volgende aanbevolen instellingen tooget gestart met behulp van FMLE streaming.</span><span class="sxs-lookup"><span data-stu-id="949c2-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="949c2-159">Indeling: H.264 framesnelheid: 30,00</span><span class="sxs-lookup"><span data-stu-id="949c2-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="949c2-160">De grootte van de invoer: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="949c2-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="949c2-161">Bitsnelheid: 5000 Kbps (kan worden aangepast op basis van de beperkingen op het netwerk)</span><span class="sxs-lookup"><span data-stu-id="949c2-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="949c2-163">Wanneer met behulp van interlaced gegevensbronnen, neem vinkje Hallo 'Zonder interliniëring'-optie</span><span class="sxs-lookup"><span data-stu-id="949c2-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="949c2-164">Selecteer Hallo Moersleutel pictogram volgende tooFormat, deze extra instellingen worden:</span><span class="sxs-lookup"><span data-stu-id="949c2-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="949c2-165">Profiel: Main</span><span class="sxs-lookup"><span data-stu-id="949c2-165">Profile: Main</span></span>
   * <span data-ttu-id="949c2-166">Niveau: 4.0</span><span class="sxs-lookup"><span data-stu-id="949c2-166">Level: 4.0</span></span>
   * <span data-ttu-id="949c2-167">Keyframe frequentie: 2 seconden</span><span class="sxs-lookup"><span data-stu-id="949c2-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="949c2-169">Stel Hallo belangrijk audio-instellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="949c2-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="949c2-170">Indeling: AAC</span><span class="sxs-lookup"><span data-stu-id="949c2-170">Format: AAC</span></span>
   * <span data-ttu-id="949c2-171">Samplefrequentie: 44100 Hz</span><span class="sxs-lookup"><span data-stu-id="949c2-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="949c2-172">Bitrate: 192 Kbps</span><span class="sxs-lookup"><span data-stu-id="949c2-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="949c2-174">Hallo-kanaal invoer-URL ophalen in volgorde tooassign het toohello FMLE van **RTMP eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="949c2-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="949c2-175">Navigeer terug toohello AMSE-hulpprogramma, en controleren op Hallo kanaal voltooiingsstatus weer.</span><span class="sxs-lookup"><span data-stu-id="949c2-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="949c2-176">Zodra het Hallo-status is gewijzigd van **starten** te**met**, krijgt u Hallo invoer-URL.</span><span class="sxs-lookup"><span data-stu-id="949c2-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="949c2-177">Wanneer Hallo kanaal wordt uitgevoerd, klik met de rechtermuisknop op Hallo kanaalnaam, omlaag toohover gaan via **invoer-URL kopiëren tooclipboard** en selecteer vervolgens **primaire invoer-URL**.</span><span class="sxs-lookup"><span data-stu-id="949c2-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="949c2-179">Deze informatie plakken in Hallo **FMS URL** veld sectie Hallo-uitvoer, en wijst u de naam van een gegevensstroom.</span><span class="sxs-lookup"><span data-stu-id="949c2-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="949c2-181">Herhaal deze stappen Hello secundaire invoer-URL voor extra redundantie.</span><span class="sxs-lookup"><span data-stu-id="949c2-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="949c2-182">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="949c2-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="949c2-183">Voordat u op **Connect**, u **moet** ervoor te zorgen dat het Hallo-kanaal klaar is.</span><span class="sxs-lookup"><span data-stu-id="949c2-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="949c2-184">Zorg er ook geen tooleave Hallo kanaal in een status gereed zonder een bijdrage invoer feed langer dan 15 minuten >.</span><span class="sxs-lookup"><span data-stu-id="949c2-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="949c2-185">Test afspelen</span><span class="sxs-lookup"><span data-stu-id="949c2-185">Test playback</span></span>

<span data-ttu-id="949c2-186">Navigeer toohello AMSE-hulpprogramma en Hallo kanaal toobe getest met de rechtermuisknop op.</span><span class="sxs-lookup"><span data-stu-id="949c2-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="949c2-187">Hallo menu Beweeg de muisaanwijzer over **afspelen Hallo Preview** en selecteer **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="949c2-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="949c2-188">Als Hallo stroom wordt weergegeven in Hallo-speler, heeft Hallo encoder correct geconfigureerde tooconnect tooAMS zijn.</span><span class="sxs-lookup"><span data-stu-id="949c2-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="949c2-189">Als een fout wordt ontvangen, moet Hallo kanaal toobe opnieuw instellen en coderingsprogramma instellingen aangepast.</span><span class="sxs-lookup"><span data-stu-id="949c2-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="949c2-190">Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="949c2-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="949c2-191">Een programma maken</span><span class="sxs-lookup"><span data-stu-id="949c2-191">Create a program</span></span>
1. <span data-ttu-id="949c2-192">Nadat het kanaal afspelen is bevestigd, maak een programma.</span><span class="sxs-lookup"><span data-stu-id="949c2-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="949c2-193">Onder Hallo **Live** tabblad Hallo AMSE-hulpprogramma, klik met de rechtermuisknop in Hallo programma gebied en selecteer **nieuw programma maken**.</span><span class="sxs-lookup"><span data-stu-id="949c2-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="949c2-195">Hallo-programma een naam en wijzig indien nodig, Hallo **lengte van een archiefvenster** (welke standaardwaarden too4 uur).</span><span class="sxs-lookup"><span data-stu-id="949c2-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="949c2-196">U kunt ook opgeven van een opslaglocatie of laat als Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="949c2-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="949c2-197">Controleer de Hallo **Start Hallo programma nu** vak.</span><span class="sxs-lookup"><span data-stu-id="949c2-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="949c2-198">Klik op **programma maken**.</span><span class="sxs-lookup"><span data-stu-id="949c2-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="949c2-199">Maken van het programma kost minder tijd dan het maken van kanaal.</span><span class="sxs-lookup"><span data-stu-id="949c2-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="949c2-200">Zodra het Hallo-programma wordt uitgevoerd, bevestigt u afspelen met de rechtermuisknop te klikken op het Hallo-programma en te navigeren**afspelen Hallo-programma's** en selecteren **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="949c2-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="949c2-201">Zodra bevestigd, klik met de rechtermuisknop Hallo programma opnieuw en selecteer **kopiëren Hallo uitvoer URL tooClipboard** (of deze informatie ophalen van Hallo **programma gegevens en instellingen** optie uit Hallo menu).</span><span class="sxs-lookup"><span data-stu-id="949c2-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="949c2-202">Hallo-stroom is nu gereed toobe ingesloten in een speler of gedistribueerde tooan doelgroep voor live weergeven.</span><span class="sxs-lookup"><span data-stu-id="949c2-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="949c2-203">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="949c2-203">Troubleshooting</span></span>
<span data-ttu-id="949c2-204">Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="949c2-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="949c2-205">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="949c2-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="949c2-206">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="949c2-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
