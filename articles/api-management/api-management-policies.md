---
title: Azure API Management-beleidsregels | Microsoft Docs
description: Meer informatie over het beschikbaar voor gebruik in Azure API Management-beleid.
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
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="4121d-103">API Management-beleidsregels</span><span class="sxs-lookup"><span data-stu-id="4121d-103">API Management policies</span></span>
<span data-ttu-id="4121d-104">Deze sectie bevat een verwijzing voor de volgende API Management-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="4121d-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="4121d-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4121d-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="4121d-106">Beleidsregels zijn een krachtige mogelijkheid van het systeem waarmee de uitgever het gedrag van de API via configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4121d-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="4121d-107">Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op de aanvraag of antwoord van een API.</span><span class="sxs-lookup"><span data-stu-id="4121d-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="4121d-108">Populaire instructies omvatten Indelingsconversie van XML in JSON en snelheidsbeperking als u wilt beperken, de hoeveelheid inkomende aanroepen van een ontwikkelaar aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4121d-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="4121d-109">Veel meer beleidsregels zijn gebruiksklaar beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4121d-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="4121d-110">Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels, tenzij het beleid iets anders aangeeft.</span><span class="sxs-lookup"><span data-stu-id="4121d-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="4121d-111">Sommige beleidsregels, zoals de beleidsregels [Stroom controleren](api-management-advanced-policies.md#choose) en [Variabele instellen](api-management-advanced-policies.md#set-variable), zijn gebaseerd op beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="4121d-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="4121d-112">Zie voor meer informatie [Geavanceerde beleidsregels](api-management-advanced-policies.md#AdvancedPolicies) en [beleidsexpressies](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="4121d-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="4121d-113"><a name="ProxyPolicies"></a>Beleid</span><span class="sxs-lookup"><span data-stu-id="4121d-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="4121d-114">Beleid voor toegangsbeperking</span><span class="sxs-lookup"><span data-stu-id="4121d-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="4121d-115">[Controle van HTTP-header](api-management-access-restriction-policies.md#CheckHTTPHeader) -afdwingt bestaan en/of de waarde van een HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="4121d-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="4121d-116">[Aanroepfrequentie per abonnement](api-management-access-restriction-policies.md#LimitCallRate) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per abonnement op basis van een.</span><span class="sxs-lookup"><span data-stu-id="4121d-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="4121d-117">[Aanroepfrequentie per sleutel](api-management-access-restriction-policies.md#LimitCallRateByKey) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per sleutel op basis van een.</span><span class="sxs-lookup"><span data-stu-id="4121d-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="4121d-118">[Aanroeper IP-adressen beperken](api-management-access-restriction-policies.md#RestrictCallerIPs) -Filters (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="4121d-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="4121d-119">[Gebruiksquotum per abonnement instellen](api-management-access-restriction-policies.md#SetUsageQuota) -Hiermee kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van per abonnement afdwingen.</span><span class="sxs-lookup"><span data-stu-id="4121d-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="4121d-120">[Gebruiksquotum instellen door sleutel](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -Hiermee kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van de sleutel per afdwingen.</span><span class="sxs-lookup"><span data-stu-id="4121d-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="4121d-121">[Valideren van JWT](api-management-access-restriction-policies.md#ValidateJWT) -afdwingt bestaan en de geldigheid van een JWT opgehaald uit een opgegeven HTTP-koptekst of een opgegeven queryparameter.</span><span class="sxs-lookup"><span data-stu-id="4121d-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="4121d-122">Geavanceerde beleidsregels</span><span class="sxs-lookup"><span data-stu-id="4121d-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="4121d-123">[Transportbesturing](api-management-advanced-policies.md#choose) - voorwaardelijk beleidsverklaringen op basis van de evaluatie van Booleaanse expressies van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="4121d-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="4121d-124">[Doorsturen van aanvraag](api-management-advanced-policies.md#ForwardRequest) -stuurt de aanvraag naar de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="4121d-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="4121d-125">[Logboek naar Event Hub](api-management-advanced-policies.md#log-to-eventhub) -berichten in de opgegeven indeling voor een berichtdoel gedefinieerd door een entiteit berichtenlogboek verzendt.</span><span class="sxs-lookup"><span data-stu-id="4121d-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="4121d-126">[Probeer](api-management-advanced-policies.md#Retry) -uitvoering van de ingesloten beleidsverklaringen pogingen als en pas de voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="4121d-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="4121d-127">Uitvoering wordt herhaald op de opgegeven tijdsintervallen en tot het opgegeven aantal nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="4121d-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="4121d-128">[Antwoord retourneren](api-management-advanced-policies.md#ReturnResponse) -pipeline-uitvoering wordt afgebroken en retourneert het opgegeven antwoord rechtstreeks naar de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="4121d-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="4121d-129">[Eenzijdige aanvraag verzenden](api-management-advanced-policies.md#SendOneWayRequest) -verzendt een aanvraag naar de opgegeven URL zonder te wachten op reactie.</span><span class="sxs-lookup"><span data-stu-id="4121d-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="4121d-130">[Aanvraag verzenden](api-management-advanced-policies.md#SendRequest) -verzendt een aanvraag naar de opgegeven URL.</span><span class="sxs-lookup"><span data-stu-id="4121d-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="4121d-131">[Variabele instellen](api-management-advanced-policies.md#set-variable) -persistent maken van een waarde in een variabele met de naam context voor later toegang.</span><span class="sxs-lookup"><span data-stu-id="4121d-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="4121d-132">[Stel aanvraagmethode](api-management-advanced-policies.md#SetRequestMethod) -kunt u de HTTP-methode voor een aanvraag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4121d-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="4121d-133">[Statuscode ingesteld](api-management-advanced-policies.md#SetStatus) -wijzigingen van de HTTP-statuscode in de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="4121d-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="4121d-134">[Tracering](api-management-advanced-policies.md#Trace) -voegt een tekenreeks in de [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4121d-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="4121d-135">[Wacht](api-management-advanced-policies.md#Wait) -wacht voor ingesloten [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), of [transportbesturing](api-management-advanced-policies.md#choose) beleid om te voltooien voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="4121d-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="4121d-136">Verificatiebeleid</span><span class="sxs-lookup"><span data-stu-id="4121d-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="4121d-137">[Verificatie met Basic](api-management-authentication-policies.md#Basic) -verificatie met een back-endservice basisverificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4121d-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="4121d-138">[Verificatie met een clientcertificaat](api-management-authentication-policies.md#ClientCertificate) -verificatie met een back-endservice met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="4121d-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="4121d-139">Cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="4121d-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="4121d-140">[Ophalen uit de cache](api-management-caching-policies.md#GetFromCache) -cache uitvoeren opzoeken en retourneren een geldige cacheantwoord indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4121d-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="4121d-141">[Store aan cache](api-management-caching-policies.md#StoreToCache) -antwoord volgens de configuratie opgegeven cache opslaat in de cache.</span><span class="sxs-lookup"><span data-stu-id="4121d-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="4121d-142">[Waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey) -ophalen van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="4121d-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="4121d-143">[Waarde opslaan in cache](api-management-caching-policies.md#StoreToCacheByKey) -opslaan van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="4121d-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="4121d-144">[Waarde verwijderen uit de cache](api-management-caching-policies.md#RemoveCacheByKey) -verwijderen van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="4121d-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="4121d-145">Beleid voor meerdere domeinen</span><span class="sxs-lookup"><span data-stu-id="4121d-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="4121d-146">[Aanroepen tussen domeinen toestaan](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -de API van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients toegankelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="4121d-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="4121d-147">[CORS](api-management-cross-domain-policies.md#CORS) -cross-origin-resource delen (CORS) ondersteuning voor een bewerking of een API om toe te staan tussen domeinen aanroepen van clients op basis van een browser wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4121d-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="4121d-148">[JSONP](api-management-cross-domain-policies.md#JSONP) -JSON wordt toegevoegd met ondersteuning voor een bewerking of een API om toe te staan tussen domeinen aanroepen vanuit JavaScript-browser gebaseerde clients opvulling (JSONP).</span><span class="sxs-lookup"><span data-stu-id="4121d-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="4121d-149">Transformatiebeleid</span><span class="sxs-lookup"><span data-stu-id="4121d-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="4121d-150">[JSON converteren naar XML](api-management-transformation-policies.md#ConvertJSONtoXML) : zet aanvraag of antwoord body van JSON naar XML.</span><span class="sxs-lookup"><span data-stu-id="4121d-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="4121d-151">[XML niet converteren naar JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : zet aanvraag of antwoord body van XML naar JSON.</span><span class="sxs-lookup"><span data-stu-id="4121d-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="4121d-152">[Zoeken en vervangen tekenreeks in de hoofdtekst](api-management-transformation-policies.md#Findandreplacestringinbody) - zoeken naar een subtekenreeks aanvraag of antwoord en wordt vervangen door een andere subtekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4121d-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="4121d-153">[URL's in de inhoud te maskeren](api-management-transformation-policies.md#MaskURLSContent) -koppelingen herschrijft (maskers) in het antwoord body zodat deze naar de equivalente koppeling via de gateway verwijzen.</span><span class="sxs-lookup"><span data-stu-id="4121d-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="4121d-154">[Stel de back-endservice](api-management-transformation-policies.md#SetBackendService) -wijzigingen van de back-endservice voor de binnenkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="4121d-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="4121d-155">[Instantie ingesteld](api-management-transformation-policies.md#SetBody) -Hiermee stelt u de berichttekst voor binnenkomende en uitgaande aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4121d-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="4121d-156">[Set HTTP-header](api-management-transformation-policies.md#SetHTTPheader) : een waarde wordt toegewezen aan een bestaande antwoord en/of de aanvraag-header of voegt een nieuwe antwoord en/of de aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="4121d-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="4121d-157">[Querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) - wordt toegevoegd, vervangt de waarde van of verwijderd van de aanvraag queryreeksparameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="4121d-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="4121d-158">[Herschrijven van URL](api-management-transformation-policies.md#RewriteURL) -converteert van een aanvraag-URL van de openbare vorm aan het formulier dat werd verwacht door de webservice.</span><span class="sxs-lookup"><span data-stu-id="4121d-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="4121d-159">[XML met behulp van een XSLT transformeren](api-management-transformation-policies.md#XSLTransform) -geldt een XSL-transformatie voor XML in de hoofdtekst van de aanvraag of antwoord.</span><span class="sxs-lookup"><span data-stu-id="4121d-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="4121d-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4121d-160">Next steps</span></span>
<span data-ttu-id="4121d-161">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4121d-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
