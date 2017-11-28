---
title: aaaDetect gezichts- en Emotion met Azure Media Analytics | Microsoft Docs
description: In dit onderwerp wordt beschreven hoe toodetect bespreekt en emoties met Azure Media Analytics.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="8ea4f-103">Face en Emotion met Azure Media Analytics detecteren</span><span class="sxs-lookup"><span data-stu-id="8ea4f-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="8ea4f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8ea4f-104">Overview</span></span>
<span data-ttu-id="8ea4f-105">Hallo **Azure Media Face detectie** Mediaprocessor (MP) kunt u toocount, de bewegingen bijhouden, en zelfs meter doelgroep deelname en reactie via bedacht.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="8ea4f-106">Deze service bevat twee functies:</span><span class="sxs-lookup"><span data-stu-id="8ea4f-106">This service contains two features:</span></span> 

* <span data-ttu-id="8ea4f-107">**Face-detectie**</span><span class="sxs-lookup"><span data-stu-id="8ea4f-107">**Face detection**</span></span>
  
    <span data-ttu-id="8ea4f-108">Face-detectie zoekt en houdt menselijke vlakken binnen een video.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="8ea4f-109">Meerdere vlakken kunnen worden gedetecteerd en vervolgens worden bijgehouden als ze onderweg, met Hallo-metagegevens en de locatie geretourneerd in een JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="8ea4f-110">Tijdens de bijhouden, wordt geprobeerd toogive een consistente ID toohello dezelfde geconfronteerd terwijl Hallo persoon is navigeren op het scherm, zelfs als ze zijn ondervindt hinder van obstakels of kort Hallo frame laat.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8ea4f-111">Deze service voert geen gezichtsherkenning.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="8ea4f-112">Een persoon die Hallo frame verlaat of ondervindt voor wordt hinder van obstakels te lang krijgt een nieuwe ID wanneer ze terugkeren.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="8ea4f-113">**Emotiedetectie**</span><span class="sxs-lookup"><span data-stu-id="8ea4f-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="8ea4f-114">Emotiedetectie is een optioneel onderdeel van Hallo Face Detection Media Processor op dat analyse op meerdere emotionele kenmerken van Hallo vlakken gedetecteerd retourneert, met inbegrip van gelukkig, sadness bang, volgt uitzien en meer.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="8ea4f-115">Hallo **Azure Media Face detectie** MP is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="8ea4f-116">Dit onderwerp bevat informatie over **Azure Media Face detectie** en ziet u hoe toouse met Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="8ea4f-117">Detectie-invoerbestanden geconfronteerd</span><span class="sxs-lookup"><span data-stu-id="8ea4f-117">Face Detector input files</span></span>
<span data-ttu-id="8ea4f-118">Videobestanden.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-118">Video files.</span></span> <span data-ttu-id="8ea4f-119">Op dit moment Hallo volgende indelingen worden ondersteund: MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="8ea4f-120">Detectie uitvoerbestanden geconfronteerd</span><span class="sxs-lookup"><span data-stu-id="8ea4f-120">Face Detector output files</span></span>
<span data-ttu-id="8ea4f-121">Hallo face detection en bijhouden API biedt hoge precisie face locatie detectie en bijhouden die up too64 menselijke vlakken in een video kan detecteren.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="8ea4f-122">Voorzijde vlakken bieden de beste resultaten Hallo tijdens vlakken kant- en kleine vlakken (minder dan of gelijk zijn aan too24x24 pixels) mogelijk niet nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="8ea4f-123">Hallo gedetecteerde en bijgehouden vlakken worden geretourneerd met coördinaten (links, top, breedte en hoogte) Hallo-locatie van vlakken in Hallo afbeelding in pixels die aangeeft, evenals een face ID getal dat aangeeft dat afzonderlijke bijhouden Hallo.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="8ea4f-124">Face-id-nummers zijn foutgevoelige tooreset omstandigheden wanneer Hallo voorzijde face verloren is gegaan of elkaar overlappen in Hallo-frame, waardoor bepaalde personen ophalen van meerdere id's toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="8ea4f-125"><a id="output_elements"></a>Elementen van Hallo uitvoer JSON-bestand</span><span class="sxs-lookup"><span data-stu-id="8ea4f-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="8ea4f-126">Face-detectie maakt gebruik van technieken van fragmentatie (waarbij Hallo metagegevens kan worden opgesplitst in segmenten op basis van tijd en u kunt downloaden wat u nodig hebt) en segmentering (waarbij Hallo gebeurtenissen worden opgedeeld geval ze te groot krijgen).</span><span class="sxs-lookup"><span data-stu-id="8ea4f-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="8ea4f-127">Enkele eenvoudige berekeningen kunt u Hallo gegevens transformeren.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="8ea4f-128">Bijvoorbeeld, als een gebeurtenis wordt gestart om 6300 (maten) met een tijdschaal van 2997 (ticks per seconde) en framesnelheid van vervolgens 29,97 (frames per seconde):</span><span class="sxs-lookup"><span data-stu-id="8ea4f-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="8ea4f-129">Start/tijdschaal = 2.1 seconden</span><span class="sxs-lookup"><span data-stu-id="8ea4f-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="8ea4f-130">Seconden x Framerate 63 frames =</span><span class="sxs-lookup"><span data-stu-id="8ea4f-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="8ea4f-131">Geconfronteerd detectie invoer en uitvoer voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8ea4f-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="8ea4f-132">Invoervideo</span><span class="sxs-lookup"><span data-stu-id="8ea4f-132">Input video</span></span>
[<span data-ttu-id="8ea4f-133">Invoervideo</span><span class="sxs-lookup"><span data-stu-id="8ea4f-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="8ea4f-134">Taken configureren (standaardoptie)</span><span class="sxs-lookup"><span data-stu-id="8ea4f-134">Task configuration (preset)</span></span>
<span data-ttu-id="8ea4f-135">Bij het maken van een taak met **Azure Media Face detectie**, moet u een configuratie-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="8ea4f-136">Hallo na configuratie definitie is slechts voor face detection.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="8ea4f-137">Beschrijvingen van kenmerken</span><span class="sxs-lookup"><span data-stu-id="8ea4f-137">Attribute descriptions</span></span>
| <span data-ttu-id="8ea4f-138">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="8ea4f-138">Attribute name</span></span> | <span data-ttu-id="8ea4f-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8ea4f-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ea4f-140">Modus</span><span class="sxs-lookup"><span data-stu-id="8ea4f-140">Mode</span></span> |<span data-ttu-id="8ea4f-141">Snel - verwerking snel van de snelheid, maar minder nauwkeurig (standaard).</span><span class="sxs-lookup"><span data-stu-id="8ea4f-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="8ea4f-142">JSON-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8ea4f-142">JSON output</span></span>
<span data-ttu-id="8ea4f-143">Voorbeeld van JSON-uitvoer na Hallo is afgebroken.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="8ea4f-144">Emotiedetectie invoer en uitvoer voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8ea4f-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="8ea4f-145">Invoervideo</span><span class="sxs-lookup"><span data-stu-id="8ea4f-145">Input video</span></span>
[<span data-ttu-id="8ea4f-146">Invoervideo</span><span class="sxs-lookup"><span data-stu-id="8ea4f-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="8ea4f-147">Taken configureren (standaardoptie)</span><span class="sxs-lookup"><span data-stu-id="8ea4f-147">Task configuration (preset)</span></span>
<span data-ttu-id="8ea4f-148">Bij het maken van een taak met **Azure Media Face detectie**, moet u een configuratie-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="8ea4f-149">Hallo na configuratie voorinstelling geeft toocreate die JSON op basis van Hallo emotiedetectie.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="8ea4f-150">Beschrijvingen van kenmerken</span><span class="sxs-lookup"><span data-stu-id="8ea4f-150">Attribute descriptions</span></span>
| <span data-ttu-id="8ea4f-151">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="8ea4f-151">Attribute name</span></span> | <span data-ttu-id="8ea4f-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8ea4f-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ea4f-153">Modus</span><span class="sxs-lookup"><span data-stu-id="8ea4f-153">Mode</span></span> |<span data-ttu-id="8ea4f-154">Vlakken: Komen alleen voor detectie.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="8ea4f-155">PerFaceEmotion: Retourneren emotion onafhankelijk voor elke face-detectie.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="8ea4f-156">AggregateEmotion: Return gemiddelde emotion waarden voor alle vlakken in frame.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="8ea4f-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="8ea4f-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="8ea4f-158">Gebruik deze optie als AggregateEmotion modus geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="8ea4f-159">Hiermee geeft u Hallo lengte van video gebruikte tooproduce elk cumulatieve resultaat in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="8ea4f-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="8ea4f-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="8ea4f-161">Gebruik deze optie als AggregateEmotion modus geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="8ea4f-162">Hiermee geeft u aan met welke frequentie tooproduce statistische functie resulteert.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="8ea4f-163">Cumulatieve standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="8ea4f-163">Aggregate defaults</span></span>
<span data-ttu-id="8ea4f-164">Hieronder worden aanbevolen waarden voor statistische vensterfunctie hello en intervalinstellingen.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="8ea4f-165">AggregateEmotionWindowMs mag niet langer zijn dan AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="8ea4f-166">Standaardinstellingen (s)</span><span class="sxs-lookup"><span data-stu-id="8ea4f-166">Defaults(s)</span></span> | <span data-ttu-id="8ea4f-167">Min(s)</span><span class="sxs-lookup"><span data-stu-id="8ea4f-167">Min(s)</span></span> | <span data-ttu-id="8ea4f-168">Max(s)</span><span class="sxs-lookup"><span data-stu-id="8ea4f-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="8ea4f-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="8ea4f-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="8ea4f-170">0.5</span><span class="sxs-lookup"><span data-stu-id="8ea4f-170">0.5</span></span> |<span data-ttu-id="8ea4f-171">2</span><span class="sxs-lookup"><span data-stu-id="8ea4f-171">2</span></span> |<span data-ttu-id="8ea4f-172">0.25</span><span class="sxs-lookup"><span data-stu-id="8ea4f-172">0.25</span></span>|
| <span data-ttu-id="8ea4f-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="8ea4f-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="8ea4f-174">0.5</span><span class="sxs-lookup"><span data-stu-id="8ea4f-174">0.5</span></span> |<span data-ttu-id="8ea4f-175">1</span><span class="sxs-lookup"><span data-stu-id="8ea4f-175">1</span></span> |<span data-ttu-id="8ea4f-176">0.25</span><span class="sxs-lookup"><span data-stu-id="8ea4f-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="8ea4f-177">JSON-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8ea4f-177">JSON output</span></span>
<span data-ttu-id="8ea4f-178">JSON-uitvoer voor cumulatieve emotion (afgekapt):</span><span class="sxs-lookup"><span data-stu-id="8ea4f-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="8ea4f-179">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="8ea4f-179">Limitations</span></span>
* <span data-ttu-id="8ea4f-180">Hallo ondersteund video-invoerindelingen zijn MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="8ea4f-181">Hallo waarneembaar face grootte bereik is 24 x 24 too2048x2048 pixels.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="8ea4f-182">Hallo vlakken buiten dit bereik wordt niet gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="8ea4f-183">Maximum aantal vlakken geretourneerd Hallo is voor elke video 64.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="8ea4f-184">Sommige vlakken mogelijk niet gedetecteerd vanwege tootechnical uitdagingen; bijvoorbeeld zeer grote face hoeken (head-ven) en grote Occlusie.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="8ea4f-185">Voorzijde en in de buurt binnen handbereik hebt Hallo krijgt de beste resultaten.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="8ea4f-186">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="8ea4f-186">.NET sample code</span></span>

<span data-ttu-id="8ea4f-187">Hallo volgende programma toont hoe:</span><span class="sxs-lookup"><span data-stu-id="8ea4f-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="8ea4f-188">Maak een asset en upload een mediabestand naar Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="8ea4f-189">Een taak maken met een face detection-taak op basis van een configuratiebestand met Hallo json-definitie te volgen.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="8ea4f-190">Hallo uitvoer JSON-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="8ea4f-191">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="8ea4f-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="8ea4f-192">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8ea4f-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="8ea4f-193">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8ea4f-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="8ea4f-194">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="8ea4f-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8ea4f-195">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="8ea4f-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="8ea4f-196">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="8ea4f-196">Related links</span></span>
[<span data-ttu-id="8ea4f-197">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="8ea4f-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="8ea4f-198">Azure Media Analytics-demo 's</span><span class="sxs-lookup"><span data-stu-id="8ea4f-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

