---
title: aaaDetect bewegingen met Azure Media Analytics | Microsoft Docs
description: Hallo Azure Media beweging detectie media processor (MP) kunt u tooefficiently secties van belang zijn binnen een video anders lang en probleemloze identificeren.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="c25a3-103">Bewegingen met Azure Media Analytics detecteren</span><span class="sxs-lookup"><span data-stu-id="c25a3-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="c25a3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c25a3-104">Overview</span></span>
<span data-ttu-id="c25a3-105">Hallo **Azure Media beweging detectie** media processor (MP) kunt u tooefficiently secties van belang zijn binnen een video anders lang en probleemloze identificeren.</span><span class="sxs-lookup"><span data-stu-id="c25a3-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="c25a3-106">Bewegingsdetectie kan worden gebruikt voor statische camera beeldmateriaal tooidentify secties van Hallo video waar beweging optreedt.</span><span class="sxs-lookup"><span data-stu-id="c25a3-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="c25a3-107">Er wordt een JSON-bestand met een metagegevens met tijdstempels en de regio waar Hallo gebeurtenis heeft plaatsgevonden voor begrenzingsvak Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c25a3-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="c25a3-108">Gericht op beveiliging video feeds, is deze technologie kunnen toocategorize beweging in de relevante gebeurtenissen en fout-positieven zoals schaduwen en licht wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="c25a3-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="c25a3-109">Hiermee kunt u toogenerate beveiligingswaarschuwingen van de camera feeds zonder terwijl tooextract kunnen momenten van belang van zeer lange toezicht video's met oneindige irrelevante gebeurtenissen, spam.</span><span class="sxs-lookup"><span data-stu-id="c25a3-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="c25a3-110">Hallo **Azure Media beweging detectie** MP is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="c25a3-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="c25a3-111">Dit onderwerp bevat informatie over **Azure Media beweging detectie** en ziet u hoe toouse met Media Services SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="c25a3-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="c25a3-112">Beweging detectie invoerbestanden</span><span class="sxs-lookup"><span data-stu-id="c25a3-112">Motion Detector input files</span></span>
<span data-ttu-id="c25a3-113">Videobestanden.</span><span class="sxs-lookup"><span data-stu-id="c25a3-113">Video files.</span></span> <span data-ttu-id="c25a3-114">Op dit moment Hallo volgende indelingen worden ondersteund: MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="c25a3-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="c25a3-115">Taken configureren (standaardoptie)</span><span class="sxs-lookup"><span data-stu-id="c25a3-115">Task configuration (preset)</span></span>
<span data-ttu-id="c25a3-116">Bij het maken van een taak met **Azure Media beweging detectie**, moet u een configuratie-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="c25a3-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c25a3-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="c25a3-117">Parameters</span></span>
<span data-ttu-id="c25a3-118">U kunt Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="c25a3-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="c25a3-119">Naam</span><span class="sxs-lookup"><span data-stu-id="c25a3-119">Name</span></span> | <span data-ttu-id="c25a3-120">Opties</span><span class="sxs-lookup"><span data-stu-id="c25a3-120">Options</span></span> | <span data-ttu-id="c25a3-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c25a3-121">Description</span></span> | <span data-ttu-id="c25a3-122">Standaard</span><span class="sxs-lookup"><span data-stu-id="c25a3-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c25a3-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="c25a3-123">sensitivityLevel</span></span> |<span data-ttu-id="c25a3-124">Tekenreeks: 'laag', 'Gemiddeld', 'hoog'</span><span class="sxs-lookup"><span data-stu-id="c25a3-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="c25a3-125">Hiermee stelt Hallo gevoeligheid niveau op welke bewegingen wordt gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="c25a3-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="c25a3-126">Deze fout-positieven tooadjust hoeveelheid aanpassen.</span><span class="sxs-lookup"><span data-stu-id="c25a3-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="c25a3-127">'Gemiddeld'</span><span class="sxs-lookup"><span data-stu-id="c25a3-127">'medium'</span></span> |
| <span data-ttu-id="c25a3-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="c25a3-128">frameSamplingValue</span></span> |<span data-ttu-id="c25a3-129">Positief geheel getal</span><span class="sxs-lookup"><span data-stu-id="c25a3-129">Positive integer</span></span> |<span data-ttu-id="c25a3-130">Hiermee stelt u Hallo frequentie op waaronder de algoritme wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c25a3-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="c25a3-131">elk frame gelijk aan-1, 2 betekent dat elke 2e frame, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c25a3-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="c25a3-132">1</span><span class="sxs-lookup"><span data-stu-id="c25a3-132">1</span></span> |
| <span data-ttu-id="c25a3-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="c25a3-133">detectLightChange</span></span> |<span data-ttu-id="c25a3-134">Boolean-waarde: 'true', 'onwaar'</span><span class="sxs-lookup"><span data-stu-id="c25a3-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="c25a3-135">Hiermee wordt ingesteld of lichte wijzigingen worden gerapporteerd in Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="c25a3-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="c25a3-136">'False'</span><span class="sxs-lookup"><span data-stu-id="c25a3-136">'False'</span></span> |
| <span data-ttu-id="c25a3-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="c25a3-137">mergeTimeThreshold</span></span> |<span data-ttu-id="c25a3-138">Tijd voor xs:: Mm: ss</span><span class="sxs-lookup"><span data-stu-id="c25a3-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="c25a3-139">Voorbeeld: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="c25a3-139">Example: 00:00:03</span></span> |<span data-ttu-id="c25a3-140">Hiermee geeft u het tijdvenster Hallo tussen beweging gebeurtenissen waarbij 2 gebeurtenissen wordt gecombineerd en gerapporteerd als 1.</span><span class="sxs-lookup"><span data-stu-id="c25a3-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="c25a3-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="c25a3-141">00:00:00</span></span> |
| <span data-ttu-id="c25a3-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="c25a3-142">detectionZones</span></span> |<span data-ttu-id="c25a3-143">Een matrix van zones voor detectie:</span><span class="sxs-lookup"><span data-stu-id="c25a3-143">An array of detection zones:</span></span><br/><span data-ttu-id="c25a3-144">-Zone detectie is een matrix met punten 3 of meer</span><span class="sxs-lookup"><span data-stu-id="c25a3-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="c25a3-145">-Punt is een x en y van 0 too1 coördinaat.</span><span class="sxs-lookup"><span data-stu-id="c25a3-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="c25a3-146">Hierin wordt beschreven Hallo lijst met detectie van veelhoekige zones toobe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c25a3-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="c25a3-147">Resultaten met Hallo zones worden vermeld als een ID, eerst een wordt 'id' Hello: 0</span><span class="sxs-lookup"><span data-stu-id="c25a3-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="c25a3-148">Enkele zone die de hele frame Hallo dekt.</span><span class="sxs-lookup"><span data-stu-id="c25a3-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="c25a3-149">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c25a3-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="c25a3-150">Beweging detectie uitvoerbestanden</span><span class="sxs-lookup"><span data-stu-id="c25a3-150">Motion Detector output files</span></span>
<span data-ttu-id="c25a3-151">Een motion detection-taak retourneren een JSON-bestand in Hallo uitvoerasset waarin Hallo beweging waarschuwingen en hun categorieën, binnen Hallo video worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="c25a3-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="c25a3-152">Hallo-bestand bevat informatie over het Hallo-tijd en de duur van gedetecteerd in Hallo video motion.</span><span class="sxs-lookup"><span data-stu-id="c25a3-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="c25a3-153">Hallo beweging detectie API biedt indicatoren zodra er objecten in beweging in een vaste achtergrond video (bijvoorbeeld een toezicht video zijn).</span><span class="sxs-lookup"><span data-stu-id="c25a3-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="c25a3-154">Hallo beweging detectie is getraind tooreduce gegeven, zoals licht en wijzigingen van de schaduwkopie.</span><span class="sxs-lookup"><span data-stu-id="c25a3-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="c25a3-155">Huidige beperkingen van Hallo algoritmen zijn nacht visie video's, semi-transparante objecten en kleine objecten.</span><span class="sxs-lookup"><span data-stu-id="c25a3-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="c25a3-156"><a id="output_elements"></a>Elementen van Hallo uitvoer JSON-bestand</span><span class="sxs-lookup"><span data-stu-id="c25a3-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="c25a3-157">In de meest recente release Hallo Hallo uitvoer JSON-indeling is gewijzigd en een belangrijke wijziging voor sommige klanten kan vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="c25a3-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="c25a3-158">Hallo beschrijft volgende tabel de elementen van Hallo uitvoer JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="c25a3-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="c25a3-159">Element</span><span class="sxs-lookup"><span data-stu-id="c25a3-159">Element</span></span> | <span data-ttu-id="c25a3-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c25a3-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c25a3-161">Versie</span><span class="sxs-lookup"><span data-stu-id="c25a3-161">Version</span></span> |<span data-ttu-id="c25a3-162">Dit verwijst toohello versie Hallo Video API.</span><span class="sxs-lookup"><span data-stu-id="c25a3-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="c25a3-163">Er is een fout opgetreden in de huidige versie Hallo 2.</span><span class="sxs-lookup"><span data-stu-id="c25a3-163">hello current version is 2.</span></span> |
| <span data-ttu-id="c25a3-164">Tijdschaal</span><span class="sxs-lookup"><span data-stu-id="c25a3-164">Timescale</span></span> |<span data-ttu-id="c25a3-165">'Maatstreepjes' per seconde van Hallo video.</span><span class="sxs-lookup"><span data-stu-id="c25a3-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="c25a3-166">Offset</span><span class="sxs-lookup"><span data-stu-id="c25a3-166">Offset</span></span> |<span data-ttu-id="c25a3-167">Hallo tijdverschil voor tijdstempels in 'maatstreepjes'.</span><span class="sxs-lookup"><span data-stu-id="c25a3-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="c25a3-168">Versie 1.0 van Video-API's, zal dit altijd 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="c25a3-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="c25a3-169">In de toekomst scenario's die wordt ondersteund, deze waarde kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c25a3-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="c25a3-170">framesnelheid</span><span class="sxs-lookup"><span data-stu-id="c25a3-170">Framerate</span></span> |<span data-ttu-id="c25a3-171">Frames per seconde van Hallo video.</span><span class="sxs-lookup"><span data-stu-id="c25a3-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="c25a3-172">Breedte, hoogte</span><span class="sxs-lookup"><span data-stu-id="c25a3-172">Width, Height</span></span> |<span data-ttu-id="c25a3-173">Verwijst toohello breedte en hoogte van Hallo video in pixels.</span><span class="sxs-lookup"><span data-stu-id="c25a3-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="c25a3-174">Starten</span><span class="sxs-lookup"><span data-stu-id="c25a3-174">Start</span></span> |<span data-ttu-id="c25a3-175">Hallo start tijdstempel in 'maatstreepjes'.</span><span class="sxs-lookup"><span data-stu-id="c25a3-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="c25a3-176">Duur</span><span class="sxs-lookup"><span data-stu-id="c25a3-176">Duration</span></span> |<span data-ttu-id="c25a3-177">Hallo-lengte van Hallo-gebeurtenis in 'maatstreepjes'.</span><span class="sxs-lookup"><span data-stu-id="c25a3-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="c25a3-178">Interval</span><span class="sxs-lookup"><span data-stu-id="c25a3-178">Interval</span></span> |<span data-ttu-id="c25a3-179">elk item in het Hallo-gebeurtenis in 'maatstreepjes' Hello tijdsinterval.</span><span class="sxs-lookup"><span data-stu-id="c25a3-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="c25a3-180">Gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c25a3-180">Events</span></span> |<span data-ttu-id="c25a3-181">Elke gebeurtenis fragment bevat Hallo beweging binnen deze tijdsduur gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="c25a3-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="c25a3-182">Type</span><span class="sxs-lookup"><span data-stu-id="c25a3-182">Type</span></span> |<span data-ttu-id="c25a3-183">In de huidige versie hello is dit altijd '2' voor algemene beweging.</span><span class="sxs-lookup"><span data-stu-id="c25a3-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="c25a3-184">Dit label biedt Video-API's Hallo flexibiliteit toocategorize beweging in toekomstige versies.</span><span class="sxs-lookup"><span data-stu-id="c25a3-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="c25a3-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="c25a3-185">RegionID</span></span> |<span data-ttu-id="c25a3-186">Zoals hierboven vermeld, zal dit altijd 0 in deze versie zijn.</span><span class="sxs-lookup"><span data-stu-id="c25a3-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="c25a3-187">Dit label biedt Video API Hallo flexibiliteit toofind beweging in verschillende regio's in toekomstige versies.</span><span class="sxs-lookup"><span data-stu-id="c25a3-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="c25a3-188">Regio's</span><span class="sxs-lookup"><span data-stu-id="c25a3-188">Regions</span></span> |<span data-ttu-id="c25a3-189">Gebied van de toohello in uw video waarin u het belangrijkst over beweging verwijst.</span><span class="sxs-lookup"><span data-stu-id="c25a3-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="c25a3-190">-Hallo regio gebied 'id' aangeeft: in deze versie er is slechts één ID 0.</span><span class="sxs-lookup"><span data-stu-id="c25a3-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="c25a3-191">-'type' hello vorm van Hallo regio die u voor beweging interesseren vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c25a3-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="c25a3-192">Op dit moment worden 'rechthoek' en 'veelhoek' ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c25a3-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="c25a3-193">Als u 'rechthoek' hebt opgegeven, heeft Hallo regio dimensies in X, Y, Width en Height.</span><span class="sxs-lookup"><span data-stu-id="c25a3-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="c25a3-194">Hallo X en Y-coördinaten vertegenwoordigen Hallo bovenste linkerkant Xyserver coördinaten van Hallo gebied in een genormaliseerde schaal van 0,0 too1.0.</span><span class="sxs-lookup"><span data-stu-id="c25a3-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="c25a3-195">Hallo breedte en hoogte vertegenwoordigen Hallo grootte van Hallo gebied in een genormaliseerde schaal van 0,0 too1.0.</span><span class="sxs-lookup"><span data-stu-id="c25a3-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="c25a3-196">In de huidige versie hello, zijn X, Y, Width en Height altijd vast op 0, 0 en 1, 1.</span><span class="sxs-lookup"><span data-stu-id="c25a3-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="c25a3-197">Als u 'veelhoek' hebt opgegeven, heeft Hallo regio dimensies in punten.</span><span class="sxs-lookup"><span data-stu-id="c25a3-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="c25a3-198">fragmenten</span><span class="sxs-lookup"><span data-stu-id="c25a3-198">Fragments</span></span> |<span data-ttu-id="c25a3-199">Hallo metagegevens is up chunked in verschillende segmenten fragmenten aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c25a3-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="c25a3-200">Elke fragment bevat een start, duur, Intervalnummer en gebeurtenis(sen).</span><span class="sxs-lookup"><span data-stu-id="c25a3-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="c25a3-201">Een fragment met er zijn geen gebeurtenissen betekent dat er geen beweging is aangetroffen tijdens die begintijd en duur.</span><span class="sxs-lookup"><span data-stu-id="c25a3-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="c25a3-202">[]-Haken</span><span class="sxs-lookup"><span data-stu-id="c25a3-202">Brackets []</span></span> |<span data-ttu-id="c25a3-203">Elke accolade vertegenwoordigt één interval in Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="c25a3-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="c25a3-204">Lege haakjes voor dat interval betekent dat er geen beweging is gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="c25a3-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="c25a3-205">Locaties</span><span class="sxs-lookup"><span data-stu-id="c25a3-205">locations</span></span> |<span data-ttu-id="c25a3-206">Deze nieuwe vermelding onder gebeurtenissen bevat Hallo-locatie waar Hallo beweging zich heeft voorgedaan.</span><span class="sxs-lookup"><span data-stu-id="c25a3-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="c25a3-207">Dit is meer specifieke dan Hallo detectie zones.</span><span class="sxs-lookup"><span data-stu-id="c25a3-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="c25a3-208">Hallo Hier volgt een voorbeeld van een JSON-uitvoer</span><span class="sxs-lookup"><span data-stu-id="c25a3-208">hello following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="c25a3-209">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="c25a3-209">Limitations</span></span>
* <span data-ttu-id="c25a3-210">Hallo ondersteund video-invoerindelingen zijn MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="c25a3-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="c25a3-211">Bewegingsdetectie is geoptimaliseerd voor stilstaan achtergrond video's.</span><span class="sxs-lookup"><span data-stu-id="c25a3-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="c25a3-212">Hallo-algoritme is gericht op het verminderen van gegeven, zoals licht wijzigingen en schaduwen.</span><span class="sxs-lookup"><span data-stu-id="c25a3-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="c25a3-213">Sommige beweging mogelijk niet gedetecteerd vanwege tootechnical uitdagingen; bijvoorbeeld 's avonds visie video's, semi-transparante objecten en kleine objecten.</span><span class="sxs-lookup"><span data-stu-id="c25a3-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="c25a3-214">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="c25a3-214">.NET sample code</span></span>

<span data-ttu-id="c25a3-215">Hallo volgende programma toont hoe:</span><span class="sxs-lookup"><span data-stu-id="c25a3-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="c25a3-216">Maak een asset en upload een mediabestand naar Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="c25a3-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="c25a3-217">Een taak maken met een video motion detection-taak op basis van een configuratiebestand met Hallo json-definitie te volgen.</span><span class="sxs-lookup"><span data-stu-id="c25a3-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="c25a3-218">Hallo uitvoer JSON-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="c25a3-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c25a3-219">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="c25a3-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c25a3-220">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c25a3-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="c25a3-221">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c25a3-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="c25a3-222">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="c25a3-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c25a3-223">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="c25a3-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c25a3-224">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="c25a3-224">Related links</span></span>
[<span data-ttu-id="c25a3-225">Azure Media Services beweging detectie-blog</span><span class="sxs-lookup"><span data-stu-id="c25a3-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="c25a3-226">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="c25a3-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c25a3-227">Azure Media Analytics-demo 's</span><span class="sxs-lookup"><span data-stu-id="c25a3-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

