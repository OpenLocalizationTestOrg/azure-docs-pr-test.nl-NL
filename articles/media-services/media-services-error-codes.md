---
title: Media Services-foutcodes aaaAzure | Microsoft Docs
description: Hallo onderwerp overzicht een van Azure Media Services-foutcodes.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Azure Media Services-foutcodes
Wanneer u Microsoft Azure Media Services gebruikt, krijgt u HTTP-foutcodes van Hallo-service, afhankelijk van de problemen zoals verificatietokens verloopt tooactions die niet worden ondersteund in een Media Services. Hallo volgt een lijst met **HTTP-foutcodes** die door Media Services kunnen worden geretourneerd en Hallo mogelijke oorzaken voor deze.  

## <a name="400-bad-request"></a>400 onjuiste aanvraag
Hallo-aanvraag bevat ongeldige gegevens en wordt geweigerd vanwege tooone Hallo volgende redenen:

* Een niet-ondersteunde API-versie is opgegeven. Zie voor de meest recente versie Hallo [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).
* Hallo API-versie van Media Services is niet opgegeven. Zie voor informatie over hoe toospecify Hallo API-versie, [Media Services Operations REST API-verwijzing](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).
  
  > [!NOTE]
  > Als u Hallo .NET of Java SDK's tooconnect tooMedia Services, Hallo API-versie is opgegeven voor u wanneer u probeert en uitvoeren van een bepaalde actie op basis van Media Services.
  > 
  > 
* Een ongedefinieerde eigenschap er is opgegeven. Hallo-eigenschapsnaam is in Hallo-bericht. Alleen de eigenschappen die deel uitmaken van een bepaalde entiteit kunnen worden opgegeven. Zie [Azure Media Services REST API-verwijzing](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) voor een lijst met entiteiten en hun eigenschappen.
* Een ongeldige waarde er is opgegeven. Hallo-eigenschapsnaam is in Hallo-bericht. Zie de vorige koppeling voor geldige eigenschaptypen Hallo en hun waarden.
* De waarde van een eigenschap ontbreekt en is vereist.
* Onderdeel van de opgegeven Hallo-URL bevat een ongeldige waarde.
* Een poging is gedaan tooupdate een WriteOnce-eigenschap.
* Een poging is gedaan toocreate een taak met een invoer Asset met een primaire AssetFile die is niet opgegeven of kan niet worden bepaald.
* Een poging is gedaan tooupdate een SAS-Locator. SAS-locators kunnen alleen worden gemaakt of verwijderd. Streaming-locators kan worden bijgewerkt. Zie voor meer informatie [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).
* Een niet-ondersteunde bewerking of de query is ingediend.

## <a name="401-unauthorized"></a>401-niet toegestaan
Hallo-aanvraag kan niet worden geverifieerd (voordat deze kan worden geautoriseerd) vanwege tooone Hallo volgende redenen:

* Ontbrekende verificatieheader.
* Ongeldige verificatie header-waarde.
  * Hallo-token is verlopen. 
  * Hallo token bevat een ongeldige handtekening.

## <a name="403-forbidden"></a>403-verboden
Hallo-aanvraag is niet toegestaan vanwege tooone Hallo volgende redenen:

* Hallo Media Services-account kan niet worden gevonden of is verwijderd.
* Hallo Media Services-account is uitgeschakeld en Hallo van het type is geen HTTP GET. Servicebewerkingen wordt ook een 403 antwoord geretourneerd.
* Hallo-verificatietoken bevat geen referentie-informatie van de gebruiker Hallo: AccountName en/of abonnements-id. U vindt deze informatie in Hallo Media Services-UI-uitbreiding voor uw Media Services-account in hello Azure Management Portal.
* Hallo resource kan niet worden geopend.
  
  * Een poging is gedaan toouse een MediaProcessor die niet beschikbaar voor uw Media Services-account.
  * Een poging gedaan een taaksjabloon gedefinieerd tooupdate door Media Services.
  * Een poging is gedaan toooverwrite sommige andere Media Services-account van Locator.
  * Een poging is gedaan toooverwrite sommige andere Media Services-account van ContentKey.
* Hallo resource kan niet worden gemaakt vanwege tooa service quota die voor Hallo Media Services-account is bereikt. Zie voor meer informatie over Hallo servicequota [quota's en beperkingen](media-services-quotas-and-limitations.md).

## <a name="404-not-found"></a>404 – Niet gevonden
Hallo-aanvraag is niet toegestaan voor een bron vanwege tooone Hallo volgende redenen:

* Een poging is gedaan tooupdate een entiteit die niet bestaat.
* Een poging is gedaan toodelete een entiteit die niet bestaat.
* Een poging is gedaan toocreate een entiteit die is gekoppeld aan tooan entiteit die niet bestaat.
* Een poging is gedaan tooGET een entiteit die niet bestaat.
* Een poging is gedaan toospecify een opslagaccount dat is niet gekoppeld aan Hallo Media Services-account.  

## <a name="409-conflict"></a>409 conflict
Hallo-aanvraag is niet toegestaan vanwege tooone Hallo volgende redenen:

* Meer dan één AssetFile heeft de opgegeven naam Hallo binnen Hallo Asset.
* Er is geprobeerd toocreate een tweede primaire AssetFile binnen Hallo Asset.
* Er is geprobeerd een ContentKey Hello toocreate opgegeven Id is al gebruikt.
* Er is geprobeerd een Locator Hello toocreate opgegeven Id is al gebruikt.
* Meer dan één IngestManifestFile heeft de opgegeven naam Hallo binnen Hallo IngestManifest.
* Een poging is gedaan toolink een tweede opslag versleuteling ContentKey toohello Asset opslag versleuteld.
* Er is geprobeerd toolink Hallo dezelfde ContentKey toohello Asset.
* Er is een poging gedaan een locator tooan Asset waarvan storage-container ontbreekt of is niet meer gekoppeld aan Asset Hallo toocreate.
* Een poging is gedaan toocreate een locator tooan actief die al in gebruik 5 locators is. (Azure-opslag zorgt er Hallo-limiet van vijf gedeeld toegangsbeleid op één opslagcontainer.)
* Storage-account van een Asset tooan IngestManifestAsset koppelen is geen Hallo dezelfde zijn als Hallo storage-account die wordt gebruikt door Hallo bovenliggende IngestManifest.  

## <a name="500-internal-server-error"></a>Interne serverfout 500
Media Services aangetroffen tijdens de verwerking van aanvraag Hallo Hallo er is een fout waardoor het Hallo-verwerking niet door kan gaan. Dit kan worden veroorzaakt door tooone Hallo volgende redenen:

* Maken van een activum of de taak mislukt, omdat de servicegegevens quotum Hallo Media Services account tijdelijk niet beschikbaar is.
* Maken van een activum of IngestManifest blob storage-container mislukt, omdat de accountgegevens voor opslag van het Hallo-account is tijdelijk niet beschikbaar.
* Andere onverwachte fout opgetreden.

## <a name="503-service-unavailable"></a>503 Service niet beschikbaar
Hallo-server is momenteel niet mogelijk tooreceive aanvragen. Deze fout kan worden veroorzaakt door overmatige aanvragen toohello service. Media Services mechanisme beperking beperkt Hallo Resourcegebruik voor toepassingen die overmatige aanvraag toohello service maken.

> [!NOTE]
> Selectievakje Hallo fout bericht en de fout code tekenreeks tooget meer gedetailleerde informatie over de reden van Hallo die u hebt verkregen Hallo 503-fout. Deze fout betekent niet altijd beperking.
> 
> 

Beschrijvingen van de mogelijke status zijn:

* 'De server is bezet. Eerder uitgevoerde van dit soort aanvraag duurde langer dan {0} seconden."
* 'De server is bezet. Meer dan {0} aanvragen per seconde kan worden beperkt."
* 'De server is bezet. Meer dan {0} aanvragen binnen enkele seconden {1} kunnen worden beperkt."

toohandle deze fout, wordt u aangeraden Pogingslogica voor exponentiële back uitschakelen. Dit betekent dat met behulp van geleidelijk langer wacht tussen nieuwe pogingen voor opeenvolgende foutberichten.  Zie voor meer informatie [tijdelijke fout afhandeling van Application Block](https://msdn.microsoft.com/library/hh680905.aspx).

> [!NOTE]
> Als u [Azure Media Services SDK voor .net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), Hallo Pogingslogica voor Hallo 503-fout is geïmplementeerd door Hallo SDK.  
> 
> 

## <a name="see-also"></a>Zie ook
[Media Services-Management-foutcodes](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

