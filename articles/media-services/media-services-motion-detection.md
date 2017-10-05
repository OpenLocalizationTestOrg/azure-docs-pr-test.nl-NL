---
title: Detecteren bewegingen met Azure Media Analytics | Microsoft Docs
description: "De processor voor Azure Media beweging detectie media (MP) kunt u secties van belang zijn binnen een video anders lang en probleemloze efficiënt te identificeren."
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
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="eac72-103">Bewegingen met Azure Media Analytics detecteren</span><span class="sxs-lookup"><span data-stu-id="eac72-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="eac72-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="eac72-104">Overview</span></span>
<span data-ttu-id="eac72-105">De **Azure Media beweging detectie** Mediaprocessor (MP) kunt u secties van belang zijn binnen een video anders lang en probleemloze efficiënt te identificeren.</span><span class="sxs-lookup"><span data-stu-id="eac72-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="eac72-106">Bewegingsdetectie kan worden gebruikt voor statische camerabeelden identificeren secties van de video waar beweging optreedt.</span><span class="sxs-lookup"><span data-stu-id="eac72-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="eac72-107">Er wordt een JSON-bestand met een metagegevens met tijdstempels en het selectiegebied waarop de gebeurtenis heeft plaatsgevonden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="eac72-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="eac72-108">Deze technologie is gericht op beveiliging video-kanalen, kunnen beweging categoriseren in relevante gebeurtenissen en fout-positieven zoals schaduwen en licht wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="eac72-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="eac72-109">Hiermee kunt u voor het genereren van beveiligingswaarschuwingen van de camera feeds zonder kunnen momenten van belang extraheren van zeer lange toezicht video's met oneindige irrelevante gebeurtenissen, spam.</span><span class="sxs-lookup"><span data-stu-id="eac72-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="eac72-110">De **Azure Media beweging detectie** MP is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="eac72-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="eac72-111">Dit onderwerp bevat informatie over **Azure Media beweging detectie** en laat zien hoe u deze gebruiken met Media Services SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="eac72-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="eac72-112">Beweging detectie invoerbestanden</span><span class="sxs-lookup"><span data-stu-id="eac72-112">Motion Detector input files</span></span>
<span data-ttu-id="eac72-113">Videobestanden.</span><span class="sxs-lookup"><span data-stu-id="eac72-113">Video files.</span></span> <span data-ttu-id="eac72-114">Op dit moment wordt de volgende indelingen worden ondersteund: MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="eac72-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="eac72-115">Taken configureren (standaardoptie)</span><span class="sxs-lookup"><span data-stu-id="eac72-115">Task configuration (preset)</span></span>
<span data-ttu-id="eac72-116">Bij het maken van een taak met **Azure Media beweging detectie**, moet u een configuratie-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="eac72-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="eac72-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="eac72-117">Parameters</span></span>
<span data-ttu-id="eac72-118">U kunt de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="eac72-118">You can use the following parameters:</span></span>

| <span data-ttu-id="eac72-119">Naam</span><span class="sxs-lookup"><span data-stu-id="eac72-119">Name</span></span> | <span data-ttu-id="eac72-120">Opties</span><span class="sxs-lookup"><span data-stu-id="eac72-120">Options</span></span> | <span data-ttu-id="eac72-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="eac72-121">Description</span></span> | <span data-ttu-id="eac72-122">Standaard</span><span class="sxs-lookup"><span data-stu-id="eac72-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eac72-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="eac72-123">sensitivityLevel</span></span> |<span data-ttu-id="eac72-124">Tekenreeks: 'laag', 'Gemiddeld', 'hoog'</span><span class="sxs-lookup"><span data-stu-id="eac72-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="eac72-125">Hiermee stelt u het gevoeligheidsniveau op welke bewegingen wordt gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="eac72-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="eac72-126">Dit om aan te passen hoeveelheid valse positieven aanpassen.</span><span class="sxs-lookup"><span data-stu-id="eac72-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="eac72-127">'Gemiddeld'</span><span class="sxs-lookup"><span data-stu-id="eac72-127">'medium'</span></span> |
| <span data-ttu-id="eac72-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="eac72-128">frameSamplingValue</span></span> |<span data-ttu-id="eac72-129">Positief geheel getal</span><span class="sxs-lookup"><span data-stu-id="eac72-129">Positive integer</span></span> |<span data-ttu-id="eac72-130">Hiermee stelt u de frequentie aan welk algoritme wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="eac72-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="eac72-131">elk frame gelijk aan-1, 2 betekent dat elke 2e frame, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="eac72-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="eac72-132">1</span><span class="sxs-lookup"><span data-stu-id="eac72-132">1</span></span> |
| <span data-ttu-id="eac72-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="eac72-133">detectLightChange</span></span> |<span data-ttu-id="eac72-134">Boolean-waarde: 'true', 'onwaar'</span><span class="sxs-lookup"><span data-stu-id="eac72-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="eac72-135">Hiermee wordt ingesteld of lichte wijzigingen in de resultaten worden gemeld</span><span class="sxs-lookup"><span data-stu-id="eac72-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="eac72-136">'False'</span><span class="sxs-lookup"><span data-stu-id="eac72-136">'False'</span></span> |
| <span data-ttu-id="eac72-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="eac72-137">mergeTimeThreshold</span></span> |<span data-ttu-id="eac72-138">Tijd voor xs:: Mm: ss</span><span class="sxs-lookup"><span data-stu-id="eac72-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="eac72-139">Voorbeeld: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="eac72-139">Example: 00:00:03</span></span> |<span data-ttu-id="eac72-140">Hiermee geeft u de periode tussen beweging gebeurtenissen waarbij 2 gebeurtenissen wordt gecombineerd en gerapporteerd als 1.</span><span class="sxs-lookup"><span data-stu-id="eac72-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="eac72-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="eac72-141">00:00:00</span></span> |
| <span data-ttu-id="eac72-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="eac72-142">detectionZones</span></span> |<span data-ttu-id="eac72-143">Een matrix van zones voor detectie:</span><span class="sxs-lookup"><span data-stu-id="eac72-143">An array of detection zones:</span></span><br/><span data-ttu-id="eac72-144">-Zone detectie is een matrix met punten 3 of meer</span><span class="sxs-lookup"><span data-stu-id="eac72-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="eac72-145">-Punt is een x en y coördinaat tussen 0 en 1.</span><span class="sxs-lookup"><span data-stu-id="eac72-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="eac72-146">Hierin wordt beschreven in de lijst met detectie van veelhoekige zones moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="eac72-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="eac72-147">Resultaten met de zones worden vermeld als een ID, met de eerste afbeelding wordt 'id': 0</span><span class="sxs-lookup"><span data-stu-id="eac72-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="eac72-148">Enkele zone die wordt ingegaan op het gehele frame.</span><span class="sxs-lookup"><span data-stu-id="eac72-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="eac72-149">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="eac72-149">JSON example</span></span>
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


## <a name="motion-detector-output-files"></a><span data-ttu-id="eac72-150">Beweging detectie uitvoerbestanden</span><span class="sxs-lookup"><span data-stu-id="eac72-150">Motion Detector output files</span></span>
<span data-ttu-id="eac72-151">Een motion detection-taak retourneren een JSON-bestand in de uitvoerasset waarin de beweging waarschuwingen en hun categorieën, binnen de video worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="eac72-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="eac72-152">Het bestand bevat informatie over de tijd en de duur van gedetecteerd in de video motion.</span><span class="sxs-lookup"><span data-stu-id="eac72-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="eac72-153">De beweging detectie-API biedt indicatoren zodra er objecten in beweging in een vaste achtergrond video (bijvoorbeeld een toezicht video zijn).</span><span class="sxs-lookup"><span data-stu-id="eac72-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="eac72-154">De detectie van de beweging wordt te verminderen gegeven, zoals licht en wijzigingen van de schaduw getraind.</span><span class="sxs-lookup"><span data-stu-id="eac72-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="eac72-155">Huidige beperkingen van de algoritmen zijn nacht visie video's, semi-transparante objecten en kleine objecten.</span><span class="sxs-lookup"><span data-stu-id="eac72-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="eac72-156"><a id="output_elements"></a>Elementen van de JSON-bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="eac72-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="eac72-157">In de nieuwste versie, de uitvoer JSON-indeling is gewijzigd en een belangrijke wijziging voor sommige klanten kan vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="eac72-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="eac72-158">De volgende tabel beschrijft de elementen van de JSON-bestand voor uitvoer.</span><span class="sxs-lookup"><span data-stu-id="eac72-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="eac72-159">Element</span><span class="sxs-lookup"><span data-stu-id="eac72-159">Element</span></span> | <span data-ttu-id="eac72-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="eac72-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eac72-161">Versie</span><span class="sxs-lookup"><span data-stu-id="eac72-161">Version</span></span> |<span data-ttu-id="eac72-162">Dit verwijst naar de versie van de Video-API.</span><span class="sxs-lookup"><span data-stu-id="eac72-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="eac72-163">De huidige versie is 2.</span><span class="sxs-lookup"><span data-stu-id="eac72-163">The current version is 2.</span></span> |
| <span data-ttu-id="eac72-164">Tijdschaal</span><span class="sxs-lookup"><span data-stu-id="eac72-164">Timescale</span></span> |<span data-ttu-id="eac72-165">'Maatstreepjes' per seconde van de video.</span><span class="sxs-lookup"><span data-stu-id="eac72-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="eac72-166">Offset</span><span class="sxs-lookup"><span data-stu-id="eac72-166">Offset</span></span> |<span data-ttu-id="eac72-167">De time-offset voor tijdstempels in 'maatstreepjes'.</span><span class="sxs-lookup"><span data-stu-id="eac72-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="eac72-168">Versie 1.0 van Video-API's, zal dit altijd 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="eac72-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="eac72-169">In de toekomst scenario's die wordt ondersteund, deze waarde kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="eac72-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="eac72-170">framesnelheid</span><span class="sxs-lookup"><span data-stu-id="eac72-170">Framerate</span></span> |<span data-ttu-id="eac72-171">Frames per seconde van de video.</span><span class="sxs-lookup"><span data-stu-id="eac72-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="eac72-172">Breedte, hoogte</span><span class="sxs-lookup"><span data-stu-id="eac72-172">Width, Height</span></span> |<span data-ttu-id="eac72-173">Verwijst naar de breedte en hoogte van de video in pixels.</span><span class="sxs-lookup"><span data-stu-id="eac72-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="eac72-174">Starten</span><span class="sxs-lookup"><span data-stu-id="eac72-174">Start</span></span> |<span data-ttu-id="eac72-175">De tijdstempel begin in 'maatstreepjes'.</span><span class="sxs-lookup"><span data-stu-id="eac72-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="eac72-176">Duur</span><span class="sxs-lookup"><span data-stu-id="eac72-176">Duration</span></span> |<span data-ttu-id="eac72-177">De lengte van de gebeurtenis, in 'maatstreepjes'.</span><span class="sxs-lookup"><span data-stu-id="eac72-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="eac72-178">Interval</span><span class="sxs-lookup"><span data-stu-id="eac72-178">Interval</span></span> |<span data-ttu-id="eac72-179">Het interval van elke vermelding in de gebeurtenis, in 'maatstreepjes'.</span><span class="sxs-lookup"><span data-stu-id="eac72-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="eac72-180">Gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="eac72-180">Events</span></span> |<span data-ttu-id="eac72-181">Elke gebeurtenis fragment bevat de beweging binnen deze tijdsduur gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="eac72-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="eac72-182">Type</span><span class="sxs-lookup"><span data-stu-id="eac72-182">Type</span></span> |<span data-ttu-id="eac72-183">In de huidige versie is dit altijd '2' voor algemene beweging.</span><span class="sxs-lookup"><span data-stu-id="eac72-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="eac72-184">Hierdoor kunnen label Video-API's de flexibiliteit om te categoriseren beweging in toekomstige versies.</span><span class="sxs-lookup"><span data-stu-id="eac72-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="eac72-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="eac72-185">RegionID</span></span> |<span data-ttu-id="eac72-186">Zoals hierboven vermeld, zal dit altijd 0 in deze versie zijn.</span><span class="sxs-lookup"><span data-stu-id="eac72-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="eac72-187">De dit label kunt API Video motion niet vinden in verschillende regio's in toekomstige versies.</span><span class="sxs-lookup"><span data-stu-id="eac72-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="eac72-188">Regio's</span><span class="sxs-lookup"><span data-stu-id="eac72-188">Regions</span></span> |<span data-ttu-id="eac72-189">Verwijst naar het gedeelte in uw video waarin u het belangrijkst over beweging.</span><span class="sxs-lookup"><span data-stu-id="eac72-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="eac72-190">-het gebied regio 'id' aangeeft: in deze versie er is slechts één ID 0.</span><span class="sxs-lookup"><span data-stu-id="eac72-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="eac72-191">-'type' de vorm van de regio die u voor beweging interesseren vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="eac72-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="eac72-192">Op dit moment worden 'rechthoek' en 'veelhoek' ondersteund.</span><span class="sxs-lookup"><span data-stu-id="eac72-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="eac72-193">Als u 'rechthoek' hebt opgegeven, heeft de regio dimensies in X, Y, Width en Height.</span><span class="sxs-lookup"><span data-stu-id="eac72-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="eac72-194">De X en Y-coördinaten vertegenwoordigen de bovenste linkerkant Xyserver coördinaten van het gebied in een genormaliseerde schaal van 0,0 en 1,0.</span><span class="sxs-lookup"><span data-stu-id="eac72-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="eac72-195">De breedte en hoogte vertegenwoordigen de grootte van de regio in een genormaliseerde schaal van 0,0 en 1,0.</span><span class="sxs-lookup"><span data-stu-id="eac72-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="eac72-196">In de huidige versie zijn X, Y, Width en Height altijd vast op 0, 0 en 1, 1.</span><span class="sxs-lookup"><span data-stu-id="eac72-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="eac72-197">Als u 'veelhoek' hebt opgegeven, heeft de regio dimensies in punten.</span><span class="sxs-lookup"><span data-stu-id="eac72-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="eac72-198">fragmenten</span><span class="sxs-lookup"><span data-stu-id="eac72-198">Fragments</span></span> |<span data-ttu-id="eac72-199">De metagegevens wordt gesegmenteerde in verschillende segmenten fragmenten aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eac72-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="eac72-200">Elke fragment bevat een start, duur, Intervalnummer en gebeurtenis(sen).</span><span class="sxs-lookup"><span data-stu-id="eac72-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="eac72-201">Een fragment met er zijn geen gebeurtenissen betekent dat er geen beweging is aangetroffen tijdens die begintijd en duur.</span><span class="sxs-lookup"><span data-stu-id="eac72-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="eac72-202">[]-Haken</span><span class="sxs-lookup"><span data-stu-id="eac72-202">Brackets []</span></span> |<span data-ttu-id="eac72-203">Elke accolade vertegenwoordigt één interval in de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="eac72-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="eac72-204">Lege haakjes voor dat interval betekent dat er geen beweging is gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="eac72-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="eac72-205">Locaties</span><span class="sxs-lookup"><span data-stu-id="eac72-205">locations</span></span> |<span data-ttu-id="eac72-206">Deze nieuwe vermelding onder gebeurtenissen vindt u de locatie waar de beweging zich heeft voorgedaan.</span><span class="sxs-lookup"><span data-stu-id="eac72-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="eac72-207">Dit is een meer specifiek zijn dan de zones van de detectie.</span><span class="sxs-lookup"><span data-stu-id="eac72-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="eac72-208">Hier volgt een voorbeeld van een JSON-uitvoer</span><span class="sxs-lookup"><span data-stu-id="eac72-208">The following is a JSON output example</span></span>

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
## <a name="limitations"></a><span data-ttu-id="eac72-209">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="eac72-209">Limitations</span></span>
* <span data-ttu-id="eac72-210">De ondersteunde video-invoerindelingen zijn MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="eac72-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="eac72-211">Bewegingsdetectie is geoptimaliseerd voor stilstaan achtergrond video's.</span><span class="sxs-lookup"><span data-stu-id="eac72-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="eac72-212">De algoritme is gericht op het verminderen van gegeven, zoals licht wijzigingen en schaduwen.</span><span class="sxs-lookup"><span data-stu-id="eac72-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="eac72-213">Sommige beweging kan niet worden herkend vanwege technische moeilijkheden; bijvoorbeeld 's avonds visie video's, semi-transparante objecten en kleine objecten.</span><span class="sxs-lookup"><span data-stu-id="eac72-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="eac72-214">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="eac72-214">.NET sample code</span></span>

<span data-ttu-id="eac72-215">De volgende programma toont hoe:</span><span class="sxs-lookup"><span data-stu-id="eac72-215">The following program shows how to:</span></span>

1. <span data-ttu-id="eac72-216">Maak een asset en upload een mediabestand naar de asset.</span><span class="sxs-lookup"><span data-stu-id="eac72-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="eac72-217">Een taak maken met een video motion detection-taak op basis van een configuratiebestand met de volgende json-definitie.</span><span class="sxs-lookup"><span data-stu-id="eac72-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
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
3. <span data-ttu-id="eac72-218">De uitvoer JSON-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="eac72-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="eac72-219">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="eac72-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="eac72-220">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="eac72-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="eac72-221">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="eac72-221">Example</span></span>


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
            // Read values from the App.config file.
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="eac72-222">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="eac72-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="eac72-223">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="eac72-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="eac72-224">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="eac72-224">Related links</span></span>
[<span data-ttu-id="eac72-225">Azure Media Services beweging detectie-blog</span><span class="sxs-lookup"><span data-stu-id="eac72-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="eac72-226">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="eac72-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="eac72-227">Azure Media Analytics-demo 's</span><span class="sxs-lookup"><span data-stu-id="eac72-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

