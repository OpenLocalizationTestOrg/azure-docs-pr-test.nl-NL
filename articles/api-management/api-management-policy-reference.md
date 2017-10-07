---
title: aaaAzure documentatie voor API Management-beleid
description: Meer informatie over Hallo beleidsregels beschikbaar tooconfigure API Management.
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a>Documentatie voor Azure API Management-beleid
Deze sectie bevat een index voor Hallo-beleid in Hallo [documentatie voor API Management-beleid][API Management policy reference]. Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management][Policies in API Management].

Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels hello, tenzij Hallo beleid iets anders aangeeft. Sommige beleidsregels zoals Hallo [transportbesturing] [ Control flow] en [variabele instellen] [ Set variable] beleid is gebaseerd op beleidsexpressies. Zie voor meer informatie [Geavanceerde beleidsregels] [ Advanced policies] en [beleidsexpressies][Policy expressions]

## <a name="policy-reference-index"></a>Index referentie naar beleid
* [Softwarerestrictiebeleid toegang][Access restriction policies]
  * [Controle van HTTP-header] [ Check HTTP header] -afdwingt bestaan en/of de waarde van een HTTP-Header.
  * [Aanroepfrequentie per abonnement] [ Limit call rate by subscription] -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per abonnement op basis van een.
  * [Aanroepfrequentie per sleutel](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per sleutel op basis van een.
  * [Aanroeper IP-adressen beperken] [ Restrict caller IPs] -Filters (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.
  * [Gebruiksquotum per abonnement instellen] [ Set usage quota by subscription] -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van per abonnement.
  * [Gebruiksquotum instellen door sleutel](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van de per-sleutel.
  * [Valideren van JWT] [ Validate JWT] -afdwingt bestaan en de geldigheid van een JWT opgehaald uit een opgegeven HTTP-koptekst of een opgegeven queryparameter.
* [Geavanceerde beleidsregels][Advanced policies]
  * [Transportbesturing] [ Control flow] - voorwaardelijk is van toepassing op basis van resultaten van de evaluatie van Booleaanse waarde Hallo Hallo beleidsverklaringen [expressies][expressions].
  * [Doorsturen van aanvraag] [ Forward request] -stuurt Hallo aanvraag toohello back-endservice.
  * [Meld u tooEvent Hub] [ Log tooEvent Hub] -berichten verzendt in Hallo opgegeven indeling tooa berichtdoel gedefinieerd door een [berichtenlogboek](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entiteit.
  * [Probeer](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -uitvoering van de nieuwe pogingen van Hallo ingesloten beleidsverklaringen, als en totdat Hallo-voorwaarde is voldaan. Uitvoering wordt herhaald op Hallo opgegeven tijdsintervallen en up toohello opgegeven aantal nieuwe pogingen.
  * [Antwoord retourneren](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -wordt afgebroken pijplijn uitvoering en retourneert Hallo opgegeven antwoord rechtstreeks toohello aanroeper.
  * [Eenzijdige aanvraag verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -verzendt een aanvraag toohello URL opgegeven zonder te wachten op reactie.
  * [Aanvraag verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -verzendt een aanvraag toohello URL opgegeven.
  * [Stel aanvraagmethode](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -kunt u toochange Hallo HTTP-methode voor een aanvraag.
  * [Status instellen](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -wijzigingen Hallo HTTP status code toohello opgegeven waarde.
  * [Variabele instellen] [ Set variable] -persistent maken van een waarde in een benoemde [context] [ context] variabele voor latere toegang.
  * [Tracering](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -wordt een tekenreeks toegevoegd in Hallo [API Inspector](api-management-howto-api-inspector.md) uitvoer.
  * [Wacht](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - wacht ingesloten verzenden aanvragen, waarde niet ophalen uit de cache of beheren van stroom beleid toocomplete voordat u doorgaat.
* [Verificatiebeleid][Authentication policies]
  * [Verificatie met Basic] [ Authenticate with Basic] -verificatie met een back-endservice basisverificatie wordt gebruikt.
  * [Verificatie met een clientcertificaat] [ Authenticate with client certificate] -verificatie met een back-endservice met behulp van clientcertificaten.
* [Cachebeleidsregels][Caching policies] 
  * [Ophalen uit de cache] [ Get from cache] -cache uitvoeren opzoeken en retourneren een geldige cacheantwoord indien beschikbaar.
  * [Opslaan van toocache] [ Store toocache] -Caches antwoord toohello op basis van opgegeven configuratie van de cache-besturingselement.
  * [Waarde niet ophalen uit de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) -ophalen van een item in de cache per sleutel.
  * [Waarde opslaan in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -opslaan van een item in Hallo cache per sleutel.
  * [Waarde verwijderen uit de cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -verwijderen van een item in Hallo cache per sleutel.
* [Cross-domeinbeleid][Cross domain policies] 
  * [Aanroepen tussen domeinen toestaan] [ Allow cross-domain calls] -Hallo API toegankelijk van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.
  * [CORS] [ CORS] -voegt tooan cross-origin-resource delen (CORS) ondersteunen of een API tooallow tussen domeinen aanroepen van clients op basis van een browser.
  * [JSONP] [ JSONP] - JSON toegevoegd met de ondersteuning tooan bewerking opvulling (JSONP) of een API tooallow tussen domeinen aanroepen vanuit JavaScript-clients op basis van een browser.
* [Claimtransformatiebeleidsinstellingen][Transformation policies] 
  * [Converteren van JSON tooXML] [ Convert JSON tooXML] : zet aanvraag of antwoord body van JSON tooXML.
  * [Converteren van XML-tooJSON] [ Convert XML tooJSON] : zet aanvraag of antwoord body van XML-tooJSON.
  * [Zoeken en vervangen tekenreeks in de hoofdtekst] [ Find and replace string in body] - zoeken naar een subtekenreeks aanvraag of antwoord en wordt vervangen door een andere subtekenreeks.
  * [URL's in de inhoud te maskeren] [ Mask URLs in content] -koppelingen herschrijft (maskers) antwoord Hallo body zodat ze equivalente koppeling toohello via Hallo gateway wijst.
  * [Instellen van de back-endservice] [ Set backend service] -back-endservice Hallo voor de binnenkomende aanvraag wordt gewijzigd.
  * [Instantie ingesteld] [ Set body] -hoofdtekst van het Hallo-bericht voor binnenkomende en uitgaande aanvragen ingesteld.
  * [Set HTTP-header] [ Set HTTP header] : een waarde tooan bestaande antwoord en/of de aanvraagheader wijst of voegt een nieuwe antwoord en/of de aanvraag-header.
  * [Querytekenreeksparameter ingesteld] [ Set query string parameter] - wordt toegevoegd, vervangt de waarde van of verwijderd van de aanvraag queryreeksparameter opgeven.
  * [Herschrijven van URL's] [ Rewrite URL] -zet u een aanvraag-URL van de openbare formulier toohello vorm werd verwacht door Hallo-webservice.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over beleidsexpressies Hallo video te volgen.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


