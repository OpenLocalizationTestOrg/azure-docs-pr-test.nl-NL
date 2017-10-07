---
title: Autorisatiebeleid voor Inhoudssleutels met behulp van aaaConfigure hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe tooconfigure een verificatiebeleid voor een inhoudssleutel.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>Autorisatiebeleid voor Inhoudssleutels configureren
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Overzicht
Microsoft Azure Media Services kunt u toodeliver MPEG-DASH-, Smooth Streaming- en HTTP-Live-Streaming (HLS)-streams beveiligd met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits) of [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS ook kunt u toodeliver DASH-streams versleuteld met Widevine DRM. Zowel PlayReady als Widevine zijn versleuteld volgens de specificatie Common Encryption (ISO/IEC 23001-7 CENC) Hallo.

Media Services biedt ook een **Service voor het leveren van sleutel/licentie** waarvan clients kunt AES-sleutels ophalen of PlayReady/Widevine-licenties tooplay Hallo versleutelde inhoud.

Dit onderwerp leest hoe toouse hello Azure portal tooconfigure Hallo autorisatiebeleid voor inhoudssleutels. Hallo-sleutel kan later worden gebruikt toodynamically versleutelen van uw inhoud. Opmerking dat op dit moment kunt u coderen Hallo volgende streaming-indelingen: HLS, MPEG DASH en Smooth Streaming. U kunt progressief downloaden niet coderen.

Wanneer een speler aanvraagt een stroom die is ingesteld toobe dynamisch worden versleuteld, versleutelen Media Services gebruikt Hallo geconfigureerd sleutel toodynamically uw inhoud met behulp van versleuteling AES of DRM. toodecrypt hello stream, Hallo player vraagt de Hallo sleutel van Hallo sleutellevering-service. toodecide of Hallo gebruiker is gemachtigd tooget Hallo sleutel, Hallo service beoordeelt Hallo autorisatiebeleid die u hebt opgegeven voor Hallo-sleutel.

Als u meerdere inhoudssleutels voor toohave plannen of toospecify wilt een **Service voor het leveren van sleutel/licentie** URL dan Hallo Media Services sleutellevering-service, gebruikt Media Services .NET SDK of REST-API's.

[Autorisatiebeleid voor Inhoudssleutels met Media Services .NET SDK configureren](media-services-dotnet-configure-content-key-auth-policy.md)

[Autorisatiebeleid voor Inhoudssleutels met Media Services REST-API configureren](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>Hierbij geldt het volgende:
* Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. toostart streaming van uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling, uw streaming-eindpunt heeft toobe in Hallo **met** status. 
* Uw asset moet een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden bevatten. Zie voor meer informatie [een asset coderen](media-services-encode-asset.md).
* Hallo service voor het leveren van de sleutel in de cache opgeslagen ContentKeyAuthorizationPolicy en de verwante objecten (beleidsopties en beperkingen) gedurende 15 minuten.  Als u een ContentKeyAuthorizationPolicy maakt en toouse '' tokenbeperking opgeven en vervolgens testen en werk vervolgens Hallo beleid te 'Open' beperking, duurt het ongeveer 15 minuten voordat Hallo beleid switches toohello 'Open' versie van Hallo-beleid.

## <a name="how-to-configure-hello-key-authorization-policy"></a>Hoe: Hallo autorisatiebeleid voor inhoudssleutels configureren
tooconfigure hello autorisatiebeleid voor inhoudssleutels, selecteer Hallo **INHOUDSBEVEILIGING** pagina.

Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen. Hallo autorisatiebeleid voor inhoudssleutels kan hebben **openen**, **token**, of **IP** autorisatiebeperkingen (**IP** kan worden geconfigureerd met SDK voor .NET of REST).

### <a name="open-restriction"></a>Open beperking
Hallo **openen** beperking betekent Hallo system levert sleutel tooanyone Hallo die sleutels aanvragen. Deze beperking kan handig zijn voor testdoeleinden.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>Tokenbeperking
toochoose hello token beperkt beleid, drukt u op Hallo **TOKEN** knop.

Hallo **token** beleid voor de beperkte vergezeld van een token dat is uitgegeven door een **Secure Token Service** (STS). Media Services ondersteunt tokens in Hallo **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) indeling en **JSON Web Token** (JWT)-indeling. Zie voor informatie [JWT tokenverificatie](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Media Services biedt geen **Secure Token Services**. U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS tooissue tokens. Hallo STS moet geconfigureerde toocreate token van een ondertekend met Hallo opgegeven sleutel- en claims die u hebt opgegeven in de configuratie van Hallo tokenbeperking. Hallo retourneert Media Services sleutellevering-service Hallo encryption key toohello client als Hallo token geldig is en hello claims in Hallo token overeenkomen met die zijn geconfigureerd voor de inhoudssleutel Hallo. Zie voor meer informatie [gebruik Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).

Bij het configureren van Hallo **TOKEN** beperkte beleid, moet u waarden voor instellen **verificatie sleutel**, **verlener** en **doelgroep**. Hallo verificatie van de primaire sleutel bevat Hallo key of Hallo-token is ondertekend met, de uitgever Hallo secure token-service die het Hallo-token uitgeeft. Hallo doelgroep (ook wel bereik genoemd) wordt beschreven Hallo bedoeling van Hallo token of Hallo resource Hallo token gemachtigd voor toegang tot. Hallo Media Services-service voor sleutellevering valideert dat deze waarden in Hallo token Hallo-waarden in de sjabloon Hallo overeenkomen.

### <a name="playready"></a>PlayReady
Bij het beveiligen van uw inhoud met **PlayReady**, wordt er één toospecify in uw autorisatiebeleid is Hallo dingen die u moet een XML-tekenreeks die Hallo PlayReady-licentiesjabloon definieert. Standaard is Hallo na beleid ingesteld:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"><LicenseTemplates> <PlayReadyLicenseTemplate> <AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>Nonpersistent</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>toegestane</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates></PlayReadyLicenseResponseTemplate>

U kunt klikken op Hallo **beleid-xml importeren** knop en geef een andere XML, die conform toohello XML-Schema gedefinieerd [hier](media-services-playready-license-template-overview.md).

## <a name="next-step"></a>Volgende stap
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

