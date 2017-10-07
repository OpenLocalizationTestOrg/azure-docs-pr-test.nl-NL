---
title: aaa"inhoud Hello Azure-portal publiceren | Microsoft Docs'
description: Deze zelfstudie wordt u begeleid Hallo stappen voor het publiceren van uw inhoud Hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>Inhoud Hello Azure-portal publiceren
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Overzicht
> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
> 
> 

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

Zie voor meer informatie [leveren van inhoud overzicht](media-services-deliver-content-overview.md).

> [!NOTE]
> Als u Hallo portal toocreate locators vóór maart 2015 gebruikt, zijn locators met een vervaldatum van twee jaar gemaakt.  
> 
> 

tooupdate een vervaldatum op een locator, gebruik [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) of [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API's. Houd er rekening mee dat wanneer u de vervaldatum Hallo van een SAS-locator bijwerkt, Hallo URL gewijzigd.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello portal toopublish een asset
toouse hello portal toopublish een asset Hallo te volgen:

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.
2. Selecteer **Instellingen** > **Assets**.
3. Selecteer Hallo asset die u toopublish wilt.
4. Klik op Hallo **publiceren** knop.
5. Selecteer Hallo locator type.
6. Klik op **Toevoegen**.
   
    ![Publiceren](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Hallo-URL wordt toegevoegd toohello lijst met **gepubliceerde URL's**.

## <a name="play-content-from-hello-portal"></a>Inhoud afspelen vanuit Hallo-portal
Hello Azure portal biedt een speler inhoud die u tootest uw video gebruiken kunt.

Klik op Hallo gewenste video en klik vervolgens op Hallo **afspelen** knop.

![Publiceren](./media/media-services-portal-vod-get-started/media-services-play.png)

Hierbij geldt het volgende:

* Zorg ervoor dat Hallo video is gepubliceerd.
* Dit **mediaspeler** speelt af vanaf Hallo standaard streaming-eindpunt. Als u wilt dat tooplay van een niet-standaard streaming-eindpunt, klikt u op toocopy Hallo URL en gebruikt een andere speler. Bijvoorbeeld [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* Hallo streaming-eindpunt van waaruit u streaming moet worden uitgevoerd.  

## <a name="next-steps"></a>Volgende stappen
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

