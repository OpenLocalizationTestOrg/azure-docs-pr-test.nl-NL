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
# <a name="media-analytics-on-hello-media-services-platform"></a>Media Analytics op Hallo Media Services-platform
## <a name="overview"></a>Overzicht
Meer organisaties video als voorkeur gemiddeld tootrain Hallo hun werknemers gebruikt, hun klanten en document bedrijfsfuncties benaderen. Cloud computing biedt een toostore manier stream en toegang tot deze grote mediabestanden. Maar als bibliotheek van video-inhoud van een bedrijf groeit, moet een even efficiënt middel insights extraheren uit Hallo inhoud. 

tooaddress deze groeiende behoefte Azure Media Services biedt Azure Media Analytics. Media Analytics is een verzameling spraakonderdelen en visuele onderdelen waarmee eenvoudiger voor organisaties en bedrijven tooderive bruikbare inzichten aan hun video's. Gebouwd met behulp van Media Services Hallo-platform hoofdonderdelen, kunnen Media Analytics media verwerken op grote schaal op dag één verwerken.

Met Media Analytics kunnen ontwikkelaars snel geavanceerde functionaliteit van de video doen in toepassingen. Het biedt bedrijfsomgevingen Hallo volledige schaal, naleving, beveiliging en globale bereiken die vereist zijn voor grote organisaties.

Hallo volgende diagram toont Media Analytics en andere belangrijke onderdelen van Hallo Media Services-platform. 

![VoD-werkstroom](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

Media Analytics-mediaprocessoren produceren MP4- of JSON-bestanden. Als een Mediaprocessor een MP4-bestand produceert, kunt u Hallo bestand progressief downloaden. Als een Mediaprocessor een JSON-bestand produceert, kunt u Hallo-bestand downloaden uit Azure Blob-opslag. 

## <a name="media-analytics-services"></a>Media Analytics-services

### <a name="indexer"></a>Indexer
Met Azure Media Indexer, kunt u inhoud doorzoekbare en houdt gesloten ondertiteling te genereren. Vergeleken toohello eerdere versie, Azure Media Indexer 2 Preview heeft sneller indexering en breder taal ondersteunen. Ondersteunde talen zijn Engels, Spaans, Frans, Duits, Italiaans, Chinees, Portugees en Arabisch. Zie voor gedetailleerde informatie en voorbeelden [video's verwerken met Azure Media Indexer 2](media-services-process-content-with-indexer2.md).
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse combineert video stabilization en time-lapse mogelijkheid toocreate snelle, verbruikbare video's van uw inhoud lange vorm. U kunt naast het maken van time-lapse video Hyperlapse toocreate stabiele video's van beelden video's die zijn vastgelegd via mobiele telefoons en camcorders gebruiken. Zie voor gedetailleerde informatie en voorbeelden [Hyperlapse media-bestanden met Azure Media Hyperlapse](media-services-hyperlapse-content.md).
### <a name="motion-detector"></a>Bewegingsherkenning
U kunt beweging detectie toodetect beweging gebruiken in een video met een stilstaan achtergrond. Dit maakt het mogelijk toocheck voor fout-positieven op motion gebeurtenissen gedetecteerd door bewakingscamera's te gebruiken. Zie voor gedetailleerde informatie en voorbeelden [Bewegingsdetectie voor Azure Media Analytics](media-services-motion-detection.md).
### <a name="face-detector"></a>Gezichtsherkenning
Face-detectie gebruikt, kunt u vlakken van gebruikers en hun emoties, inclusief gelukkig, sadness en onverwacht detecteren. Dit heeft verschillende nuttig toepassingen in sectoren verderop, met inbegrip van aggregeren en analyseren van reacties van mensen die een gebeurtenis. Zie voor gedetailleerde informatie en voorbeelden [gezichts- en emotion detectie voor Azure Media Analytics](media-services-face-and-emotion-detection.md).
### <a name="video-summarization"></a>Samenvatting van de video
Samenvatting van de video kan helpen u bij het maken van samenvattingen van lange video's door interessante codefragmenten automatisch selecteren van bronvideo Hallo. Dit is handig als u wilt dat een snel overzicht van welke tooexpect in een lange video tooprovide. Zie voor gedetailleerde informatie en voorbeelden [samenvatting van gebruik Azure Media Video miniaturen toocreate de video](media-services-video-summarization.md).
### <a name="optical-character-recognition"></a>Optische tekenherkenning
Met Azure Media OCR (OCR), kunt u tekstinhoud in videobestanden converteren naar een bewerkbare, doorzoekbaar digitale tekst. U kunt vervolgens Hallo extractie van zinvolle metagegevens van de video signaal Hallo van uw media automatiseren.
### <a name="scalable-face-redaction"></a>Schaalbare face redactie
Azure Media Redactor is een processor van Media Analytics media die schaalbare face redactie in Hallo cloud biedt. Face redactie gebruikt, kunt u uw video tooblur vlakken van geselecteerde gebruikers wijzigen. U kunt toouse Hallo face redactie service nieuws media of wanneer de openbare veiligheid is betrokken. Een paar minuten beeldmateriaal waarin meerdere vlakken handmatig tooredact uur kunnen duren, maar met deze service face redactie duurt een paar eenvoudige stappen. Zie voor meer informatie, Hallo [Redigeren vlakken met Azure Media Analytics](media-services-face-redaction.md) artikel.

## <a name="common-scenarios"></a>Algemene scenario's
Organisaties kunnen helpen bij Media Analytics en ondernemingen verzamelen inzichten van video en meer effectief beheer van grote hoeveelheden video-inhoud. Hier volgen enkele scenario's:

* **Roep centers**. Zelfs met Hallo komst van sociale media vergemakkelijken klantenservice aanroep afdelingen nog steeds een groot percentage van de klantenservice transacties. In deze audiogegevens gecodeerd, is een grote hoeveelheid klantgegevens die kan worden geanalyseerd tooachieve hogere klanttevredenheid. Organisaties kunnen met behulp van Media Indexer Haal de tekst en maak zoekindexen en dashboards. Vervolgens kunnen ze intelligence rond de algemene klachten bronnen van klachten en andere relevante gegevens extraheren.
* **Gebruikers gegenereerde inhoud toezicht**. Veel organisaties hebben van nieuws media aansluitingen toopolice afdelingen openbare portals die gebruiker gegenereerde media zoals video's en afbeeldingen te accepteren. Hallo volume van de inhoud kunt pieken toounexpected gebeurtenissen. In deze scenario's is het moeilijk tooconduct effectieve handmatige beoordelingen van inhoud voor geschiktheid. Klanten kunnen afhankelijk zijn van Hallo inhoud toezicht service toofocus voor inhoud die geschikt is.
* **Toezicht**. Hello komt groei in het gebruik van IP-camera's een groeiende inventarisatie van toezicht video. Handmatig controleren toezicht video is fout tijdrovende en foutgevoelige toohuman. Media Analytics biedt services zoals bewegingsdetectie face detection en Hyperlapse toomake Hallo proces controleren, beheren en afleidingen gemakkelijker te maken.

## <a name="media-analytics-media-processors"></a>Media Analytics-mediaprocessoren
Deze sectie door lijsten Hallo Media Analytics-mediaprocessoren en toont hoe toouse .NET of REST tooget een media-processor (MP)-object.

### <a name="mp-names"></a>MP-namen
* Preview van Azure Media Indexer 2
* Azure Media Indexer
* Azure Media Hyperlapse
* Azure Media Face Detector
* Azure Media Motion Detector
* Azure Media Video Thumbnails
* Azure Media OCR

### <a name="net"></a>.NET
Hallo volgende functie duurt een Hallo opgegeven MP namen en een MP-object geretourneerd.

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


### <a name="rest"></a>REST
Aanvraag:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

Antwoord:

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

## <a name="demos"></a>Demo 's
Zie [Azure Media Analytics demo's](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).

## <a name="next-steps"></a>Volgende stappen
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Verwante artikelen:
Zie [Media Services Analytics aankondiging](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
