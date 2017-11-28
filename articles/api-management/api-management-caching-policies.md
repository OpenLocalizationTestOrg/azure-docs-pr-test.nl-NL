---
title: aaaAzure API Management cachebeleidsregels | Microsoft Docs
description: Meer informatie over Hallo cachebeleidsregels beschikbaar voor gebruik in Azure API Management.
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
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="d5bbc-103">De cachebeleidsregels API Management</span><span class="sxs-lookup"><span data-stu-id="d5bbc-103">API Management caching policies</span></span>
<span data-ttu-id="d5bbc-104">Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="d5bbc-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="d5bbc-106"><a name="CachingPolicies"></a>Cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="d5bbc-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="d5bbc-107">Antwoord cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="d5bbc-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="d5bbc-108">[Ophalen uit de cache](api-management-caching-policies.md#GetFromCache) -cache uitvoeren opzoeken en retourneren een geldige in cache opgeslagen reacties indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="d5bbc-109">[Opslaan van toocache](api-management-caching-policies.md#StoreToCache) - Caches reacties op basis van toohello opgegeven cache-control-configuratie.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="d5bbc-110">Waarde cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="d5bbc-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="d5bbc-111">[Waarde niet ophalen uit de cache](#GetFromCacheByKey) -ophalen van een item in de cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="d5bbc-112">[Waarde opslaan in cache](#StoreToCacheByKey) -opslaan van een item in Hallo cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="d5bbc-113">[Waarde verwijderen uit de cache](#RemoveCacheByKey) -verwijderen van een item in Hallo cache per sleutel.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="d5bbc-114"><a name="GetFromCache"></a>Ophalen uit de cache</span><span class="sxs-lookup"><span data-stu-id="d5bbc-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="d5bbc-115">Gebruik Hallo `cache-lookup` tooperform beleidscache opzoeken en retourneren een geldige cacheantwoord indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="d5bbc-116">Dit beleid kan worden toegepast in gevallen waar antwoordinhoud statisch gedurende een periode blijft.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="d5bbc-117">Antwoord in cache opslaan minder bandbreedte en verwerking van vereisten opgelegd voor het Hallo back-end web server en lagere latentie, waargenomen door de consument API.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5bbc-118">Dit beleid moet zijn gekoppeld aan een [Store toocache](api-management-caching-policies.md#StoreToCache) beleid.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5bbc-119">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="d5bbc-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="d5bbc-120">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="d5bbc-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="d5bbc-121">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d5bbc-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="d5bbc-122">Voorbeeld met behulp van beleidsexpressies</span><span class="sxs-lookup"><span data-stu-id="d5bbc-122">Example using policy expressions</span></span>  
 <span data-ttu-id="d5bbc-123">Dit voorbeeld ziet u hoe tootooconfigure API Management antwoord in cache plaatsen dat overeenkomt met het antwoord in cache opslaan van back-endservice zoals opgegeven door Hallo HALLO hallo duur van de service back `Cache-Control` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="d5bbc-124">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too25:25 vooruit.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="d5bbc-125">Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d5bbc-126">Elementen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-126">Elements</span></span>  
  
|<span data-ttu-id="d5bbc-127">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-127">Name</span></span>|<span data-ttu-id="d5bbc-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-128">Description</span></span>|<span data-ttu-id="d5bbc-129">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5bbc-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="d5bbc-130">cache-lookup</span></span>|<span data-ttu-id="d5bbc-131">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-131">Root element.</span></span>|<span data-ttu-id="d5bbc-132">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-132">Yes</span></span>|  
|<span data-ttu-id="d5bbc-133">door header Vary</span><span class="sxs-lookup"><span data-stu-id="d5bbc-133">vary-by-header</span></span>|<span data-ttu-id="d5bbc-134">De antwoorden per waarde voor de opgegeven header, zoals accepteren, Accept-Charset Accept-Encoding, Accept-Language autorisatie Expect, van de Host, cache beginnen op If-Match.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="d5bbc-135">Nee</span><span class="sxs-lookup"><span data-stu-id="d5bbc-135">No</span></span>|  
|<span data-ttu-id="d5bbc-136">variëren door-query-parameter</span><span class="sxs-lookup"><span data-stu-id="d5bbc-136">vary-by-query-parameter</span></span>|<span data-ttu-id="d5bbc-137">De cache beginnen op antwoorden per waarde voor opgegeven queryparameters.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="d5bbc-138">Voer één of meerdere parameters.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="d5bbc-139">Gebruik puntkomma als scheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-139">Use semicolon as a separator.</span></span> <span data-ttu-id="d5bbc-140">Als niets wordt opgegeven, worden alle queryparameters gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="d5bbc-141">Nee</span><span class="sxs-lookup"><span data-stu-id="d5bbc-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5bbc-142">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="d5bbc-142">Attributes</span></span>  
  
|<span data-ttu-id="d5bbc-143">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-143">Name</span></span>|<span data-ttu-id="d5bbc-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-144">Description</span></span>|<span data-ttu-id="d5bbc-145">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-145">Required</span></span>|<span data-ttu-id="d5bbc-146">Standaard</span><span class="sxs-lookup"><span data-stu-id="d5bbc-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5bbc-147">toestaan dat persoonlijke-antwoord-schrijfcache</span><span class="sxs-lookup"><span data-stu-id="d5bbc-147">allow-private-response-caching</span></span>|<span data-ttu-id="d5bbc-148">Als de waarde te`true`, kunt opslaan in cache van aanvragen met een autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="d5bbc-149">Nee</span><span class="sxs-lookup"><span data-stu-id="d5bbc-149">No</span></span>|<span data-ttu-id="d5bbc-150">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="d5bbc-150">false</span></span>|  
|<span data-ttu-id="d5bbc-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="d5bbc-151">downstream-caching-type</span></span>|<span data-ttu-id="d5bbc-152">Dit kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="d5bbc-153">-none - downstream opslaan in cache is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="d5bbc-154">-persoonlijke - downstream persoonlijke opslaan in cache is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="d5bbc-155">-openbaar: persoonlijke en gedeelde downstream cache is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="d5bbc-156">Nee</span><span class="sxs-lookup"><span data-stu-id="d5bbc-156">No</span></span>|<span data-ttu-id="d5bbc-157">Geen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-157">none</span></span>|  
|<span data-ttu-id="d5bbc-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="d5bbc-158">must-revalidate</span></span>|<span data-ttu-id="d5bbc-159">Als downstream caching is ingeschakeld dit kenmerk wordt in- of uitschakelen Hallo `must-revalidate` cache-control-instructie in de antwoorden van de gateway.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="d5bbc-160">Nee</span><span class="sxs-lookup"><span data-stu-id="d5bbc-160">No</span></span>|<span data-ttu-id="d5bbc-161">De waarde True</span><span class="sxs-lookup"><span data-stu-id="d5bbc-161">true</span></span>|  
|<span data-ttu-id="d5bbc-162">door ontwikkelaars variëren</span><span class="sxs-lookup"><span data-stu-id="d5bbc-162">vary-by-developer</span></span>|<span data-ttu-id="d5bbc-163">Stel te`true` toocache antwoorden per developer-sleutel.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="d5bbc-164">Nee</span><span class="sxs-lookup"><span data-stu-id="d5bbc-164">No</span></span>|<span data-ttu-id="d5bbc-165">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="d5bbc-165">false</span></span>|  
|<span data-ttu-id="d5bbc-166">variëren-in-developer-groepen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-166">vary-by-developer-groups</span></span>|<span data-ttu-id="d5bbc-167">Stel te`true` toocache antwoorden per gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="d5bbc-168">Nee</span><span class="sxs-lookup"><span data-stu-id="d5bbc-168">No</span></span>|<span data-ttu-id="d5bbc-169">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="d5bbc-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5bbc-170">Gebruik</span><span class="sxs-lookup"><span data-stu-id="d5bbc-170">Usage</span></span>  
 <span data-ttu-id="d5bbc-171">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5bbc-172">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="d5bbc-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d5bbc-173">**Beleid scopes:** API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="d5bbc-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="d5bbc-174"><a name="StoreToCache"></a>Store toocache</span><span class="sxs-lookup"><span data-stu-id="d5bbc-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="d5bbc-175">Hallo `cache-store` beleid caches reacties op basis van toohello cache-instellingen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="d5bbc-176">Dit beleid kan worden toegepast in gevallen waar antwoordinhoud statisch gedurende een periode blijft.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="d5bbc-177">Antwoord in cache opslaan minder bandbreedte en verwerking van vereisten opgelegd voor het Hallo back-end web server en lagere latentie, waargenomen door de consument API.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5bbc-178">Dit beleid moet zijn gekoppeld aan een [ophalen uit de cache](api-management-caching-policies.md#GetFromCache) beleid.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5bbc-179">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="d5bbc-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="d5bbc-180">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="d5bbc-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="d5bbc-181">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d5bbc-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="d5bbc-182">Voorbeeld met behulp van beleidsexpressies</span><span class="sxs-lookup"><span data-stu-id="d5bbc-182">Example using policy expressions</span></span>  
 <span data-ttu-id="d5bbc-183">Dit voorbeeld ziet u hoe tootooconfigure API Management antwoord in cache plaatsen dat overeenkomt met het antwoord in cache opslaan van back-endservice zoals opgegeven door Hallo HALLO hallo duur van de service back `Cache-Control` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="d5bbc-184">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too25:25 vooruit.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="d5bbc-185">Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d5bbc-186">Elementen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-186">Elements</span></span>  
  
|<span data-ttu-id="d5bbc-187">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-187">Name</span></span>|<span data-ttu-id="d5bbc-188">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-188">Description</span></span>|<span data-ttu-id="d5bbc-189">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5bbc-190">opslag van de cache</span><span class="sxs-lookup"><span data-stu-id="d5bbc-190">cache-store</span></span>|<span data-ttu-id="d5bbc-191">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-191">Root element.</span></span>|<span data-ttu-id="d5bbc-192">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5bbc-193">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="d5bbc-193">Attributes</span></span>  
  
|<span data-ttu-id="d5bbc-194">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-194">Name</span></span>|<span data-ttu-id="d5bbc-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-195">Description</span></span>|<span data-ttu-id="d5bbc-196">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-196">Required</span></span>|<span data-ttu-id="d5bbc-197">Standaard</span><span class="sxs-lookup"><span data-stu-id="d5bbc-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5bbc-198">Duur</span><span class="sxs-lookup"><span data-stu-id="d5bbc-198">duration</span></span>|<span data-ttu-id="d5bbc-199">Time-to-live Hallo in cache opgeslagen vermeldingen, in seconden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="d5bbc-200">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-200">Yes</span></span>|<span data-ttu-id="d5bbc-201">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5bbc-202">Gebruik</span><span class="sxs-lookup"><span data-stu-id="d5bbc-202">Usage</span></span>  
 <span data-ttu-id="d5bbc-203">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5bbc-204">**Beleid secties:** uitgaand</span><span class="sxs-lookup"><span data-stu-id="d5bbc-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="d5bbc-205">**Beleid scopes:** API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="d5bbc-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="d5bbc-206"><a name="GetFromCacheByKey"></a>Waarde niet ophalen uit de cache</span><span class="sxs-lookup"><span data-stu-id="d5bbc-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="d5bbc-207">Gebruik Hallo `cache-lookup-value` beleid tooperform opzoeken in de cache per sleutel en een in cache opgeslagen waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="d5bbc-208">Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5bbc-209">Dit beleid moet zijn gekoppeld aan een [waarde opslaan in cache](#StoreToCacheByKey) beleid.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5bbc-210">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="d5bbc-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="d5bbc-211">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d5bbc-211">Example</span></span>  
 <span data-ttu-id="d5bbc-212">Zie voor meer informatie over en voorbeelden van dit beleid, [aangepast opslaan in cache in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="d5bbc-213">Elementen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-213">Elements</span></span>  
  
|<span data-ttu-id="d5bbc-214">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-214">Name</span></span>|<span data-ttu-id="d5bbc-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-215">Description</span></span>|<span data-ttu-id="d5bbc-216">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5bbc-217">cache-lookup-waarde</span><span class="sxs-lookup"><span data-stu-id="d5bbc-217">cache-lookup-value</span></span>|<span data-ttu-id="d5bbc-218">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-218">Root element.</span></span>|<span data-ttu-id="d5bbc-219">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5bbc-220">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="d5bbc-220">Attributes</span></span>  
  
|<span data-ttu-id="d5bbc-221">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-221">Name</span></span>|<span data-ttu-id="d5bbc-222">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-222">Description</span></span>|<span data-ttu-id="d5bbc-223">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-223">Required</span></span>|<span data-ttu-id="d5bbc-224">Standaard</span><span class="sxs-lookup"><span data-stu-id="d5bbc-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5bbc-225">standaard-waarde</span><span class="sxs-lookup"><span data-stu-id="d5bbc-225">default-value</span></span>|<span data-ttu-id="d5bbc-226">Een waarde die wordt toegewezen variabele toohello als sleutel zoeken in het cachegeheugen Hallo geresulteerd in een ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="d5bbc-227">Als dit kenmerk niet is opgegeven, `null` is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="d5bbc-228">Nee</span><span class="sxs-lookup"><span data-stu-id="d5bbc-228">No</span></span>|`null`|  
|<span data-ttu-id="d5bbc-229">sleutel</span><span class="sxs-lookup"><span data-stu-id="d5bbc-229">key</span></span>|<span data-ttu-id="d5bbc-230">Toouse sleutelwaarde in Hallo opzoeken in de cache.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="d5bbc-231">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-231">Yes</span></span>|<span data-ttu-id="d5bbc-232">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-232">N/A</span></span>|  
|<span data-ttu-id="d5bbc-233">naam variabele</span><span class="sxs-lookup"><span data-stu-id="d5bbc-233">variable-name</span></span>|<span data-ttu-id="d5bbc-234">Naam van Hallo [context variabele](api-management-policy-expressions.md#ContextVariables) Hallo opgezocht waarde wordt toegewezen als de zoekopdracht is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="d5bbc-235">Als lookup in een ontbreekt resulteert, Hallo variabele waarde Hallo Hallo wordt toegewezen `default-value` kenmerk of `null`als hello `default-value` kenmerk wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="d5bbc-236">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-236">Yes</span></span>|<span data-ttu-id="d5bbc-237">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5bbc-238">Gebruik</span><span class="sxs-lookup"><span data-stu-id="d5bbc-238">Usage</span></span>  
 <span data-ttu-id="d5bbc-239">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5bbc-240">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="d5bbc-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d5bbc-241">**Beleid scopes:** algemeen API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="d5bbc-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="d5bbc-242"><a name="StoreToCacheByKey"></a>Waarde opslaan in cache</span><span class="sxs-lookup"><span data-stu-id="d5bbc-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="d5bbc-243">Hallo `cache-store-value` opslag van de cache per sleutel uitvoert.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="d5bbc-244">Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5bbc-245">Dit beleid moet zijn gekoppeld aan een [waarde niet ophalen uit de cache](#GetFromCacheByKey) beleid.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5bbc-246">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="d5bbc-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="d5bbc-247">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d5bbc-247">Example</span></span>  
 <span data-ttu-id="d5bbc-248">Zie voor meer informatie over en voorbeelden van dit beleid, [aangepast opslaan in cache in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="d5bbc-249">Elementen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-249">Elements</span></span>  
  
|<span data-ttu-id="d5bbc-250">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-250">Name</span></span>|<span data-ttu-id="d5bbc-251">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-251">Description</span></span>|<span data-ttu-id="d5bbc-252">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5bbc-253">cache-store-waarde</span><span class="sxs-lookup"><span data-stu-id="d5bbc-253">cache-store-value</span></span>|<span data-ttu-id="d5bbc-254">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-254">Root element.</span></span>|<span data-ttu-id="d5bbc-255">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5bbc-256">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="d5bbc-256">Attributes</span></span>  
  
|<span data-ttu-id="d5bbc-257">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-257">Name</span></span>|<span data-ttu-id="d5bbc-258">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-258">Description</span></span>|<span data-ttu-id="d5bbc-259">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-259">Required</span></span>|<span data-ttu-id="d5bbc-260">Standaard</span><span class="sxs-lookup"><span data-stu-id="d5bbc-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5bbc-261">Duur</span><span class="sxs-lookup"><span data-stu-id="d5bbc-261">duration</span></span>|<span data-ttu-id="d5bbc-262">Waarde wordt in de cache voor Hallo opgegeven duurwaarde, in seconden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="d5bbc-263">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-263">Yes</span></span>|<span data-ttu-id="d5bbc-264">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-264">N/A</span></span>|  
|<span data-ttu-id="d5bbc-265">sleutel</span><span class="sxs-lookup"><span data-stu-id="d5bbc-265">key</span></span>|<span data-ttu-id="d5bbc-266">Waarde van de belangrijkste Hallo cache worden opgeslagen onder.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="d5bbc-267">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-267">Yes</span></span>|<span data-ttu-id="d5bbc-268">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-268">N/A</span></span>|  
|<span data-ttu-id="d5bbc-269">waarde</span><span class="sxs-lookup"><span data-stu-id="d5bbc-269">value</span></span>|<span data-ttu-id="d5bbc-270">Hallo waarde toobe in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-270">hello value toobe cached.</span></span>|<span data-ttu-id="d5bbc-271">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-271">Yes</span></span>|<span data-ttu-id="d5bbc-272">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5bbc-273">Gebruik</span><span class="sxs-lookup"><span data-stu-id="d5bbc-273">Usage</span></span>  
 <span data-ttu-id="d5bbc-274">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5bbc-275">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="d5bbc-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d5bbc-276">**Beleid scopes:** algemeen API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="d5bbc-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="d5bbc-277"><a name="RemoveCacheByKey"></a>Waarde uit cache verwijderen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="d5bbc-278">Hallo `cache-remove-value` een geïdentificeerd door de sleutel in de cache-item wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="d5bbc-279">Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="d5bbc-280">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="d5bbc-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="d5bbc-281">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d5bbc-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="d5bbc-282">Elementen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-282">Elements</span></span>  
  
|<span data-ttu-id="d5bbc-283">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-283">Name</span></span>|<span data-ttu-id="d5bbc-284">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-284">Description</span></span>|<span data-ttu-id="d5bbc-285">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5bbc-286">cache-remove-waarde</span><span class="sxs-lookup"><span data-stu-id="d5bbc-286">cache-remove-value</span></span>|<span data-ttu-id="d5bbc-287">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-287">Root element.</span></span>|<span data-ttu-id="d5bbc-288">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="d5bbc-289">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="d5bbc-289">Attributes</span></span>  
  
|<span data-ttu-id="d5bbc-290">Naam</span><span class="sxs-lookup"><span data-stu-id="d5bbc-290">Name</span></span>|<span data-ttu-id="d5bbc-291">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d5bbc-291">Description</span></span>|<span data-ttu-id="d5bbc-292">Vereist</span><span class="sxs-lookup"><span data-stu-id="d5bbc-292">Required</span></span>|<span data-ttu-id="d5bbc-293">Standaard</span><span class="sxs-lookup"><span data-stu-id="d5bbc-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5bbc-294">sleutel</span><span class="sxs-lookup"><span data-stu-id="d5bbc-294">key</span></span>|<span data-ttu-id="d5bbc-295">Hallo-sleutel van Hallo is eerder in cache opgeslagen waarde toobe verwijderd uit het Hallo-cachegeheugen.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="d5bbc-296">Ja</span><span class="sxs-lookup"><span data-stu-id="d5bbc-296">Yes</span></span>|<span data-ttu-id="d5bbc-297">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="d5bbc-298">Gebruik</span><span class="sxs-lookup"><span data-stu-id="d5bbc-298">Usage</span></span>  
 <span data-ttu-id="d5bbc-299">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="d5bbc-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="d5bbc-300">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="d5bbc-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d5bbc-301">**Beleid scopes:** algemeen API, bewerking, product</span><span class="sxs-lookup"><span data-stu-id="d5bbc-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="d5bbc-302">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d5bbc-302">Next steps</span></span>
<span data-ttu-id="d5bbc-303">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  