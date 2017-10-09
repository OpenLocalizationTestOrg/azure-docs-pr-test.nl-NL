---
title: aaaDevelop-speler toepassingen
description: Hallo-onderwerp vindt u koppelingen tooPlayer Frameworks en -invoegtoepassingen die u kunt gebruiken toodevelop uw eigen clienttoepassingen die streamingmedia van Media Services kunnen gebruiken.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>Videospelertoepassingen ontwikkelen
## <a name="overview"></a>Overzicht
Azure Media Services biedt u hulpprogramma's voor Hallo moet toocreate rijke, dynamische clientspelertoepassingen voor de meeste platforms, waaronder: iOS-apparaten, Android-apparaten, Windows, Windows Phone, Xbox en Set-top vakken. Dit onderwerp bevat ook koppelingen tooSDKs en Frameworks voor spelers die u kunt gebruiken toodevelop uw eigen clienttoepassingen die streamingmedia van Azure Media Services kunnen gebruiken.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 
 
## <a name="azure-media-player"></a>Azure Media Player
[Azure Media Player](http://aka.ms/ampinfo) is een web-speler gebouwd tooplay back media-inhoud van Microsoft Azure Media Services op een groot aantal verschillende browsers en apparaten. Azure Media Player maakt gebruik van industrienormen zoals HTML5 Media bron-extensies (muis) en versleuteld Media-extensies (EME) tooprovide een verrijkt ervaring voor adaptief streamen. Wanneer deze normen wordt voldaan, niet beschikbaar op een apparaat of in een browser zijn, gebruikt Azure Media Player Flash en Silverlight als terugval technologie. Ongeacht Hallo afspelen technologie gebruikt, moeten ontwikkelaars een uniforme interface JavaScript-tooaccess API's. Dit zorgt ervoor dat inhoud door Azure Media Services toobe gespeeld over een wide-bereik van apparaten en browsers zonder eventuele extra inspanning behandeld.

Microsoft Azure Media Services kunt u inhoud toobe aangeboden met DASH, Smooth Streaming en streaming-indelingen tooplay HLS back-inhoud. Azure Media Player rekening wordt gehouden deze verschillende indelingen en automatisch wordt afgespeeld best koppeling op basis van het platform/browsermogelijkheden Hallo Hallo. Microsoft Azure Media Services biedt tevens mogelijkheden voor dynamische versleuteling van activa met PlayReady-versleuteling of AES-128-bits envelop codering. Azure Media Player kunnen voor het ontsleutelen van PlayReady en AES-128-bits gecodeerde inhoud wanneer er op de juiste wijze geconfigureerd. 

Voor meer informatie:

* [Azure Media Player](http://aka.ms/ampinfo)
* [Azure Media Player-documentatie](http://aka.ms/ampdocs) 
* [Azure MediaPlayer ophalen Blog gestart](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [Aanmelden toostay up toodate Hello nieuwste van Azure Media Player](http://aka.ms/ampsignup)
* [Toevoegen van nieuwe functieaanvragen, ideeën, feedback](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>Andere hulpprogramma's voor het maken van Player-toepassingen
U kunt ook alle volgende SDK's Hallo gebruiken:

* [Vloeiende Streaming Client SDK](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [Smooth Streaming Windows Store-App](media-services-build-smooth-streaming-apps.md)
* [Microsoft Media-Platform: Player Framework](http://playerframework.codeplex.com/) 
* [HTML5 Documentatie Player-Framework](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [Microsoft Smooth Streaming-invoegtoepassing voor OSMF](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Licentieverlening Microsoft® Smooth Streaming Client Kit overdragen](http://aka.ms/sspk) 
* [XBOX Video toepassingsontwikkeling](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>Adverteren
Azure Media Services biedt ondersteuning voor het invoegen van ad via Hallo Windows Media-Platform: Frameworks voor spelers. Er zijn frameworks voor spelers met ad-ondersteuning beschikbaar voor Windows 8, Silverlight, Windows Phone 8 en iOS-apparaten. Elke player-framework bevat voorbeeldcode die laat u hoe zien een toepassing player tooimplement. Er zijn drie soorten advertenties die u in uw media invoegen kunt:

Lineaire – volledige frame advertenties die Hallo belangrijkste video onderbreken

Niet-lineaire – overlay advertenties die worden weergegeven als de belangrijkste video hello wordt afgespeeld, meestal een logo of andere statische afbeelding geplaatst in Hallo player

Aanvullende – advertenties die buiten Hallo player worden weergegeven

Advertenties kunnen op elk punt in de tijdlijn Hallo belangrijkste video worden geplaatst. U moet de hoogte Hallo player wanneer tooplay Hallo ad en welke tooplay advertenties. Dit wordt gedaan met behulp van een reeks standaard XML-bestanden: Video Ad-Service-sjabloon (VAST), digitale Video meerdere Ad afspeellijst (VMAP), Media abstracte sequentiëren sjabloon (b) en digitale Video Player Ad Interface Definition (VPAID). GROTE bestanden opgeven welke toodisplay advertenties. VMAP bestanden opgeven wanneer tooplay verschillende advertenties en ENORME XML bevatten. B-bestanden zijn een andere manier toosequence advertenties die tevens VAST XML kunnen bevatten. VPAID bestanden definiëren een interface tussen Hallo-speler en Hallo ad of ad-server. Zie voor meer informatie [invoegen advertenties](https://msdn.microsoft.com/library/dn387398.aspx).

Zie voor meer informatie over de ondertiteling en ads-ondersteuning in Live streaming video's [ondersteund gesloten ondertiteling en Ad invoegen standaarden](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[Een adaptieve MPEG-DASH-videostream insluiten in een HTML5-toepassing met DASH.js](media-services-embed-mpeg-dash-in-html5.md)

[GitHub-opslagplaats voor dash.js](https://github.com/Dash-Industry-Forum/dash.js)

