---
title: aaaRedact vlakken met Azure Media Analytics | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooredact bespreekt met Azure media analytics.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="c0fbd-103">Redigeren vlakken met Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="c0fbd-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="c0fbd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c0fbd-104">Overview</span></span>
<span data-ttu-id="c0fbd-105">**Azure Media Redactor** is een [Azure Media Analytics](media-services-analytics-overview.md) Mediaprocessor (MP) die schaalbare face redactie in Hallo cloud biedt.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="c0fbd-106">Face redactie kunt u toomodify uw video in volgorde tooblur vlakken van geselecteerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="c0fbd-107">U kunt toouse Hallo face redactie service in openbare veiligheid en nieuws media scenario's.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="c0fbd-108">Een paar minuten beeldmateriaal waarin meerdere vlakken handmatig tooredact uur kunnen duren, maar met deze service Hallo face redactie proces een paar eenvoudige stappen is vereist.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="c0fbd-109">Zie voor meer informatie [dit](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="c0fbd-110">Dit onderwerp bevat informatie over **Azure Media Redactor** en ziet u hoe toouse met Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="c0fbd-111">Hallo **Azure Media Redactor** MP is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="c0fbd-112">Is beschikbaar in alle openbare Azure-regio's, evenals US Government en China datacenters.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="c0fbd-113">Dit voorbeeld is momenteel gratis.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="c0fbd-114">Face redactie modi</span><span class="sxs-lookup"><span data-stu-id="c0fbd-114">Face redaction modes</span></span>
<span data-ttu-id="c0fbd-115">Analyseert redactie werkt door vlakken opsporen in elke frame van video en bij te houden Hallo face object beide voorwaarts en achterwaarts in de tijd, zodat hello dezelfde persoon kan worden vervaagd vanuit andere hoeken ook.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="c0fbd-116">Hallo geautomatiseerde redactie proces is zeer complex en 100% van de gewenste uitvoer geen altijd om deze reden die Media Analytics u over een aantal manieren toomodify Hallo uiteindelijke uitvoer beschikt produceert.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="c0fbd-117">In de toevoeging tooa volledig automatische modus is er een werkstroom twee keer waarmee Hallo selectie/de-selection gevonden vlakken via een lijst met id.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="c0fbd-118">Bovendien toomake willekeurige per frame aanpassingen Hallo MP maakt gebruik van een bestand met metagegevens in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="c0fbd-119">Deze werkstroom is onderverdeeld in **analyseren** en **Redact** modi.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="c0fbd-120">U kunt de twee modi Hallo in één iteratie die beide taken in één taak uitvoert; combineren Deze modus wordt aangeroepen **gecombineerde**.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="c0fbd-121">Gecombineerde modus</span><span class="sxs-lookup"><span data-stu-id="c0fbd-121">Combined mode</span></span>
<span data-ttu-id="c0fbd-122">Het resultaat is een geredigeerde mp4 automatisch zonder handmatige invoer.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="c0fbd-123">Fase</span><span class="sxs-lookup"><span data-stu-id="c0fbd-123">Stage</span></span> | <span data-ttu-id="c0fbd-124">Bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="c0fbd-124">File Name</span></span> | <span data-ttu-id="c0fbd-125">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c0fbd-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0fbd-126">Invoer asset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-126">Input asset</span></span> |<span data-ttu-id="c0fbd-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="c0fbd-127">foo.bar</span></span> |<span data-ttu-id="c0fbd-128">Video in WMV, MOV of MP4-indeling</span><span class="sxs-lookup"><span data-stu-id="c0fbd-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="c0fbd-129">Invoer config</span><span class="sxs-lookup"><span data-stu-id="c0fbd-129">Input config</span></span> |<span data-ttu-id="c0fbd-130">De configuratie van definitie</span><span class="sxs-lookup"><span data-stu-id="c0fbd-130">Job configuration preset</span></span> |<span data-ttu-id="c0fbd-131">{{'version':'1.0 ","opties": {'mode': 'gecombineerd'}}</span><span class="sxs-lookup"><span data-stu-id="c0fbd-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="c0fbd-132">Uitvoerasset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-132">Output asset</span></span> |<span data-ttu-id="c0fbd-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="c0fbd-133">foo_redacted.mp4</span></span> |<span data-ttu-id="c0fbd-134">Video met zorgt voor een vervaging toegepast</span><span class="sxs-lookup"><span data-stu-id="c0fbd-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="c0fbd-135">Voorbeeld van invoer:</span><span class="sxs-lookup"><span data-stu-id="c0fbd-135">Input example:</span></span>
[<span data-ttu-id="c0fbd-136">Bekijk deze video</span><span class="sxs-lookup"><span data-stu-id="c0fbd-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="c0fbd-137">Voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c0fbd-137">Output example:</span></span>
[<span data-ttu-id="c0fbd-138">Bekijk deze video</span><span class="sxs-lookup"><span data-stu-id="c0fbd-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="c0fbd-139">Modus analyseren</span><span class="sxs-lookup"><span data-stu-id="c0fbd-139">Analyze mode</span></span>
<span data-ttu-id="c0fbd-140">Hallo **analyseren** pass van Hallo twee keer werkstroom neemt een video-invoer en resulteert in een JSON-bestand van face locaties en jpg-afbeeldingen van elke face gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="c0fbd-141">Fase</span><span class="sxs-lookup"><span data-stu-id="c0fbd-141">Stage</span></span> | <span data-ttu-id="c0fbd-142">Bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="c0fbd-142">File Name</span></span> | <span data-ttu-id="c0fbd-143">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c0fbd-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0fbd-144">Invoer asset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-144">Input asset</span></span> |<span data-ttu-id="c0fbd-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="c0fbd-145">foo.bar</span></span> |<span data-ttu-id="c0fbd-146">Video in WMV, MPV of MP4-indeling</span><span class="sxs-lookup"><span data-stu-id="c0fbd-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="c0fbd-147">Invoer config</span><span class="sxs-lookup"><span data-stu-id="c0fbd-147">Input config</span></span> |<span data-ttu-id="c0fbd-148">De configuratie van definitie</span><span class="sxs-lookup"><span data-stu-id="c0fbd-148">Job configuration preset</span></span> |<span data-ttu-id="c0fbd-149">{{'version':'1.0 ","opties": {'mode': 'analyseren'}}</span><span class="sxs-lookup"><span data-stu-id="c0fbd-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="c0fbd-150">Uitvoerasset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-150">Output asset</span></span> |<span data-ttu-id="c0fbd-151">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="c0fbd-151">foo_annotations.json</span></span> |<span data-ttu-id="c0fbd-152">De gegevens van de aantekening van face locaties in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="c0fbd-153">Dit kan worden bewerkt met de Hallo gebruiker toomodify Hallo zorgt voor een vervaging begrenzingsvak vakken.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="c0fbd-154">Zie onderstaand voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-154">See sample below.</span></span> |
| <span data-ttu-id="c0fbd-155">Uitvoerasset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-155">Output asset</span></span> |<span data-ttu-id="c0fbd-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="c0fbd-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="c0fbd-157">Een bijgesneden jpg van elke gezicht, waarbij Hallo Hallo labelId van Hallo gezicht geeft gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="c0fbd-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="c0fbd-158">Voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c0fbd-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="c0fbd-159">Modus Redigeren</span><span class="sxs-lookup"><span data-stu-id="c0fbd-159">Redact mode</span></span>
<span data-ttu-id="c0fbd-160">tweede stap van de werkstroom Hallo Hallo duurt een groter aantal invoerwaarden die moeten worden samengevoegd in één element.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="c0fbd-161">Dit omvat een lijst met id's tooblur Hallo oorspronkelijke video en Hallo aantekeningen JSON.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="c0fbd-162">Deze modus gebruikt Hallo aantekeningen tooapply vervaging op Hallo invoervideo.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="c0fbd-163">Hallo omvat uitvoer van Hallo analyseren pass geen Hallo oorspronkelijke video.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="c0fbd-164">Hallo video moet toobe geüpload naar de invoer asset Hallo voor Hallo Redact modus taak en geselecteerd als primaire Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="c0fbd-165">Fase</span><span class="sxs-lookup"><span data-stu-id="c0fbd-165">Stage</span></span> | <span data-ttu-id="c0fbd-166">Bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="c0fbd-166">File Name</span></span> | <span data-ttu-id="c0fbd-167">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c0fbd-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0fbd-168">Invoer asset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-168">Input asset</span></span> |<span data-ttu-id="c0fbd-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="c0fbd-169">foo.bar</span></span> |<span data-ttu-id="c0fbd-170">Video WMV, MPV of MP4-indeling.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="c0fbd-171">Hetzelfde als in stap 1 video.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="c0fbd-172">Invoer asset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-172">Input asset</span></span> |<span data-ttu-id="c0fbd-173">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="c0fbd-173">foo_annotations.json</span></span> |<span data-ttu-id="c0fbd-174">metagegevensbestand aantekeningen uit stap 1, optionele wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="c0fbd-175">Invoer asset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-175">Input asset</span></span> |<span data-ttu-id="c0fbd-176">foo_IDList.txt (optioneel)</span><span class="sxs-lookup"><span data-stu-id="c0fbd-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="c0fbd-177">Optionele nieuwe regel gescheiden lijst van id's tooredact gezicht.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="c0fbd-178">Als dit leeg laat, vervaging dit alle vlakken.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="c0fbd-179">Invoer config</span><span class="sxs-lookup"><span data-stu-id="c0fbd-179">Input config</span></span> |<span data-ttu-id="c0fbd-180">De configuratie van definitie</span><span class="sxs-lookup"><span data-stu-id="c0fbd-180">Job configuration preset</span></span> |<span data-ttu-id="c0fbd-181">{{'version':'1.0 ","opties": {'mode': 'Redigeren'}}</span><span class="sxs-lookup"><span data-stu-id="c0fbd-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="c0fbd-182">Uitvoerasset</span><span class="sxs-lookup"><span data-stu-id="c0fbd-182">Output asset</span></span> |<span data-ttu-id="c0fbd-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="c0fbd-183">foo_redacted.mp4</span></span> |<span data-ttu-id="c0fbd-184">Video met zorgt voor een vervaging toegepast op basis van aantekeningen</span><span class="sxs-lookup"><span data-stu-id="c0fbd-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="c0fbd-185">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="c0fbd-185">Example output</span></span>
<span data-ttu-id="c0fbd-186">Dit is Hallo-uitvoer van een IDList met een ID die geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="c0fbd-187">Bekijk deze video</span><span class="sxs-lookup"><span data-stu-id="c0fbd-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="c0fbd-188">Voorbeeld foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="c0fbd-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="c0fbd-189">Typen vervagen</span><span class="sxs-lookup"><span data-stu-id="c0fbd-189">Blur types</span></span>

<span data-ttu-id="c0fbd-190">In Hallo **gecombineerde** of **Redact** modus, er zijn 5 vervaging verschillende modi u uit via Hallo JSON-invoer configuratie kiezen kunt: **laag**, **Med**, **Hoge**, **Debug**, en **zwart**.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="c0fbd-191">Standaard **Med** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-191">By default **Med** is used.</span></span>

<span data-ttu-id="c0fbd-192">Vindt u voorbeelden van Hallo vervagen hieronder typen.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="c0fbd-193">Voorbeeld JSON:</span><span class="sxs-lookup"><span data-stu-id="c0fbd-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="c0fbd-194">Laag</span><span class="sxs-lookup"><span data-stu-id="c0fbd-194">Low</span></span>

![Laag](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="c0fbd-196">Med</span><span class="sxs-lookup"><span data-stu-id="c0fbd-196">Med</span></span>

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="c0fbd-198">Hoog</span><span class="sxs-lookup"><span data-stu-id="c0fbd-198">High</span></span>

![Hoog](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="c0fbd-200">Fouten opsporen</span><span class="sxs-lookup"><span data-stu-id="c0fbd-200">Debug</span></span>

![Fouten opsporen](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="c0fbd-202">Zwart</span><span class="sxs-lookup"><span data-stu-id="c0fbd-202">Black</span></span>

![Zwart](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="c0fbd-204">Elementen van Hallo uitvoer JSON-bestand</span><span class="sxs-lookup"><span data-stu-id="c0fbd-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="c0fbd-205">Hallo redactie MP biedt hoge precisie face locatie detectie en bijhouden die up too64 menselijke vlakken in een video frame kan detecteren.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="c0fbd-206">Voorzijde vlakken bieden de beste resultaten Hallo tijdens vlakken kant- en kleine vlakken (minder dan of gelijk zijn aan too24x24 pixels) lastig zijn.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="c0fbd-207">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="c0fbd-207">.NET sample code</span></span>

<span data-ttu-id="c0fbd-208">Hallo volgende programma toont hoe:</span><span class="sxs-lookup"><span data-stu-id="c0fbd-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="c0fbd-209">Maak een asset en upload een mediabestand naar Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="c0fbd-210">Een taak maken met een face redactie taak op basis van een configuratiebestand met Hallo json-definitie te volgen.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="c0fbd-211">Hallo uitvoer JSON-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c0fbd-212">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="c0fbd-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c0fbd-213">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c0fbd-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="c0fbd-214">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c0fbd-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
            ErrorDetail error = job.Tasks.First().ErrorDetails.First();
            Console.WriteLine(string.Format("Error: {0}. {1}",
                            error.Code,
                            error.Message));
            return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
            file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

        static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                   mediaProcessorName));

            return processor;
        }

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished.");
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                // LogJobStop(job.Id);
                break;
            default:
                break;
            }
        }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="c0fbd-215">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0fbd-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c0fbd-216">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="c0fbd-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c0fbd-217">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="c0fbd-217">Related links</span></span>
[<span data-ttu-id="c0fbd-218">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="c0fbd-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c0fbd-219">Azure Media Analytics-demo 's</span><span class="sxs-lookup"><span data-stu-id="c0fbd-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

