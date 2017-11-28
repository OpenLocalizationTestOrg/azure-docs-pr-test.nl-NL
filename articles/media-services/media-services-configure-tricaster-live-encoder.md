---
title: aaaConfigure Hallo NewTek TriCaster encoder toosend een single-bitrate live stream | Microsoft Docs
description: Dit onderwerp leest hoe tooconfigure hello Tricaster live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="2bd27-103">Hallo NewTek TriCaster encoder toosend een single-bitrate live stream gebruiken</span><span class="sxs-lookup"><span data-stu-id="2bd27-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2bd27-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="2bd27-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="2bd27-105">Live elemental</span><span class="sxs-lookup"><span data-stu-id="2bd27-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="2bd27-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="2bd27-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="2bd27-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="2bd27-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="2bd27-108">Dit onderwerp wordt beschreven hoe tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="2bd27-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="2bd27-109">Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="2bd27-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="2bd27-110">Deze zelfstudie laat zien hoe toomanage Azure Media Services (AMS) met Azure Media Services Explorer (AMSE)-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="2bd27-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="2bd27-111">Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC.</span><span class="sxs-lookup"><span data-stu-id="2bd27-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="2bd27-112">Als u op Mac- of Linux, gebruikt u Azure portal toocreate hello [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="2bd27-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2bd27-113">Wanneer met Tricaster voor het verzenden van een bijdrage feed tooAMS kanalen die zijn ingeschakeld voor live codering, kunnen er video en audio haperingen in uw live gebeurtenis als u bepaalde functies van Tricaster, zoals snelle knippen tussen feeds of overschakelen van Smartphones gebruiken .</span><span class="sxs-lookup"><span data-stu-id="2bd27-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="2bd27-114">Hallo AMS-team werkt op deze problemen tot die tijd is hersteld, is niet raadzaam toouse deze functies.</span><span class="sxs-lookup"><span data-stu-id="2bd27-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="2bd27-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2bd27-115">Prerequisites</span></span>
* [<span data-ttu-id="2bd27-116">Een Azure Media Services-account maken</span><span class="sxs-lookup"><span data-stu-id="2bd27-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="2bd27-117">Zorg dat er een Streaming-eindpunt is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2bd27-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="2bd27-118">Zie voor meer informatie [Streaming-eindpunten beheren in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="2bd27-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="2bd27-119">Installeer de meest recente versie Hallo Hallo [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="2bd27-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="2bd27-120">Hallo hulpprogramma start en tooyour AMS-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="2bd27-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="2bd27-121">Tips</span><span class="sxs-lookup"><span data-stu-id="2bd27-121">Tips</span></span>
* <span data-ttu-id="2bd27-122">Gebruik indien mogelijk een internetverbinding ' hardwired '.</span><span class="sxs-lookup"><span data-stu-id="2bd27-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="2bd27-123">Een goede vuistregel bij het bepalen van de vereiste bandbreedte is toodouble Hallo bitsnelheden streaming.</span><span class="sxs-lookup"><span data-stu-id="2bd27-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="2bd27-124">Hoewel dit niet verplicht is, wordt deze verminderen Hallo impact van opstoppingen in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="2bd27-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="2bd27-125">Wanneer met behulp van software gebaseerd coderingsprogramma's, sluit u alle onnodige programma's.</span><span class="sxs-lookup"><span data-stu-id="2bd27-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="2bd27-126">Een kanaal maken</span><span class="sxs-lookup"><span data-stu-id="2bd27-126">Create a channel</span></span>
1. <span data-ttu-id="2bd27-127">Navigeer in Hallo AMSE-hulpprogramma, toohello **Live** tabblad en klik met de rechtermuisknop in Hallo kanaal gebied.</span><span class="sxs-lookup"><span data-stu-id="2bd27-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="2bd27-128">Selecteer **kanaal maken...**</span><span class="sxs-lookup"><span data-stu-id="2bd27-128">Select **Create channel…**</span></span> <span data-ttu-id="2bd27-129">Hallo upmenu.</span><span class="sxs-lookup"><span data-stu-id="2bd27-129">from hello menu.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="2bd27-131">Geef een kanaalnaam Hallo beschrijvingsveld is optioneel.</span><span class="sxs-lookup"><span data-stu-id="2bd27-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="2bd27-132">Selecteer onder instellingen voor kanaal **standaard** voor Hallo optie Live Encoding, hello invoer Protocol ingesteld te**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="2bd27-133">U kunt alle andere instellingen zoals is laten.</span><span class="sxs-lookup"><span data-stu-id="2bd27-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="2bd27-134">Zorg ervoor dat Hallo **Start Hallo nieuw kanaal nu** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2bd27-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="2bd27-135">Klik op **kanaal maken**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-135">Click **Create Channel**.</span></span>

   ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="2bd27-137">Hallo kanaal kan 20 minuten toostart zo lang duren.</span><span class="sxs-lookup"><span data-stu-id="2bd27-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="2bd27-138">Tijdens het Hallo-kanaal wordt gestart. u kunt [Hallo-codering configureren](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="2bd27-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bd27-139">Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed.</span><span class="sxs-lookup"><span data-stu-id="2bd27-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="2bd27-140">Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="2bd27-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="2bd27-141"><a id=configure_tricaster_rtmp></a>Hallo NewTek TriCaster-codering configureren</span><span class="sxs-lookup"><span data-stu-id="2bd27-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="2bd27-142">In deze zelfstudie Hallo volgende uitvoerinstellingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2bd27-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="2bd27-143">Hallo rest van deze sectie beschrijft de configuratiestappen in meer detail.</span><span class="sxs-lookup"><span data-stu-id="2bd27-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="2bd27-144">**Video**:</span><span class="sxs-lookup"><span data-stu-id="2bd27-144">**Video**:</span></span>

* <span data-ttu-id="2bd27-145">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="2bd27-145">Codec: H.264</span></span>
* <span data-ttu-id="2bd27-146">Profiel: Hoge (niveau 4.0)</span><span class="sxs-lookup"><span data-stu-id="2bd27-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="2bd27-147">Bitrate: 5000 kbps</span><span class="sxs-lookup"><span data-stu-id="2bd27-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="2bd27-148">Sleutelframe: 2 seconden (60 seconden)</span><span class="sxs-lookup"><span data-stu-id="2bd27-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="2bd27-149">Frequentie frame: 30</span><span class="sxs-lookup"><span data-stu-id="2bd27-149">Frame Rate: 30</span></span>

<span data-ttu-id="2bd27-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="2bd27-150">**Audio**:</span></span>

* <span data-ttu-id="2bd27-151">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="2bd27-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="2bd27-152">Bitrate: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="2bd27-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="2bd27-153">Samplefrequentie: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="2bd27-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="2bd27-154">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="2bd27-154">Configuration steps</span></span>
1. <span data-ttu-id="2bd27-155">Maak een nieuwe **NewTek TriCaster** project, afhankelijk van welke video-invoerbron wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2bd27-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="2bd27-156">Eenmaal in dat project Hallo zoeken **stroom** en klik op Hallo tandwielpictogram pictogram volgende tooit tooaccess Hallo configuratie menu stream.</span><span class="sxs-lookup"><span data-stu-id="2bd27-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="2bd27-158">Zodra het Hallo-menu heeft geopend, klikt u op **nieuw** onder Hallo verbinding kop.</span><span class="sxs-lookup"><span data-stu-id="2bd27-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="2bd27-159">Als u wordt gevraagd voor het verbindingstype hello, selecteer **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="2bd27-161">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-161">Click **OK**.</span></span>
5. <span data-ttu-id="2bd27-162">Een profiel FMLE kan nu worden geïmporteerd door te klikken op Hallo vervolgkeuzepijl onder **Streaming profiel** en te navigeren**Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="2bd27-164">Navigeer toowhere Hallo geconfigureerd FMLE profiel is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2bd27-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="2bd27-165">Selecteer deze en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="2bd27-166">Zodra het Hallo-profiel is geüpload, gaat u verder toohello volgende stap.</span><span class="sxs-lookup"><span data-stu-id="2bd27-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="2bd27-167">Hallo-kanaal invoer-URL ophalen in volgorde tooassign het toohello Tricaster **RTMP eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="2bd27-168">Navigeer terug toohello AMSE-hulpprogramma, en controleren op Hallo kanaal voltooiingsstatus weer.</span><span class="sxs-lookup"><span data-stu-id="2bd27-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="2bd27-169">Zodra het Hallo-status is gewijzigd van **starten** te**met**, krijgt u Hallo invoer-URL.</span><span class="sxs-lookup"><span data-stu-id="2bd27-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="2bd27-170">Wanneer Hallo kanaal wordt uitgevoerd, klik met de rechtermuisknop op Hallo kanaalnaam, omlaag toohover gaan via **invoer-URL kopiëren tooclipboard** en selecteer vervolgens **primaire invoer-URL**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="2bd27-172">Deze informatie plakken in Hallo **locatie** veld onder **Flash Server** binnen Hallo Tricaster-project.</span><span class="sxs-lookup"><span data-stu-id="2bd27-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="2bd27-173">Ook de Stroomnaam van een in Hallo toewijzen **stroom-ID** veld.</span><span class="sxs-lookup"><span data-stu-id="2bd27-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="2bd27-174">Als stream informatie is toegevoegd toohello FMLE profiel, het kan ook worden geïmporteerd toothis sectie door te klikken op **importinstellingen**, toohello opgeslagen FMLE profiel navigeren en op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="2bd27-175">Hallo relevante Flash Server velden moeten gevuld met Hallo gegevens van FMLE.</span><span class="sxs-lookup"><span data-stu-id="2bd27-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="2bd27-177">Wanneer u klaar bent, klikt u op **OK** Hallo onder welkomstscherm aan.</span><span class="sxs-lookup"><span data-stu-id="2bd27-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="2bd27-178">Wanneer de video en audio-ingangen in Hallo Tricaster klaar bent, moet u beginnen tooAMS streaming door te klikken op Hallo **stroom** knop.</span><span class="sxs-lookup"><span data-stu-id="2bd27-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="2bd27-180">Voordat u op **stroom**, u **moet** ervoor te zorgen dat het Hallo-kanaal klaar is.</span><span class="sxs-lookup"><span data-stu-id="2bd27-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="2bd27-181">Zorg er ook geen tooleave Hallo kanaal in een status gereed zonder een bijdrage invoer feed langer dan 15 minuten >.</span><span class="sxs-lookup"><span data-stu-id="2bd27-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="2bd27-182">Test afspelen</span><span class="sxs-lookup"><span data-stu-id="2bd27-182">Test playback</span></span>
<span data-ttu-id="2bd27-183">Navigeer toohello AMSE-hulpprogramma en Hallo kanaal toobe getest met de rechtermuisknop op.</span><span class="sxs-lookup"><span data-stu-id="2bd27-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="2bd27-184">Hallo menu Beweeg de muisaanwijzer over **afspelen Hallo Preview** en selecteer **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="2bd27-185">Als Hallo stroom wordt weergegeven in Hallo-speler, heeft Hallo encoder correct geconfigureerde tooconnect tooAMS zijn.</span><span class="sxs-lookup"><span data-stu-id="2bd27-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="2bd27-186">Als een fout wordt ontvangen, moet Hallo kanaal toobe opnieuw instellen en coderingsprogramma instellingen aangepast.</span><span class="sxs-lookup"><span data-stu-id="2bd27-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="2bd27-187">Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="2bd27-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="2bd27-188">Een programma maken</span><span class="sxs-lookup"><span data-stu-id="2bd27-188">Create a program</span></span>
1. <span data-ttu-id="2bd27-189">Nadat het kanaal afspelen is bevestigd, maak een programma.</span><span class="sxs-lookup"><span data-stu-id="2bd27-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="2bd27-190">Onder Hallo **Live** tabblad Hallo AMSE-hulpprogramma, klik met de rechtermuisknop in Hallo programma gebied en selecteer **nieuw programma maken**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="2bd27-192">Hallo-programma een naam en wijzig indien nodig, Hallo **lengte van een archiefvenster** (welke standaardwaarden too4 uur).</span><span class="sxs-lookup"><span data-stu-id="2bd27-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="2bd27-193">U kunt ook opgeven van een opslaglocatie of laat als Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="2bd27-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="2bd27-194">Controleer de Hallo **Start Hallo programma nu** vak.</span><span class="sxs-lookup"><span data-stu-id="2bd27-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="2bd27-195">Klik op **programma maken**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="2bd27-196">Maken van het programma kost minder tijd dan het maken van kanaal.</span><span class="sxs-lookup"><span data-stu-id="2bd27-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="2bd27-197">Zodra het Hallo-programma wordt uitgevoerd, bevestigt u afspelen met de rechtermuisknop te klikken op het Hallo-programma en te navigeren**afspelen Hallo-programma's** en selecteren **met Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="2bd27-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="2bd27-198">Zodra bevestigd, klik met de rechtermuisknop Hallo programma opnieuw en selecteer **kopiëren Hallo uitvoer URL tooClipboard** (of deze informatie ophalen van Hallo **programma gegevens en instellingen** optie uit Hallo menu).</span><span class="sxs-lookup"><span data-stu-id="2bd27-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="2bd27-199">Hallo-stroom is nu gereed toobe ingesloten in een speler of gedistribueerde tooan doelgroep voor live weergeven.</span><span class="sxs-lookup"><span data-stu-id="2bd27-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="2bd27-200">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="2bd27-200">Troubleshooting</span></span>
<span data-ttu-id="2bd27-201">Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.</span><span class="sxs-lookup"><span data-stu-id="2bd27-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="2bd27-202">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="2bd27-202">Next step</span></span>
<span data-ttu-id="2bd27-203">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="2bd27-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2bd27-204">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="2bd27-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
