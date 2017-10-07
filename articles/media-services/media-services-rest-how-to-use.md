---
title: overzicht van aaaMedia Services operations REST-API | Microsoft Docs
description: REST-API voor Media Services-overzicht
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Media Services operations REST-API-overzicht
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Hallo **Media Services Operations REST** API wordt gebruikt voor het maken van taken, assets, beleidsregels voor toegang en andere bewerkingen voor objecten in een Media Service-account. Zie voor meer informatie [naslaginformatie over REST API van Media Services Operations](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).

Microsoft Azure Media Services is een service die op basis van een OData-HTTP-aanvragen accepteert en terug in de uitgebreide JSON of atom + pub kan reageren. Omdat het Media Services voldoet tooAzure ontwerprichtlijnen, is er een reeks vereiste HTTP-headers die elke client gebruiken moet wanneer u verbinding maakt tooMedia Services, evenals een aantal optionele headers die kunnen worden gebruikt. Hallo volgende secties beschrijven Hallo headers en HTTP-termen die u kunt gebruiken bij maken van aanvragen en antwoorden ontvangen van Media Services.

In dit onderwerp een overzicht van hoe toouse REST v2 met Media Services.

## <a name="considerations"></a>Overwegingen

Hallo na overwegingen van toepassing wanneer u de REST.

* Tijdens het opvragen van entiteiten, moet u er een limiet van 1000 entiteiten in één keer wordt geretourneerd omdat openbare REST v2 queryresultaten resultaten too1000 beperkt is. U moet toouse **overslaan** en **nemen** (.NET) / **boven** (REST) zoals beschreven in [in dit voorbeeld .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) en [deze REST-API voorbeeld](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* Wanneer met behulp van JSON en geven toouse hello **__metadata** sleutelwoord in Hallo aanvraag (bijvoorbeeld tooreferences gekoppelde objecten), moet u Hallo instellen **accepteren** header te[uitgebreide JSON-indeling ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (Zie het volgende voorbeeld Hallo). OData Hallo niet begrijpt **__metadata** eigenschap in Hallo aanvraagt, tenzij u deze tooverbose instellen.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>Standaard HTTP-aanvraagheaders ondersteund door Media Services
Voor elke aanroep die u in Media Services aanbrengt wordt een reeks vereiste headers die u in uw aanvraag opnemen moet is en ook een set optionele headers kunt u tooinclude. Hallo tabel lijsten Hallo na headers vereist:

| Koptekst | Type | Waarde |
| --- | --- | --- |
| Autorisatie |Bearer |Bearer is Hallo autorisatiemechanismen alleen geaccepteerd. Hallo-waarde moet ook Hallo access token dat is opgegeven door de ACS. |
| x-ms-version |Decimale |2.11 |
| DataServiceVersion |Decimale |3.0 |
| MaxDataServiceVersion |Decimale |3.0 |

> [!NOTE]
> Omdat de onderliggende opslag van de metagegevens asset via REST API's, Hallo DataServiceVersion en MaxDataServiceVersion headers moet worden opgenomen in elk verzoek; OData-tooexpose maakt gebruik van Media Services echter als dat niet het geval is, klikt u vervolgens op dit moment Media Services wordt ervan uitgegaan dat bedrijfswaarde Hallo DataServiceVersion 3.0.
> 
> 

Hallo volgende is een set optionele headers:

| Koptekst | Type | Waarde |
| --- | --- | --- |
| Date |RFC 1123 datum |Tijdstempel van Hallo-aanvraag |
| Accepteren |Type inhoud |Hallo aangevraagd type inhoud voor antwoord Hallo zoals Hallo volgende:<p> -application/json; odata = verbose<p> -application/atom + xml<p> Antwoorden mogelijk een ander inhoudstype, zoals een blob-ophalen waarbij een geslaagde reactie Hallo blob stroom Hallo nettolading bevat. |
| Accepteer codering |Gzip, deflate |GZIP en DEFLATE codering, indien van toepassing. Opmerking: Voor grote bronnen Media Services kunnen deze header negeren en niet-gecomprimeerde gegevens retourneren. |
| Accepteer taal |'en', 'es', enzovoort. |Hiermee geeft u Hallo voorkeurs-taal voor antwoord Hallo. |
| Accepteer Charset |Type Charset zoals "UTF-8" |Standaardwaarde is UTF-8. |
| X-HTTP-methode |HTTP-methode |Kan de clients of firewalls bieden geen ondersteuning voor HTTP-methoden zoals toouse plaatsen of verwijder deze methoden, via een tunnel via een GET-aanroep. |
| Content-Type |Type inhoud |Type inhoud van de aanvraagtekst Hallo in PUT- of POST-aanvragen. |
| client-request-id |Tekenreeks |Een door de aanroeper gedefinieerde waarde die Hallo aanvraag opgegeven aangeeft. Indien opgegeven, wordt deze waarde in het antwoordbericht Hallo als een manier toomap Hallo aanvraag opgenomen. <p><p>**Belangrijk**<p>Waarden moeten worden beperkt tot 2096b (2k). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Standaard-HTTP-antwoordheaders ondersteund door Media Services
Hallo volgende is een set van headers die kunnen worden geretourneerd tooyou afhankelijk van het Hallo-resource die u zijn aangevraagd en Hallo gewenste tooperform in te grijpen.

| Koptekst | Type | Waarde |
| --- | --- | --- |
| aanvraag-id |Tekenreeks |Een unieke id voor de huidige bewerking hello, service gegenereerd. |
| client-request-id |Tekenreeks |Een id die is opgegeven door de aanroeper Hallo Hallo oorspronkelijke aanvraag, indien aanwezig. |
| Date |RFC 1123 datum |Hallo datum die Hallo-aanvraag is verwerkt. |
| Content-Type |Varieert |Hallo-inhoudstype van de tekst hello van. |
| Codering van inhoud |Varieert |Gzip of verkleinen, indien nodig. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Standaard HTTP-termen die door Media Services worden ondersteund
Hallo Hier volgt een volledige lijst met HTTP-termen die kunnen worden gebruikt bij het maken van HTTP-aanvragen:

| Term | Beschrijving |
| --- | --- |
| TOEVOEGEN |Retourneert Hallo huidige waarde van een object. |
| VERZENDEN |Hiermee maakt u een object op basis van Hallo gegevens opgegeven of een opdracht verzonden. |
| PLAATSEN |Maakt een benoemd object (indien van toepassing) of een object vervangt. |
| VERWIJDEREN |Hiermee verwijdert u een object. |
| SAMENVOEGEN |Een bestaand object met benoemde eigenschapswijzigingen bijgewerkt. |
| HEAD |Retourneert de metagegevens van een object voor een GET-antwoord. |

## <a name="discover-media-services-model"></a>Media Services-model detecteren
toomake Media Services entiteiten meer kan worden gedetecteerd, Hallo $metadata bewerking kunnen worden gebruikt. Hiermee kunt u tooretrieve alle geldige Entiteitstypen, entiteitseigenschappen, koppelingen, functies, acties, enzovoort. Hallo volgende voorbeeld laat zien hoe tooconstruct URI Hallo: https://media.windows.net/API/$ metagegevens.

U moet toevoegen '? api-version=2.x ' toohello einde van Hallo URI als u wilt dat tooview Hallo metagegevens in een browser of Hallo x-ms-version-header niet in uw aanvraag opnemen.

## <a name="connect-toomedia-services"></a>Verbinding maken met tooMedia Services

Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md). Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services. U moet de volgende aanroepen toohello ervoor nieuwe URI.

## <a name="next-steps"></a>Volgende stappen

tooaccess AMS APIs met REST, Zie [met Azure AD authentication tooaccess hello Azure Media Services-API met REST](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

