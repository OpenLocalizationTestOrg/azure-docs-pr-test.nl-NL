---
title: Tekst met Azure Media Analytics OCR gedigitaliseerd | Microsoft Docs
description: Azure Media Analytics OCR (OCR) kunt u tekstinhoud in videobestanden converteren naar bewerkbare, doorzoekbaar digitale tekst.  Hiermee kunt u de extractie van zinvolle metagegevens van de video signaal van uw media te automatiseren.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 43f5b3a9bbec243e668c79702045094fcfedbdda
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="939f6-104">Azure Media Analytics gebruiken voor het converteren van tekstinhoud in videobestanden in digitale tekst</span><span class="sxs-lookup"><span data-stu-id="939f6-104">Use Azure Media Analytics to convert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="939f6-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="939f6-105">Overview</span></span>
<span data-ttu-id="939f6-106">Als u moet voor tekstinhoud extraheren uit uw video's en het genereren van een digitale tekst worden bewerkt, doorzoekbaar, moet u Azure Media Analytics OCR (OCR).</span><span class="sxs-lookup"><span data-stu-id="939f6-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="939f6-107">Deze Azure Media Processor tekstinhoud detecteert in uw video's en genereert tekstbestanden voor het gebruik.</span><span class="sxs-lookup"><span data-stu-id="939f6-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="939f6-108">OCR kunt u de extractie van zinvolle metagegevens van de video signaal van uw media te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="939f6-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span></span>

<span data-ttu-id="939f6-109">Wanneer gebruikt in combinatie met een zoekmachine, kunt u eenvoudig uw media indexering van tekst en verbeteren van de detectie van uw inhoud.</span><span class="sxs-lookup"><span data-stu-id="939f6-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span></span> <span data-ttu-id="939f6-110">Dit is zeer nuttig zijn bij zeer tekstuele video, zoals een video-opname of een schermopname van een diavoorstelling.</span><span class="sxs-lookup"><span data-stu-id="939f6-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="939f6-111">De Azure OCR Media-Processor is geoptimaliseerd voor digitale tekst.</span><span class="sxs-lookup"><span data-stu-id="939f6-111">The Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="939f6-112">De **Azure Media OCR** Mediaprocessor is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="939f6-112">The **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="939f6-113">Dit onderwerp bevat informatie over **Azure Media OCR** en laat zien hoe u deze gebruiken met Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="939f6-113">This topic gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span></span> <span data-ttu-id="939f6-114">Zie voor meer informatie en voorbeelden [deze blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="939f6-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="939f6-115">De invoerbestanden OCR</span><span class="sxs-lookup"><span data-stu-id="939f6-115">OCR input files</span></span>
<span data-ttu-id="939f6-116">Videobestanden.</span><span class="sxs-lookup"><span data-stu-id="939f6-116">Video files.</span></span> <span data-ttu-id="939f6-117">Op dit moment wordt de volgende indelingen worden ondersteund: MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="939f6-117">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="939f6-118">Taken configureren</span><span class="sxs-lookup"><span data-stu-id="939f6-118">Task configuration</span></span>
<span data-ttu-id="939f6-119">Taken configureren (standaardoptie).</span><span class="sxs-lookup"><span data-stu-id="939f6-119">Task configuration (preset).</span></span> <span data-ttu-id="939f6-120">Bij het maken van een taak met **Azure Media OCR**, moet u een configuratie met JSON of XML-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="939f6-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="939f6-121">De engine OCR duurt slechts een installatiekopie-regio met minimale 40 pixels en maximale 32000 pixels als een geldige invoer in beide hoogte/breedte.</span><span class="sxs-lookup"><span data-stu-id="939f6-121">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="939f6-122">Beschrijvingen van kenmerken</span><span class="sxs-lookup"><span data-stu-id="939f6-122">Attribute descriptions</span></span>
| <span data-ttu-id="939f6-123">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="939f6-123">Attribute name</span></span> | <span data-ttu-id="939f6-124">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="939f6-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="939f6-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="939f6-125">AdvancedOutput</span></span>| <span data-ttu-id="939f6-126">Als u AdvancedOutput ingesteld op true, wordt de JSON-uitvoer positionele gegevens voor elke één woord (in aanvulling op zinnen en regio's) bevatten.</span><span class="sxs-lookup"><span data-stu-id="939f6-126">If you set AdvancedOutput to true, the JSON output will contain positional data for every single word (in addition to phrases and regions).</span></span> <span data-ttu-id="939f6-127">Als u niet zien van deze gegevens wilt, moet u de vlag ingesteld op false.</span><span class="sxs-lookup"><span data-stu-id="939f6-127">If you do not want to see these details, set the flag to false.</span></span> <span data-ttu-id="939f6-128">De standaardwaarde is ingesteld op false.</span><span class="sxs-lookup"><span data-stu-id="939f6-128">The default value is false.</span></span> <span data-ttu-id="939f6-129">Zie voor meer informatie [deze blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="939f6-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="939f6-130">Taal</span><span class="sxs-lookup"><span data-stu-id="939f6-130">Language</span></span> |<span data-ttu-id="939f6-131">(optioneel) een beschrijving van de taal van de tekst waarnaar moet worden gezocht.</span><span class="sxs-lookup"><span data-stu-id="939f6-131">(optional) describes the language of text for which to look.</span></span> <span data-ttu-id="939f6-132">Een van de volgende: AutoDetect (standaard), Arabisch, ChineseSimplified, ChineseTraditional, Tsjechisch Deens, Nederlands, Engels, Fins, Frans, Duits, Grieks, Hongaars, Italiaans, Japans, Koreaans, Noors, Pools, Portugees, Roemeens, Russisch, SerbianCyrillic, SerbianLatin, Slowaaks, Spaans, Zweeds, Turks.</span><span class="sxs-lookup"><span data-stu-id="939f6-132">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="939f6-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="939f6-133">TextOrientation</span></span> |<span data-ttu-id="939f6-134">(optioneel) een beschrijving van de richting van tekst voor waarnaar moet worden gezocht.</span><span class="sxs-lookup"><span data-stu-id="939f6-134">(optional) describes the orientation of text for which to look.</span></span>  <span data-ttu-id="939f6-135">"Left" betekent dat er met de bovenkant van alle letters waarnaar wordt verwezen naar links.</span><span class="sxs-lookup"><span data-stu-id="939f6-135">"Left" means that the top of all letters are pointed towards the left.</span></span>  <span data-ttu-id="939f6-136">De standaardtekst (zoals die die kunnen worden gevonden in een boek) kan worden aangeroepen 'Van' objectgeoriënteerde.</span><span class="sxs-lookup"><span data-stu-id="939f6-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="939f6-137">Een van de volgende: AutoDetect (standaard), maximaal, rechts, omlaag, links.</span><span class="sxs-lookup"><span data-stu-id="939f6-137">One of the following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="939f6-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="939f6-138">TimeInterval</span></span> |<span data-ttu-id="939f6-139">(optioneel) wordt de samplingfrequentie beschreven.</span><span class="sxs-lookup"><span data-stu-id="939f6-139">(optional) describes the sampling rate.</span></span>  <span data-ttu-id="939f6-140">Standaard is elke seconde 1/2.</span><span class="sxs-lookup"><span data-stu-id="939f6-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="939f6-141">JSON-indeling –: mm: ss. SSS (standaard 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="939f6-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="939f6-142">XML-indeling W3C XSD duur primitieve (standaard PT0.5)</span><span class="sxs-lookup"><span data-stu-id="939f6-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="939f6-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="939f6-143">DetectRegions</span></span> |<span data-ttu-id="939f6-144">(optioneel) Een matrix van DetectRegion objecten regio's binnen de video frame waarin u voor het detecteren van tekst opgeven.</span><span class="sxs-lookup"><span data-stu-id="939f6-144">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span></span><br/><span data-ttu-id="939f6-145">Een object DetectRegion bestaat de volgende vier waarden:</span><span class="sxs-lookup"><span data-stu-id="939f6-145">A DetectRegion object is made of the following four integer values:</span></span><br/><span data-ttu-id="939f6-146">Links: pixels van de linkermarge</span><span class="sxs-lookup"><span data-stu-id="939f6-146">Left – pixels from the left-margin</span></span><br/><span data-ttu-id="939f6-147">Top – pixels van de bovenmarge</span><span class="sxs-lookup"><span data-stu-id="939f6-147">Top – pixels from the top-margin</span></span><br/><span data-ttu-id="939f6-148">Breedte – breedte van de regio in pixels</span><span class="sxs-lookup"><span data-stu-id="939f6-148">Width – width of the region in pixels</span></span><br/><span data-ttu-id="939f6-149">Hoogte – hoogte van de regio in pixels</span><span class="sxs-lookup"><span data-stu-id="939f6-149">Height – height of the region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="939f6-150">Vooraf gedefinieerde JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="939f6-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="939f6-151">Vooraf gedefinieerde XML-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="939f6-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="939f6-152">De uitvoerbestanden OCR</span><span class="sxs-lookup"><span data-stu-id="939f6-152">OCR output files</span></span>
<span data-ttu-id="939f6-153">De uitvoer van de processor van de media OCR is een JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="939f6-153">The output of the OCR media processor is a JSON file.</span></span>

### <a name="elements-of-the-output-json-file"></a><span data-ttu-id="939f6-154">Elementen van de JSON-bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="939f6-154">Elements of the output JSON file</span></span>
<span data-ttu-id="939f6-155">De uitvoer van de Video OCR biedt tijd gesegmenteerde gegevens van de tekens in uw video gevonden.</span><span class="sxs-lookup"><span data-stu-id="939f6-155">The Video OCR output provides time-segmented data on the characters found in your video.</span></span>  <span data-ttu-id="939f6-156">U kunt kenmerken, zoals taal of de afdrukstand hone in op woorden dat u geïnteresseerd in analyseren bent.</span><span class="sxs-lookup"><span data-stu-id="939f6-156">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span></span> 

<span data-ttu-id="939f6-157">De uitvoer bevat de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="939f6-157">The output contains the following attributes:</span></span>

| <span data-ttu-id="939f6-158">Element</span><span class="sxs-lookup"><span data-stu-id="939f6-158">Element</span></span> | <span data-ttu-id="939f6-159">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="939f6-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="939f6-160">Tijdschaal</span><span class="sxs-lookup"><span data-stu-id="939f6-160">Timescale</span></span> |<span data-ttu-id="939f6-161">'maatstreepjes' per seconde van de video</span><span class="sxs-lookup"><span data-stu-id="939f6-161">"ticks" per second of the video</span></span> |
| <span data-ttu-id="939f6-162">Offset</span><span class="sxs-lookup"><span data-stu-id="939f6-162">Offset</span></span> |<span data-ttu-id="939f6-163">tijdzoneverschil voor tijdstempels.</span><span class="sxs-lookup"><span data-stu-id="939f6-163">time offset for timestamps.</span></span> <span data-ttu-id="939f6-164">Versie 1.0 van Video-API's, zal dit altijd 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="939f6-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="939f6-165">framesnelheid</span><span class="sxs-lookup"><span data-stu-id="939f6-165">Framerate</span></span> |<span data-ttu-id="939f6-166">Frames per seconde van de video</span><span class="sxs-lookup"><span data-stu-id="939f6-166">Frames per second of the video</span></span> |
| <span data-ttu-id="939f6-167">Breedte</span><span class="sxs-lookup"><span data-stu-id="939f6-167">width</span></span> |<span data-ttu-id="939f6-168">breedte van de video in pixels</span><span class="sxs-lookup"><span data-stu-id="939f6-168">width of the video in pixels</span></span> |
| <span data-ttu-id="939f6-169">Hoogte</span><span class="sxs-lookup"><span data-stu-id="939f6-169">height</span></span> |<span data-ttu-id="939f6-170">hoogte van de video in pixels</span><span class="sxs-lookup"><span data-stu-id="939f6-170">height of the video in pixels</span></span> |
| <span data-ttu-id="939f6-171">fragmenten</span><span class="sxs-lookup"><span data-stu-id="939f6-171">Fragments</span></span> |<span data-ttu-id="939f6-172">matrix van reeksen video waarin de metagegevens wordt gesegmenteerde op basis van tijd</span><span class="sxs-lookup"><span data-stu-id="939f6-172">array of time-based chunks of video into which the metadata is chunked</span></span> |
| <span data-ttu-id="939f6-173">start</span><span class="sxs-lookup"><span data-stu-id="939f6-173">start</span></span> |<span data-ttu-id="939f6-174">Begintijd van een fragment in 'maatstreepjes'</span><span class="sxs-lookup"><span data-stu-id="939f6-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="939f6-175">Duur</span><span class="sxs-lookup"><span data-stu-id="939f6-175">duration</span></span> |<span data-ttu-id="939f6-176">lengte van een fragment in 'maatstreepjes'</span><span class="sxs-lookup"><span data-stu-id="939f6-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="939f6-177">Interval</span><span class="sxs-lookup"><span data-stu-id="939f6-177">interval</span></span> |<span data-ttu-id="939f6-178">het interval van elke gebeurtenis in het opgegeven fragment</span><span class="sxs-lookup"><span data-stu-id="939f6-178">interval of each event within the given fragment</span></span> |
| <span data-ttu-id="939f6-179">events</span><span class="sxs-lookup"><span data-stu-id="939f6-179">events</span></span> |<span data-ttu-id="939f6-180">matrix met regio 's</span><span class="sxs-lookup"><span data-stu-id="939f6-180">array containing regions</span></span> |
| <span data-ttu-id="939f6-181">Regio</span><span class="sxs-lookup"><span data-stu-id="939f6-181">region</span></span> |<span data-ttu-id="939f6-182">object dat vertegenwoordigt woorden of zinnen gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="939f6-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="939f6-183">taal</span><span class="sxs-lookup"><span data-stu-id="939f6-183">language</span></span> |<span data-ttu-id="939f6-184">taal van de tekst binnen een regio gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="939f6-184">language of the text detected within a region</span></span> |
| <span data-ttu-id="939f6-185">afdrukstand</span><span class="sxs-lookup"><span data-stu-id="939f6-185">orientation</span></span> |<span data-ttu-id="939f6-186">richting van de tekst binnen een regio gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="939f6-186">orientation of the text detected within a region</span></span> |
| <span data-ttu-id="939f6-187">regels</span><span class="sxs-lookup"><span data-stu-id="939f6-187">lines</span></span> |<span data-ttu-id="939f6-188">matrix van regels tekst binnen een regio gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="939f6-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="939f6-189">Tekst</span><span class="sxs-lookup"><span data-stu-id="939f6-189">text</span></span> |<span data-ttu-id="939f6-190">de werkelijke tekst</span><span class="sxs-lookup"><span data-stu-id="939f6-190">the actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="939f6-191">Voorbeeld van JSON-uitvoer</span><span class="sxs-lookup"><span data-stu-id="939f6-191">JSON output example</span></span>
<span data-ttu-id="939f6-192">Het volgende Uitvoervoorbeeld bevat de algemene video informatie en verschillende video fragmenten.</span><span class="sxs-lookup"><span data-stu-id="939f6-192">The following output example contains the general video information and several video fragments.</span></span> <span data-ttu-id="939f6-193">In elke video fragment bevat elke regio die wordt gedetecteerd door OCR MP met de taal en de richting van tekst.</span><span class="sxs-lookup"><span data-stu-id="939f6-193">In every video fragment, it contains every region which is detected by OCR MP with the language and its text orientation.</span></span> <span data-ttu-id="939f6-194">De regio bevat ook elke regel woord in deze regio met de regel tekst, de positie van de regel en elke word-gegevens (word-inhoud, positie en vertrouwen) in deze regel.</span><span class="sxs-lookup"><span data-stu-id="939f6-194">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="939f6-195">Hier volgt een voorbeeld en ik bepaalde inline opmerkingen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="939f6-195">The following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // the time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // the detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including the text and the position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="939f6-196">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="939f6-196">.NET sample code</span></span>

<span data-ttu-id="939f6-197">De volgende programma toont hoe:</span><span class="sxs-lookup"><span data-stu-id="939f6-197">The following program shows how to:</span></span>

1. <span data-ttu-id="939f6-198">Maak een asset en upload een mediabestand naar de asset.</span><span class="sxs-lookup"><span data-stu-id="939f6-198">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="939f6-199">Een taak maken met een OCR configuration/voorinstelling-bestand.</span><span class="sxs-lookup"><span data-stu-id="939f6-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="939f6-200">De uitvoer JSON-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="939f6-200">Download the output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="939f6-201">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="939f6-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="939f6-202">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="939f6-202">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="939f6-203">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="939f6-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
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

                // Run the OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference to Azure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="939f6-204">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="939f6-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="939f6-205">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="939f6-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="939f6-206">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="939f6-206">Related links</span></span>
[<span data-ttu-id="939f6-207">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="939f6-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

