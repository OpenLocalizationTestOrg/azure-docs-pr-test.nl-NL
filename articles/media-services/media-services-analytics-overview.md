---
title: aaaMedia Analytics op Hallo Media Services-platform | Microsoft Docs
description: Overzicht van de openbare preview van Media Analytics, een verzameling spraakonderdelen en computer vision-services op enterprise schaal, naleving, beveiliging en globale bereiken
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="2b39c-103">Media Analytics op Hallo Media Services-platform</span><span class="sxs-lookup"><span data-stu-id="2b39c-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="2b39c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2b39c-104">Overview</span></span>
<span data-ttu-id="2b39c-105">Meer organisaties video als voorkeur gemiddeld tootrain Hallo hun werknemers gebruikt, hun klanten en document bedrijfsfuncties benaderen.</span><span class="sxs-lookup"><span data-stu-id="2b39c-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="2b39c-106">Cloud computing biedt een toostore manier stream en toegang tot deze grote mediabestanden.</span><span class="sxs-lookup"><span data-stu-id="2b39c-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="2b39c-107">Maar als bibliotheek van video-inhoud van een bedrijf groeit, moet een even efficiënt middel insights extraheren uit Hallo inhoud.</span><span class="sxs-lookup"><span data-stu-id="2b39c-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="2b39c-108">tooaddress deze groeiende behoefte Azure Media Services biedt Azure Media Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b39c-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="2b39c-109">Media Analytics is een verzameling spraakonderdelen en visuele onderdelen waarmee eenvoudiger voor organisaties en bedrijven tooderive bruikbare inzichten aan hun video's.</span><span class="sxs-lookup"><span data-stu-id="2b39c-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="2b39c-110">Gebouwd met behulp van Media Services Hallo-platform hoofdonderdelen, kunnen Media Analytics media verwerken op grote schaal op dag één verwerken.</span><span class="sxs-lookup"><span data-stu-id="2b39c-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="2b39c-111">Met Media Analytics kunnen ontwikkelaars snel geavanceerde functionaliteit van de video doen in toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2b39c-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="2b39c-112">Het biedt bedrijfsomgevingen Hallo volledige schaal, naleving, beveiliging en globale bereiken die vereist zijn voor grote organisaties.</span><span class="sxs-lookup"><span data-stu-id="2b39c-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="2b39c-113">Hallo volgende diagram toont Media Analytics en andere belangrijke onderdelen van Hallo Media Services-platform.</span><span class="sxs-lookup"><span data-stu-id="2b39c-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![VoD-werkstroom](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="2b39c-115">Media Analytics-mediaprocessoren produceren MP4- of JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="2b39c-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="2b39c-116">Als een Mediaprocessor een MP4-bestand produceert, kunt u Hallo bestand progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="2b39c-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="2b39c-117">Als een Mediaprocessor een JSON-bestand produceert, kunt u Hallo-bestand downloaden uit Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="2b39c-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="2b39c-118">Media Analytics-services</span><span class="sxs-lookup"><span data-stu-id="2b39c-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="2b39c-119">Indexer</span><span class="sxs-lookup"><span data-stu-id="2b39c-119">Indexer</span></span>
<span data-ttu-id="2b39c-120">Met Azure Media Indexer, kunt u inhoud doorzoekbare en houdt gesloten ondertiteling te genereren.</span><span class="sxs-lookup"><span data-stu-id="2b39c-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="2b39c-121">Vergeleken toohello eerdere versie, Azure Media Indexer 2 Preview heeft sneller indexering en breder taal ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="2b39c-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="2b39c-122">Ondersteunde talen zijn Engels, Spaans, Frans, Duits, Italiaans, Chinees, Portugees en Arabisch.</span><span class="sxs-lookup"><span data-stu-id="2b39c-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="2b39c-123">Zie voor gedetailleerde informatie en voorbeelden [video's verwerken met Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="2b39c-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="2b39c-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="2b39c-124">Hyperlapse</span></span>
<span data-ttu-id="2b39c-125">Microsoft Hyperlapse combineert video stabilization en time-lapse mogelijkheid toocreate snelle, verbruikbare video's van uw inhoud lange vorm.</span><span class="sxs-lookup"><span data-stu-id="2b39c-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="2b39c-126">U kunt naast het maken van time-lapse video Hyperlapse toocreate stabiele video's van beelden video's die zijn vastgelegd via mobiele telefoons en camcorders gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2b39c-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="2b39c-127">Zie voor gedetailleerde informatie en voorbeelden [Hyperlapse media-bestanden met Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="2b39c-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="2b39c-128">Bewegingsherkenning</span><span class="sxs-lookup"><span data-stu-id="2b39c-128">Motion Detector</span></span>
<span data-ttu-id="2b39c-129">U kunt beweging detectie toodetect beweging gebruiken in een video met een stilstaan achtergrond.</span><span class="sxs-lookup"><span data-stu-id="2b39c-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="2b39c-130">Dit maakt het mogelijk toocheck voor fout-positieven op motion gebeurtenissen gedetecteerd door bewakingscamera's te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2b39c-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="2b39c-131">Zie voor gedetailleerde informatie en voorbeelden [Bewegingsdetectie voor Azure Media Analytics](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="2b39c-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="2b39c-132">Gezichtsherkenning</span><span class="sxs-lookup"><span data-stu-id="2b39c-132">Face Detector</span></span>
<span data-ttu-id="2b39c-133">Face-detectie gebruikt, kunt u vlakken van gebruikers en hun emoties, inclusief gelukkig, sadness en onverwacht detecteren.</span><span class="sxs-lookup"><span data-stu-id="2b39c-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="2b39c-134">Dit heeft verschillende nuttig toepassingen in sectoren verderop, met inbegrip van aggregeren en analyseren van reacties van mensen die een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2b39c-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="2b39c-135">Zie voor gedetailleerde informatie en voorbeelden [gezichts- en emotion detectie voor Azure Media Analytics](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="2b39c-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="2b39c-136">Samenvatting van de video</span><span class="sxs-lookup"><span data-stu-id="2b39c-136">Video summarization</span></span>
<span data-ttu-id="2b39c-137">Samenvatting van de video kan helpen u bij het maken van samenvattingen van lange video's door interessante codefragmenten automatisch selecteren van bronvideo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b39c-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="2b39c-138">Dit is handig als u wilt dat een snel overzicht van welke tooexpect in een lange video tooprovide.</span><span class="sxs-lookup"><span data-stu-id="2b39c-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="2b39c-139">Zie voor gedetailleerde informatie en voorbeelden [samenvatting van gebruik Azure Media Video miniaturen toocreate de video](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="2b39c-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="2b39c-140">Optische tekenherkenning</span><span class="sxs-lookup"><span data-stu-id="2b39c-140">Optical character recognition</span></span>
<span data-ttu-id="2b39c-141">Met Azure Media OCR (OCR), kunt u tekstinhoud in videobestanden converteren naar een bewerkbare, doorzoekbaar digitale tekst.</span><span class="sxs-lookup"><span data-stu-id="2b39c-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="2b39c-142">U kunt vervolgens Hallo extractie van zinvolle metagegevens van de video signaal Hallo van uw media automatiseren.</span><span class="sxs-lookup"><span data-stu-id="2b39c-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="2b39c-143">Schaalbare face redactie</span><span class="sxs-lookup"><span data-stu-id="2b39c-143">Scalable face redaction</span></span>
<span data-ttu-id="2b39c-144">Azure Media Redactor is een processor van Media Analytics media die schaalbare face redactie in Hallo cloud biedt.</span><span class="sxs-lookup"><span data-stu-id="2b39c-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="2b39c-145">Face redactie gebruikt, kunt u uw video tooblur vlakken van geselecteerde gebruikers wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2b39c-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="2b39c-146">U kunt toouse Hallo face redactie service nieuws media of wanneer de openbare veiligheid is betrokken.</span><span class="sxs-lookup"><span data-stu-id="2b39c-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="2b39c-147">Een paar minuten beeldmateriaal waarin meerdere vlakken handmatig tooredact uur kunnen duren, maar met deze service face redactie duurt een paar eenvoudige stappen.</span><span class="sxs-lookup"><span data-stu-id="2b39c-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="2b39c-148">Zie voor meer informatie, Hallo [Redigeren vlakken met Azure Media Analytics](media-services-face-redaction.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="2b39c-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="2b39c-149">Algemene scenario's</span><span class="sxs-lookup"><span data-stu-id="2b39c-149">Common scenarios</span></span>
<span data-ttu-id="2b39c-150">Organisaties kunnen helpen bij Media Analytics en ondernemingen verzamelen inzichten van video en meer effectief beheer van grote hoeveelheden video-inhoud.</span><span class="sxs-lookup"><span data-stu-id="2b39c-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="2b39c-151">Hier volgen enkele scenario's:</span><span class="sxs-lookup"><span data-stu-id="2b39c-151">Here are several scenarios:</span></span>

* <span data-ttu-id="2b39c-152">**Roep centers**.</span><span class="sxs-lookup"><span data-stu-id="2b39c-152">**Call centers**.</span></span> <span data-ttu-id="2b39c-153">Zelfs met Hallo komst van sociale media vergemakkelijken klantenservice aanroep afdelingen nog steeds een groot percentage van de klantenservice transacties.</span><span class="sxs-lookup"><span data-stu-id="2b39c-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="2b39c-154">In deze audiogegevens gecodeerd, is een grote hoeveelheid klantgegevens die kan worden geanalyseerd tooachieve hogere klanttevredenheid.</span><span class="sxs-lookup"><span data-stu-id="2b39c-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="2b39c-155">Organisaties kunnen met behulp van Media Indexer Haal de tekst en maak zoekindexen en dashboards.</span><span class="sxs-lookup"><span data-stu-id="2b39c-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="2b39c-156">Vervolgens kunnen ze intelligence rond de algemene klachten bronnen van klachten en andere relevante gegevens extraheren.</span><span class="sxs-lookup"><span data-stu-id="2b39c-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="2b39c-157">**Gebruikers gegenereerde inhoud toezicht**.</span><span class="sxs-lookup"><span data-stu-id="2b39c-157">**User-generated content moderation**.</span></span> <span data-ttu-id="2b39c-158">Veel organisaties hebben van nieuws media aansluitingen toopolice afdelingen openbare portals die gebruiker gegenereerde media zoals video's en afbeeldingen te accepteren.</span><span class="sxs-lookup"><span data-stu-id="2b39c-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="2b39c-159">Hallo volume van de inhoud kunt pieken toounexpected gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="2b39c-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="2b39c-160">In deze scenario's is het moeilijk tooconduct effectieve handmatige beoordelingen van inhoud voor geschiktheid.</span><span class="sxs-lookup"><span data-stu-id="2b39c-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="2b39c-161">Klanten kunnen afhankelijk zijn van Hallo inhoud toezicht service toofocus voor inhoud die geschikt is.</span><span class="sxs-lookup"><span data-stu-id="2b39c-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="2b39c-162">**Toezicht**.</span><span class="sxs-lookup"><span data-stu-id="2b39c-162">**Surveillance**.</span></span> <span data-ttu-id="2b39c-163">Hello komt groei in het gebruik van IP-camera's een groeiende inventarisatie van toezicht video.</span><span class="sxs-lookup"><span data-stu-id="2b39c-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="2b39c-164">Handmatig controleren toezicht video is fout tijdrovende en foutgevoelige toohuman.</span><span class="sxs-lookup"><span data-stu-id="2b39c-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="2b39c-165">Media Analytics biedt services zoals bewegingsdetectie face detection en Hyperlapse toomake Hallo proces controleren, beheren en afleidingen gemakkelijker te maken.</span><span class="sxs-lookup"><span data-stu-id="2b39c-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="2b39c-166">Media Analytics-mediaprocessoren</span><span class="sxs-lookup"><span data-stu-id="2b39c-166">Media Analytics media processors</span></span>
<span data-ttu-id="2b39c-167">Deze sectie door lijsten Hallo Media Analytics-mediaprocessoren en toont hoe toouse .NET of REST tooget een media-processor (MP)-object.</span><span class="sxs-lookup"><span data-stu-id="2b39c-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="2b39c-168">MP-namen</span><span class="sxs-lookup"><span data-stu-id="2b39c-168">MP names</span></span>
* <span data-ttu-id="2b39c-169">Preview van Azure Media Indexer 2</span><span class="sxs-lookup"><span data-stu-id="2b39c-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="2b39c-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="2b39c-170">Azure Media Indexer</span></span>
* <span data-ttu-id="2b39c-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="2b39c-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="2b39c-172">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="2b39c-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="2b39c-173">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="2b39c-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="2b39c-174">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="2b39c-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="2b39c-175">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="2b39c-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="2b39c-176">.NET</span><span class="sxs-lookup"><span data-stu-id="2b39c-176">.NET</span></span>
<span data-ttu-id="2b39c-177">Hallo volgende functie duurt een Hallo opgegeven MP namen en een MP-object geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="2b39c-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="2b39c-178">REST</span><span class="sxs-lookup"><span data-stu-id="2b39c-178">REST</span></span>
<span data-ttu-id="2b39c-179">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="2b39c-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="2b39c-180">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="2b39c-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="2b39c-181">Demo 's</span><span class="sxs-lookup"><span data-stu-id="2b39c-181">Demos</span></span>
<span data-ttu-id="2b39c-182">Zie [Azure Media Analytics demo's](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="2b39c-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b39c-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b39c-183">Next steps</span></span>
<span data-ttu-id="2b39c-184">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="2b39c-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2b39c-185">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="2b39c-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="2b39c-186">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="2b39c-186">Related articles</span></span>
<span data-ttu-id="2b39c-187">Zie [Media Services Analytics aankondiging](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="2b39c-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
