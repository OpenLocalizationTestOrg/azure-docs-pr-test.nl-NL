---
title: aaaProtect uw inhoud met Azure Media Services | Microsoft Docs
description: In dit artikel biedt een overzicht van de beveiliging van inhoud met Media Services.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>Overzicht van de inhoud beveiligen
Microsoft Azure Media Services kunt u toosecure uw media Hallo tijd vanaf uw computer via de opslag, verwerking en levering. Media Services kunt u toodeliver uw inhoud live en on-demand dynamisch versleuteld met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits) of een van de belangrijkste DRM's Hallo: Microsoft PlayReady en Google Widevine FairPlay van Apple. Media Services biedt ook een service voor het leveren van AES-sleutels en DRM (PlayReady, Widevine en FairPlay) licenties tooauthorized clients. 

Hallo volgende afbeelding ziet u Hallo inhoudsbeveiliging werkstromen die ondersteuning biedt voor AMS. 

![Beveiligen met PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 

Dit onderwerp wordt uitgelegd [concepten en terminologie](media-services-content-protection-overview.md) relevante toounderstanding inhoudsbeveiliging met AMS. Hallo onderwerp bevat ook [koppelingen](media-services-content-protection-overview.md#common-scenarios) tootopics die laten zien hoe tooachieve beveiligingstaken inhoud. 

## <a name="dynamic-encryption"></a>Dynamische versleuteling
Microsoft Azure Media Services kunt u uw inhoud dynamisch versleuteld met AES wissen key of DRM codering toodeliver: Microsoft PlayReady en Google Widevine FairPlay van Apple.

Op dit moment kunt u Hallo volgende streaming-indelingen kunt versleutelen: HLS, MPEG DASH en Smooth Streaming. U kunt progressief downloaden niet coderen.

Als u voor Media Services tooencrypt een asset wilt, kunt u tooassociate een versleutelingssleutel (CommonEncryption of EnvelopeEncryption) moet aan uw asset en autorisatiebeleid voor Hallo sleutel ook configureren.

U moet ook leveringsbeleid tooconfigure Hallo asset. Als u toostream een gecodeerde asset opslag wilt, moet u ervoor dat toospecify hoe u wilt toodeliver door het leveringsbeleid voor Assets configureren.

Wanneer een stream is aangevraagd door een speler, Media Services gebruikt Hallo opgegeven sleutel toodynamically versleutelen van uw inhoud met behulp van AES wissen key of DRM-versleuteling. toodecrypt hello stream, Hallo player vraagt de Hallo sleutel van Hallo sleutellevering-service. toodecide of Hallo gebruiker is gemachtigd tooget Hallo sleutel, Hallo service beoordeelt Hallo autorisatiebeleid die u hebt opgegeven voor Hallo-sleutel.


## <a name="storage-encryption"></a>Versleuteling van opslag
Gebruik storage encryption tooencrypt uw versleutelde inhoud lokaal met AES 256-bitsversleuteling en upload het tooAzure opslag wordt bewaard in rust versleuteld. Automatisch worden beveiligd met storage encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset. Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is dat u wilt toosecure uw invoer mediabestanden van hoge kwaliteit met sterke versleuteling-op schijf rest.

In de volgorde toodeliver een gecodeerde asset opslag, moet u beleid voor de levering van Hallo actief configureren zodat Media Services weet hoe u toodeliver uw inhoud wilt. Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid (bijvoorbeeld, AES, common encryption of er wordt geen versleuteling).

## <a name="common-encryption-cenc"></a>Common encryption (CENC)
Algemene versleuteling wordt gebruikt bij het versleutelen van uw inhoud met PlayReady of / en Widewine.

## <a name="using-cbcs-aapl-encryption"></a>Met behulp van versleuteling cbcs-aapl
Cbcs-aapl wordt gebruikt bij het versleutelen van uw inhoud met FairPlay.

## <a name="envelope-encryption"></a>Versleuteling van de enveloppe
Gebruik deze optie als u wilt dat tooprotect uw inhoud met de lege sleutel AES-128. Als u een veiligere optie wilt, kunt u een van de Hallo DRM's die worden vermeld in dit onderwerp. 

## <a name="licenses-and-keys-delivery-service"></a>Licenties en sleutels service voor het leveren
Media Services biedt een service voor het leveren van licenties DRM (PlayReady, Widevine, FairPlay) en AES wissen sleutels tooauthorized clients. U kunt [hello Azure-portal](media-services-portal-protect-content.md), REST-API of Media Services SDK voor .NET tooconfigure autorisatie en verificatie-beleid voor uw licenties en sleutels.

## <a name="token-restriction"></a>Tokenbeperking
Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: openen of tokenbeperking beperking. Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS). Media Services ondersteunt tokens in Hallo Simple Web Tokens (SWT) en JSON Web Token (JWT)-indeling. Media Services biedt geen Token Services beveiligen. U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS tooissue tokens. Hallo STS moet geconfigureerde toocreate token van een ondertekend met Hallo opgegeven sleutel- en claims die u hebt opgegeven in de configuratie van Hallo tokenbeperking. Hallo Media Services sleutellevering service Hallo aangevraagd toohello (of licentiegegevens)-client retourneert als Hallo token geldig is en Hallo claims in Hallo token overeenkomen met die zijn geconfigureerd voor hello (of licentiegegevens).

Wanneer u Hallo token beperkte beleid configureert, kunt u Hallo verificatie van de primaire sleutel, uitgever en doelgroep parameters moet opgeven. Hallo verificatie van de primaire sleutel bevat Hallo key of Hallo-token is ondertekend met, de uitgever Hallo secure token-service die het Hallo-token uitgeeft. Hallo doelgroep (ook wel bereik genoemd) wordt beschreven Hallo bedoeling van Hallo token of Hallo resource Hallo token gemachtigd voor toegang tot. Hallo Media Services-service voor sleutellevering valideert dat deze waarden in Hallo token Hallo-waarden in de sjabloon Hallo overeenkomen.

## <a name="streaming-urls"></a>Streaming-URL 's
Als uw asset is versleuteld met meer dan één DRM, moet u een tag versleuteling in Hallo streaming-URL: (format = 'm3u8-aapl', versleuteling = 'xxx').

Hallo overwegingen volgende van toepassing:

* Alleen nul of één versleutelingstype kan worden opgegeven.
* Coderingstype biedt geen toobe opgegeven in Hallo url als er slechts één versleuteling toegepaste toohello actief is.
* Coderingstype is niet hoofdlettergevoelig.
* Hallo na versleutelingstypen kan worden opgegeven:  
  * **cenc**: Common encryption (Playready of Widevine)
  * **cbcs-aapl**: Fairplay
  * **CBC**: AES envelope-codering.

## <a name="common-scenarios"></a>Algemene scenario's
Hallo volgende onderwerpen wordt uitgelegd hoe tooprotect inhoud in de opslag, heeft een dynamisch versleutelde streamingmedia, gebruik AMS-service voor het leveren van sleutel/licentie

* [Beveiligen met AES](media-services-protect-with-aes128.md) 
* [Beveiligen met PlayReady en/of Widevine](media-services-protect-with-drm.md)
* [Uw HLS inhoud beveiligd met Apple FairPlay en/of PlayReady Stream](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>Overige scenario's
* [Hoe toointegrate Azure PlayReady licentie service met een eigen server encryptor/streaming](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).
* [Met behulp van castLabs toodeliver DRM-licenties tooAzure Media Services](media-services-castlabs-integration.md)

>[!NOTE]
>Een scenario waarin u een externe DRM server(technology) en stroom van AMS gebruiken is momenteel niet ondersteund.


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Verwante koppelingen
[PlayReady als een service en AES dynamische versleuteling met Azure Media Services aankondigen](http://mingfeiy.com/playready)

[Azure Media Services PlayReady licentie levering prijzen uitgelegd](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Hoe toodebug voor AES versleuteld stream in Azure Media Services](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[JWT-token authenitcation](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Azure Media Services OWIN MVC op basis van app integreren met Azure Active Directory en beperken van de belangrijkste inhouddistributie op basis van claims JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Gebruik Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
