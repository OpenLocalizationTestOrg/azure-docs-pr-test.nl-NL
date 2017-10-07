---
title: API Management-beleidsregels aaaAzure | Microsoft Docs
description: Meer informatie over Hallo beleidsregels beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a>API Management-beleidsregels
Deze sectie bevat een verwijzing voor Hallo API Management-beleidsregels te volgen. Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](api-management-howto-policies.md).  
  
 Beleidsregels zijn een krachtige functie Hallo-systeem dat Hallo publisher toochange Hallo gedrag Hallo API via configuratie toestaan. Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op Hallo aanvraag of antwoord van een API. Populaire instructies omvatten Indelingsconversie van XML-tooJSON en snelheidsbeperking toorestrict Hallo hoeveelheid inkomende aanroepen van een ontwikkelaar aanroepen. Veel meer beleidsregels zijn out of box Hallo beschikbaar.  
  
 Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels hello, tenzij Hallo beleid iets anders aangeeft. Sommige beleidsregels zoals Hallo [transportbesturing](api-management-advanced-policies.md#choose) en [variabele instellen](api-management-advanced-policies.md#set-variable) beleid is gebaseerd op beleidsexpressies. Zie voor meer informatie [Geavanceerde beleidsregels](api-management-advanced-policies.md#AdvancedPolicies) en [beleidsexpressies](api-management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a>Beleid  
  
-   [Beleid voor toegangsbeperking](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [Controle van HTTP-header](api-management-access-restriction-policies.md#CheckHTTPHeader) -afdwingt bestaan en/of de waarde van een HTTP-Header.  
  
    -   [Aanroepfrequentie per abonnement](api-management-access-restriction-policies.md#LimitCallRate) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per abonnement op basis van een.  
  
    -   [Aanroepfrequentie per sleutel](api-management-access-restriction-policies.md#LimitCallRateByKey) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per sleutel op basis van een.  
  
    -   [Aanroeper IP-adressen beperken](api-management-access-restriction-policies.md#RestrictCallerIPs) -Filters (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.  
  
    -   [Gebruiksquotum per abonnement instellen](api-management-access-restriction-policies.md#SetUsageQuota) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van per abonnement.  
  
    -   [Gebruiksquotum instellen door sleutel](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van de per-sleutel.  
  
    -   [Valideren van JWT](api-management-access-restriction-policies.md#ValidateJWT) -afdwingt bestaan en de geldigheid van een JWT opgehaald uit een opgegeven HTTP-koptekst of een opgegeven queryparameter.  
  
-   [Geavanceerde beleidsregels](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Transportbesturing](api-management-advanced-policies.md#choose) - voorwaardelijk is van toepassing op basis van evaluatie van Booleaanse expressies Hallo beleidsverklaringen.  
  
    -   [Doorsturen van aanvraag](api-management-advanced-policies.md#ForwardRequest) -stuurt Hallo aanvraag toohello back-endservice.  
  
    -   [Meld u tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) -berichten verzendt in Hallo opgegeven indeling tooa berichtdoel gedefinieerd door een entiteit berichtenlogboek.  
  
    -   [Probeer](api-management-advanced-policies.md#Retry) -uitvoering van de nieuwe pogingen van Hallo ingesloten beleidsverklaringen, als en totdat Hallo-voorwaarde is voldaan. Uitvoering wordt herhaald op Hallo opgegeven tijdsintervallen en up toohello opgegeven aantal nieuwe pogingen.  
  
    -   [Antwoord retourneren](api-management-advanced-policies.md#ReturnResponse) -wordt afgebroken pijplijn uitvoering en retourneert Hallo opgegeven antwoord rechtstreeks toohello aanroeper.  
  
    -   [Eenzijdige aanvraag verzenden](api-management-advanced-policies.md#SendOneWayRequest) -verzendt een aanvraag toohello URL opgegeven zonder te wachten op reactie.  
  
    -   [Aanvraag verzenden](api-management-advanced-policies.md#SendRequest) -verzendt een aanvraag toohello URL opgegeven.  
  
    -   [Variabele instellen](api-management-advanced-policies.md#set-variable) -persistent maken van een waarde in een variabele met de naam context voor later toegang.  
  
    -   [Stel aanvraagmethode](api-management-advanced-policies.md#SetRequestMethod) -kunt u toochange Hallo HTTP-methode voor een aanvraag.  
  
    -   [Statuscode ingesteld](api-management-advanced-policies.md#SetStatus) -wijzigingen Hallo HTTP status code toohello opgegeven waarde.  
  
    -   [Tracering](api-management-advanced-policies.md#Trace) -wordt een tekenreeks toegevoegd in Hallo [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer.  
  
    -   [Wacht](api-management-advanced-policies.md#Wait) -wacht voor ingesloten [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), of [transportbesturing](api-management-advanced-policies.md#choose) beleid toocomplete voordat u doorgaat.  
  
-   [Verificatiebeleid](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [Verificatie met Basic](api-management-authentication-policies.md#Basic) -verificatie met een back-endservice basisverificatie wordt gebruikt.  
  
    -   [Verificatie met een clientcertificaat](api-management-authentication-policies.md#ClientCertificate) -verificatie met een back-endservice met behulp van clientcertificaten.  
  
-   [Cachebeleidsregels](api-management-caching-policies.md#CachingPolicies)  
  
    -   [Ophalen uit de cache](api-management-caching-policies.md#GetFromCache) -cache uitvoeren opzoeken en retourneren een geldige cacheantwoord indien beschikbaar.  
  
    -   [Opslaan van toocache](api-management-caching-policies.md#StoreToCache) -Caches antwoord toohello op basis van opgegeven configuratie van de cache-besturingselement.  
  
    -   [Waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey) -ophalen van een item in de cache per sleutel.  
  
    -   [Waarde opslaan in cache](api-management-caching-policies.md#StoreToCacheByKey) -opslaan van een item in Hallo cache per sleutel.  
  
    -   [Waarde verwijderen uit de cache](api-management-caching-policies.md#RemoveCacheByKey) -verwijderen van een item in Hallo cache per sleutel.  
  
-   [Beleid voor meerdere domeinen](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Aanroepen tussen domeinen toestaan](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -Hallo API toegankelijk van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -voegt tooan cross-origin-resource delen (CORS) ondersteunen of een API tooallow tussen domeinen aanroepen van clients op basis van een browser.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) - JSON toegevoegd met de ondersteuning tooan bewerking opvulling (JSONP) of een API tooallow tussen domeinen aanroepen vanuit JavaScript-clients op basis van een browser.  
  
-   [Transformatiebeleid](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [Converteren van JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) : zet aanvraag of antwoord body van JSON tooXML.  
  
    -   [Converteren van XML-tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : zet aanvraag of antwoord body van XML-tooJSON.  
  
    -   [Zoeken en vervangen tekenreeks in de hoofdtekst](api-management-transformation-policies.md#Findandreplacestringinbody) - zoeken naar een subtekenreeks aanvraag of antwoord en wordt vervangen door een andere subtekenreeks.  
  
    -   [URL's in de inhoud te maskeren](api-management-transformation-policies.md#MaskURLSContent) -koppelingen herschrijft (maskers) antwoord Hallo body zodat ze equivalente koppeling toohello via Hallo gateway wijst.  
  
    -   [Instellen van de back-endservice](api-management-transformation-policies.md#SetBackendService) -back-endservice Hallo voor de binnenkomende aanvraag wordt gewijzigd.  
  
    -   [Instantie ingesteld](api-management-transformation-policies.md#SetBody) -hoofdtekst van het Hallo-bericht voor binnenkomende en uitgaande aanvragen ingesteld.  
  
    -   [Set HTTP-header](api-management-transformation-policies.md#SetHTTPheader) : een waarde tooan bestaande antwoord en/of de aanvraagheader wijst of voegt een nieuwe antwoord en/of de aanvraag-header.  
  
    -   [Querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) - wordt toegevoegd, vervangt de waarde van of verwijderd van de aanvraag queryreeksparameter opgeven.  
  
    -   [Herschrijven van URL](api-management-transformation-policies.md#RewriteURL) -zet u een aanvraag-URL van de openbare formulier toohello vorm werd verwacht door Hallo-webservice.  
  
    -   [XML met behulp van een XSLT transformeren](api-management-transformation-policies.md#XSLTransform) -een XSL-transformatie tooXML in de hoofdtekst van de aanvraag of antwoord van de Hallo van toepassing is.  
  
## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).  
