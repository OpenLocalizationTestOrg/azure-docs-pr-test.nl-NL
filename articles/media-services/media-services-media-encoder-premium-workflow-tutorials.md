---
title: aaaAvanced Media Encoder Premium werkstroom zelfstudies
description: Dit document bevat scenario's die laten zien hoe tooperform geavanceerde taken met Media Encoder Premium Workflow en ook hoe toocreate complexe werkstromen met Workflow Designer.
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="7a832-103">Geavanceerde werkstroom voor Media Encoder Premium zelfstudies</span><span class="sxs-lookup"><span data-stu-id="7a832-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="7a832-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7a832-104">Overview</span></span>
<span data-ttu-id="7a832-105">Dit document bevat scenario's die laten zien hoe toocustomize werkstromen met **Workflow Designer**.</span><span class="sxs-lookup"><span data-stu-id="7a832-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="7a832-106">U vindt Hallo werkelijke Werkstroombestanden [hier](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="7a832-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="7a832-107">INHOUDSOPGAVE</span><span class="sxs-lookup"><span data-stu-id="7a832-107">TOC</span></span>
<span data-ttu-id="7a832-108">Hallo volgende onderwerpen komen aan bod:</span><span class="sxs-lookup"><span data-stu-id="7a832-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="7a832-109">MXF naar een single-bitrate MP4-codering</span><span class="sxs-lookup"><span data-stu-id="7a832-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="7a832-110">Een nieuwe werkstroom starten</span><span class="sxs-lookup"><span data-stu-id="7a832-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="7a832-111">Met behulp van Hallo Media bestandsinvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="7a832-112">Streaming media te bekijken</span><span class="sxs-lookup"><span data-stu-id="7a832-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="7a832-113">Toevoegen van een video encoder voor. MP4-bestand genereren</span><span class="sxs-lookup"><span data-stu-id="7a832-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="7a832-114">Codering Hallo audiostroom</span><span class="sxs-lookup"><span data-stu-id="7a832-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="7a832-115">Audio en Video-streams multiplex in een MP4-container</span><span class="sxs-lookup"><span data-stu-id="7a832-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="7a832-116">Hallo MP4-bestand schrijven</span><span class="sxs-lookup"><span data-stu-id="7a832-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="7a832-117">Maken van een Media Services-activum van Hallo-bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="7a832-118">Test Hallo lokaal werkstroom is voltooid</span><span class="sxs-lookup"><span data-stu-id="7a832-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="7a832-119">MXF in multibitrate MP4s - codering dynamische pakketten ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="7a832-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="7a832-120">Toevoegen van een of meer extra MP4-uitvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="7a832-121">Configureren Hallo uitvoer bestandsnamen</span><span class="sxs-lookup"><span data-stu-id="7a832-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="7a832-122">Toevoegen van een afzonderlijke-nummer</span><span class="sxs-lookup"><span data-stu-id="7a832-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="7a832-123">Hallo toe te voegen. ISM SMIL-bestand</span><span class="sxs-lookup"><span data-stu-id="7a832-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="7a832-124">MXF in multibitrate MP4 - verbeterde blauwdruk codering</span><span class="sxs-lookup"><span data-stu-id="7a832-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="7a832-125">Werkstroom overzicht tooenhance</span><span class="sxs-lookup"><span data-stu-id="7a832-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="7a832-126">Naamgevingsregels voor bestanden</span><span class="sxs-lookup"><span data-stu-id="7a832-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="7a832-127">Eigenschappen van onderdeel op Hallo werkstroom hoofdmap publiceren</span><span class="sxs-lookup"><span data-stu-id="7a832-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="7a832-128">Uitvoerbestand namen zijn afhankelijk van de gepubliceerde eigenschapswaarden hebt gegenereerd</span><span class="sxs-lookup"><span data-stu-id="7a832-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="7a832-129">Miniaturen toomultibitrate MP4 uitvoer toevoegen</span><span class="sxs-lookup"><span data-stu-id="7a832-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="7a832-130">Werkstroom overzicht tooadd miniatuurweergaven voor</span><span class="sxs-lookup"><span data-stu-id="7a832-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="7a832-131">Toe te voegen JPG-codering</span><span class="sxs-lookup"><span data-stu-id="7a832-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="7a832-132">Omgaan met de conversie van de werkruimte</span><span class="sxs-lookup"><span data-stu-id="7a832-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="7a832-133">Schrijven Hallo miniaturen</span><span class="sxs-lookup"><span data-stu-id="7a832-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="7a832-134">Fouten opsporen in een werkstroom</span><span class="sxs-lookup"><span data-stu-id="7a832-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="7a832-135">Werkstroom is voltooid</span><span class="sxs-lookup"><span data-stu-id="7a832-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="7a832-136">Op basis van tijd worden ingekort door multibitrate MP4-uitvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="7a832-137">Werkstroom overzicht toostart bijsnijden aan toe te voegen</span><span class="sxs-lookup"><span data-stu-id="7a832-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="7a832-138">Hallo stroom Trimmer gebruiken</span><span class="sxs-lookup"><span data-stu-id="7a832-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="7a832-139">Werkstroom is voltooid</span><span class="sxs-lookup"><span data-stu-id="7a832-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="7a832-140">Introducing hello onderdeel in een script vastgelegd</span><span class="sxs-lookup"><span data-stu-id="7a832-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="7a832-141">Uitvoeren van scripts in een werkstroom: Hallo wereld</span><span class="sxs-lookup"><span data-stu-id="7a832-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="7a832-142">Op basis van het frame worden ingekort door multibitrate MP4-uitvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="7a832-143">Blauwdruk overzicht toostart bijsnijden aan toe te voegen</span><span class="sxs-lookup"><span data-stu-id="7a832-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="7a832-144">Met behulp van Hallo Clip lijst XML</span><span class="sxs-lookup"><span data-stu-id="7a832-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="7a832-145">Hallo clip lijst van een onderdeel in een script vastgelegd wijzigen</span><span class="sxs-lookup"><span data-stu-id="7a832-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="7a832-146">De eigenschap van een ClippingEnabled gemak toe te voegen</span><span class="sxs-lookup"><span data-stu-id="7a832-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="7a832-147"><a id="MXF_to_MP4"></a>MXF naar een single-bitrate MP4-codering</span><span class="sxs-lookup"><span data-stu-id="7a832-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="7a832-148">In dit scenario maakt u een single bitrate. MP4-bestand met AAC HE gecodeerde audio van een. Het invoerbestand MXF.</span><span class="sxs-lookup"><span data-stu-id="7a832-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="7a832-149"><a id="MXF_to_MP4_start_new"></a>Een nieuwe werkstroom starten</span><span class="sxs-lookup"><span data-stu-id="7a832-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="7a832-150">Workflow Designer openen en selecteer 'File '-' nieuwe werkruimte'-' transcoderen blauwdruk'</span><span class="sxs-lookup"><span data-stu-id="7a832-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="7a832-151">de nieuwe werkstroom Hello wordt 3 elementen weergeven:</span><span class="sxs-lookup"><span data-stu-id="7a832-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="7a832-152">Primaire bronbestand</span><span class="sxs-lookup"><span data-stu-id="7a832-152">Primary Source File</span></span>
* <span data-ttu-id="7a832-153">Clip XML-lijst</span><span class="sxs-lookup"><span data-stu-id="7a832-153">Clip List XML</span></span>
* <span data-ttu-id="7a832-154">Uitvoerasset bestand</span><span class="sxs-lookup"><span data-stu-id="7a832-154">Output File/Asset</span></span>  

![Nieuwe codering werkstroom](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="7a832-156">*Nieuwe codering werkstroom*</span><span class="sxs-lookup"><span data-stu-id="7a832-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="7a832-157"><a id="MXF_to_MP4_with_file_input"></a>Met behulp van Hallo Media bestandsinvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="7a832-158">In de volgorde tooaccept onze invoer mediabestand een begint met Media bestand invoer onderdelen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a832-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="7a832-159">tooadd een onderdeel toohello werkstroom, zoekt in het zoekvak Hallo-opslagplaats en sleep Hallo gewenst vermelding op Hallo designer deelvenster.</span><span class="sxs-lookup"><span data-stu-id="7a832-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="7a832-160">Dit doen voor Hallo Media bestand invoer en Hallo primaire bronbestand onderdeel toohello Filename invoer pincode vanaf Media bestand invoer Hallo verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="7a832-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Verbonden mediabestand invoer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="7a832-162">*Verbonden mediabestand invoer*</span><span class="sxs-lookup"><span data-stu-id="7a832-162">*Connected Media File Input*</span></span>

<span data-ttu-id="7a832-163">Voordat we veel anders doen kunt, moet u eerst tooindicate toohello werkstroomontwerper welke voorbeeldbestand willen we graag toouse toodesign onze werkstroom met.</span><span class="sxs-lookup"><span data-stu-id="7a832-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="7a832-164">toodo geval is, klikt u op Hallo designer deelvenster achtergrond en te bekijken voor Hallo primaire bronbestand-eigenschap op Hallo eigenschap rechter deelvenster.</span><span class="sxs-lookup"><span data-stu-id="7a832-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="7a832-165">Klik op Hallo mappictogram en selecteer Hallo gewenst bestand tootest Hallo werkstroom met.</span><span class="sxs-lookup"><span data-stu-id="7a832-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="7a832-166">Zodra dit is gebeurd, wordt de Hallo Media bestandsinvoer onderdeel Hallo bestand controleren en de zijn pincodes tooreflect Hallo uitvoerbestand die deze geïnspecteerd vullen.</span><span class="sxs-lookup"><span data-stu-id="7a832-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Invoer van mediabestand ingevuld](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="7a832-168">*Invoer van mediabestand ingevuld*</span><span class="sxs-lookup"><span data-stu-id="7a832-168">*Populated Media File Input*</span></span>

<span data-ttu-id="7a832-169">Terwijl u hiermee met wat willen we graag toowork met invoer, niet duidelijk nog waar Hallo gecodeerde uitvoer moet gaan.</span><span class="sxs-lookup"><span data-stu-id="7a832-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="7a832-170">Vergelijkbare toohow Hallo primaire bestand van de bron is geconfigureerd, worden nu Hallo uitvoer map variabele eigenschap, net onder configureren.</span><span class="sxs-lookup"><span data-stu-id="7a832-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Geconfigureerde invoer en uitvoer eigenschappen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="7a832-172">*Geconfigureerde invoer en uitvoer eigenschappen*</span><span class="sxs-lookup"><span data-stu-id="7a832-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="7a832-173"><a id="MXF_to_MP4_streams"></a>Streaming media te bekijken</span><span class="sxs-lookup"><span data-stu-id="7a832-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="7a832-174">Vaak het gewenst tooknow Hallo stroom weergave die loopt via Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="7a832-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="7a832-175">tooinspect een stroom op elk gewenst moment in de werkstroom hello, klik op een uitvoer- of invoer van de pincode op Hallo-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="7a832-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="7a832-176">In dit geval probeert te klikken op Hallo niet-gecomprimeerde Video uitvoer pincode van de invoer van onze Media-bestand.</span><span class="sxs-lookup"><span data-stu-id="7a832-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="7a832-177">Een dialoogvenster wordt geopend waarmee tooinspect Hallo uitgaande video.</span><span class="sxs-lookup"><span data-stu-id="7a832-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![Niet-gecomprimeerde Video uitvoer inspecteren Hallo pincode](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="7a832-179">*Niet-gecomprimeerde Video uitvoer inspecteren Hallo pincode*</span><span class="sxs-lookup"><span data-stu-id="7a832-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="7a832-180">In ons geval vertelt ons bijvoorbeeld dat we je omgaan met een invoer 1920 x 1080 op 24 frames per seconde in 4:2:2 steekproeven voor een video van bijna 2 minuten.</span><span class="sxs-lookup"><span data-stu-id="7a832-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="7a832-181"><a id="MXF_to_MP4_file_generation"></a>Toevoegen van een video encoder voor. MP4-bestand genereren</span><span class="sxs-lookup"><span data-stu-id="7a832-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="7a832-182">Houd er rekening mee dat nu, een niet-gecomprimeerde Video's en meerdere niet-gecomprimeerde Audio-uitvoer pincodes zijn beschikbaar voor gebruik van onze invoer Media-bestand.</span><span class="sxs-lookup"><span data-stu-id="7a832-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="7a832-183">In de volgorde tooencode Hallo inkomende video, moeten we een codering onderdeel - in dit geval voor het genereren van. MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="7a832-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="7a832-184">tooencode Hallo videostream tooH.264, Hallo AVC Video Encoder onderdeel toohello ontwerpoppervlak toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a832-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="7a832-185">Dit onderdeel wordt een decomprimeren videostream als invoer en biedt een gecomprimeerde AVC-videostream op de pincode van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7a832-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Niet-verbonden AVC-codering](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="7a832-187">*Niet-verbonden AVC-codering*</span><span class="sxs-lookup"><span data-stu-id="7a832-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="7a832-188">De eigenschappen kunt u bepalen hoe Hallo codering precies wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="7a832-189">We hebben een overzicht van enkele Hallo meer belangrijke instellingen:</span><span class="sxs-lookup"><span data-stu-id="7a832-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="7a832-190">Uitvoer breedte en hoogte van de uitvoer: deze Hallo resolutie van Hallo gecodeerde video bepalen.</span><span class="sxs-lookup"><span data-stu-id="7a832-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="7a832-191">In ons geval gaan we met 640 x 360</span><span class="sxs-lookup"><span data-stu-id="7a832-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="7a832-192">Framesnelheid: wanneer set toopassthrough gewoon Hallo bron framesnelheid aannemen, is het mogelijk toooverride dit al.</span><span class="sxs-lookup"><span data-stu-id="7a832-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="7a832-193">Houd er rekening mee dat dergelijke framesnelheid conversie is niet beweging-gecompenseerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="7a832-194">Profiel en het niveau: deze bepalen Hallo AVC-profiel en niveau.</span><span class="sxs-lookup"><span data-stu-id="7a832-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="7a832-195">tooconveniently u meer informatie over de verschillende niveaus Hallo en -profielen, klikt u op Hallo vraagteken Hallo AVC Video Encoder onderdeel en Hallo help-pagina meer details over elk Hallo niveaus wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7a832-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="7a832-196">Voor onze voorbeeld we kiezen Main-profiel op niveau 3.2 (Hallo standaard).</span><span class="sxs-lookup"><span data-stu-id="7a832-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="7a832-197">Beoordeel besturingselement modus en Bitrate (kbps): in ons scenario we kiezen voor een constante uitvoer voor 1200 kbps bitrate (CBR)</span><span class="sxs-lookup"><span data-stu-id="7a832-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="7a832-198">Video-indeling: dit is over Hallo VUI (Video bruikbaarheid informatie) die in Hallo H.264 stroom wordt geschreven (side-informatie die kan worden gebruikt door een decoder tooenhance Hallo weergave, maar niet essentieel toocorrectly te decoderen):</span><span class="sxs-lookup"><span data-stu-id="7a832-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="7a832-199">NTSC (standaard voor VS of Japan, met behulp van 30 fps)</span><span class="sxs-lookup"><span data-stu-id="7a832-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="7a832-200">PAL (standaard voor Europa, met behulp van 25 fps)</span><span class="sxs-lookup"><span data-stu-id="7a832-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="7a832-201">Modus van de grootte GOP: geconfigureerd vaste GOP grootte voor onze toepassing met een Interval van twee seconden van de sleutel met GOPs gesloten.</span><span class="sxs-lookup"><span data-stu-id="7a832-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="7a832-202">Dit zorgt voor compatibiliteit met Hallo die dynamische pakketten Azure Media Services biedt.</span><span class="sxs-lookup"><span data-stu-id="7a832-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="7a832-203">toofeed onze encoder AVC Hallo niet-gecomprimeerde Video-uitvoer pincode vanaf Hallo Media bestand invoer onderdeel toohello niet-gecomprimeerde Video invoer pincode van Hallo AVC coderingsprogramma verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="7a832-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Verbonden AVC-codering](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="7a832-205">*Verbonden AVC Main-codering*</span><span class="sxs-lookup"><span data-stu-id="7a832-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="7a832-206"><a id="MXF_to_MP4_audio"></a>Codering Hallo audiostroom</span><span class="sxs-lookup"><span data-stu-id="7a832-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="7a832-207">Op dit moment hebben we video gecodeerd maar Hallo oorspronkelijke niet-gecomprimeerde audiostroom moet nog steeds toobe gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="7a832-208">Voor dit gaan we met AAC codering door Hallo onderdeel AAC codering (Dolby).</span><span class="sxs-lookup"><span data-stu-id="7a832-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="7a832-209">Deze werkstroom toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a832-209">Add it toohello workflow.</span></span>

![Niet-verbonden AVC-codering](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="7a832-211">*Niet-verbonden AAC codering*</span><span class="sxs-lookup"><span data-stu-id="7a832-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="7a832-212">Nu is er een incompatibiliteit: Er is alleen een één niet-gecomprimeerde audio-invoer pincode van Hallo AAC Encoder terwijl meer dan waarschijnlijk Hallo Media bestand invoer heeft twee verschillende audiostroom beschikbaar ongecomprimeerde: één voor Hallo audio kanaal en één voor Hallo links recht.</span><span class="sxs-lookup"><span data-stu-id="7a832-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="7a832-213">(Als u bent omgaan met rond geluid, dat is 6 kanalen.) Zodat het is niet mogelijk verbinding toodirectly Hallo audio van Hallo Media bestand invoerbron naar Hallo AAC audio-codering.</span><span class="sxs-lookup"><span data-stu-id="7a832-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="7a832-214">Hallo AAC onderdeel verwacht een zogenaamde 'interleaved' audiostroom: één stream met beide Hallo links en Hallo rechts kanalen interleaved met elkaar.</span><span class="sxs-lookup"><span data-stu-id="7a832-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="7a832-215">Wanneer we weten uit onze media-bronbestand wat welke audio-nummers zijn in welke positie in de bron hello, kunnen we correct dergelijke interleaved audiostroom Hello genereren spreker posities voor links of rechts toegewezen.</span><span class="sxs-lookup"><span data-stu-id="7a832-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="7a832-216">Eerst moet een toogenerated een interleaved stroom uit Hallo vereist bron audio-kanalen.</span><span class="sxs-lookup"><span data-stu-id="7a832-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="7a832-217">Hallo Audio Stream Interleaver onderdeel verwerken dit voor ons.</span><span class="sxs-lookup"><span data-stu-id="7a832-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="7a832-218">Deze werkstroom toohello toevoegen en maak verbinding Hallo audio-uitvoer van Hallo Media bestandsinvoer in de App.</span><span class="sxs-lookup"><span data-stu-id="7a832-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Verbonden audiostroom Interleaver](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="7a832-220">*Verbonden audiostroom Interleaver*</span><span class="sxs-lookup"><span data-stu-id="7a832-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="7a832-221">Nu dat we een interleaved audiostroom hebben, opgeven we nog steeds niet waar tooassign Hallo naar links of rechts spreker posities aan.</span><span class="sxs-lookup"><span data-stu-id="7a832-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="7a832-222">In de volgorde van toospecify dit, we kunnen gebruikmaken van Hallo spreker positie wel statusrapporten.</span><span class="sxs-lookup"><span data-stu-id="7a832-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Toevoegen van een spreker positie wel statusrapporten](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="7a832-224">*Toevoegen van een spreker positie wel statusrapporten*</span><span class="sxs-lookup"><span data-stu-id="7a832-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="7a832-225">Hallo spreker positie wel statusrapporten voor gebruik met een aansluiting invoerstroom configureren via een Encoder vooraf ingestelde Filter van 'Custom' en Hallo kanaal voorinstelling "2.0 (L, R)" genoemd.</span><span class="sxs-lookup"><span data-stu-id="7a832-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="7a832-226">(Dit wordt Hallo links spreker positie toochannel 1 en Hallo rechts spreker positie toochannel 2 toewijzen).</span><span class="sxs-lookup"><span data-stu-id="7a832-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="7a832-227">Verbinding maken met uitvoer Hallo van Hallo spreker positie wel statusrapporten toohello invoer Hallo AAC Encoder.</span><span class="sxs-lookup"><span data-stu-id="7a832-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="7a832-228">Vervolgens geeft u op Hallo AAC Encoder toowork met een '2.0 (L, R)' kanaal vooraf ingesteld, zodat deze toodeal met stereogeluid als invoer.</span><span class="sxs-lookup"><span data-stu-id="7a832-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="7a832-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Audio en Video-streams multiplex in een MP4-container</span><span class="sxs-lookup"><span data-stu-id="7a832-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="7a832-230">Gegeven onze AVC gecodeerde videostream en onze AAC gecodeerd audiostroom, kunnen we beide in vastleggen een. MP4-container.</span><span class="sxs-lookup"><span data-stu-id="7a832-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="7a832-231">Hallo-proces van de combinatie van verschillende stromen in een enkel wordt 'multiplex' (of 'muxing') genoemd.</span><span class="sxs-lookup"><span data-stu-id="7a832-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="7a832-232">In dit geval bent we Hallo audio en video streams Hallo in één samenhangende interleaving. MP4-pakket.</span><span class="sxs-lookup"><span data-stu-id="7a832-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="7a832-233">Hallo-onderdeel dat coördineert dit voor een. MP4-container wordt Hallo Multiplexer ISO MPEG-4 genoemd.</span><span class="sxs-lookup"><span data-stu-id="7a832-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="7a832-234">Toevoegen van een toohello ontwerpoppervlak en verbind Hallo AVC Video Encoder zowel Hallo AAC Encoder tooits invoer.</span><span class="sxs-lookup"><span data-stu-id="7a832-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![Verbonden MPEG4 Multiplexer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="7a832-236">*Verbonden MPEG4 Multiplexer*</span><span class="sxs-lookup"><span data-stu-id="7a832-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="7a832-237"><a id="MXF_to_MP4_writing_mp4"></a>Hallo MP4-bestand schrijven</span><span class="sxs-lookup"><span data-stu-id="7a832-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="7a832-238">Bij het schrijven van een bestand voor uitvoer wordt Hallo bestand Output-component gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7a832-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="7a832-239">We kunnen deze uitvoer toohello Hallo ISO MPEG-4 Multiplexer verbinding maken zodat de uitvoer opgehaald toodisk geschreven.</span><span class="sxs-lookup"><span data-stu-id="7a832-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="7a832-240">toodo, verbinding maken met de Hallo Container (MPEG-4) uitvoer pincode toohello schrijven invoer pincode Hallo uitvoer in een bestand.</span><span class="sxs-lookup"><span data-stu-id="7a832-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![Verbonden uitvoer in een bestand](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="7a832-242">*Verbonden uitvoer in een bestand*</span><span class="sxs-lookup"><span data-stu-id="7a832-242">*Connected File Output*</span></span>

<span data-ttu-id="7a832-243">Hallo filename die wordt gebruikt, wordt bepaald door Hallo bestandseigenschap.</span><span class="sxs-lookup"><span data-stu-id="7a832-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="7a832-244">Die eigenschap kan hardcoded tooa gegeven waarde zijn, kan een tooset zult deze via een expressie in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="7a832-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="7a832-245">toohave hello werkstroom automatisch bepalen Hallo uitvoer bestand van de eigenschap name van een expressie, klikt u op Hallo buton volgende toohello bestandsnaam (volgende toohello mappictogram).</span><span class="sxs-lookup"><span data-stu-id="7a832-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="7a832-246">Van Hallo vervolgkeuzemenu en selecteer vervolgens 'Expressie'.</span><span class="sxs-lookup"><span data-stu-id="7a832-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="7a832-247">Er verschijnt nu Hallo expressie-editor.</span><span class="sxs-lookup"><span data-stu-id="7a832-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="7a832-248">Schakel eerst Hallo-inhoud van het Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="7a832-248">Clear hello contents of hello editor first.</span></span>

![Lege expressie-Editor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="7a832-250">*Lege expressie-Editor*</span><span class="sxs-lookup"><span data-stu-id="7a832-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="7a832-251">Hallo expressie-editor kunt tooenter een letterlijke waarde, gecombineerd met een of meer variabelen.</span><span class="sxs-lookup"><span data-stu-id="7a832-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="7a832-252">Variabelen beginnen met een dollarteken.</span><span class="sxs-lookup"><span data-stu-id="7a832-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="7a832-253">Als u Hallo $ sleutel raakt, ziet Hallo editor vervolgkeuzelijst met beschikbare variabelen met een keuze.</span><span class="sxs-lookup"><span data-stu-id="7a832-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="7a832-254">In ons geval gebruikt u een combinatie van Hallo uitvoer directory en Hallo base invoerbestand naamvariabele:</span><span class="sxs-lookup"><span data-stu-id="7a832-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Gevuld uit de expressie-Editor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="7a832-256">*Gevuld uit de expressie-Editor*</span><span class="sxs-lookup"><span data-stu-id="7a832-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="7a832-257">In volgorde Raadpleeg toosee een bestand voor uitvoer van de coderingstaak in Azure, moet u een waarde in de expressie-editor Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="7a832-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="7a832-258">Als u Hallo expressie bevestigt door roept ok, voorbeeld Hallo eigenschappenvenster op dit moment van deze toowhat waarde Hallo bestand eigenschap wordt omgezet.</span><span class="sxs-lookup"><span data-stu-id="7a832-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![Expressie voor uitvoer dir wordt opgelost](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="7a832-260">*Expressie voor uitvoer dir wordt opgelost*</span><span class="sxs-lookup"><span data-stu-id="7a832-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="7a832-261"><a id="MXF_to_MP4_asset_from_output"></a>Maken van een Media Services-activum van Hallo-bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="7a832-262">Terwijl we een MP4-bestand voor uitvoer geschreven hebben, moeten we nog steeds tooindicate dat dit bestand toohello hoort uitvoer asset welke mediaservices wordt gegenereerd als gevolg van deze werkstroom wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="7a832-263">toothis einde Hallo Uitvoerasset bestand knooppunt op Hallo werkstroom canvas wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7a832-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="7a832-264">Alle binnenkomende bestanden in dit knooppunt maakt deel uit van Hallo resulterende Azure Media Services actief zijn.</span><span class="sxs-lookup"><span data-stu-id="7a832-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="7a832-265">Verbinding maken met Hallo uitvoer in een bestand onderdeel toohello Uitvoerasset bestand onderdeel toofinish Hallo werkstroom.</span><span class="sxs-lookup"><span data-stu-id="7a832-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Werkstroom is voltooid](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="7a832-267">*Werkstroom is voltooid*</span><span class="sxs-lookup"><span data-stu-id="7a832-267">*Finished Workflow*</span></span>

### <span data-ttu-id="7a832-268"><a id="MXF_to_MP4_test"></a>Test Hallo lokaal werkstroom is voltooid</span><span class="sxs-lookup"><span data-stu-id="7a832-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="7a832-269">lokaal tootest Hallo-werkstroom bereikt Hallo afspeelknop in de werkbalk boven Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a832-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="7a832-270">Als de werkstroom Hallo uitgevoerd, inspecteren Hallo uitvoer wordt gegenereerd in de uitvoermap Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="7a832-271">U ziet Hallo MP4-bestand voor uitvoer die is gecodeerd uit Hallo MXF invoerbron bestand is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7a832-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="7a832-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Codering MXF in MP4 - multibitrate dynamische pakketten ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="7a832-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="7a832-273">In dit scenario maakt u een set van meerdere bitrate MP4-bestanden met AAC gecodeerde audio van één. Het invoerbestand MXF.</span><span class="sxs-lookup"><span data-stu-id="7a832-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="7a832-274">Wanneer een multi-bitrate asset uitvoer vereist is voor gebruik in combinatie met Hallo dynamische pakketten functies die worden aangeboden door Azure Media Services, meerdere GOP uitgelijnde MP4-bestanden van elk een andere bitrate en de resolutie toobe gegenereerd moet.</span><span class="sxs-lookup"><span data-stu-id="7a832-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="7a832-275">toodo dus Hallo [MXF naar een single-bitrate MP4-codering](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) scenario bevat ons een goed uitgangspunt.</span><span class="sxs-lookup"><span data-stu-id="7a832-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Werkstroom starten](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="7a832-277">*Werkstroom starten*</span><span class="sxs-lookup"><span data-stu-id="7a832-277">*Starting Workflow*</span></span>

### <span data-ttu-id="7a832-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Toevoegen van een of meer extra MP4-uitvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="7a832-279">Alle MP4-bestanden in onze resulterende Azure Media Services actief wordt ondersteuning voor een andere bitrate en resolutie.</span><span class="sxs-lookup"><span data-stu-id="7a832-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="7a832-280">Stel een of meer MP4 uitvoer bestanden toohello werkstroom toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a832-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="7a832-281">toomake ervoor dat we hebben alle onze video coderingsprogramma's die zijn gemaakt met dezelfde instellingen Hallo, de meest geschikte tooduplicate Hallo al bestaande AVC Video Encoder en configureer een andere combinatie van de resolutie en bitrate (we toevoegen van een van de 960 x 540 op 25 frames per seconde op 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="7a832-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="7a832-282">bestaande encoder tooduplicate hello, kopie plakt u deze op Hallo ontwerpoppervlak.</span><span class="sxs-lookup"><span data-stu-id="7a832-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="7a832-283">Verbinding maken met Hallo niet-gecomprimeerde Video-uitvoer pincode Hallo Media bestandsinvoer in onze nieuwe AVC-component.</span><span class="sxs-lookup"><span data-stu-id="7a832-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Tweede AVC encoder verbonden](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="7a832-285">*Tweede AVC encoder verbonden*</span><span class="sxs-lookup"><span data-stu-id="7a832-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="7a832-286">Nu aan te passen Hallo-configuratie voor onze nieuwe AVC encoder toooutput 960 x 540 met 2,5 Mbps.</span><span class="sxs-lookup"><span data-stu-id="7a832-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="7a832-287">(Gebruik de eigenschappen 'uitvoer breedte', 'Uitvoer hoogte' en 'Bitrate (kbps)' voor deze.)</span><span class="sxs-lookup"><span data-stu-id="7a832-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="7a832-288">Opgegeven willen we toouse Hallo resulterende asset samen met Azure Media Services dynamische pakketten, Hallo streaming-eindpunt moet toobe geschikt is voor het genereren van deze MP4-bestanden HLS/Fragmented MP4/DASH-fragmenten die exact uitgelijnde tooeach andere op een manier zijn dat clients die zijn schakelen tussen verschillende bitsnelheden een enkele smooth continue video en audio-ervaring krijgen.</span><span class="sxs-lookup"><span data-stu-id="7a832-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="7a832-289">toomake die optreden, moeten we dat in de eigenschappen van beide encoders AVC Hallo Hallo GOP ('groep afbeeldingen')-grootte voor beide MP4-bestanden is ingesteld tooensure too2 seconden, dat kunnen worden gedaan door:</span><span class="sxs-lookup"><span data-stu-id="7a832-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="7a832-290">Hallo GOP grootte modus tooFixed GOP grootte wordt ingesteld en</span><span class="sxs-lookup"><span data-stu-id="7a832-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="7a832-291">Hallo sleutel Frame Interval tootwo in seconden.</span><span class="sxs-lookup"><span data-stu-id="7a832-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="7a832-292">Hallo GOP IDR besturingselement tooClosed GOP tooensure alle GOP permanent zijn ook instellen op hun eigen zonder afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="7a832-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="7a832-293">toomake onze handige toounderstand werkstroom Hallo eerste AVC encoder te wijzigen "AVC Video Encoder 640 x 360 1200kbps ' en het tweede AVC-encoder Hallo ' AVC-Video Encoder 960 x 540 2500 kbps '.</span><span class="sxs-lookup"><span data-stu-id="7a832-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="7a832-294">Een tweede ISO MPEG-4 Multiplexer en de uitvoer van een tweede bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a832-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="7a832-295">Hallo multiplexer toohello nieuwe AVC encoder verbinding en zorg ervoor dat de uitvoer naar Hallo uitvoer in een bestand wordt geleid.</span><span class="sxs-lookup"><span data-stu-id="7a832-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="7a832-296">Sluit ook Hallo AAC audio encoder uitvoer toohello nieuwe multiplexer van invoer.</span><span class="sxs-lookup"><span data-stu-id="7a832-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="7a832-297">Hallo uitvoer in een bestand op zijn beurt vervolgens kan worden verbonden toohello Uitvoerasset bestand knooppunt tooadd het toohello Media Services Asset die wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a832-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Tweede mixer en uitvoer in een bestand verbonden](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="7a832-299">*Tweede mixer en uitvoer in een bestand verbonden*</span><span class="sxs-lookup"><span data-stu-id="7a832-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="7a832-300">Voor compatibiliteit met Azure Media Services dynamische pakketten, configureer Hallo multiplexer van Chunk modus tooGOP aantal of de duur en Hallo GOPs per segment too1 ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7a832-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="7a832-301">(Dit is standaard Hallo.)</span><span class="sxs-lookup"><span data-stu-id="7a832-301">(This should be hello default.)</span></span>

![Mixer Chunk modi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="7a832-303">*Mixer Chunk modi*</span><span class="sxs-lookup"><span data-stu-id="7a832-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="7a832-304">Opmerking: u kunt toorepeat dit proces voor alle andere bitrate en resolutie combinaties die u wilt dat toohave toohello asset uitvoer toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7a832-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="7a832-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configureren Hallo uitvoer bestandsnamen</span><span class="sxs-lookup"><span data-stu-id="7a832-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="7a832-306">Er is meer dan één enkel bestand toegevoegde toohello uitvoerasset.</span><span class="sxs-lookup"><span data-stu-id="7a832-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="7a832-307">Dit biedt een noodzaak toomake ervoor Hallo bestandsnamen voor elk Hallo bestanden zijn van elkaar verschillen en mogelijk zelfs van toepassing een naamgevingsconventie daarom het wissen van de bestandsnaam Hallo bent u omgaan is met uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7a832-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="7a832-308">Uitvoer benoemen kan worden beheerd via de expressies in Hallo designer.</span><span class="sxs-lookup"><span data-stu-id="7a832-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="7a832-309">Open Hallo deelvenster met de eigenschap voor een van de onderdelen van Hallo-uitvoer in een bestand en open Hallo expressie-editor voor Hallo bestandseigenschap.</span><span class="sxs-lookup"><span data-stu-id="7a832-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="7a832-310">Ons eerste uitvoerbestand via de volgende expressie Hallo is geconfigureerd (Zie Hallo-zelfstudie voor het beste van [MXF tooa single-bitrate MP4-uitvoer](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="7a832-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="7a832-311">Dit betekent dat onze filename wordt bepaald door twee variabelen: Hallo uitvoer directory toowrite in en hello basisnaam van bron.</span><span class="sxs-lookup"><span data-stu-id="7a832-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="7a832-312">Hallo voormalige wordt blootgesteld als eigenschap op Hallo werkstroom hoofdmap en Hallo laatstgenoemde wordt bepaald door de inkomende hello-bestand.</span><span class="sxs-lookup"><span data-stu-id="7a832-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="7a832-313">Houd er rekening mee dat uitvoermap hello wordt gebruikt voor het lokale testen; Deze eigenschap wordt overschreven door Hallo workflowengine wanneer Hallo werkstroom door Hallo cloud-gebaseerde Mediaprocessor in Azure Media Services wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="7a832-314">toogive beide onze uitvoerbestanden aan de naamgeving van een consistente uitvoer, wijziging Hallo naming expressie voor het eerst bestandsnaam:</span><span class="sxs-lookup"><span data-stu-id="7a832-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="7a832-315">en de tweede Hallo naar:</span><span class="sxs-lookup"><span data-stu-id="7a832-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="7a832-316">Uitvoeren van een tussenliggende testuitvoering toomake ervoor dat beide MP4-bestanden voor uitvoer correct worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="7a832-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Toevoegen van een afzonderlijke-nummer</span><span class="sxs-lookup"><span data-stu-id="7a832-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="7a832-318">Later zullen we zien wanneer er een ISM-bestand toogo met onze MP4-bestanden voor uitvoer gegenereerd, wordt ook moet een MP4-bestand alleen audio als Hallo-nummer voor onze adaptief streamen.</span><span class="sxs-lookup"><span data-stu-id="7a832-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="7a832-319">toocreate dit bestand, een extra mixer toohello-werkstroom (ISO-MPEG-4 Multiplexer) toevoegen en Hallo AAC encoder uitvoer pincode verbinden met de pincode van de invoer voor Track 1.</span><span class="sxs-lookup"><span data-stu-id="7a832-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Audio mixer toegevoegd](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="7a832-321">*Audio mixer toegevoegd*</span><span class="sxs-lookup"><span data-stu-id="7a832-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="7a832-322">Maken van een derde bestand onderdeel toooutput Hallo uitgaande uitvoerstroom van Hallo mixer en Hallo bestand naming expressie als configureren:</span><span class="sxs-lookup"><span data-stu-id="7a832-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Audio mixer maken van de uitvoer van bestand](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="7a832-324">*Audio mixer maken van de uitvoer van bestand*</span><span class="sxs-lookup"><span data-stu-id="7a832-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="7a832-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Hallo toe te voegen. ISM SMIL-bestand</span><span class="sxs-lookup"><span data-stu-id="7a832-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="7a832-326">Voor Hallo dynamische pakketten toowork in combinatie met beide MP4-bestanden (en alleen audio MP4 Hallo) in onze asset Media Services moet er ook een manifestbestand (ook wel een 'SMIL'-bestand: Synchronized Multimedia Integration Language).</span><span class="sxs-lookup"><span data-stu-id="7a832-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="7a832-327">Dit bestand geeft tooAzure Media Services aan welke MP4-bestanden zijn beschikbaar voor dynamische pakketten en welke van deze tooconsider voor Hallo audio streaming.</span><span class="sxs-lookup"><span data-stu-id="7a832-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="7a832-328">Een typische manifestbestand voor een set MP4 van met een enkele audiostroom ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a832-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="7a832-329">Hallo ISM-bestand bevat binnen een switch-instructie een verwijzing tooeach van Hallo afzonderlijke MP4 videobestanden en daarnaast audiobestand toothose ook een (of meer) verwijst naar tooan MP4 alleen met Hallo audio.</span><span class="sxs-lookup"><span data-stu-id="7a832-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="7a832-330">Hallo manifestbestand voor onze van MP4-set kan worden gedaan door middel van een component Hallo 'AMS Manifest Writer' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7a832-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="7a832-331">toouse, sleep deze naar het oppervlak Hallo en Hallo 'Schrijven voltooid' uitvoer pincodes vanaf Hallo drie uitvoer in een bestand onderdelen toohello AMS Manifest Writer invoer verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="7a832-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="7a832-332">Controleer zeker tooconnect Hallo-uitvoer van Hallo AMS Manifest Writer toohello Uitvoerasset bestand.</span><span class="sxs-lookup"><span data-stu-id="7a832-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="7a832-333">Net als bij onze andere bestand uitvoer-onderdelen, Hallo ISM uitvoer bestandsnaam configureren met een expressie:</span><span class="sxs-lookup"><span data-stu-id="7a832-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="7a832-334">Onze klaar werkstroom ziet er Hallo hieronder:</span><span class="sxs-lookup"><span data-stu-id="7a832-334">Our finished workflow looks like hello below:</span></span>

![Voltooide MXF toomultibitrate MP4-werkstroom](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="7a832-336">*Voltooide MXF toomultibitrate MP4-werkstroom*</span><span class="sxs-lookup"><span data-stu-id="7a832-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="7a832-337"><a id="MXF_to__multibitrate_MP4"></a>MXF in multibitrate MP4 - verbeterde blauwdruk codering</span><span class="sxs-lookup"><span data-stu-id="7a832-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="7a832-338">In Hallo [vorige werkstroom procedure](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we hebt gezien hoe een enkel MXF invoer actief kan worden geconverteerd naar een uitvoerasset met multi-bitrate MP4-bestanden, een alleen-audio MP4-bestand en een manifestbestand voor gebruik in combinatie met Azure Media Services dynamische pakketten.</span><span class="sxs-lookup"><span data-stu-id="7a832-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="7a832-339">In dit scenario wordt weergegeven hoe sommige aspecten van Hallo kunnen worden verbeterd en eenvoudiger gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a832-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="7a832-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Werkstroom overzicht tooenhance</span><span class="sxs-lookup"><span data-stu-id="7a832-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Multibitrate MP4 werkstroom tooenhance](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="7a832-342">*Multibitrate MP4 werkstroom tooenhance*</span><span class="sxs-lookup"><span data-stu-id="7a832-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="7a832-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Naamgevingsregels voor bestanden</span><span class="sxs-lookup"><span data-stu-id="7a832-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="7a832-344">In de vorige werkstroom Hallo we een eenvoudige expressie als Hallo basis voor het genereren van bestandsnamen uitvoer opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7a832-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="7a832-345">We enkele duplicatie al hebben: Hallo Hallo afzonderlijke uitvoer bestand componenten opgegeven dergelijke expressie.</span><span class="sxs-lookup"><span data-stu-id="7a832-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="7a832-346">Bijvoorbeeld: onze onderdeel bestand uitvoer voor de eerste videobestand hello wordt geconfigureerd met deze expressie:</span><span class="sxs-lookup"><span data-stu-id="7a832-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="7a832-347">Voor de tweede uitvoer voor Hallo is video, hebben we een expressie zoals:</span><span class="sxs-lookup"><span data-stu-id="7a832-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="7a832-348">Zou niet het schonere minder fout foutgevoelige en gemakkelijker als we kan Verwijder enkele van deze duplicaten en dingen in plaats daarvan meer configureerbaar maken?</span><span class="sxs-lookup"><span data-stu-id="7a832-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="7a832-349">Gelukkig kunnen we: Hallo designer van expressie mogelijkheden in combinatie met Hallo mogelijkheid toocreate aangepaste eigenschappen in de hoofdmap van de werkstroom Geef ons een extra beveiligingslaag gemak.</span><span class="sxs-lookup"><span data-stu-id="7a832-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="7a832-350">Stel, dat we je filename configuratie-station van Hallo bitsnelheden Hallo afzonderlijke MP4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="7a832-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="7a832-351">Deze bitsnelheden beogen wij tooconfigure op één centrale plaats (op Hallo root van onze grafiek), vanaf waar zij gebruikte tooconfigure en het station genereren bestandsnaam moeten worden.</span><span class="sxs-lookup"><span data-stu-id="7a832-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="7a832-352">toodo, begin met het publiceren van Hallo bitrate eigenschap vanuit beide AVC coderingsprogramma's toohello hoofdmap van de werkstroom, zodat deze toegankelijk is vanaf beide Hallo-hoofdmap ook vanuit Hallo AVC coderingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="7a832-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="7a832-353">(Zelfs als in twee verschillende plaatsen weergegeven, er is slechts één onderliggende waarde.)</span><span class="sxs-lookup"><span data-stu-id="7a832-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="7a832-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Eigenschappen van onderdeel op Hallo werkstroom hoofdmap publiceren</span><span class="sxs-lookup"><span data-stu-id="7a832-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="7a832-355">Hallo eerste AVC encoder openen, toohello Bitrate (kbps) eigenschap gaat en kies uit de vervolgkeuzelijst Hallo publiceren.</span><span class="sxs-lookup"><span data-stu-id="7a832-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Publicatie Hallo bitrate-eigenschap](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="7a832-357">*Publicatie Hallo bitrate-eigenschap*</span><span class="sxs-lookup"><span data-stu-id="7a832-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="7a832-358">Hallo configureren dialoogvenster toopublish toohello basis van onze grafiek werkstroom met een gepubliceerde naam 'video1bitrate' en 'Video 1 Bitrate' de leesbare weergavenaam publiceren.</span><span class="sxs-lookup"><span data-stu-id="7a832-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="7a832-359">Configureren van een aangepaste groepsnaam 'Bitsnelheden Streaming' genoemd en publiceren bereikt.</span><span class="sxs-lookup"><span data-stu-id="7a832-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Publicatie Hallo bitrate-eigenschap](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="7a832-361">*Publishing dialoogvenster voor de eigenschap bitrate*</span><span class="sxs-lookup"><span data-stu-id="7a832-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="7a832-362">Herhaal Hallo dezelfde voor Hallo bitrate eigenschap Hallo tweede AVC-codering en noem deze 'video2bitrate' met de weergavenaam 'Bitrate Video 2', in Hallo dezelfde aangepaste 'Bitsnelheden Streaming' groeperen.</span><span class="sxs-lookup"><span data-stu-id="7a832-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="7a832-363">Als we nu Hallo hoofdmap werkstroomeigenschappen controleren, zien we onze aangepaste groep Hello twee gepubliceerde eigenschappen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7a832-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="7a832-364">Beide zijn opgetreden bij het Hallo-waarde van hun respectieve AVC encoder bitrate weergeven.</span><span class="sxs-lookup"><span data-stu-id="7a832-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![Eigenschappen van gepubliceerde bitrate op basis van de werkstroom](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="7a832-366">Wanneer we tooaccess deze eigenschappen van code of van een expressie willen, kunnen we dit doen als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a832-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="7a832-367">vanuit Inlinecode van een onderdeel direct onder de hoofdmap Hallo: node.getPropertyAsString('.. / video1bitrate', null)</span><span class="sxs-lookup"><span data-stu-id="7a832-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="7a832-368">in een expressie: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="7a832-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="7a832-369">Laten we onze-nummer bitrate ook op deze publicatie volledig Hallo 'Bitsnelheden Streaming' groep.</span><span class="sxs-lookup"><span data-stu-id="7a832-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="7a832-370">In de eigenschappen van de Hallo Hallo AAC codering, Hallo Bitrate instelling zoekt en selecteert u publiceren in Hallo dropdown volgende tooit.</span><span class="sxs-lookup"><span data-stu-id="7a832-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="7a832-371">Toohello hoofdmap van de grafiek met de naam 'audio1bitrate' Hallo publiceren en naam "Bitrate Audio 1" in onze aangepaste groep 'Bitsnelheden Streaming' weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7a832-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Publishing dialoogvenster voor audio bitrate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="7a832-373">*Publishing dialoogvenster voor audio bitrate*</span><span class="sxs-lookup"><span data-stu-id="7a832-373">*Publishing dialog for audio bitrate*</span></span>

![Resulterende video en audio-eigenschappen in de hoofdmap van](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="7a832-375">*Resulterende video en audio-eigenschappen in de hoofdmap van*</span><span class="sxs-lookup"><span data-stu-id="7a832-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="7a832-376">Houd er rekening mee dat als u een van deze drie wijzigt ook opnieuw configureert waarden en wijzigingen Hallo waarden op de betreffende onderdelen Hallo ze zijn gekoppeld aan (en indien gepubliceerd vanuit).</span><span class="sxs-lookup"><span data-stu-id="7a832-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="7a832-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Uitvoerbestand namen zijn afhankelijk van de gepubliceerde eigenschapswaarden hebt gegenereerd</span><span class="sxs-lookup"><span data-stu-id="7a832-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="7a832-378">In plaats van hardcoderen onze gegenereerde bestandsnamen we kunnen nu wijzigen onze expressie filename op elk Hallo uitvoer in een bestand onderdelen toorely op Hallo bitrate eigenschappen die we zojuist hebt gepubliceerd op basis van Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="7a832-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="7a832-379">Beginnen met het eerste bestandsuitvoer, Hallo bestandseigenschap vinden en bewerken Hallo expressie als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a832-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="7a832-380">Hallo andere parameters in deze expressie kunnen worden geopend en die zijn ingevoerd door roept Hallo dollarteken op Hallo toetsenbord in Hallo expressievenster.</span><span class="sxs-lookup"><span data-stu-id="7a832-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="7a832-381">Een van de beschikbare parameters Hallo is onze video1bitrate-eigenschap die we eerder hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Toegang tot de parameters in een expressie](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="7a832-383">*Toegang tot de parameters in een expressie*</span><span class="sxs-lookup"><span data-stu-id="7a832-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="7a832-384">Hallo dezelfde voor Hallo bestandsuitvoer voor onze tweede video:</span><span class="sxs-lookup"><span data-stu-id="7a832-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="7a832-385">en voor Hallo bestand met alleen audio-uitvoer:</span><span class="sxs-lookup"><span data-stu-id="7a832-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="7a832-386">Als we nu Hallo bitrate voor Hallo video of audio-bestanden wijzigen, de respectieve encoder Hallo opnieuw wordt geconfigureerd en Hallo bitrate-bestand naamconventie gehonoreerd alle automatische.</span><span class="sxs-lookup"><span data-stu-id="7a832-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="7a832-387"><a id="thumbnails_to__multibitrate_MP4"></a>Miniaturen toomultibitrate MP4 uitvoer toevoegen</span><span class="sxs-lookup"><span data-stu-id="7a832-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="7a832-388">Een werkstroom die wordt gegenereerd vanaf [een multibitrate MP4-uitvoer van een invoer MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we nu zoeken in de miniaturen toohello uitvoer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a832-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="7a832-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Werkstroom overzicht tooadd miniatuurweergaven voor</span><span class="sxs-lookup"><span data-stu-id="7a832-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Multibitrate MP4 werkstroom toostart uit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="7a832-391">*Multibitrate MP4 werkstroom toostart uit*</span><span class="sxs-lookup"><span data-stu-id="7a832-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="7a832-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Toe te voegen JPG-codering</span><span class="sxs-lookup"><span data-stu-id="7a832-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="7a832-393">Hallo hart van onze miniaturen generatie worden Hallo JPG-Encoder onderdeel, kunnen toooutput JPG-bestanden.</span><span class="sxs-lookup"><span data-stu-id="7a832-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![JPG-codering](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="7a832-395">*JPG-codering*</span><span class="sxs-lookup"><span data-stu-id="7a832-395">*JPG Encoder*</span></span>

<span data-ttu-id="7a832-396">Kan geen echter rechtstreeks verbinding wordt gemaakt onze stroom niet-gecomprimeerde Video van Hallo Media bestandsinvoer in Hallo JPG-codering.</span><span class="sxs-lookup"><span data-stu-id="7a832-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="7a832-397">In plaats daarvan verwacht het toobe doorgegeven afzonderlijke frames.</span><span class="sxs-lookup"><span data-stu-id="7a832-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="7a832-398">Dit we kunt doen via Hallo Video Frame-Gate onderdeel.</span><span class="sxs-lookup"><span data-stu-id="7a832-398">This, we can do through hello Video Frame Gate component.</span></span>

![Verbinding maken met een frame-gate toohello JPG-encoder](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="7a832-400">*Verbinding maken met een frame-gate toohello JPG-encoder*</span><span class="sxs-lookup"><span data-stu-id="7a832-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="7a832-401">Hallo frame-gate nadat elke zoveel seconden of frames kunt een video frame toopass.</span><span class="sxs-lookup"><span data-stu-id="7a832-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="7a832-402">Hallo interval en Hallo tijdzoneverschil met waarop dit gebeurt, kan worden geconfigureerd in de eigenschappen van Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a832-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Eigenschappen van video Frame-Gate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="7a832-404">*Eigenschappen van video Frame-Gate*</span><span class="sxs-lookup"><span data-stu-id="7a832-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="7a832-405">Laten we een miniatuur van elke minuut door in te stellen Hallo modus tooTime (seconden) maken en Hallo too60 Interval.</span><span class="sxs-lookup"><span data-stu-id="7a832-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="7a832-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Omgaan met de conversie van de werkruimte</span><span class="sxs-lookup"><span data-stu-id="7a832-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="7a832-407">Hoewel lijkt het logisch zowel niet-gecomprimeerde Video pincodes van Hallo frame-gate en de Hallo Media bestandsinvoer kunnen nu worden verbonden, zouden we krijg een waarschuwing als er zou doen.</span><span class="sxs-lookup"><span data-stu-id="7a832-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Invoerkleur ruimte fout](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="7a832-409">*Invoerkleur ruimte fout*</span><span class="sxs-lookup"><span data-stu-id="7a832-409">*Input color space error*</span></span>

<span data-ttu-id="7a832-410">Dit is omdat Hallo manier in welke kleur informatie wordt weergegeven in de oorspronkelijke onbewerkte niet-gecomprimeerde videostream, afkomstig zijn van onze MXF wijkt af van wat Hallo JPG-codering verwacht.</span><span class="sxs-lookup"><span data-stu-id="7a832-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="7a832-411">Meer specifiek, een zogenaamde ' kleur ruimte ' van 'RGB-' of 'Grijswaarden' tooflow in verwacht.</span><span class="sxs-lookup"><span data-stu-id="7a832-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="7a832-412">Dit betekent dat Hallo Video Frame-Gate van inkomende videostream moet toohave een conversie met betrekking tot de kleurenruimte als eerste toegepast.</span><span class="sxs-lookup"><span data-stu-id="7a832-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="7a832-413">Sleep Hallo werkstroom Hallo kleur ruimte Converter - Intel en verbind deze tooour frame-gate.</span><span class="sxs-lookup"><span data-stu-id="7a832-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Verbinding maken met een conversieprogramma voor kleur ruimte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="7a832-415">*Verbinding maken met een conversieprogramma voor kleur ruimte*</span><span class="sxs-lookup"><span data-stu-id="7a832-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="7a832-416">Kies in het venster Eigenschappen Hallo Hallo BGR 24 vermelding uit de lijst met vooraf ingestelde Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a832-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="7a832-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Schrijven Hallo miniaturen</span><span class="sxs-lookup"><span data-stu-id="7a832-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="7a832-418">Verschillende op onze MP4-video, Hallo JPG-Encoder onderdeel wordt de uitvoer van meer dan één bestand.</span><span class="sxs-lookup"><span data-stu-id="7a832-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="7a832-419">In de volgorde toodeal dit, een onderdeel van de schrijver Scene zoeken JPG-bestand kan worden gebruikt: wordt Hallo binnenkomende JPG miniaturen nemen en geschreven, elke bestandsnaam wordt voorafgegaan door een ander nummer.</span><span class="sxs-lookup"><span data-stu-id="7a832-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="7a832-420">(Hallo getal wordt gewoonlijk aangeeft Hallo aantal seconden/eenheden in welke miniatuur Hallo is afkomstig van Hallo-stroom)</span><span class="sxs-lookup"><span data-stu-id="7a832-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Inleiding tot Hallo Writer Scene zoeken JPG-bestand](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="7a832-422">*Inleiding tot Hallo Writer Scene zoeken JPG-bestand*</span><span class="sxs-lookup"><span data-stu-id="7a832-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="7a832-423">Hallo map uitvoerpad eigenschap configureren met de Hallo expressie: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="7a832-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="7a832-424">en Hallo eigenschap Filename voorvoegsel met:</span><span class="sxs-lookup"><span data-stu-id="7a832-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="7a832-425">Hallo voorvoegsel wordt bepalen hoe de miniatuur Hallo-bestanden worden wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="7a832-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="7a832-426">Ze wordt voorafgegaan door een aantal die duiden Hallo miniatuur van positie in Hallo-stroom.</span><span class="sxs-lookup"><span data-stu-id="7a832-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Eigenschappen van de zoekopdracht JPG-bestand Writer Scene](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="7a832-428">*Eigenschappen van de zoekopdracht JPG-bestand Writer Scene*</span><span class="sxs-lookup"><span data-stu-id="7a832-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="7a832-429">Verbinding maken met Hallo Scene zoeken JPG-bestand Writer toohello Uitvoerasset bestand knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7a832-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="7a832-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Fouten opsporen in een werkstroom</span><span class="sxs-lookup"><span data-stu-id="7a832-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="7a832-431">Verbinding maken met invoer Hallo van Hallo kleur ruimte converter toohello onbewerkte niet-gecomprimeerde video-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7a832-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="7a832-432">Nu een lokale test uitvoeren voor Hallo werkstroom uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7a832-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="7a832-433">Er is een goede kans Hallo werkstroom plotseling wordt niet langer uitgevoerd en geven met een rode omtrek op Hallo-onderdeel dat is een fout opgetreden:</span><span class="sxs-lookup"><span data-stu-id="7a832-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Kleur ruimte Converter fout](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="7a832-435">*Kleur ruimte Converter fout*</span><span class="sxs-lookup"><span data-stu-id="7a832-435">*Color Space Converter error*</span></span>

<span data-ttu-id="7a832-436">Klikt u op Hallo enigszins red "E" pictogram in Hallo rechtsboven Hallo kleur ruimte Converter onderdeel toosee wat is Hallo reden Hallo codering poging is mislukt.</span><span class="sxs-lookup"><span data-stu-id="7a832-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Kleur ruimte Converter foutberichtvenster](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="7a832-438">*Kleur ruimte Converter foutberichtvenster*</span><span class="sxs-lookup"><span data-stu-id="7a832-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="7a832-439">Het blijkt, zoals u kunt zien, dat Hallo binnenkomende kleurruimte standaard voor Hallo kleur ruimte converter toobe rec601 voor onze aangevraagde conversie van YUV tooRGB heeft.</span><span class="sxs-lookup"><span data-stu-id="7a832-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="7a832-440">Onze stroom wordt niet blijkbaar van rec601 aangegeven.</span><span class="sxs-lookup"><span data-stu-id="7a832-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="7a832-441">(Rec 601 is een standaard voor het coderen van elkaar kruisende analoge video signalen in digitale video vorm.</span><span class="sxs-lookup"><span data-stu-id="7a832-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="7a832-442">Hiermee wordt een actieve regio die betrekking hebben op 720 helderheid voorbeelden en 360 chrominantie voorbeelden per regel.</span><span class="sxs-lookup"><span data-stu-id="7a832-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="7a832-443">Hallo kleur system codering wordt ook wel YCbCr 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="7a832-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="7a832-444">toofix, geven we je op Hallo metagegevens van onze stroom die we je rec601 inhoud betreft.</span><span class="sxs-lookup"><span data-stu-id="7a832-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="7a832-445">toodo gebruiken we een Video gegevens Type Updater onderdeel, die we Between onze onbewerkte bron- en Hallo kleur ruimte conversieonderdeel hebt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="7a832-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="7a832-446">Dit type gegevens updater kunt u handmatig bijwerken van bepaalde video gegevens Hallo type-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="7a832-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="7a832-447">Een kleur ruimte Standard van 'Rec 601' tooindicate configureren.</span><span class="sxs-lookup"><span data-stu-id="7a832-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="7a832-448">Als er geen kleurruimte nog gedefinieerd is, wordt hierdoor Hallo Video gegevens Type Updater tootag Hallo stream met Hallo 'Rec 601' kleurruimte.</span><span class="sxs-lookup"><span data-stu-id="7a832-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="7a832-449">(Niet overschrijft alle bestaande metagegevens als Hallo onderdrukking selectievakje is ingeschakeld.)</span><span class="sxs-lookup"><span data-stu-id="7a832-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Bijwerken van kleur ruimte standaard op Hallo gegevens Type Updater](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="7a832-451">*Bijwerken van kleur ruimte standaard op Hallo gegevens Type Updater*</span><span class="sxs-lookup"><span data-stu-id="7a832-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="7a832-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Werkstroom is voltooid</span><span class="sxs-lookup"><span data-stu-id="7a832-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="7a832-453">Nu ons onze werkstroom is voltooid, doet u een andere testuitvoering toosee deze aan.</span><span class="sxs-lookup"><span data-stu-id="7a832-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Voltooide werkstroom voor meerdere mp4-uitvoer met miniaturen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="7a832-455">*Voltooide werkstroom voor meerdere mp4-uitvoer met miniaturen*</span><span class="sxs-lookup"><span data-stu-id="7a832-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="7a832-456"><a id="time_based_trim"></a>Op basis van tijd worden ingekort door multibitrate MP4-uitvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="7a832-457">Een werkstroom die wordt gegenereerd vanaf [een multibitrate MP4-uitvoer van een invoer MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we wordt nu op zoek zijn naar bijsnijden Hallo bronvideo op basis van tijdstempels.</span><span class="sxs-lookup"><span data-stu-id="7a832-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="7a832-458"><a id="time_based_trim_start"></a>Werkstroom overzicht toostart bijsnijden aan toe te voegen</span><span class="sxs-lookup"><span data-stu-id="7a832-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![Werkstroom tooadd bijsnijden te starten](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="7a832-460">*Werkstroom tooadd bijsnijden te starten*</span><span class="sxs-lookup"><span data-stu-id="7a832-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="7a832-461"><a id="time_based_trim_use_stream_trimmer"></a>Hallo stroom Trimmer gebruiken</span><span class="sxs-lookup"><span data-stu-id="7a832-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="7a832-462">Hallo stroom Trimmer component kunt tootrim Hallo begin en einde van een invoerstroom op basis van informatie over de tijdsinstellingen (seconden, minuten,...). Hallo trimmer biedt geen ondersteuning voor op basis van het frame-opmaak.</span><span class="sxs-lookup"><span data-stu-id="7a832-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Stroom Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="7a832-464">*Stroom Trimmer*</span><span class="sxs-lookup"><span data-stu-id="7a832-464">*Stream Trimmer*</span></span>

<span data-ttu-id="7a832-465">In plaats van rechtstreeks Hallo AVC coderingsprogramma's en spreker positie wel statusrapporten toohello Media bestandsinvoer koppelt, moet we tussen deze stroom Hallo trimmer plaatsen.</span><span class="sxs-lookup"><span data-stu-id="7a832-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="7a832-466">(Één voor de video signaal Hallo en één voor Hallo interleaved audio signaal).</span><span class="sxs-lookup"><span data-stu-id="7a832-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Stroom Trimmer tussen plaatsen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="7a832-468">*Stroom Trimmer tussen plaatsen*</span><span class="sxs-lookup"><span data-stu-id="7a832-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="7a832-469">Laten we Hallo trimmer zodanig configureren dat we alleen video en audio tussen 15 en 60 seconden in Hallo video verwerkt.</span><span class="sxs-lookup"><span data-stu-id="7a832-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="7a832-470">Ga toohello eigenschappen van Hallo Video stroom Trimmer en zowel de begintijd (15s) en de eigenschappen van de eindtijd (60s) configureren.</span><span class="sxs-lookup"><span data-stu-id="7a832-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="7a832-471">toomake zorgen zowel onze trimmer audio en video altijd geconfigureerde toohello dezelfde beginnen en eindigen waarden, komen we deze hoofdmap toohello van Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="7a832-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Start tijdeigenschap van stroom Trimmer publiceren](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="7a832-473">*Start tijdeigenschap van stroom Trimmer publiceren*</span><span class="sxs-lookup"><span data-stu-id="7a832-473">*Publish start time property from Stream Trimmer*</span></span>

![Dialoogvenster Eigenschappen voor de begintijd publiceren](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="7a832-475">*Dialoogvenster Eigenschappen voor de begintijd publiceren*</span><span class="sxs-lookup"><span data-stu-id="7a832-475">*Publish property dialog for start time*</span></span>

![Dialoogvenster Eigenschappen voor de eindtijd publiceren](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="7a832-477">*Dialoogvenster Eigenschappen voor de eindtijd publiceren*</span><span class="sxs-lookup"><span data-stu-id="7a832-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="7a832-478">Als we nu Hallo hoofdmap van de werkstroom controleren, beide eigenschappen worden netjes weergegeven en kunnen worden geconfigureerd vanaf daar.</span><span class="sxs-lookup"><span data-stu-id="7a832-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Gepubliceerde eigenschappen die beschikbaar zijn in de hoofdmap van](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="7a832-480">*Gepubliceerde eigenschappen die beschikbaar zijn in de hoofdmap van*</span><span class="sxs-lookup"><span data-stu-id="7a832-480">*Published properties available on root*</span></span>

<span data-ttu-id="7a832-481">Nu Hallo bijsnijden eigenschappen openen vanuit Hallo audio trimmer en zowel begin- en eindtijden configureren met een expressie die toohello verwijst eigenschappen op basis van onze werkstroom Hallo gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="7a832-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="7a832-482">Voor Hallo audio bijsnijden begintijd:</span><span class="sxs-lookup"><span data-stu-id="7a832-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="7a832-483">en voor de eindtijd:</span><span class="sxs-lookup"><span data-stu-id="7a832-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="7a832-484"><a id="time_based_trim_finish"></a>Werkstroom is voltooid</span><span class="sxs-lookup"><span data-stu-id="7a832-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Werkstroom is voltooid](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="7a832-486">*Werkstroom is voltooid*</span><span class="sxs-lookup"><span data-stu-id="7a832-486">*Finished Workflow*</span></span>

## <span data-ttu-id="7a832-487"><a id="scripting"></a>Introducing hello onderdeel in een script vastgelegd</span><span class="sxs-lookup"><span data-stu-id="7a832-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="7a832-488">Script onderdelen kunnen willekeurige scripts uitvoeren tijdens Hallo uitvoering fasen van de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="7a832-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="7a832-489">Er zijn vier verschillende scripts die kunnen worden uitgevoerd, elk met specifieke kenmerken en hun eigen plaats in Hallo werkstroom levenscyclus:</span><span class="sxs-lookup"><span data-stu-id="7a832-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="7a832-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="7a832-490">**commandScript**</span></span>
* <span data-ttu-id="7a832-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="7a832-491">**realizeScript**</span></span>
* <span data-ttu-id="7a832-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="7a832-492">**processInputScript**</span></span>
* <span data-ttu-id="7a832-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="7a832-493">**lifeCycleScript**</span></span>

<span data-ttu-id="7a832-494">Hallo documentatie Hallo onderdeel in een script vastgelegd gaat in meer detail voor elk van de bovenstaande Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a832-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="7a832-495">In [Hallo volgende sectie](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), Hallo **realizeScript** scripting onderdeel is gebruikte tooconstruct een cliplist xml op Hallo snel wanneer Hallo werkstroom wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7a832-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="7a832-496">Dit script wordt aangeroepen tijdens setup Hallo onderdelen die slechts één keer wordt uitgevoerd in de levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="7a832-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="7a832-497"><a id="scripting_hello_world"></a>Uitvoeren van scripts in een werkstroom: Hallo wereld</span><span class="sxs-lookup"><span data-stu-id="7a832-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="7a832-498">Sleep een onderdeel in een script vastgelegd naar het ontwerpoppervlak Hallo en wijzig de naam (bijvoorbeeld ' SetClipListXML').</span><span class="sxs-lookup"><span data-stu-id="7a832-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Script onderdelen toevoegen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="7a832-500">*Script onderdelen toevoegen*</span><span class="sxs-lookup"><span data-stu-id="7a832-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="7a832-501">Wanneer u de eigenschappen van Hallo inspecteert Hallo Component in een script vastgelegd, Hallo vier verschillende scripttypen worden weergegeven, elk ander configureerbare tooa-script.</span><span class="sxs-lookup"><span data-stu-id="7a832-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Eigenschappen van scripts](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="7a832-503">*Eigenschappen van scripts*</span><span class="sxs-lookup"><span data-stu-id="7a832-503">*Scripted Component properties*</span></span>

<span data-ttu-id="7a832-504">Wissen Hallo processInputScript en open de editor voor Hallo realizeScript Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a832-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="7a832-505">Nu we alles hebt ingesteld en klaar toostart scripting.</span><span class="sxs-lookup"><span data-stu-id="7a832-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="7a832-506">Scripts worden geschreven in Groovy, een dynamisch gecompileerde scripttaal voor Hallo Java-platform die compatibel is met Java behoudt.</span><span class="sxs-lookup"><span data-stu-id="7a832-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="7a832-507">De meeste Java-code is daadwerkelijk, geldige Groovy code.</span><span class="sxs-lookup"><span data-stu-id="7a832-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="7a832-508">We gaan een eenvoudige hello world groovy script schrijven in de context van onze realizeScript Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a832-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="7a832-509">Voer Hallo volgende in Hallo-editor:</span><span class="sxs-lookup"><span data-stu-id="7a832-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="7a832-510">Een lokale testuitvoering nu uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7a832-510">Now execute a local test run.</span></span> <span data-ttu-id="7a832-511">Controleer na het uitvoeren (via het tabblad voor het systeem op Hallo Hallo onderdeel in een script vastgelegd) Hallo logboeken-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="7a832-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Hello world logboekuitvoer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="7a832-513">*Hello world logboekuitvoer*</span><span class="sxs-lookup"><span data-stu-id="7a832-513">*Hello world log output*</span></span>

<span data-ttu-id="7a832-514">Hallo knooppuntobject we Hallo logboek methode niet aanroepen voor, verwijst tooour huidige 'knooppunt' of we je scripting binnen Hallo-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="7a832-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="7a832-515">Elk onderdeel heeft als zodanig Hallo mogelijkheid toooutput logboekgegevens, beschikbaar via het tabblad Hallo-systeem. In dit geval uitvoer we Hallo string literal "Hallo wereld".</span><span class="sxs-lookup"><span data-stu-id="7a832-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="7a832-516">Belangrijke toounderstand hier is dat dit toobe een foutopsporing waardevol hulpmiddel bewijzen kan, zonder dat u inzicht in welke script Hallo daadwerkelijk doet.</span><span class="sxs-lookup"><span data-stu-id="7a832-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="7a832-517">Van in onze scriptomgeving hebben we ook toegang tooproperties van andere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="7a832-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="7a832-518">Probeer dit:</span><span class="sxs-lookup"><span data-stu-id="7a832-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="7a832-519">Onze logboekvenster weergeven ons hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="7a832-519">Our log window will show us hello following:</span></span>

![De uitvoer voor toegang tot de Knooppuntpaden](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="7a832-521">*De uitvoer voor toegang tot de Knooppuntpaden*</span><span class="sxs-lookup"><span data-stu-id="7a832-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="7a832-522"><a id="frame_based_trim"></a>Op basis van het frame worden ingekort door multibitrate MP4-uitvoer</span><span class="sxs-lookup"><span data-stu-id="7a832-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="7a832-523">Een werkstroom die wordt gegenereerd vanaf [een multibitrate MP4-uitvoer van een invoer MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we wordt nu op zoek zijn naar bijsnijden Hallo bronvideo op basis van het frame.</span><span class="sxs-lookup"><span data-stu-id="7a832-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="7a832-524"><a id="frame_based_trim_start"></a>Blauwdruk overzicht toostart bijsnijden aan toe te voegen</span><span class="sxs-lookup"><span data-stu-id="7a832-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![Werkstroom toostart bijsnijden aan toe te voegen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="7a832-526">*Werkstroom toostart bijsnijden aan toe te voegen*</span><span class="sxs-lookup"><span data-stu-id="7a832-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="7a832-527"><a id="frame_based_trim_clip_list"></a>Met behulp van Hallo Clip lijst XML</span><span class="sxs-lookup"><span data-stu-id="7a832-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="7a832-528">In alle vorige werkstroom zelfstudies gebruikt we Hallo Media bestand invoer onderdeel als onze video-invoerbron.</span><span class="sxs-lookup"><span data-stu-id="7a832-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="7a832-529">Voor dit specifieke scenario echter worden gebruikt Hallo Clip lijst brononderdeel in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="7a832-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="7a832-530">Houd er rekening mee dat dit mag geen Hallo voorkeur manier van werken; Hallo Clip lijst bron alleen gebruiken wanneer er een echte reden toodo dus (Hallo hieronder geval waar we doorvoeren, zoals gebruik van Hallo clip lijst bijsnijden mogelijkheden).</span><span class="sxs-lookup"><span data-stu-id="7a832-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="7a832-531">tooswitch van onze Media bestandsinvoer toohello Clip lijst bron, Hallo Clip lijst brononderdeel naar het ontwerpoppervlak Hallo slepen en maak verbinding Hallo Clip lijst XML pincode toohello Clip lijst XML-knooppunt van Hallo workflow designer.</span><span class="sxs-lookup"><span data-stu-id="7a832-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="7a832-532">Dit Hallo Clip lijst bron met uitvoer pincodes, tooour invoervideo op basis van gegevens moet voorzien.</span><span class="sxs-lookup"><span data-stu-id="7a832-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="7a832-533">Hallo niet-gecomprimeerde Video en Audio van niet-gecomprimeerde pincodes nu verbinding te maken van Hallo Hallo Clip lijst bron toohello respectieve AVC coderingsprogramma's en Audio-stroom Interleaver.</span><span class="sxs-lookup"><span data-stu-id="7a832-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="7a832-534">Verwijder nu Hallo Media bestandsinvoer.</span><span class="sxs-lookup"><span data-stu-id="7a832-534">Now remove hello Media File Input.</span></span>

![Hallo Media bestandsinvoer vervangen door Hallo Clip lijst bron](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="7a832-536">*Hallo Media bestandsinvoer vervangen door Hallo Clip lijst bron*</span><span class="sxs-lookup"><span data-stu-id="7a832-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="7a832-537">Hallo Clip lijst brononderdeel neemt als invoer een 'Clip lijst XML'.</span><span class="sxs-lookup"><span data-stu-id="7a832-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="7a832-538">Als u lokaal Hallo bron bestand tootest met, is deze clip lijst xml automatisch ingevuld voor u.</span><span class="sxs-lookup"><span data-stu-id="7a832-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Automatisch ingevuld Clip lijst XML-eigenschap](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="7a832-540">*Automatisch ingevuld Clip lijst XML-eigenschap*</span><span class="sxs-lookup"><span data-stu-id="7a832-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="7a832-541">Zoek een beetje dichter toohello xml, is dit hoe het eruit:</span><span class="sxs-lookup"><span data-stu-id="7a832-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Dialoogvenster met de lijst clip bewerken](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="7a832-543">*Dialoogvenster met de lijst clip bewerken*</span><span class="sxs-lookup"><span data-stu-id="7a832-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="7a832-544">Dit echter doorgevoerd niet Hallo-mogelijkheden van XML-Hallo clip lijst.</span><span class="sxs-lookup"><span data-stu-id="7a832-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="7a832-545">Een optie die we hebben is tooadd een element 'Trim' onder Hallo video en audio-bron, als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a832-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Een lijst van element knippen toohello clip toevoegen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="7a832-547">*Een lijst van element knippen toohello clip toevoegen*</span><span class="sxs-lookup"><span data-stu-id="7a832-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="7a832-548">Als u XML-lijst van Hallo-clip als volgt hierboven wijzigen en uitvoeren van een lokale test uitgevoerd, ziet u Hallo video correct zijn afgekapt tussen 10 en 20 seconden in Hallo video.</span><span class="sxs-lookup"><span data-stu-id="7a832-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="7a832-549">Strijdig toowhat gebeurt wanneer u een lokale uitvoering doen, hoewel deze zeer dezelfde cliplist xml geen Hallo hetzelfde effect als toegepast in een werkstroom die wordt uitgevoerd in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="7a832-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="7a832-550">Wanneer Azure Premium-codering wordt gestart, Hallo cliplist xml wordt gegenereerd telkens opnieuw op basis van het Hallo invoerbestand Hallo codering is taak opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7a832-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="7a832-551">Dit betekent dat eventuele wijzigingen die we op Hallo xml doen helaas zou worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="7a832-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="7a832-552">toocounter hello cliplist xml wordt gewist wanneer een codeertaak wordt gestart, we kunt opnieuw gegenereerd op Hallo snel direct na Hallo begin van de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="7a832-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="7a832-553">Deze aangepaste acties kunnen worden uitgevoerd via wat een 'in een script vastgelegd onderdeel' wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="7a832-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="7a832-554">Zie voor meer informatie [Introducing hello onderdeel in een script vastgelegd](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="7a832-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="7a832-555">Sleep een onderdeel in een script vastgelegd naar het ontwerpoppervlak Hallo en wijzig deze te 'SetClipListXML'.</span><span class="sxs-lookup"><span data-stu-id="7a832-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Script onderdelen toevoegen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="7a832-557">*Script onderdelen toevoegen*</span><span class="sxs-lookup"><span data-stu-id="7a832-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="7a832-558">Wanneer u de eigenschappen van Hallo inspecteert Hallo Component in een script vastgelegd, Hallo vier verschillende scripttypen worden weergegeven, elk ander configureerbare tooa-script.</span><span class="sxs-lookup"><span data-stu-id="7a832-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Eigenschappen van scripts](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="7a832-560">*Eigenschappen van scripts*</span><span class="sxs-lookup"><span data-stu-id="7a832-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="7a832-561"><a id="frame_based_trim_modify_clip_list"></a>Hallo clip lijst van een onderdeel in een script vastgelegd wijzigen</span><span class="sxs-lookup"><span data-stu-id="7a832-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="7a832-562">Voordat we Hallo cliplist XML-bestand dat wordt gegenereerd tijdens het opstarten van de werkstroom opnieuw schrijven kunt, moeten we toohave access toohello cliplist xml-eigenschap en de inhoud.</span><span class="sxs-lookup"><span data-stu-id="7a832-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="7a832-563">We kunnen dit doen als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a832-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Binnenkomende clip lijst aan te melden](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="7a832-565">*Binnenkomende clip lijst aan te melden*</span><span class="sxs-lookup"><span data-stu-id="7a832-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="7a832-566">Eerst moet u een manier toodetermine vanaf dat moment tot dat moment we tootrim willen Hallo video.</span><span class="sxs-lookup"><span data-stu-id="7a832-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="7a832-567">toomake deze handige toohello minder technische gebruiker van de werkstroom hello, publiceren twee eigenschappen toohello root van Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="7a832-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="7a832-568">toodo dit ontwerpoppervlak Hallo Klik met de rechtermuisknop en selecteer 'Eigenschap toevoegen':</span><span class="sxs-lookup"><span data-stu-id="7a832-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="7a832-569">Eerste eigenschap: 'ClippingTimeStart' van het type: 'TIJDCODE'</span><span class="sxs-lookup"><span data-stu-id="7a832-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="7a832-570">Tweede eigenschap: 'ClippingTimeEnd' van het type: 'TIJDCODE'</span><span class="sxs-lookup"><span data-stu-id="7a832-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Dialoogvenster van eigenschappen toevoegen voor de begintijd knippen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="7a832-572">*Dialoogvenster van eigenschappen toevoegen voor de begintijd knippen*</span><span class="sxs-lookup"><span data-stu-id="7a832-572">*Add Property dialog for clipping start time*</span></span>

![Gepubliceerde eigenschappen van de tijd knipsel in de hoofdmap van de werkstroom van](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="7a832-574">*Gepubliceerde eigenschappen van de tijd knipsel in de hoofdmap van de werkstroom van*</span><span class="sxs-lookup"><span data-stu-id="7a832-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="7a832-575">Beide eigenschappen tooa geschikte waarde configureren:</span><span class="sxs-lookup"><span data-stu-id="7a832-575">Configure both properties tooa suitable value:</span></span>

![Hallo knipsel begin- en eigenschappen configureren](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="7a832-577">*Hallo knipsel begin- en eigenschappen configureren*</span><span class="sxs-lookup"><span data-stu-id="7a832-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="7a832-578">Nu uit in onze script we hebben toegang tot beide eigenschappen, als volgt:</span><span class="sxs-lookup"><span data-stu-id="7a832-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Venster van het logboek met begin en einde van knippen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="7a832-580">*Venster van het logboek met begin en einde van knippen*</span><span class="sxs-lookup"><span data-stu-id="7a832-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="7a832-581">Laten we parseren Hallo tijdcode tekenreeksen in een handiger toouse formulier, met behulp van een eenvoudige reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="7a832-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Het venster met de uitvoer van de geparseerde tijdcode](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="7a832-583">*Het venster met de uitvoer van de geparseerde tijdcode*</span><span class="sxs-lookup"><span data-stu-id="7a832-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="7a832-584">Met deze informatie bij de hand we nu Hallo cliplist xml tooreflect Hallo start kunt wijzigen en eindtijden voor Hallo frame nauwkeurige paginaknipsel van Hallo film gewenst.</span><span class="sxs-lookup"><span data-stu-id="7a832-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Script code tooadd trim-elementen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="7a832-586">*Script code tooadd trim-elementen*</span><span class="sxs-lookup"><span data-stu-id="7a832-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="7a832-587">Dit is gedaan door de normale tekenreeks bestandsbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="7a832-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="7a832-588">Hallo resulterende gewijzigde illustratie lijst xml teruggeschreven toohello clipListXML-eigenschap op basis van Hallo-werkstroom via de methode 'setProperty' Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a832-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="7a832-589">Hallo logboekvenster na het uitvoeren van een andere test zou ons Hallo volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7a832-589">hello log window after another test run would show us hello following:</span></span>

![Hallo resulterende clip lijst logboekregistratie](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="7a832-591">*Hallo resulterende clip lijst logboekregistratie*</span><span class="sxs-lookup"><span data-stu-id="7a832-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="7a832-592">Voer een test uitgevoerd toosee hoe Hallo video en audio-stromen hebben is afgekapt.</span><span class="sxs-lookup"><span data-stu-id="7a832-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="7a832-593">Als u meer dan één testuitvoering met verschillende waarden voor Hallo bijsnijden punten doet, ziet u dat deze wordt geen rekening worden gehouden echter!</span><span class="sxs-lookup"><span data-stu-id="7a832-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="7a832-594">Hallo reden hiervoor is dat designer hello, in tegenstelling tot hello Azure runtime, niet overschrijven Hallo cliplist xml elke gebeurt.</span><span class="sxs-lookup"><span data-stu-id="7a832-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="7a832-595">Dit betekent dat alleen hello zeer eerste keer dat u hebt ingesteld Hallo in en uit punten zullen Hallo xml tootransform, alle andere tijden onze component guard Hallo (als (clipListXML.indexOf ('<trim>') == van -1)) verhindert dat Hallo werkstroom toe te voegen op een andere knippen element als er al een aanwezig.</span><span class="sxs-lookup"><span data-stu-id="7a832-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="7a832-596">toomake onze werkstroom handige tootest lokaal we best house-keeping code die als een beperkende element aanwezig was inspecteert toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a832-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="7a832-597">Als dit het geval is, kunnen we deze verwijderen voordat u doorgaat doordat Hallo xml met Hallo nieuwe waarden.</span><span class="sxs-lookup"><span data-stu-id="7a832-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="7a832-598">In plaats van gewone tekenreeksmanipulatie, is het waarschijnlijk veiliger toodo dit via echte xml-object model parseren.</span><span class="sxs-lookup"><span data-stu-id="7a832-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="7a832-599">Voordat we deze code toebehoort echter toevoegen kunt, moeten we een aantal importinstructies op Hallo eerst van onze script starten tooadd:</span><span class="sxs-lookup"><span data-stu-id="7a832-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="7a832-600">Hierna kunt we Hallo vereist reinigen code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7a832-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="7a832-601">Deze code gaat erboven Hallo punt waarop we Hallo trim elementen toohello cliplist xml toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7a832-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="7a832-602">We kunnen op dit moment worden uitgevoerd en onze werkstroom zoals net als we willen dat bij dat Hallo wijzigingen toegepast ooit tijd wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7a832-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="7a832-603"><a id="frame_based_trim_clippingenabled_prop"></a>De eigenschap van een ClippingEnabled gemak toe te voegen</span><span class="sxs-lookup"><span data-stu-id="7a832-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="7a832-604">Als u wilt u mogelijk niet altijd bijsnijden toohappen, gaan we voltooien uit onze werkstroom door toe te voegen een handige Booleaanse vlag die aangeeft of we wilt tooenable knippen / knipsel.</span><span class="sxs-lookup"><span data-stu-id="7a832-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="7a832-605">Publiceren voordat u, net zoals een nieuwe eigenschap toohello basis van onze werkstroom aangeroepen 'ClippingEnabled' van het type 'BOOLEAN'.</span><span class="sxs-lookup"><span data-stu-id="7a832-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Een eigenschap voor het inschakelen van knipsel gepubliceerd](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="7a832-607">*Een eigenschap voor het inschakelen van knipsel gepubliceerd*</span><span class="sxs-lookup"><span data-stu-id="7a832-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="7a832-608">Met Hallo hieronder eenvoudige guard component, kunnen we controleren of bijsnijden vereist is en beslissen of u onze lijst clip toobe gewijzigd of niet als zodanig moet.</span><span class="sxs-lookup"><span data-stu-id="7a832-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="7a832-609"><a id="code"></a>Volledige code</span><span class="sxs-lookup"><span data-stu-id="7a832-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="7a832-610">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7a832-610">Also see</span></span>
[<span data-ttu-id="7a832-611">Inleiding tot Premium codering in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="7a832-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="7a832-612">Hoe tooUse Premium codering in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="7a832-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="7a832-613">Codering van inhoud op aanvraag met Azure mediaservice</span><span class="sxs-lookup"><span data-stu-id="7a832-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="7a832-614">Indelingen en codecs voor Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="7a832-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="7a832-615">Werkstroom voorbeeldbestanden</span><span class="sxs-lookup"><span data-stu-id="7a832-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="7a832-616">Azure Media Services Explorer-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="7a832-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="7a832-617">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="7a832-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7a832-618">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="7a832-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
