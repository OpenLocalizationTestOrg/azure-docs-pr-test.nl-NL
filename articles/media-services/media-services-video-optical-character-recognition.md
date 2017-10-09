---
title: aaaDigitize tekst met Azure Media Analytics OCR | Microsoft Docs
description: Azure Media Analytics OCR (OCR) kunt u de tekstinhoud tooconvert in videobestanden naar bewerkbare, doorzoekbaar digitale tekst.  Hiermee kunt u tooautomate Hallo extractie van zinvolle metagegevens van de video signaal Hallo van uw media.
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
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="8e170-104">Gebruik Azure Media Analytics tooconvert tekstinhoud in videobestanden in digitale tekst</span><span class="sxs-lookup"><span data-stu-id="8e170-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="8e170-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8e170-105">Overview</span></span>
<span data-ttu-id="8e170-106">Als u tekst tooextract inhoud van uw video's moet en een bewerkbare, doorzoekbaar digitale tekst wordt gegenereerd, moet u Azure Media Analytics OCR (OCR).</span><span class="sxs-lookup"><span data-stu-id="8e170-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="8e170-107">Deze Azure Media Processor tekstinhoud detecteert in uw video's en genereert tekstbestanden voor het gebruik.</span><span class="sxs-lookup"><span data-stu-id="8e170-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="8e170-108">OCR kunt u tooautomate Hallo extractie van zinvolle metagegevens van de video signaal Hallo van uw media.</span><span class="sxs-lookup"><span data-stu-id="8e170-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="8e170-109">Wanneer gebruikt in combinatie met een zoekmachine, kunt u eenvoudig uw media indexering van tekst en Hallo detectie van uw inhoud verbeteren.</span><span class="sxs-lookup"><span data-stu-id="8e170-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="8e170-110">Dit is zeer nuttig zijn bij zeer tekstuele video, zoals een video-opname of een schermopname van een diavoorstelling.</span><span class="sxs-lookup"><span data-stu-id="8e170-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="8e170-111">Hello Azure OCR Mediaprocessor is geoptimaliseerd voor digitale tekst.</span><span class="sxs-lookup"><span data-stu-id="8e170-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="8e170-112">Hallo **Azure Media OCR** Mediaprocessor is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="8e170-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="8e170-113">Dit onderwerp bevat informatie over **Azure Media OCR** en ziet u hoe toouse met Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="8e170-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="8e170-114">Zie voor meer informatie en voorbeelden [deze blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="8e170-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="8e170-115">De invoerbestanden OCR</span><span class="sxs-lookup"><span data-stu-id="8e170-115">OCR input files</span></span>
<span data-ttu-id="8e170-116">Videobestanden.</span><span class="sxs-lookup"><span data-stu-id="8e170-116">Video files.</span></span> <span data-ttu-id="8e170-117">Op dit moment Hallo volgende indelingen worden ondersteund: MP4 MOV en WMV.</span><span class="sxs-lookup"><span data-stu-id="8e170-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="8e170-118">Taken configureren</span><span class="sxs-lookup"><span data-stu-id="8e170-118">Task configuration</span></span>
<span data-ttu-id="8e170-119">Taken configureren (standaardoptie).</span><span class="sxs-lookup"><span data-stu-id="8e170-119">Task configuration (preset).</span></span> <span data-ttu-id="8e170-120">Bij het maken van een taak met **Azure Media OCR**, moet u een configuratie met JSON of XML-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="8e170-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="8e170-121">Hallo OCR-engine duurt slechts een installatiekopie-regio met minimale 40 pixels toomaximum 32000 pixels als een geldige invoer in beide hoogte/breedte.</span><span class="sxs-lookup"><span data-stu-id="8e170-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="8e170-122">Beschrijvingen van kenmerken</span><span class="sxs-lookup"><span data-stu-id="8e170-122">Attribute descriptions</span></span>
| <span data-ttu-id="8e170-123">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="8e170-123">Attribute name</span></span> | <span data-ttu-id="8e170-124">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8e170-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="8e170-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="8e170-125">AdvancedOutput</span></span>| <span data-ttu-id="8e170-126">Als u AdvancedOutput tootrue instelt, wordt in Hallo JSON-uitvoer positionele gegevens voor elke één woord (in aanvulling toophrases en regio's) bevatten.</span><span class="sxs-lookup"><span data-stu-id="8e170-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="8e170-127">Als u niet dat toosee wilt vlag deze details kunt set Hallo toofalse.</span><span class="sxs-lookup"><span data-stu-id="8e170-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="8e170-128">Hallo-standaardwaarde is false.</span><span class="sxs-lookup"><span data-stu-id="8e170-128">hello default value is false.</span></span> <span data-ttu-id="8e170-129">Zie voor meer informatie [deze blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="8e170-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="8e170-130">Taal</span><span class="sxs-lookup"><span data-stu-id="8e170-130">Language</span></span> |<span data-ttu-id="8e170-131">(optioneel) beschrijft Hallo taal van de tekst voor welke toolook.</span><span class="sxs-lookup"><span data-stu-id="8e170-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="8e170-132">Een van de volgende Hallo: AutoDetect (standaard), Arabisch, ChineseSimplified, ChineseTraditional, Tsjechisch Deens, Nederlands, Engels, Fins, Frans, Duits, Grieks, Hongaars, Italiaans, Japans, Koreaans, Noors, Pools, Portugees, Roemeens, Russisch, SerbianCyrillic, SerbianLatin, Slowaaks, Spaans, Zweeds, Turks.</span><span class="sxs-lookup"><span data-stu-id="8e170-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="8e170-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="8e170-133">TextOrientation</span></span> |<span data-ttu-id="8e170-134">(optioneel) beschrijft Hallo richting van tekst voor welke toolook.</span><span class="sxs-lookup"><span data-stu-id="8e170-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="8e170-135">"Left" betekent dat Hallo boven aan alle letters worden waarnaar wordt verwezen naar Hallo links.</span><span class="sxs-lookup"><span data-stu-id="8e170-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="8e170-136">De standaardtekst (zoals die die kunnen worden gevonden in een boek) kan worden aangeroepen 'Van' objectgeoriënteerde.</span><span class="sxs-lookup"><span data-stu-id="8e170-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="8e170-137">Een van de volgende Hallo: AutoDetect (standaard), maximaal, rechts, omlaag, links.</span><span class="sxs-lookup"><span data-stu-id="8e170-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="8e170-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="8e170-138">TimeInterval</span></span> |<span data-ttu-id="8e170-139">(optioneel) wordt de samplingfrequentie Hallo beschreven.</span><span class="sxs-lookup"><span data-stu-id="8e170-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="8e170-140">Standaard is elke seconde 1/2.</span><span class="sxs-lookup"><span data-stu-id="8e170-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="8e170-141">JSON-indeling –: mm: ss. SSS (standaard 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="8e170-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="8e170-142">XML-indeling W3C XSD duur primitieve (standaard PT0.5)</span><span class="sxs-lookup"><span data-stu-id="8e170-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="8e170-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="8e170-143">DetectRegions</span></span> |<span data-ttu-id="8e170-144">(optioneel) Een matrix met regio's binnen de video frame Hallo opgeven in welke tekst toodetect DetectRegion-objecten.</span><span class="sxs-lookup"><span data-stu-id="8e170-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="8e170-145">Een object DetectRegion Hallo vier integerwaarden volgende bestaat:</span><span class="sxs-lookup"><span data-stu-id="8e170-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="8e170-146">Links: pixels van Hallo linkermarge</span><span class="sxs-lookup"><span data-stu-id="8e170-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="8e170-147">Top – pixels van Hallo bovenmarge</span><span class="sxs-lookup"><span data-stu-id="8e170-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="8e170-148">Breedte – breedte van Hallo gebied in pixels</span><span class="sxs-lookup"><span data-stu-id="8e170-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="8e170-149">Hoogte – hoogte van Hallo gebied in pixels</span><span class="sxs-lookup"><span data-stu-id="8e170-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="8e170-150">Vooraf gedefinieerde JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8e170-150">JSON preset example</span></span>

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


#### <a name="xml-preset-example"></a><span data-ttu-id="8e170-151">Vooraf gedefinieerde XML-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8e170-151">XML preset example</span></span>
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

## <a name="ocr-output-files"></a><span data-ttu-id="8e170-152">De uitvoerbestanden OCR</span><span class="sxs-lookup"><span data-stu-id="8e170-152">OCR output files</span></span>
<span data-ttu-id="8e170-153">Hallo-uitvoer van Hallo OCR Mediaprocessor is een JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="8e170-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="8e170-154">Elementen van Hallo uitvoer JSON-bestand</span><span class="sxs-lookup"><span data-stu-id="8e170-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="8e170-155">Hallo Video OCR uitvoer biedt gegevens tijd gesegmenteerd op Hallo-tekens in uw video zijn gevonden.</span><span class="sxs-lookup"><span data-stu-id="8e170-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="8e170-156">Kunt u kenmerken, zoals taal of toohone in stand op precies Hallo woorden dat u geïnteresseerd in analyseren bent.</span><span class="sxs-lookup"><span data-stu-id="8e170-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="8e170-157">Hallo uitvoer bevat Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="8e170-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="8e170-158">Element</span><span class="sxs-lookup"><span data-stu-id="8e170-158">Element</span></span> | <span data-ttu-id="8e170-159">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8e170-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e170-160">Tijdschaal</span><span class="sxs-lookup"><span data-stu-id="8e170-160">Timescale</span></span> |<span data-ttu-id="8e170-161">'maatstreepjes' per seconde van Hallo video</span><span class="sxs-lookup"><span data-stu-id="8e170-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="8e170-162">Offset</span><span class="sxs-lookup"><span data-stu-id="8e170-162">Offset</span></span> |<span data-ttu-id="8e170-163">tijdzoneverschil voor tijdstempels.</span><span class="sxs-lookup"><span data-stu-id="8e170-163">time offset for timestamps.</span></span> <span data-ttu-id="8e170-164">Versie 1.0 van Video-API's, zal dit altijd 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="8e170-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="8e170-165">framesnelheid</span><span class="sxs-lookup"><span data-stu-id="8e170-165">Framerate</span></span> |<span data-ttu-id="8e170-166">Frames per seconde van Hallo video</span><span class="sxs-lookup"><span data-stu-id="8e170-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="8e170-167">Breedte</span><span class="sxs-lookup"><span data-stu-id="8e170-167">width</span></span> |<span data-ttu-id="8e170-168">breedte van Hallo video in pixels</span><span class="sxs-lookup"><span data-stu-id="8e170-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="8e170-169">Hoogte</span><span class="sxs-lookup"><span data-stu-id="8e170-169">height</span></span> |<span data-ttu-id="8e170-170">hoogte van Hallo video in pixels</span><span class="sxs-lookup"><span data-stu-id="8e170-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="8e170-171">fragmenten</span><span class="sxs-lookup"><span data-stu-id="8e170-171">Fragments</span></span> |<span data-ttu-id="8e170-172">matrix van reeksen in welke Hallo metagegevens is chunked video op basis van tijd</span><span class="sxs-lookup"><span data-stu-id="8e170-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="8e170-173">start</span><span class="sxs-lookup"><span data-stu-id="8e170-173">start</span></span> |<span data-ttu-id="8e170-174">Begintijd van een fragment in 'maatstreepjes'</span><span class="sxs-lookup"><span data-stu-id="8e170-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="8e170-175">Duur</span><span class="sxs-lookup"><span data-stu-id="8e170-175">duration</span></span> |<span data-ttu-id="8e170-176">lengte van een fragment in 'maatstreepjes'</span><span class="sxs-lookup"><span data-stu-id="8e170-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="8e170-177">interval</span><span class="sxs-lookup"><span data-stu-id="8e170-177">interval</span></span> |<span data-ttu-id="8e170-178">het interval van elke gebeurtenis binnen een gegeven fragment Hallo</span><span class="sxs-lookup"><span data-stu-id="8e170-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="8e170-179">events</span><span class="sxs-lookup"><span data-stu-id="8e170-179">events</span></span> |<span data-ttu-id="8e170-180">matrix met regio 's</span><span class="sxs-lookup"><span data-stu-id="8e170-180">array containing regions</span></span> |
| <span data-ttu-id="8e170-181">Regio</span><span class="sxs-lookup"><span data-stu-id="8e170-181">region</span></span> |<span data-ttu-id="8e170-182">object dat vertegenwoordigt woorden of zinnen gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="8e170-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="8e170-183">taal</span><span class="sxs-lookup"><span data-stu-id="8e170-183">language</span></span> |<span data-ttu-id="8e170-184">taal van Hallo tekst binnen een regio gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="8e170-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="8e170-185">afdrukstand</span><span class="sxs-lookup"><span data-stu-id="8e170-185">orientation</span></span> |<span data-ttu-id="8e170-186">richting van Hallo tekst binnen een regio gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="8e170-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="8e170-187">regels</span><span class="sxs-lookup"><span data-stu-id="8e170-187">lines</span></span> |<span data-ttu-id="8e170-188">matrix van regels tekst binnen een regio gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="8e170-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="8e170-189">Tekst</span><span class="sxs-lookup"><span data-stu-id="8e170-189">text</span></span> |<span data-ttu-id="8e170-190">de werkelijke tekst Hello</span><span class="sxs-lookup"><span data-stu-id="8e170-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="8e170-191">Voorbeeld van JSON-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8e170-191">JSON output example</span></span>
<span data-ttu-id="8e170-192">Hallo bevat volgende voorbeeld van uitvoer algemene video informatie Hallo en verschillende video fragmenten.</span><span class="sxs-lookup"><span data-stu-id="8e170-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="8e170-193">In elke video fragment bevat elke regio die wordt gedetecteerd door OCR MP met de Hallo taal en de richting van tekst.</span><span class="sxs-lookup"><span data-stu-id="8e170-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="8e170-194">Hallo regio bevat ook elke regel woord in deze regio van Hallo regel tekst hello regelpositie en elke word-gegevens (word-inhoud, positie en vertrouwen) in deze regel.</span><span class="sxs-lookup"><span data-stu-id="8e170-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="8e170-195">Hallo Hieronder volgt een voorbeeld en ik bepaalde inline opmerkingen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8e170-195">hello following is an example, and I put some comments inline.</span></span>

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
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
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

## <a name="net-sample-code"></a><span data-ttu-id="8e170-196">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="8e170-196">.NET sample code</span></span>

<span data-ttu-id="8e170-197">Hallo volgende programma toont hoe:</span><span class="sxs-lookup"><span data-stu-id="8e170-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="8e170-198">Maak een asset en upload een mediabestand naar Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="8e170-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="8e170-199">Een taak maken met een OCR configuration/voorinstelling-bestand.</span><span class="sxs-lookup"><span data-stu-id="8e170-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="8e170-200">Hallo uitvoer JSON-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="8e170-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="8e170-201">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="8e170-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="8e170-202">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8e170-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="8e170-203">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8e170-203">Example</span></span>

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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="8e170-204">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="8e170-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8e170-205">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="8e170-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="8e170-206">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="8e170-206">Related links</span></span>
[<span data-ttu-id="8e170-207">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="8e170-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

