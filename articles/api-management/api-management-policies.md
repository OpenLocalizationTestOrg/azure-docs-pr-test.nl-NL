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
# <a name="api-management-policies"></a><span data-ttu-id="f2cb4-103">API Management-beleidsregels</span><span class="sxs-lookup"><span data-stu-id="f2cb4-103">API Management policies</span></span>
<span data-ttu-id="f2cb4-104">Deze sectie bevat een verwijzing voor Hallo API Management-beleidsregels te volgen.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-104">This section provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="f2cb4-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f2cb4-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="f2cb4-106">Beleidsregels zijn een krachtige functie Hallo-systeem dat Hallo publisher toochange Hallo gedrag Hallo API via configuratie toestaan.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-106">Policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="f2cb4-107">Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op Hallo aanvraag of antwoord van een API.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-107">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="f2cb4-108">Populaire instructies omvatten Indelingsconversie van XML-tooJSON en snelheidsbeperking toorestrict Hallo hoeveelheid inkomende aanroepen van een ontwikkelaar aanroepen.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-108">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="f2cb4-109">Veel meer beleidsregels zijn out of box Hallo beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-109">Many more policies are available out of hello box.</span></span>  
  
 <span data-ttu-id="f2cb4-110">Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels hello, tenzij Hallo beleid iets anders aangeeft.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-110">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="f2cb4-111">Sommige beleidsregels zoals Hallo [transportbesturing](api-management-advanced-policies.md#choose) en [variabele instellen](api-management-advanced-policies.md#set-variable) beleid is gebaseerd op beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-111">Some policies such as hello [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="f2cb4-112">Zie voor meer informatie [Geavanceerde beleidsregels](api-management-advanced-policies.md#AdvancedPolicies) en [beleidsexpressies](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="f2cb4-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="f2cb4-113"><a name="ProxyPolicies"></a>Beleid</span><span class="sxs-lookup"><span data-stu-id="f2cb4-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="f2cb4-114">Beleid voor toegangsbeperking</span><span class="sxs-lookup"><span data-stu-id="f2cb4-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="f2cb4-115">[Controle van HTTP-header](api-management-access-restriction-policies.md#CheckHTTPHeader) -afdwingt bestaan en/of de waarde van een HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="f2cb4-116">[Aanroepfrequentie per abonnement](api-management-access-restriction-policies.md#LimitCallRate) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per abonnement op basis van een.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="f2cb4-117">[Aanroepfrequentie per sleutel](api-management-access-restriction-policies.md#LimitCallRateByKey) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per sleutel op basis van een.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="f2cb4-118">[Aanroeper IP-adressen beperken](api-management-access-restriction-policies.md#RestrictCallerIPs) -Filters (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="f2cb4-119">[Gebruiksquotum per abonnement instellen](api-management-access-restriction-policies.md#SetUsageQuota) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van per abonnement.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="f2cb4-120">[Gebruiksquotum instellen door sleutel](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van de per-sleutel.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="f2cb4-121">[Valideren van JWT](api-management-access-restriction-policies.md#ValidateJWT) -afdwingt bestaan en de geldigheid van een JWT opgehaald uit een opgegeven HTTP-koptekst of een opgegeven queryparameter.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="f2cb4-122">Geavanceerde beleidsregels</span><span class="sxs-lookup"><span data-stu-id="f2cb4-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="f2cb4-123">[Transportbesturing](api-management-advanced-policies.md#choose) - voorwaardelijk is van toepassing op basis van evaluatie van Booleaanse expressies Hallo beleidsverklaringen.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="f2cb4-124">[Doorsturen van aanvraag](api-management-advanced-policies.md#ForwardRequest) -stuurt Hallo aanvraag toohello back-endservice.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards hello request toohello backend service.</span></span>  
  
    -   <span data-ttu-id="f2cb4-125">[Meld u tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) -berichten verzendt in Hallo opgegeven indeling tooa berichtdoel gedefinieerd door een entiteit berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-125">[Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in hello specified format tooa message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="f2cb4-126">[Probeer](api-management-advanced-policies.md#Retry) -uitvoering van de nieuwe pogingen van Hallo ingesloten beleidsverklaringen, als en totdat Hallo-voorwaarde is voldaan.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="f2cb4-127">Uitvoering wordt herhaald op Hallo opgegeven tijdsintervallen en up toohello opgegeven aantal nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-127">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
    -   <span data-ttu-id="f2cb4-128">[Antwoord retourneren](api-management-advanced-policies.md#ReturnResponse) -wordt afgebroken pijplijn uitvoering en retourneert Hallo opgegeven antwoord rechtstreeks toohello aanroeper.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>  
  
    -   <span data-ttu-id="f2cb4-129">[Eenzijdige aanvraag verzenden](api-management-advanced-policies.md#SendOneWayRequest) -verzendt een aanvraag toohello URL opgegeven zonder te wachten op reactie.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="f2cb4-130">[Aanvraag verzenden](api-management-advanced-policies.md#SendRequest) -verzendt een aanvraag toohello URL opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request toohello specified URL.</span></span>  
  
    -   <span data-ttu-id="f2cb4-131">[Variabele instellen](api-management-advanced-policies.md#set-variable) -persistent maken van een waarde in een variabele met de naam context voor later toegang.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="f2cb4-132">[Stel aanvraagmethode](api-management-advanced-policies.md#SetRequestMethod) -kunt u toochange Hallo HTTP-methode voor een aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="f2cb4-133">[Statuscode ingesteld](api-management-advanced-policies.md#SetStatus) -wijzigingen Hallo HTTP status code toohello opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
    -   <span data-ttu-id="f2cb4-134">[Tracering](api-management-advanced-policies.md#Trace) -wordt een tekenreeks toegevoegd in Hallo [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="f2cb4-135">[Wacht](api-management-advanced-policies.md#Wait) -wacht voor ingesloten [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), of [transportbesturing](api-management-advanced-policies.md#choose) beleid toocomplete voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
-   [<span data-ttu-id="f2cb4-136">Verificatiebeleid</span><span class="sxs-lookup"><span data-stu-id="f2cb4-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="f2cb4-137">[Verificatie met Basic](api-management-authentication-policies.md#Basic) -verificatie met een back-endservice basisverificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="f2cb4-138">[Verificatie met een clientcertificaat](api-management-authentication-policies.md#ClientCertificate) -verificatie met een back-endservice met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="f2cb4-139">Cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="f2cb4-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="f2cb4-140">[Ophalen uit de cache](api-management-caching-policies.md#GetFromCache) -cache uitvoeren opzoeken en retourneren een geldige cacheantwoord indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="f2cb4-141">[Opslaan van toocache](api-management-caching-policies.md#StoreToCache) -Caches antwoord toohello op basis van opgegeven configuratie van de cache-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-141">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches response according toohello specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="f2cb4-142">[Waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey) -ophalen van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="f2cb4-143">[Waarde opslaan in cache](api-management-caching-policies.md#StoreToCacheByKey) -opslaan van een item in Hallo cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="f2cb4-144">[Waarde verwijderen uit de cache](api-management-caching-policies.md#RemoveCacheByKey) -verwijderen van een item in Hallo cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
-   [<span data-ttu-id="f2cb4-145">Beleid voor meerdere domeinen</span><span class="sxs-lookup"><span data-stu-id="f2cb4-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="f2cb4-146">[Aanroepen tussen domeinen toestaan](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -Hallo API toegankelijk van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="f2cb4-147">[CORS](api-management-cross-domain-policies.md#CORS) -voegt tooan cross-origin-resource delen (CORS) ondersteunen of een API tooallow tussen domeinen aanroepen van clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="f2cb4-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - JSON toegevoegd met de ondersteuning tooan bewerking opvulling (JSONP) of een API tooallow tussen domeinen aanroepen vanuit JavaScript-clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="f2cb4-149">Transformatiebeleid</span><span class="sxs-lookup"><span data-stu-id="f2cb4-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="f2cb4-150">[Converteren van JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) : zet aanvraag of antwoord body van JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-150">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
    -   <span data-ttu-id="f2cb4-151">[Converteren van XML-tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : zet aanvraag of antwoord body van XML-tooJSON.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-151">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
    -   <span data-ttu-id="f2cb4-152">[Zoeken en vervangen tekenreeks in de hoofdtekst](api-management-transformation-policies.md#Findandreplacestringinbody) - zoeken naar een subtekenreeks aanvraag of antwoord en wordt vervangen door een andere subtekenreeks.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="f2cb4-153">[URL's in de inhoud te maskeren](api-management-transformation-policies.md#MaskURLSContent) -koppelingen herschrijft (maskers) antwoord Hallo body zodat ze equivalente koppeling toohello via Hallo gateway wijst.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
    -   <span data-ttu-id="f2cb4-154">[Instellen van de back-endservice](api-management-transformation-policies.md#SetBackendService) -back-endservice Hallo voor de binnenkomende aanvraag wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="f2cb4-155">[Instantie ingesteld](api-management-transformation-policies.md#SetBody) -hoofdtekst van het Hallo-bericht voor binnenkomende en uitgaande aanvragen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="f2cb4-156">[Set HTTP-header](api-management-transformation-policies.md#SetHTTPheader) : een waarde tooan bestaande antwoord en/of de aanvraagheader wijst of voegt een nieuwe antwoord en/of de aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="f2cb4-157">[Querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) - wordt toegevoegd, vervangt de waarde van of verwijderd van de aanvraag queryreeksparameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="f2cb4-158">[Herschrijven van URL](api-management-transformation-policies.md#RewriteURL) -zet u een aanvraag-URL van de openbare formulier toohello vorm werd verwacht door Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
    -   <span data-ttu-id="f2cb4-159">[XML met behulp van een XSLT transformeren](api-management-transformation-policies.md#XSLTransform) -een XSL-transformatie tooXML in de hoofdtekst van de aanvraag of antwoord van de Hallo van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="f2cb4-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="f2cb4-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2cb4-160">Next steps</span></span>
<span data-ttu-id="f2cb4-161">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f2cb4-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
