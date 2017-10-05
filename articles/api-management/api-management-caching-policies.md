---
title: Azure API Management cachebeleidsregels | Microsoft Docs
description: Meer informatie over de cachebeleidsregels beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="00ee2-103">De cachebeleidsregels API Management</span><span class="sxs-lookup"><span data-stu-id="00ee2-103">API Management caching policies</span></span>
<span data-ttu-id="00ee2-104">Dit onderwerp bevat een verwijzing voor de volgende API Management-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="00ee2-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="00ee2-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="00ee2-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="00ee2-106"><a name="CachingPolicies"></a>Cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="00ee2-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="00ee2-107">Antwoord cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="00ee2-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="00ee2-108">[Ophalen uit de cache](api-management-caching-policies.md#GetFromCache) -cache uitvoeren opzoeken en retourneren een geldige in cache opgeslagen reacties indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="00ee2-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="00ee2-109">[Store aan cache](api-management-caching-policies.md#StoreToCache) -antwoorden volgens de configuratie opgegeven cache opslaat in de cache.</span><span class="sxs-lookup"><span data-stu-id="00ee2-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="00ee2-110">Waarde cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="00ee2-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="00ee2-111">[Waarde niet ophalen uit de cache](#GetFromCacheByKey) -ophalen van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="00ee2-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="00ee2-112">[Waarde opslaan in cache](#StoreToCacheByKey) -opslaan van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="00ee2-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="00ee2-113">[Waarde verwijderen uit de cache](#RemoveCacheByKey) -verwijderen van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="00ee2-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="00ee2-114"><a name="GetFromCache"></a>Ophalen uit de cache</span><span class="sxs-lookup"><span data-stu-id="00ee2-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="00ee2-115">Gebruik de `cache-lookup` beleid voor het uitvoeren van de cache opzoeken en retourneren een geldige cacheantwoord indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="00ee2-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="00ee2-116">Dit beleid kan worden toegepast in gevallen waar antwoordinhoud statisch gedurende een periode blijft.</span><span class="sxs-lookup"><span data-stu-id="00ee2-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="00ee2-117">Antwoord in cache opslaan minder bandbreedte en verwerking van vereisten opgelegd voor de back-end web server en lagere latentie waargenomen door de consument API.</span><span class="sxs-lookup"><span data-stu-id="00ee2-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="00ee2-118">Dit beleid moet zijn gekoppeld aan een [Store aan cache](api-management-caching-policies.md#StoreToCache) beleid.</span><span class="sxs-lookup"><span data-stu-id="00ee2-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="00ee2-119">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="00ee2-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="00ee2-120">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="00ee2-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="00ee2-121">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="00ee2-121">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="00ee2-122">Voorbeeld met behulp van beleidsexpressies</span><span class="sxs-lookup"><span data-stu-id="00ee2-122">Example using policy expressions</span></span>  
 <span data-ttu-id="00ee2-123">Dit voorbeeld ziet u hoe aan voor het configureren van API Management-antwoord in cache opslaan duur die overeenkomt met het antwoord in cache plaatsen van de back-endservice als opgegeven door de back-service `Cache-Control` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="00ee2-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="00ee2-124">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit te 25:25.</span><span class="sxs-lookup"><span data-stu-id="00ee2-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="00ee2-125">Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="00ee2-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="00ee2-126">Elementen</span><span class="sxs-lookup"><span data-stu-id="00ee2-126">Elements</span></span>  
  
|<span data-ttu-id="00ee2-127">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-127">Name</span></span>|<span data-ttu-id="00ee2-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-128">Description</span></span>|<span data-ttu-id="00ee2-129">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="00ee2-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="00ee2-130">cache-lookup</span></span>|<span data-ttu-id="00ee2-131">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="00ee2-131">Root element.</span></span>|<span data-ttu-id="00ee2-132">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-132">Yes</span></span>|  
|<span data-ttu-id="00ee2-133">door header Vary</span><span class="sxs-lookup"><span data-stu-id="00ee2-133">vary-by-header</span></span>|<span data-ttu-id="00ee2-134">De antwoorden per waarde voor de opgegeven header, zoals accepteren, Accept-Charset Accept-Encoding, Accept-Language autorisatie Expect, van de Host, cache beginnen op If-Match.</span><span class="sxs-lookup"><span data-stu-id="00ee2-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="00ee2-135">Nee</span><span class="sxs-lookup"><span data-stu-id="00ee2-135">No</span></span>|  
|<span data-ttu-id="00ee2-136">variëren door-query-parameter</span><span class="sxs-lookup"><span data-stu-id="00ee2-136">vary-by-query-parameter</span></span>|<span data-ttu-id="00ee2-137">De cache beginnen op antwoorden per waarde voor opgegeven queryparameters.</span><span class="sxs-lookup"><span data-stu-id="00ee2-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="00ee2-138">Voer één of meerdere parameters.</span><span class="sxs-lookup"><span data-stu-id="00ee2-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="00ee2-139">Gebruik puntkomma als scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="00ee2-139">Use semicolon as a separator.</span></span> <span data-ttu-id="00ee2-140">Als niets wordt opgegeven, worden alle queryparameters gebruikt.</span><span class="sxs-lookup"><span data-stu-id="00ee2-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="00ee2-141">Nee</span><span class="sxs-lookup"><span data-stu-id="00ee2-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="00ee2-142">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="00ee2-142">Attributes</span></span>  
  
|<span data-ttu-id="00ee2-143">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-143">Name</span></span>|<span data-ttu-id="00ee2-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-144">Description</span></span>|<span data-ttu-id="00ee2-145">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-145">Required</span></span>|<span data-ttu-id="00ee2-146">Standaard</span><span class="sxs-lookup"><span data-stu-id="00ee2-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="00ee2-147">toestaan dat persoonlijke-antwoord-schrijfcache</span><span class="sxs-lookup"><span data-stu-id="00ee2-147">allow-private-response-caching</span></span>|<span data-ttu-id="00ee2-148">Als de waarde `true`, kunt opslaan in cache van aanvragen met een autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="00ee2-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="00ee2-149">Nee</span><span class="sxs-lookup"><span data-stu-id="00ee2-149">No</span></span>|<span data-ttu-id="00ee2-150">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="00ee2-150">false</span></span>|  
|<span data-ttu-id="00ee2-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="00ee2-151">downstream-caching-type</span></span>|<span data-ttu-id="00ee2-152">Dit kenmerk moet worden ingesteld op een van de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="00ee2-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="00ee2-153">-none - downstream opslaan in cache is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="00ee2-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="00ee2-154">-persoonlijke - downstream persoonlijke opslaan in cache is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="00ee2-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="00ee2-155">-openbaar: persoonlijke en gedeelde downstream cache is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="00ee2-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="00ee2-156">Nee</span><span class="sxs-lookup"><span data-stu-id="00ee2-156">No</span></span>|<span data-ttu-id="00ee2-157">Geen</span><span class="sxs-lookup"><span data-stu-id="00ee2-157">none</span></span>|  
|<span data-ttu-id="00ee2-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="00ee2-158">must-revalidate</span></span>|<span data-ttu-id="00ee2-159">Wanneer downstream caching is ingeschakeld dit kenmerk schakelt in of uit de `must-revalidate` cache-control-instructie in de antwoorden van de gateway.</span><span class="sxs-lookup"><span data-stu-id="00ee2-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="00ee2-160">Nee</span><span class="sxs-lookup"><span data-stu-id="00ee2-160">No</span></span>|<span data-ttu-id="00ee2-161">De waarde True</span><span class="sxs-lookup"><span data-stu-id="00ee2-161">true</span></span>|  
|<span data-ttu-id="00ee2-162">door ontwikkelaars variëren</span><span class="sxs-lookup"><span data-stu-id="00ee2-162">vary-by-developer</span></span>|<span data-ttu-id="00ee2-163">Ingesteld op `true` aan reacties van cache per sleutel van de ontwikkelaar.</span><span class="sxs-lookup"><span data-stu-id="00ee2-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="00ee2-164">Nee</span><span class="sxs-lookup"><span data-stu-id="00ee2-164">No</span></span>|<span data-ttu-id="00ee2-165">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="00ee2-165">false</span></span>|  
|<span data-ttu-id="00ee2-166">variëren-in-developer-groepen</span><span class="sxs-lookup"><span data-stu-id="00ee2-166">vary-by-developer-groups</span></span>|<span data-ttu-id="00ee2-167">Ingesteld op `true` aan reacties van cache per gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="00ee2-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="00ee2-168">Nee</span><span class="sxs-lookup"><span data-stu-id="00ee2-168">No</span></span>|<span data-ttu-id="00ee2-169">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="00ee2-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="00ee2-170">Gebruik</span><span class="sxs-lookup"><span data-stu-id="00ee2-170">Usage</span></span>  
 <span data-ttu-id="00ee2-171">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="00ee2-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="00ee2-172">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="00ee2-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="00ee2-173">**Beleid scopes:** API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="00ee2-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="00ee2-174"><a name="StoreToCache"></a>Aan het cachegeheugen opslaan</span><span class="sxs-lookup"><span data-stu-id="00ee2-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="00ee2-175">De `cache-store` beleid in de cache opgeslagen reacties volgens de opgegeven cache-instellingen.</span><span class="sxs-lookup"><span data-stu-id="00ee2-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="00ee2-176">Dit beleid kan worden toegepast in gevallen waar antwoordinhoud statisch gedurende een periode blijft.</span><span class="sxs-lookup"><span data-stu-id="00ee2-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="00ee2-177">Antwoord in cache opslaan minder bandbreedte en verwerking van vereisten opgelegd voor de back-end web server en lagere latentie waargenomen door de consument API.</span><span class="sxs-lookup"><span data-stu-id="00ee2-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="00ee2-178">Dit beleid moet zijn gekoppeld aan een [ophalen uit de cache](api-management-caching-policies.md#GetFromCache) beleid.</span><span class="sxs-lookup"><span data-stu-id="00ee2-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="00ee2-179">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="00ee2-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="00ee2-180">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="00ee2-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="00ee2-181">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="00ee2-181">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="00ee2-182">Voorbeeld met behulp van beleidsexpressies</span><span class="sxs-lookup"><span data-stu-id="00ee2-182">Example using policy expressions</span></span>  
 <span data-ttu-id="00ee2-183">Dit voorbeeld ziet u hoe aan voor het configureren van API Management-antwoord in cache opslaan duur die overeenkomt met het antwoord in cache plaatsen van de back-endservice als opgegeven door de back-service `Cache-Control` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="00ee2-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="00ee2-184">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit te 25:25.</span><span class="sxs-lookup"><span data-stu-id="00ee2-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="00ee2-185">Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="00ee2-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="00ee2-186">Elementen</span><span class="sxs-lookup"><span data-stu-id="00ee2-186">Elements</span></span>  
  
|<span data-ttu-id="00ee2-187">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-187">Name</span></span>|<span data-ttu-id="00ee2-188">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-188">Description</span></span>|<span data-ttu-id="00ee2-189">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="00ee2-190">opslag van de cache</span><span class="sxs-lookup"><span data-stu-id="00ee2-190">cache-store</span></span>|<span data-ttu-id="00ee2-191">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="00ee2-191">Root element.</span></span>|<span data-ttu-id="00ee2-192">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="00ee2-193">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="00ee2-193">Attributes</span></span>  
  
|<span data-ttu-id="00ee2-194">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-194">Name</span></span>|<span data-ttu-id="00ee2-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-195">Description</span></span>|<span data-ttu-id="00ee2-196">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-196">Required</span></span>|<span data-ttu-id="00ee2-197">Standaard</span><span class="sxs-lookup"><span data-stu-id="00ee2-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="00ee2-198">Duur</span><span class="sxs-lookup"><span data-stu-id="00ee2-198">duration</span></span>|<span data-ttu-id="00ee2-199">Time-to-live van de vermeldingen in cache in seconden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="00ee2-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="00ee2-200">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-200">Yes</span></span>|<span data-ttu-id="00ee2-201">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="00ee2-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="00ee2-202">Gebruik</span><span class="sxs-lookup"><span data-stu-id="00ee2-202">Usage</span></span>  
 <span data-ttu-id="00ee2-203">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="00ee2-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="00ee2-204">**Beleid secties:** uitgaand</span><span class="sxs-lookup"><span data-stu-id="00ee2-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="00ee2-205">**Beleid scopes:** API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="00ee2-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="00ee2-206"><a name="GetFromCacheByKey"></a>Waarde niet ophalen uit de cache</span><span class="sxs-lookup"><span data-stu-id="00ee2-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="00ee2-207">Gebruik de `cache-lookup-value` beleid om te zoeken in het cachegeheugen worden uitgevoerd met sleutel en retourneert een waarde in de cache.</span><span class="sxs-lookup"><span data-stu-id="00ee2-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="00ee2-208">De sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="00ee2-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="00ee2-209">Dit beleid moet zijn gekoppeld aan een [waarde opslaan in cache](#StoreToCacheByKey) beleid.</span><span class="sxs-lookup"><span data-stu-id="00ee2-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="00ee2-210">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="00ee2-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="00ee2-211">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="00ee2-211">Example</span></span>  
 <span data-ttu-id="00ee2-212">Zie voor meer informatie over en voorbeelden van dit beleid, [aangepast opslaan in cache in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="00ee2-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="00ee2-213">Elementen</span><span class="sxs-lookup"><span data-stu-id="00ee2-213">Elements</span></span>  
  
|<span data-ttu-id="00ee2-214">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-214">Name</span></span>|<span data-ttu-id="00ee2-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-215">Description</span></span>|<span data-ttu-id="00ee2-216">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="00ee2-217">cache-lookup-waarde</span><span class="sxs-lookup"><span data-stu-id="00ee2-217">cache-lookup-value</span></span>|<span data-ttu-id="00ee2-218">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="00ee2-218">Root element.</span></span>|<span data-ttu-id="00ee2-219">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="00ee2-220">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="00ee2-220">Attributes</span></span>  
  
|<span data-ttu-id="00ee2-221">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-221">Name</span></span>|<span data-ttu-id="00ee2-222">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-222">Description</span></span>|<span data-ttu-id="00ee2-223">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-223">Required</span></span>|<span data-ttu-id="00ee2-224">Standaard</span><span class="sxs-lookup"><span data-stu-id="00ee2-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="00ee2-225">standaard-waarde</span><span class="sxs-lookup"><span data-stu-id="00ee2-225">default-value</span></span>|<span data-ttu-id="00ee2-226">Een waarde die wordt toegewezen aan de variabele als de sleutel zoeken in het cachegeheugen resulteerde in een ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="00ee2-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="00ee2-227">Als dit kenmerk niet is opgegeven, `null` is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="00ee2-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="00ee2-228">Nee</span><span class="sxs-lookup"><span data-stu-id="00ee2-228">No</span></span>|`null`|  
|<span data-ttu-id="00ee2-229">sleutel</span><span class="sxs-lookup"><span data-stu-id="00ee2-229">key</span></span>|<span data-ttu-id="00ee2-230">Waarde van de sleutel moet worden gebruikt in de zoekopdracht in de cache.</span><span class="sxs-lookup"><span data-stu-id="00ee2-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="00ee2-231">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-231">Yes</span></span>|<span data-ttu-id="00ee2-232">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="00ee2-232">N/A</span></span>|  
|<span data-ttu-id="00ee2-233">naam variabele</span><span class="sxs-lookup"><span data-stu-id="00ee2-233">variable-name</span></span>|<span data-ttu-id="00ee2-234">Naam van de [context variabele](api-management-policy-expressions.md#ContextVariables) de looked up waarde wordt toegewezen als de zoekopdracht is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="00ee2-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="00ee2-235">Als lookup in een ontbreekt resulteert, de variabele wordt toegewezen aan de waarde van de `default-value` kenmerk of `null`, als de `default-value` kenmerk wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="00ee2-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="00ee2-236">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-236">Yes</span></span>|<span data-ttu-id="00ee2-237">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="00ee2-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="00ee2-238">Gebruik</span><span class="sxs-lookup"><span data-stu-id="00ee2-238">Usage</span></span>  
 <span data-ttu-id="00ee2-239">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="00ee2-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="00ee2-240">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="00ee2-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="00ee2-241">**Beleid scopes:** algemeen API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="00ee2-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="00ee2-242"><a name="StoreToCacheByKey"></a>Waarde opslaan in cache</span><span class="sxs-lookup"><span data-stu-id="00ee2-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="00ee2-243">De `cache-store-value` opslag van de cache per sleutel uitvoert.</span><span class="sxs-lookup"><span data-stu-id="00ee2-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="00ee2-244">De sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="00ee2-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="00ee2-245">Dit beleid moet zijn gekoppeld aan een [waarde niet ophalen uit de cache](#GetFromCacheByKey) beleid.</span><span class="sxs-lookup"><span data-stu-id="00ee2-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="00ee2-246">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="00ee2-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="00ee2-247">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="00ee2-247">Example</span></span>  
 <span data-ttu-id="00ee2-248">Zie voor meer informatie over en voorbeelden van dit beleid, [aangepast opslaan in cache in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="00ee2-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="00ee2-249">Elementen</span><span class="sxs-lookup"><span data-stu-id="00ee2-249">Elements</span></span>  
  
|<span data-ttu-id="00ee2-250">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-250">Name</span></span>|<span data-ttu-id="00ee2-251">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-251">Description</span></span>|<span data-ttu-id="00ee2-252">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="00ee2-253">cache-store-waarde</span><span class="sxs-lookup"><span data-stu-id="00ee2-253">cache-store-value</span></span>|<span data-ttu-id="00ee2-254">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="00ee2-254">Root element.</span></span>|<span data-ttu-id="00ee2-255">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="00ee2-256">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="00ee2-256">Attributes</span></span>  
  
|<span data-ttu-id="00ee2-257">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-257">Name</span></span>|<span data-ttu-id="00ee2-258">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-258">Description</span></span>|<span data-ttu-id="00ee2-259">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-259">Required</span></span>|<span data-ttu-id="00ee2-260">Standaard</span><span class="sxs-lookup"><span data-stu-id="00ee2-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="00ee2-261">Duur</span><span class="sxs-lookup"><span data-stu-id="00ee2-261">duration</span></span>|<span data-ttu-id="00ee2-262">Waarde wordt voor de van de opgegeven duurwaarde, in seconden opgegeven in de cache worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="00ee2-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="00ee2-263">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-263">Yes</span></span>|<span data-ttu-id="00ee2-264">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="00ee2-264">N/A</span></span>|  
|<span data-ttu-id="00ee2-265">sleutel</span><span class="sxs-lookup"><span data-stu-id="00ee2-265">key</span></span>|<span data-ttu-id="00ee2-266">De waarde van de cache-sleutel worden opgeslagen onder.</span><span class="sxs-lookup"><span data-stu-id="00ee2-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="00ee2-267">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-267">Yes</span></span>|<span data-ttu-id="00ee2-268">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="00ee2-268">N/A</span></span>|  
|<span data-ttu-id="00ee2-269">waarde</span><span class="sxs-lookup"><span data-stu-id="00ee2-269">value</span></span>|<span data-ttu-id="00ee2-270">De waarde in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="00ee2-270">The value to be cached.</span></span>|<span data-ttu-id="00ee2-271">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-271">Yes</span></span>|<span data-ttu-id="00ee2-272">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="00ee2-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="00ee2-273">Gebruik</span><span class="sxs-lookup"><span data-stu-id="00ee2-273">Usage</span></span>  
 <span data-ttu-id="00ee2-274">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="00ee2-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="00ee2-275">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="00ee2-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="00ee2-276">**Beleid scopes:** algemeen API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="00ee2-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="00ee2-277"><a name="RemoveCacheByKey"></a>Waarde uit cache verwijderen</span><span class="sxs-lookup"><span data-stu-id="00ee2-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="00ee2-278">De `cache-remove-value` een geïdentificeerd door de sleutel in de cache-item wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="00ee2-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="00ee2-279">De sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="00ee2-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="00ee2-280">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="00ee2-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="00ee2-281">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="00ee2-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="00ee2-282">Elementen</span><span class="sxs-lookup"><span data-stu-id="00ee2-282">Elements</span></span>  
  
|<span data-ttu-id="00ee2-283">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-283">Name</span></span>|<span data-ttu-id="00ee2-284">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-284">Description</span></span>|<span data-ttu-id="00ee2-285">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="00ee2-286">cache-remove-waarde</span><span class="sxs-lookup"><span data-stu-id="00ee2-286">cache-remove-value</span></span>|<span data-ttu-id="00ee2-287">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="00ee2-287">Root element.</span></span>|<span data-ttu-id="00ee2-288">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="00ee2-289">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="00ee2-289">Attributes</span></span>  
  
|<span data-ttu-id="00ee2-290">Naam</span><span class="sxs-lookup"><span data-stu-id="00ee2-290">Name</span></span>|<span data-ttu-id="00ee2-291">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="00ee2-291">Description</span></span>|<span data-ttu-id="00ee2-292">Vereist</span><span class="sxs-lookup"><span data-stu-id="00ee2-292">Required</span></span>|<span data-ttu-id="00ee2-293">Standaard</span><span class="sxs-lookup"><span data-stu-id="00ee2-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="00ee2-294">sleutel</span><span class="sxs-lookup"><span data-stu-id="00ee2-294">key</span></span>|<span data-ttu-id="00ee2-295">De sleutel van de waarde uit de cache worden verwijderd uit de cache.</span><span class="sxs-lookup"><span data-stu-id="00ee2-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="00ee2-296">Ja</span><span class="sxs-lookup"><span data-stu-id="00ee2-296">Yes</span></span>|<span data-ttu-id="00ee2-297">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="00ee2-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="00ee2-298">Gebruik</span><span class="sxs-lookup"><span data-stu-id="00ee2-298">Usage</span></span>  
 <span data-ttu-id="00ee2-299">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="00ee2-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="00ee2-300">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="00ee2-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="00ee2-301">**Beleid scopes:** algemeen API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="00ee2-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="00ee2-302">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="00ee2-302">Next steps</span></span>
<span data-ttu-id="00ee2-303">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="00ee2-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  