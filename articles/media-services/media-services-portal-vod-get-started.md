---
title: aaaGet gestart met het leveren van VoD hello Azure-portal met | Microsoft Docs
description: Deze zelfstudie leert u Hallo van een basic Video-on-Demand (VoD) leveren van inhoud service implementeren met Azure Media Services (AMS)-toepassing hello Azure-portal gebruiken.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>Aan de slag met het leveren van inhoud on demand met hello Azure-portal
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Deze zelfstudie leert u Hallo van een basic Video-on-Demand (VoD) leveren van inhoud service implementeren met Azure Media Services (AMS)-toepassing hello Azure-portal gebruiken.

## <a name="prerequisites"></a>Vereisten
Hallo volgen vereist toocomplete Hallo-zelfstudie:

* Een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
* Een Media Services-account. een Media Services-account toocreate Zie [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).

Deze zelfstudie bevat Hallo taken te volgen:

1. Streaming-eindpunt starten.
2. Een videobestand uploaden.
3. Hallo-bronbestand coderen in een set adaptive bitrate MP4-bestanden.
4. Hallo asset publiceren en get streamen en progressief downloaden van URL's.  
5. Uw inhoud afspelen.

## <a name="start-streaming-endpoints"></a>Streaming-eindpunten starten 

Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo leveren van video via adaptive bitrate streaming. Media Services biedt dynamische pakketten zodat u toodeliver uw adaptive bitrate MP4-inhoud in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, zonder dat u vooraf verpakte toostore hoeft versies van elk van deze streaming-indelingen.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 

toostart Hallo streaming-eindpunt, Hallo te volgen:

1. Aanmelden op Hallo [Azure-portal](https://portal.azure.com/).
2. Klik in het venster Instellingen Hallo, Streaming-eindpunten. 
3. Klik op Hallo standaardstreaming-eindpunt. 

    Hallo DEFAULT STREAMING ENDPOINT DETAILS venster wordt weergegeven.

4. Klik op Hallo Start pictogram.
5. Klik op Hallo opslaan knop toosave uw wijzigingen.

## <a name="upload-files"></a>Bestanden uploaden
toostream video's met Azure Media Services, moet u tooupload Hallo bron video's, ze coderen in meerdere bitsnelheden en Hallo resultaat publiceren. Hallo eerste stap wordt in deze sectie beschreven. 

1. In Hallo **instelling** venster, klikt u op **activa**.
   
    ![Bestanden uploaden](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Klik op Hallo **uploaden** knop.
   
    Hallo **videoasset uploaden** venster wordt weergegeven.
   
   > [!NOTE]
   > Er geldt geen beperking voor de bestandsgrootte.
   > 
   > 
3. Blader toohello gewenste video op uw computer, selecteert u deze en klik op OK.  
   
    Hallo uploaden wordt gestart en u kunt de voortgang Hallo onder Hallo bestandsnaam bekijken.  

Nadat het Hallo uploaden is voltooid, ziet u Hallo nieuwe asset weergegeven in Hallo **activa** venster. 

## <a name="encode-assets"></a>Assets coderen

Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo adaptive bitrate streaming tooyour clients leveren. Media Services ondersteunt de volgende adaptive bitrate streaming-technologieën Hallo: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare uw video's voor adaptive bitrate streaming, moet u tooencode de bron-video in multi-bitrate-bestanden. Moet u Hallo **Media Encoder Standard** encoder tooencode uw video's.  

Media Services biedt ook dynamische pakketten zodat u toodeliver uw multi-bitrate MP4s in de volgende streaming-indelingen Hallo: MPEG DASH, HLS, Smooth Streaming, zonder dat u toorepackage in een van deze streaming-indelingen hoeft. Met dynamische pakketten hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services bouwt en Hallo juiste reactie op basis van aanvragen van een client fungeert.

tootake profiteren van dynamische pakketten hoeft u tooencode uw bronbestand in een set multi-bitrate MP4-bestanden (Hallo coderingsstappen worden uitgelegd later in deze sectie).

### <a name="toouse-hello-portal-tooencode"></a>toouse hello portal tooencode
Deze sectie beschrijft Hallo mogelijke stappen tooencode uw inhoud met Media Encoder Standard.

1. In Hallo **instellingen** Selecteer **activa**.  
2. In Hallo **activa** venster, selecteer Hallo asset dat u tooencode wilt.
3. Druk op Hallo **coderen** knop.
4. In Hallo **een asset coderen** venster, selecteer Hallo 'Media Encoder Standard' processor en een standaardinstelling. Zie [automatisch een bitrate ladder genereren](media-services-autogen-bitrate-ladder-with-mes.md) en [Standaardinstellingen voor taken in MES](media-services-mes-presets-overview.md) voor informatie over standaardinstellingen. Als u van plan toocontrol welke codering definitie wordt gebruikt bent, houd hiermee rekening: het is belangrijk tooselect Hallo voorinstelling die het meest geschikt is voor uw invoervideo. Bijvoorbeeld, als u weet dat uw invoervideo een resolutie van 1920 x 1080 pixels heeft, kan u Hallo ' standaardinstelling H264 Multiple Bitrate 1080p ' vooraf ingestelde. Als u een video met een lage resolutie (640 x 360) hebt, gebruikt u niet de standaardinstelling H264 Multiple Bitrate 1080p.
   
   Voor eenvoudiger beheer hebt u een optie bewerken Hallo-naam van de uitvoerasset hello en Hallo-naam van Hallo-taak.
   
   ![Assets coderen](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Kies **Maken**.

### <a name="monitor-encoding-job-progress"></a>De voortgang van het codering van de taak bewaken
toomonitor hello voortgang van Hallo codering van de taak, klikt u op **instellingen** (bovenaan Hallo Hallo pagina) en selecteer vervolgens **taken**.

![Taken](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>Inhoud publiceren
tooprovide uw gebruikers met een URL die kan worden gebruikt toostream of uw inhoud downloaden, u eerst hoeft te 'publiceren' uw asset door een locator te maken. Locators bieden toegang toofiles opgenomen in Hallo asset. Media Services ondersteunt twee typen locators: 

* Streaming-locators (OnDemandOrigin), die wordt gebruikt voor adaptief streamen (bijvoorbeeld toostream MPEG DASH, HLS of Smooth Streaming). een streaming-locator toocreate uw asset een ISM-bestand moet bevatten. 
* Progressieve locators (SAS) die worden gebruikt voor het leveren van video via progressief downloaden.

Een streaming-URL Hallo na indeling heeft en u tooplay Smooth Streaming-assets kunt gebruiken.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

toobuild een streaming-URL voor HLS toevoegen (format = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

toobuild een streaming-URL voor MPEG DASH toevoegen (format = mpd-time-csf) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Een SAS-URL heeft Hallo indeling te volgen.

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> Als u Hallo portal toocreate locators vóór maart 2015 gebruikt, zijn locators met een vervaldatum van twee jaar gemaakt.  
> 
> 

tooupdate een vervaldatum op een locator, gebruik [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) of [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API's. Wanneer u de vervaldatum Hallo van een SAS-locator bijwerkt, wordt Hallo URL gewijzigd.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello portal toopublish een asset
toouse hello portal toopublish een asset Hallo te volgen:

1. Selecteer **Instellingen** > **Assets**.
2. Selecteer Hallo asset die u toopublish wilt.
3. Klik op Hallo **publiceren** knop.
4. Selecteer Hallo locator type.
5. Klik op **Toevoegen**.
   
    ![Publiceren](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Hallo-URL toegevoegd toohello lijst met **gepubliceerde URL's**.

## <a name="play-content-from-hello-portal"></a>Inhoud afspelen vanuit Hallo-portal
Hello Azure portal biedt een speler inhoud die u tootest uw video gebruiken kunt.

Klik op Hallo gewenste video en klik vervolgens op Hallo **afspelen** knop.

![Publiceren](./media/media-services-portal-vod-get-started/media-services-play.png)

Hierbij geldt het volgende:

* toobegin streaming starten actieve Hallo **standaard** streaming-eindpunt.
* Zorg ervoor dat Hallo video is gepubliceerd.
* Dit **mediaspeler** speelt af vanaf Hallo standaard streaming-eindpunt. Als u wilt dat tooplay van een niet-standaard streaming-eindpunt, klikt u op toocopy Hallo URL en gebruikt een andere speler. Bijvoorbeeld [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

## <a name="next-steps"></a>Volgende stappen
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

