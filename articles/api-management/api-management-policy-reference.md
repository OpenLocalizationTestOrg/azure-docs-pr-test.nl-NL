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
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="ece8c-103">Documentatie voor Azure API Management-beleid</span><span class="sxs-lookup"><span data-stu-id="ece8c-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="ece8c-104">Deze sectie bevat een index voor Hallo-beleid in Hallo [documentatie voor API Management-beleid][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="ece8c-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="ece8c-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="ece8c-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="ece8c-106">Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels hello, tenzij Hallo beleid iets anders aangeeft.</span><span class="sxs-lookup"><span data-stu-id="ece8c-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="ece8c-107">Sommige beleidsregels zoals Hallo [transportbesturing] [ Control flow] en [variabele instellen] [ Set variable] beleid is gebaseerd op beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="ece8c-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="ece8c-108">Zie voor meer informatie [Geavanceerde beleidsregels] [ Advanced policies] en [beleidsexpressies][Policy expressions]</span><span class="sxs-lookup"><span data-stu-id="ece8c-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="ece8c-109">Index referentie naar beleid</span><span class="sxs-lookup"><span data-stu-id="ece8c-109">Policy reference index</span></span>
* <span data-ttu-id="ece8c-110">[Softwarerestrictiebeleid toegang][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="ece8c-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="ece8c-111">[Controle van HTTP-header] [ Check HTTP header] -afdwingt bestaan en/of de waarde van een HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="ece8c-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="ece8c-112">[Aanroepfrequentie per abonnement] [ Limit call rate by subscription] -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per abonnement op basis van een.</span><span class="sxs-lookup"><span data-stu-id="ece8c-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="ece8c-113">[Aanroepfrequentie per sleutel](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per sleutel op basis van een.</span><span class="sxs-lookup"><span data-stu-id="ece8c-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="ece8c-114">[Aanroeper IP-adressen beperken] [ Restrict caller IPs] -Filters (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="ece8c-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="ece8c-115">[Gebruiksquotum per abonnement instellen] [ Set usage quota by subscription] -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van per abonnement.</span><span class="sxs-lookup"><span data-stu-id="ece8c-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="ece8c-116">[Gebruiksquotum instellen door sleutel](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van de per-sleutel.</span><span class="sxs-lookup"><span data-stu-id="ece8c-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="ece8c-117">[Valideren van JWT] [ Validate JWT] -afdwingt bestaan en de geldigheid van een JWT opgehaald uit een opgegeven HTTP-koptekst of een opgegeven queryparameter.</span><span class="sxs-lookup"><span data-stu-id="ece8c-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="ece8c-118">[Geavanceerde beleidsregels][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="ece8c-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="ece8c-119">[Transportbesturing] [ Control flow] - voorwaardelijk is van toepassing op basis van resultaten van de evaluatie van Booleaanse waarde Hallo Hallo beleidsverklaringen [expressies][expressions].</span><span class="sxs-lookup"><span data-stu-id="ece8c-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="ece8c-120">[Doorsturen van aanvraag] [ Forward request] -stuurt Hallo aanvraag toohello back-endservice.</span><span class="sxs-lookup"><span data-stu-id="ece8c-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="ece8c-121">[Meld u tooEvent Hub] [ Log tooEvent Hub] -berichten verzendt in Hallo opgegeven indeling tooa berichtdoel gedefinieerd door een [berichtenlogboek](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entiteit.</span><span class="sxs-lookup"><span data-stu-id="ece8c-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="ece8c-122">[Probeer](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -uitvoering van de nieuwe pogingen van Hallo ingesloten beleidsverklaringen, als en totdat Hallo-voorwaarde is voldaan.</span><span class="sxs-lookup"><span data-stu-id="ece8c-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="ece8c-123">Uitvoering wordt herhaald op Hallo opgegeven tijdsintervallen en up toohello opgegeven aantal nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="ece8c-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="ece8c-124">[Antwoord retourneren](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -wordt afgebroken pijplijn uitvoering en retourneert Hallo opgegeven antwoord rechtstreeks toohello aanroeper.</span><span class="sxs-lookup"><span data-stu-id="ece8c-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="ece8c-125">[Eenzijdige aanvraag verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -verzendt een aanvraag toohello URL opgegeven zonder te wachten op reactie.</span><span class="sxs-lookup"><span data-stu-id="ece8c-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="ece8c-126">[Aanvraag verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -verzendt een aanvraag toohello URL opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ece8c-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="ece8c-127">[Stel aanvraagmethode](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -kunt u toochange Hallo HTTP-methode voor een aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ece8c-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="ece8c-128">[Status instellen](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -wijzigingen Hallo HTTP status code toohello opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="ece8c-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="ece8c-129">[Variabele instellen] [ Set variable] -persistent maken van een waarde in een benoemde [context] [ context] variabele voor latere toegang.</span><span class="sxs-lookup"><span data-stu-id="ece8c-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="ece8c-130">[Tracering](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -wordt een tekenreeks toegevoegd in Hallo [API Inspector](api-management-howto-api-inspector.md) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ece8c-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="ece8c-131">[Wacht](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - wacht ingesloten verzenden aanvragen, waarde niet ophalen uit de cache of beheren van stroom beleid toocomplete voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="ece8c-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="ece8c-132">[Verificatiebeleid][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="ece8c-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="ece8c-133">[Verificatie met Basic] [ Authenticate with Basic] -verificatie met een back-endservice basisverificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ece8c-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="ece8c-134">[Verificatie met een clientcertificaat] [ Authenticate with client certificate] -verificatie met een back-endservice met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="ece8c-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="ece8c-135">[Cachebeleidsregels][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="ece8c-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="ece8c-136">[Ophalen uit de cache] [ Get from cache] -cache uitvoeren opzoeken en retourneren een geldige cacheantwoord indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="ece8c-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="ece8c-137">[Opslaan van toocache] [ Store toocache] -Caches antwoord toohello op basis van opgegeven configuratie van de cache-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="ece8c-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="ece8c-138">[Waarde niet ophalen uit de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) -ophalen van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="ece8c-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="ece8c-139">[Waarde opslaan in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -opslaan van een item in Hallo cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="ece8c-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="ece8c-140">[Waarde verwijderen uit de cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -verwijderen van een item in Hallo cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="ece8c-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="ece8c-141">[Cross-domeinbeleid][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="ece8c-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="ece8c-142">[Aanroepen tussen domeinen toestaan] [ Allow cross-domain calls] -Hallo API toegankelijk van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.</span><span class="sxs-lookup"><span data-stu-id="ece8c-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="ece8c-143">[CORS] [ CORS] -voegt tooan cross-origin-resource delen (CORS) ondersteunen of een API tooallow tussen domeinen aanroepen van clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="ece8c-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="ece8c-144">[JSONP] [ JSONP] - JSON toegevoegd met de ondersteuning tooan bewerking opvulling (JSONP) of een API tooallow tussen domeinen aanroepen vanuit JavaScript-clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="ece8c-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="ece8c-145">[Claimtransformatiebeleidsinstellingen][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="ece8c-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="ece8c-146">[Converteren van JSON tooXML] [ Convert JSON tooXML] : zet aanvraag of antwoord body van JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="ece8c-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="ece8c-147">[Converteren van XML-tooJSON] [ Convert XML tooJSON] : zet aanvraag of antwoord body van XML-tooJSON.</span><span class="sxs-lookup"><span data-stu-id="ece8c-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="ece8c-148">[Zoeken en vervangen tekenreeks in de hoofdtekst] [ Find and replace string in body] - zoeken naar een subtekenreeks aanvraag of antwoord en wordt vervangen door een andere subtekenreeks.</span><span class="sxs-lookup"><span data-stu-id="ece8c-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="ece8c-149">[URL's in de inhoud te maskeren] [ Mask URLs in content] -koppelingen herschrijft (maskers) antwoord Hallo body zodat ze equivalente koppeling toohello via Hallo gateway wijst.</span><span class="sxs-lookup"><span data-stu-id="ece8c-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="ece8c-150">[Instellen van de back-endservice] [ Set backend service] -back-endservice Hallo voor de binnenkomende aanvraag wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="ece8c-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="ece8c-151">[Instantie ingesteld] [ Set body] -hoofdtekst van het Hallo-bericht voor binnenkomende en uitgaande aanvragen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ece8c-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="ece8c-152">[Set HTTP-header] [ Set HTTP header] : een waarde tooan bestaande antwoord en/of de aanvraagheader wijst of voegt een nieuwe antwoord en/of de aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="ece8c-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="ece8c-153">[Querytekenreeksparameter ingesteld] [ Set query string parameter] - wordt toegevoegd, vervangt de waarde van of verwijderd van de aanvraag queryreeksparameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="ece8c-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="ece8c-154">[Herschrijven van URL's] [ Rewrite URL] -zet u een aanvraag-URL van de openbare formulier toohello vorm werd verwacht door Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="ece8c-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ece8c-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ece8c-155">Next steps</span></span>
<span data-ttu-id="ece8c-156">Zie voor meer informatie over beleidsexpressies Hallo video te volgen.</span><span class="sxs-lookup"><span data-stu-id="ece8c-156">For more information on policy expressions, see hello following video.</span></span>

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


