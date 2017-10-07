---
title: aaaAnalyze uw media met Azure-portal Hallo | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooprocess uw media met Media Analytics-mediaprocessoren (Management Packs) met behulp van hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Analyseer uw media met behulp van hello Azure-portal
> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
> 
> 

## <a name="overview"></a>Overzicht
Azure Media Services Analytics is een verzameling spraakonderdelen en visuele onderdelen (op enterprise schaal, naleving, beveiliging en globale bereiken) waarmee het eenvoudiger voor organisaties en bedrijven tooderive bruikbare inzichten aan hun video's. Zie voor meer overzicht van Azure Media Services Analytics [dit](media-services-analytics-overview.md) onderwerp. 

Dit onderwerp wordt beschreven hoe tooprocess uw media met Media Analytics-mediaprocessoren (Management Packs) met behulp van hello Azure-portal. Media Analytics Management Packs produceren MP4-bestanden of JSON-bestanden. Als een Mediaprocessor een MP4-bestand, kunt u Hallo bestand progressief downloaden. Als een Mediaprocessor een JSON-bestand, kunt u Hallo-bestand downloaden van hello Azure blob-opslag. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Kies een asset die u tooanalyze wilt
1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.
2. In Hallo **instellingen** Selecteer **activa**.  
   .
    ![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Selecteer Hallo asset die u wilt dat tooanalyze en druk op Hallo **analyseren** knop.
   
    ![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. In Hallo **proces media asset met Media Analytics** venster, selecteer Hallo-processor. 
   
    Hallo rest van Hallo artikel wordt uitgelegd waarom en hoe toouse elke processor. 
5. Druk op **maken** toohello start een taak.

## <a name="azure-media-indexer"></a>Azure Media Indexer
Hallo **Azure Media Indexer** Mediaprocessor kunt u toomake media-bestanden en inhoud kan worden doorzocht, evenals gesloten closed captioning houdt genereren. In deze sectie biedt een aantal details van de opties die u voor deze MP opgeven kunt.

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>Taal
Hallo natuurlijke taal toobe herkend in multimedia Hallo-bestand. Engels of Spaans. 

### <a name="captions"></a>Bijschriften
U kunt een bijschrift-indeling die zal worden gegenereerd op basis van uw inhoud. Een indexing-taak kan ondertitelingsbestanden bestanden in de volgende indelingen Hallo genereren:  

* **SAMI**
* **TTML**
* **WebVTT**

Gesloten bijschrift (CC)-bestanden in de volgende indelingen kunnen worden gebruikt toomake audio en video bestanden toegankelijk toopeople met handicap horen.

### <a name="aib-file"></a>AIB bestand
Selecteer deze optie als u zou zoals toogenerate Hallo Audio Index Blob-bestand voor gebruik met Hallo IFilter van aangepaste SQL-Server. Zie voor meer informatie [dit](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.

### <a name="keywords"></a>Trefwoorden
Selecteer deze optie als u toogenerate een trefwoorden XML-bestand wilt. Dit bestand bevat trefwoorden geëxtraheerd uit Hallo spraak inhoud, met de frequentie en offset informatie.

### <a name="job-name"></a>Taaknaam
Een beschrijvende naam waarmee u Hallo taak identificeren. [Dit](media-services-portal-check-job-progress.md) artikel wordt beschreven hoe u de voortgang van een taak Hallo kunt bewaken. 

### <a name="output-file"></a>Bestand voor uitvoer
Een beschrijvende naam waarmee u Hallo uitvoer inhoud identificeren. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure Media Hyperlapse is een Management Pack dat smooth video's verstreken tijd van eerste persoon of actie camera inhoud maakt.  Raadpleeg [dit](media-services-hyperlapse-content.md) onderwerp voor meer informatie. In deze sectie biedt een aantal details van de opties die u voor deze MP opgeven kunt.

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Snelheid
Hallo snelheid met welke toospeed up Hallo invoervideo opgeven. Hallo-uitvoer is een weergave gestabiliseerd en verstreken tijd van Hallo invoervideo.

### <a name="job-name"></a>Taaknaam
Een beschrijvende naam waarmee u Hallo taak identificeren. [Dit](media-services-portal-check-job-progress.md) artikel wordt beschreven hoe u de voortgang van een taak Hallo kunt bewaken. 

### <a name="output-file"></a>Bestand voor uitvoer
Een beschrijvende naam waarmee u Hallo uitvoer inhoud identificeren. 

## <a name="azure-media-face-detector"></a>Azure Media Face Detector
Hallo **Azure Media Face detectie** Mediaprocessor (MP) kunt u toocount, de bewegingen bijhouden, en zelfs meter doelgroep deelname en reactie via bedacht. Deze service bevat twee functies: 

* **Face-detectie**
  
    Face-detectie zoekt en houdt menselijke vlakken binnen een video. Meerdere vlakken kunnen worden gedetecteerd en vervolgens worden bijgehouden als ze onderweg, met Hallo-metagegevens en de locatie geretourneerd in een JSON-bestand. Tijdens de bijhouden, wordt geprobeerd toogive een consistente ID toohello dezelfde geconfronteerd terwijl Hallo persoon is navigeren op het scherm, zelfs als ze zijn ondervindt hinder van obstakels of kort Hallo frame laat.
  
  > [!NOTE]
  > Deze services voert geen gezichtsherkenning. Een persoon die Hallo frame verlaat of ondervindt voor wordt hinder van obstakels te lang krijgt een nieuwe ID wanneer ze terugkeren.
  > 
  > 
* **Emotiedetectie**
  
    Emotiedetectie is een optioneel onderdeel van Hallo Face Detection Media Processor op dat analyse op meerdere emotionele kenmerken van Hallo vlakken gedetecteerd retourneert, met inbegrip van gelukkig, sadness bang, volgt uitzien en meer. 

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Modus voor detectie
Een van de volgende modi Hallo kan worden gebruikt door Hallo processor:

* Face-detectie
* per emotiedetectie face
* cumulatieve emotiedetectie

### <a name="job-name"></a>Taaknaam
Een beschrijvende naam waarmee u Hallo taak identificeren. [Dit](media-services-portal-check-job-progress.md) artikel wordt beschreven hoe u de voortgang van een taak Hallo kunt bewaken. 

### <a name="output-file"></a>Bestand voor uitvoer
Een beschrijvende naam waarmee u Hallo uitvoer inhoud identificeren. 

## <a name="azure-media-motion-detector"></a>Azure Media Motion Detector
Hallo **Azure Media beweging detectie** media processor (MP) kunt u tooefficiently secties van belang zijn binnen een video anders lang en probleemloze identificeren. Bewegingsdetectie kan worden gebruikt voor statische camera beeldmateriaal tooidentify secties van Hallo video waar beweging optreedt. Er wordt een JSON-bestand met een metagegevens met tijdstempels en de regio waar Hallo gebeurtenis heeft plaatsgevonden voor begrenzingsvak Hallo gegenereerd.

Gericht op beveiliging video feeds, is deze technologie kunnen toocategorize beweging in de relevante gebeurtenissen en fout-positieven zoals schaduwen en licht wijzigingen. Hiermee kunt u toogenerate beveiligingswaarschuwingen van de camera feeds zonder terwijl tooextract kunnen momenten van belang van zeer lange toezicht video's met oneindige irrelevante gebeurtenissen, spam.

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure Media Video Thumbnails
Deze processor kunt u bij het maken van samenvattingen van lange video's door interessante codefragmenten automatisch selecteren van bronvideo Hallo. Dit is handig als u wilt dat een snel overzicht van welke tooexpect in een lange video tooprovide. Zie voor gedetailleerde informatie en voorbeelden [gebruik Azure Media Video Thumbnails tooCreate samenvatting van een Video](media-services-video-summarization.md)

![Video's analyseren](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>Taaknaam
Een beschrijvende naam waarmee u Hallo taak identificeren. [Dit](media-services-portal-check-job-progress.md) artikel wordt beschreven hoe u de voortgang van een taak Hallo kunt bewaken. 

### <a name="output-file"></a>Bestand voor uitvoer
Een beschrijvende naam waarmee u Hallo uitvoer inhoud identificeren. 

## <a name="next-steps"></a>Volgende stappen
Weergave Media Services-leertrajecten.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

