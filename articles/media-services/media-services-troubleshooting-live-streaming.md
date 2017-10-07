---
title: handleiding voor live streamen aaaTroubleshooting | Microsoft Docs
description: In dit onderwerp biedt informatie over hoe tootroubleshoot live streaming problemen.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a>Handleiding voor het oplossen van problemen met live streaming
Dit onderwerp bevat suggesties voor het tootroubleshoot sommige live streaming-problemen.

## <a name="issues-related-tooon-premises-encoders"></a>Problemen tooon-premises coderingsprogramma 's
In deze sectie biedt informatie over hoe tootroubleshoot problemen gerelateerde tooon-premises coderingsprogramma's die zijn geconfigureerd voor toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.

### <a name="problem-would-like-toosee-logs"></a>Probleem: Wilt toosee Logboeken
* **Potentiële probleem**: kan niet zoeken encoder logboeken die kan helpen bij het opsporen van problemen.
  
  * **Telestream Wirecast**: meestal vindt u Logboeken onder C:\Users\{username} \AppData\Roaming\Wirecast\ 
  * **Elementaire Live**: vindt u koppelingen toologs heeft op Hallo-beheerportal. Klik op **statistieken**, klikt u vervolgens **logboeken**. Op Hallo **logboekbestanden** pagina ziet u een lijst van Logboeken voor alle items LiveEvent Hallo; Selecteer Hallo een die overeenkomt met de huidige sessie. 
  * **Flash Live Mediacoderingsprogramma**: U kunt vinden Hallo **logboekmap...**  door te navigeren toohello **codering logboek** tabblad.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Probleem: Er is geen optie voor het uitvoeren van een progressieve stream
* **Potentiële probleem**: Hallo codering wordt gebruikt niet automatisch interliniëring ongedaan maken. 
  
    **Stappen voor probleemoplossing**: zoek naar een ongedaan ineengestrengeld optie binnen Hallo encoder interface. Zodra de-interlacing is ingeschakeld, Controleer of opnieuw progressief uitvoerinstellingen. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>Probleem: Probeert verschillende instellingen voor codering uitvoer en nog steeds niet tooconnect.
* **Potentiële probleem**: Azure codering kanaal is niet juist opnieuw ingesteld. 
  
    **Stappen voor probleemoplossing**: Zorg ervoor dat Hallo encoder niet meer tooAMS pusht, stoppen en opnieuw instellen van Hallo-kanaal. Als opnieuw uit te voeren, probeert u het coderingsprogramma verbinding te maken met de nieuwe instellingen Hallo. Als dit nog niet is opgelost probleem hello, maak een nieuw kanaal volledig, soms kanalen beschadigd kunnen raken na een aantal mislukte pogingen.  
* **Potentiële probleem**: Hallo GOP grootte of Sleutelframe instellingen zijn niet optimaal. 
  
    **Stappen voor probleemoplossing**: GOP aanbevolen grootte of keyframe interval is 2 seconden. Sommige coderingsprogramma's berekenen deze instelling in het aantal frames, terwijl andere seconden. Bijvoorbeeld: bij het uitvoeren van 30fps Hallo GOP grootte is 60 frames die gelijkwaardige too2 seconden is.  
* **Potentiële probleem**: gesloten poorten blokkeren het Hallo-stroom. 
  
    **Stappen voor probleemoplossing**: Controleer bij de streaming via RTMP, firewall en/of de proxy-instellingen tooconfirm uitgaande poorten 1935 en 1936 zijn geopend. Wanneer u RTP streaming, moet u bevestigen dat de uitgaande poort 2010 open is. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>Probleem: Bij het configureren van Hallo encoder toostream Hello RTP-protocol, er is geen locatie tooenter een hostnaam.
* **Potentiële probleem**: veel RTP coderingsprogramma's niet toegestaan voor hostnamen en een IP-adres moet toobe verkregen.  
  
    **Stappen voor probleemoplossing**: toofind Hallo IP-adres, open een opdrachtprompt op elke computer. toodo open dit in Windows hello uitvoeren starten (WIN + R) en typ 'cmd' tooopen.  
  
    Zodra het Hallo-opdrachtprompt is geopend, typt u 'Ping [AMS-hostnaam]'. 
  
    Hallo-hostnaam kan worden afgeleid door Hallo poortnummer tussen hello Azure-URL voor opnemen, zoals gemarkeerd in het volgende voorbeeld Hallo weg te laten: 
  
    RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 / 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> Als na het volgen van Hallo stappen die u nog steeds niet met succes streamen indienen een ondersteuningsticket met hello Azure-portal.
> 
> 

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

