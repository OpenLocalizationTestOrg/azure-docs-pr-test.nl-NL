---
title: aaaUsing castLabs toodeliver Widevine-licenties tooAzure Media Services | Microsoft Docs
description: Dit artikel wordt beschreven hoe u Azure Media Services (AMS) toodeliver een stroom die dynamisch wordt versleuteld met AMS met PlayReady en Widevine DRM's kunt gebruiken. Hallo PlayReady-licenties afkomstig van de licentieserver Media Services PlayReady en Widevine-licentie wordt geleverd door castLabs licentieserver.
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>Met behulp van castLabs toodeliver Widevine-licenties tooAzure Media Services
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe u Azure Media Services (AMS) toodeliver een stroom die dynamisch wordt versleuteld met AMS met PlayReady en Widevine DRM's kunt gebruiken. Hallo PlayReady licentie afkomstig is van de licentieserver Media Services PlayReady en Widevine-licentie is geleverd door **castLabs** licentieserver.

tooplayback streaming van inhoud die is beveiligd door CENC (PlayReady en/of Widevine), kunt u [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Zie [AMP document](http://amp.azure.net/libs/amp/latest/docs/) voor meer informatie.

Hallo volgende diagram ziet u een architectuur op hoog niveau Azure Media Services en castLabs integratie.

![Integratie](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Typische system instellen
* Media-inhoud wordt opgeslagen in AMS.
* Sleutel-id's van inhoud sleutels worden opgeslagen in zowel castLabs als AMS.
* castLabs en AMS hebben tokenverificatie ingebouwd. verificatietokens worden besproken die Hallo uit te voeren. 
* Wanneer een client toostream Hallo video aanvraagt, Hallo inhoud dynamisch is versleuteld met **Common Encryption** (CENC) en dynamisch geleverd door AMS tooSmooth Streaming- en DASH. We bieden ook PlayReady M2TS elementaire stroom versleuteling voor streaming HLS-protocol.
* PlayReady-licentie is opgehaald uit de AMS-licentieserver en Widevine-licentie is opgehaald uit de licentieserver castLabs. 
* Mediaspeler besluit automatisch welke licentie toofetch op basis van de mogelijkheden van het platform voor Hallo-client. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Verificatie-token genereren voor het verkrijgen van een licentie
Zowel castLabs als AMS ondersteunen (JSON Web Token) JWT-token-indeling gebruikt tooauthorize een licentie. 

### <a name="jwt-token-in-ams"></a>JWT-token in AMS
Hallo volgende tabel beschrijft de JWT-token in AMS. 

| certificaatverlener | Tekenreeks van de verlener van Hallo gekozen Secure Token Service (STS) |
| --- | --- |
| Doelgroep |Tekenreeks van de doelgroep van Hallo gebruikt STS |
| Claims |Een set claims |
| NotBefore |Start de geldigheid van Hallo-token |
| Verloopt |Einde geldigheid van Hallo-token |
| SigningCredentials |Hallo-sleutel die wordt gedeeld door PlayReady-licentieserver castLabs licentieserver en STS, sleutel van zowel symmetrisch als asymmetrisch kan zijn. |

### <a name="jwt-token-in-castlabs"></a>JWT-token in castLabs
Hallo volgende tabel beschrijft de JWT-token in castLabs. 

| Naam | Beschrijving |
| --- | --- |
| optData |Een JSON-tekenreeks met informatie over u. |
| CRT |Een met JSON-tekenreeks-informatie over asset hello, de licentierechten voor gegevens en afspelen. |
| IAT |Hallo huidige datetime in epoche. |
| jti |Een unieke id over dit token (elke token kan slechts eenmaal worden gebruikt in Hallo castLabs system). |

## <a name="sample-solution-set-up"></a>Voorbeeldoplossing instellen
Hallo [oplossing steekproef](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) bestaat uit twee projecten:

* Een consoletoepassing die gebruikt tooset DRM beperkingen op een al opgenomen asset voor zowel PlayReady als Widevine worden kan.
* Een webtoepassing die handen uit beveiligingstokens die kunnen worden gezien als een zeer vereenvoudigde versie van een STS.

toouse Hallo-consoletoepassing:

1. Hallo app.config toosetup AMS referenties, castLabs referenties, STS-configuratie en gedeelde sleutel wijzigen.
2. Upload een Asset naar AMS.
3. Get Hallo UUID van Hallo Asset geüpload en 32 regel in het bestand Program.cs Hallo wijzigen:
   
      var objIAsset = _context. Assets.Where (x = > x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf '). FirstOrDefault();
4. Gebruik een item-id hebt voor de naamgeving van Hallo asset in Hallo castLabs systeem (Line 44 in het bestand Program.cs Hallo).
   
   U moet instellen item-id hebt voor **castLabs**; moet een unieke alfanumerieke tekenreeks toobe.
5. Hallo-programma uitvoeren.

toouse hello Web Application (STS):

1. Wijziging Hallo web.config toosetup castlabs verkoper-ID, Hallo STS-configuratie en Hallo gedeelde sleutel.
2. Implementeer tooAzure Websites.
3. Navigeer toohello website.

## <a name="playing-back-a-video"></a>Afspelen van video
tooplayback video versleuteld met common encryption (PlayReady en/of Widevine), kunt u Hallo [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Bij het uitvoeren van de console-app Hallo Hallo inhoud sleutel-ID en Hallo Manifest URL teruggestuurd.

1. Een nieuw tabblad openen en start de STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].
2. Ga te[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Plak in Hallo streaming-URL.
4. Klik op Hallo **geavanceerde opties** selectievakje.
5. In Hallo **beveiliging** vervolgkeuzelijst, selecteer PlayReady en/of Widevine.
6. Hallo-token die u hebt verkregen van de STS in Hallo Token tekstvak plakken. 
   
   Hallo castLab licentieserver niet hoeft Hallo ' Bearer = "voorvoegsel voor Hallo-token. Dus verwijder die vóór het verzenden van Hallo-token.
7. Hallo player bijwerken.
8. Hallo video moet worden afgespeeld.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

