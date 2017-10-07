---
title: aaaRedact vlakken met Azure Media Analytics stapsgewijze Kennismaking | Microsoft Docs
description: Dit onderwerp bevat stapsgewijze instructies over het toorun een volledige redactie werkstroom met behulp van Azure Media Services Explorer (AMSE) en Azure Media Redactor Visualizer (open-source hulpprogramma).
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Redigeren vlakken met Azure Media Analytics-overzicht

## <a name="overview"></a>Overzicht

**Azure Media Redactor** is een [Azure Media Analytics](media-services-analytics-overview.md) Mediaprocessor (MP) die schaalbare face redactie in Hallo cloud biedt. Face redactie kunt u toomodify uw video in volgorde tooblur vlakken van geselecteerde gebruikers. U kunt toouse Hallo face redactie service in openbare veiligheid en nieuws media scenario's. Een paar minuten beeldmateriaal waarin meerdere vlakken handmatig tooredact uur kunnen duren, maar met deze service Hallo face redactie proces een paar eenvoudige stappen is vereist. Zie voor meer informatie [dit](https://azure.microsoft.com/blog/azure-media-redactor/) blog.

Voor meer informatie over **Azure Media Redactor**, Zie Hallo [Face redactie overzicht](media-services-face-redaction.md) onderwerp.

Dit onderwerp bevat stapsgewijze instructies over het toorun een volledige redactie werkstroom met behulp van Azure Media Services Explorer (AMSE) en Azure Media Redactor Visualizer (open-source hulpprogramma).

Hallo **Azure Media Redactor** MP is momenteel in Preview. Is beschikbaar in alle openbare Azure-regio's, evenals US Government en China datacenters. Dit voorbeeld is momenteel gratis. In de huidige release hello, moet u er een limiet van 10 minuten is op verwerkte video lengte.

Zie voor meer informatie [dit](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.

## <a name="azure-media-services-explorer-workflow"></a>Azure Media Services Explorer-werkstroom

Hallo gemakkelijkste manier tooget gestart met Redactor is toouse Hallo open-source AMSE-hulpprogramma op github. U kunt een vereenvoudigde werkstroom via uitvoeren **gecombineerd** modus als u niet toegang toohello aantekening json of Hallo face jpg-afbeeldingen tot moet.

### <a name="download-and-setup"></a>Downloaden en installeren

1. Download Hallo AMSE-hulpprogramma op [hier](https://github.com/Azure/Azure-Media-Services-Explorer).
1. Meld u bij tooyour Media Services-account met behulp van de servicesleutel van uw.

    tooobtain Hallo accountnaam en sleutelgegevens, Ga toohello [Azure-portal](https://portal.azure.com/) en selecteert u uw AMS-account. Selecteer deze instellingen > sleutels. Hallo beheren sleutels windows hello accountnaam ziet en Hallo primaire en secundaire sleutels worden weergegeven. Kopieer de waarden van het Hallo-accountnaam en het Hallo primaire sleutel.

![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>Eerst doorgeven: modus analyseren

1. Upload uw mediabestand via Asset –> uploaden, of via slepen en neerzetten. 
1. Klik met de rechtermuisknop en verwerken van uw mediabestand Media Analytics met Azure Media Redactor –> –> analyseren modus. 


![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

Hallo uitvoer bevat een json-bestand van aantekeningen met face locatiegegevens, evenals een jpg van elke gedetecteerde gezicht. 

![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>Tweede doorgeven – Redigeren modus

1. Upload uw oorspronkelijke video asset toohello de uitvoer van de eerste stap Hallo en instellen als primaire activa. 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (Optioneel) Bestand 'Dance_idlist.txt, waaronder een lijst met locatienamen gescheiden id's die u wenst dat tooredact Hallo uploaden. 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (Optioneel) Elk bewerkingen toohello annotations.json bestand, zoals verhogen Hallo omsluitende vak grenzen maken. 
4. Hallo uitvoerasset van de eerste stap Hallo Klik met de rechtermuisknop, selecteer Hallo Redactor en uitgevoerd met Hallo **Redact** modus. 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. Download of Hallo uiteindelijke geredigeerde uitvoerasset delen. 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Azure Media Redactor Visualizer open-source hulpprogramma

Een open-source [visualizer hulpprogramma](https://github.com/Microsoft/azure-media-redactor-visualizer) ontworpen toohelp ontwikkelaars net begint met de Hallo aantekeningen indeling met parseren en Hallo uitvoer is.

Nadat u Hallo-opslagplaats in volgorde toorun Hallo-project klonen, moet u toodownload FFMPEG van hun [officiële site](https://ffmpeg.org/download.html).

Als u een ontwikkelaar tooparse Hallo JSON aantekening gegevens probeert, zoekt u in Models.MetaData voorbeeld codevoorbeelden.

### <a name="set-up-hello-tool"></a>Hallo hulpprogramma instellen

1.  Download en bouw de volledige oplossing Hallo. 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  Download FFMPEG van [hier](https://ffmpeg.org/download.html). Dit project is oorspronkelijk ontwikkeld met versie be1d324 (2016-10-04) met het statisch koppelen. 
3.  Kopieer ffmpeg.exe en ffprobe.exe toohello dezelfde uitvoermap als AzureMediaRedactor.exe. 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. AzureMediaRedactor.exe worden uitgevoerd. 

### <a name="use-hello-tool"></a>Hallo-hulpprogramma gebruiken

1. Verwerken van uw video in uw Azure Media Services-account met Hallo Redactor MP op analyseren modus. 
2. Zowel de oorspronkelijke videobestand Hallo en uitvoer Hallo Hallo redactie downloaden - taak analyseren. 
3. Voer toepassing hello uit visualizer en kies Hallo bestanden hierboven. 

    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. Bekijk het bestand. Selecteer welke u bespreekt graag tooblur via Hallo zijbalk op Hallo rechts. 
    
    ![Gezichten onherkenbaar maken](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  Hallo onder tekstveld wordt bijgewerkt met de Hallo face id's. Maak een bestand met de naam 'idlist.txt' met deze id als een lijst met locatienamen gescheiden. 

    >[!NOTE]
    > Hallo idlist.txt moet worden opgeslagen in ANSI. U kunt Kladblok toosave in ANSI.
    
6.  Het uploaden van dit bestand toohello uitvoerasset uit stap 1. Hallo oorspronkelijke video toothis asset en upload en instellen als primaire asset. 
7.  Redactie taak uitvoeren op dit activum met 'Redact' modus tooget Hallo laatste geredigeerde video. 

## <a name="next-steps"></a>Volgende stappen 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Verwante koppelingen
[Azure Media Services Analytics-overzicht](media-services-analytics-overview.md)

[Azure Media Analytics-demo 's](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Face-redactie aangekondigd voor Azure Media Analytics](https://azure.microsoft.com/blog/azure-media-redactor/)
