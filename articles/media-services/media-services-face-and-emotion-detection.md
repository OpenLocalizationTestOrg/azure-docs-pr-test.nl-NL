---
title: Detecteren gezichts- en Emotion met Azure Media Analytics | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe vlakken en emoties met Azure Media Analytics te detecteren.
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
ms.openlocfilehash: d7f3bc6c0d21db7adbb0c16c752d4ce49e99da5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="f4d31-103">Face en Emotion met Azure Media Analytics detecteren</span><span class="sxs-lookup"><span data-stu-id="f4d31-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="f4d31-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f4d31-104">Overview</span></span>
<span data-ttu-id="f4d31-105">De **Azure Media Face detectie** Mediaprocessor (MP) kunt u tellen en zelfs te meten wat doelgroep deelname en reactie via bedacht bewegingen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="f4d31-105">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="f4d31-106">Deze service bevat twee functies:</span><span class="sxs-lookup"><span data-stu-id="f4d31-106">This service contains two features:</span></span> 

* <span data-ttu-id="f4d31-107">**Face-detectie**</span><span class="sxs-lookup"><span data-stu-id="f4d31-107">**Face detection**</span></span>
  
    <span data-ttu-id="f4d31-108">Face-detectie zoekt en houdt menselijke vlakken binnen een video.</span><span class="sxs-lookup"><span data-stu-id="f4d31-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="f4d31-109">Meerdere vlakken kunnen worden gedetecteerd en vervolgens worden bijgehouden als ze onderweg, met de metagegevens van de tijd en de locatie in een JSON-bestand geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f4d31-109">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="f4d31-110">Tijdens de bijhouden, wordt geprobeerd een consistente ID geven tot de dezelfde face terwijl de persoon is navigeren op het scherm, zelfs als ze zijn ondervindt hinder van obstakels of kort het frame laat.</span><span class="sxs-lookup"><span data-stu-id="f4d31-110">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="f4d31-111">Deze service voert geen gezichtsherkenning.</span><span class="sxs-lookup"><span data-stu-id="f4d31-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="f4d31-112">Een persoon die het frame verlaat of ondervindt voor wordt hinder van obstakels te lang krijgt een nieuwe ID wanneer ze terugkeren.</span><span class="sxs-lookup"><span data-stu-id="f4d31-112">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="f4d31-113">**Emotiedetectie**</span><span class="sxs-lookup"><span data-stu-id="f4d31-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="f4d31-114">Emotiedetectie is een optioneel onderdeel van de Processor Face Detection Media die analyse op meerdere emotionele kenmerken van de vlakken gedetecteerd retourneert, met inbegrip van gelukkig, sadness bang, volgt uitzien en meer.</span><span class="sxs-lookup"><span data-stu-id="f4d31-114">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="f4d31-115">De **Azure Media Face detectie** MP is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="f4d31-115">The **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="f4d31-116">Dit onderwerp bevat informatie over **Azure Media Face detectie** en laat zien hoe u deze gebruiken met Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="f4d31-116">This topic gives details about  **Azure Media Face Detector** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="f4d31-117">Detectie-invoerbestanden geconfronteerd</span><span class="sxs-lookup"><span data-stu-id="f4d31-117">Face Detector input files</span></span>
<span data-ttu-id="f4d31-118">Videobestanden.</span><span class="sxs-lookup"><span data-stu-id="f4d31-118">Video files.</span></span> <span data-ttu-id="f4d31-119">Op dit moment wordt de volgende indelingen worden ondersteund: MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="f4d31-119">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="f4d31-120">Detectie uitvoerbestanden geconfronteerd</span><span class="sxs-lookup"><span data-stu-id="f4d31-120">Face Detector output files</span></span>
<span data-ttu-id="f4d31-121">De face-API voor detectie en bijhouden biedt hoge precisie face locatie detectie en bijhouden die maximaal 64 menselijke vlakken in een video kan detecteren.</span><span class="sxs-lookup"><span data-stu-id="f4d31-121">The face detection and tracking API provides high precision face location detection and tracking that can detect up to 64 human faces in a video.</span></span> <span data-ttu-id="f4d31-122">Voorzijde vlakken bieden de beste resultaten, terwijl side vlakken en in kleine vlakken (kleiner dan of gelijk aan 24 x 24 pixels) mogelijk niet nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="f4d31-122">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="f4d31-123">De vlakken gedetecteerde en bijgehouden met coördinaten (links, top, breedte en hoogte) worden geretourneerd die de locatie van vlakken in de afbeelding in pixels, evenals een face-id die aangeeft dat afzonderlijke volgen.</span><span class="sxs-lookup"><span data-stu-id="f4d31-123">The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual.</span></span> <span data-ttu-id="f4d31-124">Face-id-nummers zijn kwetsbaar voor opnieuw omstandigheden worden ingesteld als de voorzijde face verloren is gegaan of elkaar overlappen in het kader waardoor bepaalde personen ophalen van meerdere id's toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f4d31-124">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="f4d31-125"><a id="output_elements"></a>Elementen van de JSON-bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="f4d31-125"><a id="output_elements"></a>Elements of the output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="f4d31-126">Face-detectie maakt gebruik van technieken van fragmentatie (waar de metagegevens kan worden opgedeeld in segmenten op basis van tijd en u kunt downloaden wat u nodig hebt) en segmentering (waar de gebeurtenissen worden opgedeeld geval ze te groot krijgen).</span><span class="sxs-lookup"><span data-stu-id="f4d31-126">Face Detector uses techniques of fragmentation (where the metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where the events are broken up in case they get too large).</span></span> <span data-ttu-id="f4d31-127">Enkele eenvoudige berekeningen kunt u de gegevens transformeren.</span><span class="sxs-lookup"><span data-stu-id="f4d31-127">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="f4d31-128">Bijvoorbeeld, als een gebeurtenis wordt gestart om 6300 (maten) met een tijdschaal van 2997 (ticks per seconde) en framesnelheid van vervolgens 29,97 (frames per seconde):</span><span class="sxs-lookup"><span data-stu-id="f4d31-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="f4d31-129">Start/tijdschaal = 2.1 seconden</span><span class="sxs-lookup"><span data-stu-id="f4d31-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="f4d31-130">Seconden x Framerate 63 frames =</span><span class="sxs-lookup"><span data-stu-id="f4d31-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="f4d31-131">Geconfronteerd detectie invoer en uitvoer voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f4d31-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="f4d31-132">Invoervideo</span><span class="sxs-lookup"><span data-stu-id="f4d31-132">Input video</span></span>
[<span data-ttu-id="f4d31-133">Invoervideo</span><span class="sxs-lookup"><span data-stu-id="f4d31-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="f4d31-134">Taken configureren (standaardoptie)</span><span class="sxs-lookup"><span data-stu-id="f4d31-134">Task configuration (preset)</span></span>
<span data-ttu-id="f4d31-135">Bij het maken van een taak met **Azure Media Face detectie**, moet u een configuratie-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="f4d31-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="f4d31-136">De volgende configuratie-definitie is slechts voor face detection.</span><span class="sxs-lookup"><span data-stu-id="f4d31-136">The following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="f4d31-137">Beschrijvingen van kenmerken</span><span class="sxs-lookup"><span data-stu-id="f4d31-137">Attribute descriptions</span></span>
| <span data-ttu-id="f4d31-138">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f4d31-138">Attribute name</span></span> | <span data-ttu-id="f4d31-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f4d31-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4d31-140">Modus</span><span class="sxs-lookup"><span data-stu-id="f4d31-140">Mode</span></span> |<span data-ttu-id="f4d31-141">Snel - verwerking snel van de snelheid, maar minder nauwkeurig (standaard).</span><span class="sxs-lookup"><span data-stu-id="f4d31-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="f4d31-142">JSON-uitvoer</span><span class="sxs-lookup"><span data-stu-id="f4d31-142">JSON output</span></span>
<span data-ttu-id="f4d31-143">Het volgende voorbeeld van JSON-uitvoer is afgebroken.</span><span class="sxs-lookup"><span data-stu-id="f4d31-143">The following example of JSON output was truncated.</span></span>

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

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="f4d31-144">Emotiedetectie invoer en uitvoer voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f4d31-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="f4d31-145">Invoervideo</span><span class="sxs-lookup"><span data-stu-id="f4d31-145">Input video</span></span>
[<span data-ttu-id="f4d31-146">Invoervideo</span><span class="sxs-lookup"><span data-stu-id="f4d31-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="f4d31-147">Taken configureren (standaardoptie)</span><span class="sxs-lookup"><span data-stu-id="f4d31-147">Task configuration (preset)</span></span>
<span data-ttu-id="f4d31-148">Bij het maken van een taak met **Azure Media Face detectie**, moet u een configuratie-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="f4d31-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="f4d31-149">De volgende configuratie voorinstelling geeft als u wilt maken op basis van de emotiedetectie JSON.</span><span class="sxs-lookup"><span data-stu-id="f4d31-149">The following configuration preset specifies to create JSON based on the emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="f4d31-150">Beschrijvingen van kenmerken</span><span class="sxs-lookup"><span data-stu-id="f4d31-150">Attribute descriptions</span></span>
| <span data-ttu-id="f4d31-151">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f4d31-151">Attribute name</span></span> | <span data-ttu-id="f4d31-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f4d31-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4d31-153">Modus</span><span class="sxs-lookup"><span data-stu-id="f4d31-153">Mode</span></span> |<span data-ttu-id="f4d31-154">Vlakken: Komen alleen voor detectie.</span><span class="sxs-lookup"><span data-stu-id="f4d31-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="f4d31-155">PerFaceEmotion: Retourneren emotion onafhankelijk voor elke face-detectie.</span><span class="sxs-lookup"><span data-stu-id="f4d31-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="f4d31-156">AggregateEmotion: Return gemiddelde emotion waarden voor alle vlakken in frame.</span><span class="sxs-lookup"><span data-stu-id="f4d31-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="f4d31-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="f4d31-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="f4d31-158">Gebruik deze optie als AggregateEmotion modus geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f4d31-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="f4d31-159">Hiermee geeft u de lengte van video gebruikt voor het produceren van elk cumulatieve resultaat, in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="f4d31-159">Specifies the length of video used to produce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="f4d31-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="f4d31-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="f4d31-161">Gebruik deze optie als AggregateEmotion modus geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f4d31-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="f4d31-162">Hiermee geeft u aan met welke frequentie voor het produceren van statistische resultaten.</span><span class="sxs-lookup"><span data-stu-id="f4d31-162">Specifies with what frequency to produce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="f4d31-163">Cumulatieve standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="f4d31-163">Aggregate defaults</span></span>
<span data-ttu-id="f4d31-164">Hieronder worden aanbevolen waarden voor de cumulatieve venster en interval-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f4d31-164">Below are recommended values for the aggregate window and interval settings.</span></span> <span data-ttu-id="f4d31-165">AggregateEmotionWindowMs mag niet langer zijn dan AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="f4d31-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="f4d31-166">Standaardinstellingen (s)</span><span class="sxs-lookup"><span data-stu-id="f4d31-166">Defaults(s)</span></span> | <span data-ttu-id="f4d31-167">Min(s)</span><span class="sxs-lookup"><span data-stu-id="f4d31-167">Min(s)</span></span> | <span data-ttu-id="f4d31-168">Max(s)</span><span class="sxs-lookup"><span data-stu-id="f4d31-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="f4d31-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="f4d31-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="f4d31-170">0.5</span><span class="sxs-lookup"><span data-stu-id="f4d31-170">0.5</span></span> |<span data-ttu-id="f4d31-171">2</span><span class="sxs-lookup"><span data-stu-id="f4d31-171">2</span></span> |<span data-ttu-id="f4d31-172">0.25</span><span class="sxs-lookup"><span data-stu-id="f4d31-172">0.25</span></span>|
| <span data-ttu-id="f4d31-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="f4d31-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="f4d31-174">0.5</span><span class="sxs-lookup"><span data-stu-id="f4d31-174">0.5</span></span> |<span data-ttu-id="f4d31-175">1</span><span class="sxs-lookup"><span data-stu-id="f4d31-175">1</span></span> |<span data-ttu-id="f4d31-176">0.25</span><span class="sxs-lookup"><span data-stu-id="f4d31-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="f4d31-177">JSON-uitvoer</span><span class="sxs-lookup"><span data-stu-id="f4d31-177">JSON output</span></span>
<span data-ttu-id="f4d31-178">JSON-uitvoer voor cumulatieve emotion (afgekapt):</span><span class="sxs-lookup"><span data-stu-id="f4d31-178">JSON output for aggregate emotion (truncated):</span></span>

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

## <a name="limitations"></a><span data-ttu-id="f4d31-179">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="f4d31-179">Limitations</span></span>
* <span data-ttu-id="f4d31-180">De ondersteunde video-invoerindelingen zijn MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="f4d31-180">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="f4d31-181">Het bereik van de grootte waarneembaar face is 24 x 24 naar 2048 x 2048 pixels.</span><span class="sxs-lookup"><span data-stu-id="f4d31-181">The detectable face size range is 24x24 to 2048x2048 pixels.</span></span> <span data-ttu-id="f4d31-182">De vlakken buiten dit bereik wordt niet gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="f4d31-182">The faces out of this range will not be detected.</span></span>
* <span data-ttu-id="f4d31-183">Voor elke video is het maximum aantal vlakken geretourneerd 64.</span><span class="sxs-lookup"><span data-stu-id="f4d31-183">For each video, the maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="f4d31-184">Sommige vlakken kunnen niet worden herkend vanwege technische moeilijkheden; bijvoorbeeld zeer grote face hoeken (head-ven) en grote Occlusie.</span><span class="sxs-lookup"><span data-stu-id="f4d31-184">Some faces may not be detected due to technical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="f4d31-185">Voorzijde en in de buurt binnen handbereik vlakken hebben de beste resultaten.</span><span class="sxs-lookup"><span data-stu-id="f4d31-185">Frontal and near-frontal faces have the best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="f4d31-186">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="f4d31-186">.NET sample code</span></span>

<span data-ttu-id="f4d31-187">De volgende programma toont hoe:</span><span class="sxs-lookup"><span data-stu-id="f4d31-187">The following program shows how to:</span></span>

1. <span data-ttu-id="f4d31-188">Maak een asset en upload een mediabestand naar de asset.</span><span class="sxs-lookup"><span data-stu-id="f4d31-188">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="f4d31-189">Een taak maken met een face detection-taak op basis van een configuratiebestand met de volgende json-definitie.</span><span class="sxs-lookup"><span data-stu-id="f4d31-189">Create a job with a face detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="f4d31-190">De uitvoer JSON-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="f4d31-190">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="f4d31-191">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="f4d31-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="f4d31-192">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f4d31-192">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="f4d31-193">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f4d31-193">Example</span></span>

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

                // Run the FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference to Azure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="f4d31-194">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="f4d31-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f4d31-195">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="f4d31-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="f4d31-196">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="f4d31-196">Related links</span></span>
[<span data-ttu-id="f4d31-197">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="f4d31-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="f4d31-198">Azure Media Analytics-demo 's</span><span class="sxs-lookup"><span data-stu-id="f4d31-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

