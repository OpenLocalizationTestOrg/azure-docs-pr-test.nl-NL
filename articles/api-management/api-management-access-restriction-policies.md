---
title: aaaAzure API Management toegangsbeleid beperking | Microsoft Docs
description: Meer informatie over Hallo beperking toegangsbeleid beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="32745-103">Beperking van API Management toegangsbeleid</span><span class="sxs-lookup"><span data-stu-id="32745-103">API Management access restriction policies</span></span>
<span data-ttu-id="32745-104">Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen.</span><span class="sxs-lookup"><span data-stu-id="32745-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="32745-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="32745-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="32745-106"><a name="AccessRestrictionPolicies"></a>Softwarerestrictiebeleid toegang</span><span class="sxs-lookup"><span data-stu-id="32745-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="32745-107">[Controle van HTTP-header](api-management-access-restriction-policies.md#CheckHTTPHeader) -afdwingt bestaan en/of de waarde van een HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="32745-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="32745-108">[Aanroepfrequentie per abonnement](api-management-access-restriction-policies.md#LimitCallRate) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per abonnement op basis van een.</span><span class="sxs-lookup"><span data-stu-id="32745-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="32745-109">[Aanroepfrequentie per sleutel](#LimitCallRateByKey) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per sleutel op basis van een.</span><span class="sxs-lookup"><span data-stu-id="32745-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="32745-110">[Aanroeper IP-adressen beperken](api-management-access-restriction-policies.md#RestrictCallerIPs) -Filters (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="32745-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="32745-111">[Gebruiksquotum per abonnement instellen](api-management-access-restriction-policies.md#SetUsageQuota) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van per abonnement.</span><span class="sxs-lookup"><span data-stu-id="32745-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="32745-112">[Gebruiksquotum instellen door sleutel](#SetUsageQuotaByKey) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van de per-sleutel.</span><span class="sxs-lookup"><span data-stu-id="32745-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="32745-113">[Valideren van JWT](api-management-access-restriction-policies.md#ValidateJWT) -afdwingt bestaan en de geldigheid van een JWT opgehaald uit een opgegeven HTTP-koptekst of een opgegeven queryparameter.</span><span class="sxs-lookup"><span data-stu-id="32745-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="32745-114"><a name="CheckHTTPHeader"></a>Controleer de HTTP-header</span><span class="sxs-lookup"><span data-stu-id="32745-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="32745-115">Gebruik Hallo `check-header` beleid tooenforce dat een aanvraag een opgegeven HTTP-header heeft.</span><span class="sxs-lookup"><span data-stu-id="32745-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="32745-116">U kunt eventueel toosee controleren als Hallo-header een specifieke waarde of het selectievakje voor een bereik van toegestane waarden is.</span><span class="sxs-lookup"><span data-stu-id="32745-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="32745-117">Hallo controle mislukt, Hallo beleid aanvraagverwerking wordt beëindigd als HTTP-status code en de fout welkomstbericht opgegeven door het beleid voor Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="32745-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32745-118">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="32745-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="32745-119">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="32745-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="32745-120">Elementen</span><span class="sxs-lookup"><span data-stu-id="32745-120">Elements</span></span>  
  
|<span data-ttu-id="32745-121">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-121">Name</span></span>|<span data-ttu-id="32745-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-122">Description</span></span>|<span data-ttu-id="32745-123">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32745-124">controle-header</span><span class="sxs-lookup"><span data-stu-id="32745-124">check-header</span></span>|<span data-ttu-id="32745-125">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="32745-125">Root element.</span></span>|<span data-ttu-id="32745-126">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-126">Yes</span></span>|  
|<span data-ttu-id="32745-127">waarde</span><span class="sxs-lookup"><span data-stu-id="32745-127">value</span></span>|<span data-ttu-id="32745-128">Toegestane waarde voor HTTP-header.</span><span class="sxs-lookup"><span data-stu-id="32745-128">Allowed HTTP header value.</span></span> <span data-ttu-id="32745-129">Als meerdere elementen van de waarde worden opgegeven, Hallo selectievakje wordt beschouwd als geslaagd als een van de waarden Hallo een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="32745-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="32745-130">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32745-131">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="32745-131">Attributes</span></span>  
  
|<span data-ttu-id="32745-132">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-132">Name</span></span>|<span data-ttu-id="32745-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-133">Description</span></span>|<span data-ttu-id="32745-134">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-134">Required</span></span>|<span data-ttu-id="32745-135">Standaard</span><span class="sxs-lookup"><span data-stu-id="32745-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32745-136">kan de niet-controle-foutbericht</span><span class="sxs-lookup"><span data-stu-id="32745-136">failed-check-error-message</span></span>|<span data-ttu-id="32745-137">Fout bericht tooreturn in Hallo HTTP-antwoordtekst als Hallo header bestaat niet of een ongeldige waarde heeft.</span><span class="sxs-lookup"><span data-stu-id="32745-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="32745-138">Dit bericht moet de speciale tekens escape hebben.</span><span class="sxs-lookup"><span data-stu-id="32745-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="32745-139">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-139">Yes</span></span>|<span data-ttu-id="32745-140">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-140">N/A</span></span>|  
|<span data-ttu-id="32745-141">Kan controle httpcode</span><span class="sxs-lookup"><span data-stu-id="32745-141">failed-check-httpcode</span></span>|<span data-ttu-id="32745-142">HTTP-Status code tooreturn als Hallo header bestaat niet of een ongeldige waarde heeft.</span><span class="sxs-lookup"><span data-stu-id="32745-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="32745-143">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-143">Yes</span></span>|<span data-ttu-id="32745-144">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-144">N/A</span></span>|  
|<span data-ttu-id="32745-145">header-naam</span><span class="sxs-lookup"><span data-stu-id="32745-145">header-name</span></span>|<span data-ttu-id="32745-146">de naam van de Hallo Hallo toocheck HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="32745-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="32745-147">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-147">Yes</span></span>|<span data-ttu-id="32745-148">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-148">N/A</span></span>|  
|<span data-ttu-id="32745-149">negeren geval</span><span class="sxs-lookup"><span data-stu-id="32745-149">ignore-case</span></span>|<span data-ttu-id="32745-150">Kan worden ingesteld tooTrue of ONWAAR.</span><span class="sxs-lookup"><span data-stu-id="32745-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="32745-151">Als de set tooTrue aanvraag wordt genegeerd wanneer het Hallo-kopwaarde vergeleken met de Hallo set van acceptabele waarden.</span><span class="sxs-lookup"><span data-stu-id="32745-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="32745-152">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-152">Yes</span></span>|<span data-ttu-id="32745-153">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32745-154">Gebruik</span><span class="sxs-lookup"><span data-stu-id="32745-154">Usage</span></span>  
 <span data-ttu-id="32745-155">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="32745-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32745-156">**Beleid secties:** binnenkomende, uitgaande</span><span class="sxs-lookup"><span data-stu-id="32745-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="32745-157">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="32745-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="32745-158"><a name="LimitCallRate"></a>Aanroepfrequentie per abonnement</span><span class="sxs-lookup"><span data-stu-id="32745-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="32745-159">Hallo `rate-limit` beleid voorkomt dat het gebruik van de API pieken per abonnement op basis van een door het beperken van Hallo aanroepen snelheid tooa opgegeven aantal gedurende een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="32745-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="32745-160">Wanneer dit beleid wordt geactiveerd Hallo aanroeper ontvangt een `429 Too Many Requests` statuscode van antwoord.</span><span class="sxs-lookup"><span data-stu-id="32745-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="32745-161">Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="32745-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="32745-162">[Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van Hallo-beleid voor dit beleid.</span><span class="sxs-lookup"><span data-stu-id="32745-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32745-163">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="32745-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="32745-164">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="32745-164">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="32745-165">Elementen</span><span class="sxs-lookup"><span data-stu-id="32745-165">Elements</span></span>  
  
|<span data-ttu-id="32745-166">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-166">Name</span></span>|<span data-ttu-id="32745-167">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-167">Description</span></span>|<span data-ttu-id="32745-168">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32745-169">opgegeven limiet</span><span class="sxs-lookup"><span data-stu-id="32745-169">set-limit</span></span>|<span data-ttu-id="32745-170">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="32745-170">Root element.</span></span>|<span data-ttu-id="32745-171">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-171">Yes</span></span>|  
|<span data-ttu-id="32745-172">api</span><span class="sxs-lookup"><span data-stu-id="32745-172">api</span></span>|<span data-ttu-id="32745-173">Een of meer van deze elementen tooimpose een frequentielimiet aanroep op API's binnen Hallo product toevoegen.</span><span class="sxs-lookup"><span data-stu-id="32745-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="32745-174">Producten en -API aanroepen snelheid limieten onafhankelijk worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="32745-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="32745-175">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-175">No</span></span>|  
|<span data-ttu-id="32745-176">bewerking</span><span class="sxs-lookup"><span data-stu-id="32745-176">operation</span></span>|<span data-ttu-id="32745-177">Een of meer van deze elementen tooimpose een frequentielimiet aanroep op bewerkingen binnen een API toevoegen.</span><span class="sxs-lookup"><span data-stu-id="32745-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="32745-178">Product, API en bewerking aanroepen snelheid limieten onafhankelijk worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="32745-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="32745-179">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32745-180">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="32745-180">Attributes</span></span>  
  
|<span data-ttu-id="32745-181">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-181">Name</span></span>|<span data-ttu-id="32745-182">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-182">Description</span></span>|<span data-ttu-id="32745-183">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-183">Required</span></span>|<span data-ttu-id="32745-184">Standaard</span><span class="sxs-lookup"><span data-stu-id="32745-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32745-185">naam</span><span class="sxs-lookup"><span data-stu-id="32745-185">name</span></span>|<span data-ttu-id="32745-186">Hallo de naam van Hallo API voor welke tooapply Hallo limiet.</span><span class="sxs-lookup"><span data-stu-id="32745-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="32745-187">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-187">Yes</span></span>|<span data-ttu-id="32745-188">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-188">N/A</span></span>|  
|<span data-ttu-id="32745-189">aanroepen</span><span class="sxs-lookup"><span data-stu-id="32745-189">calls</span></span>|<span data-ttu-id="32745-190">maximum aantal aanroepen toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="32745-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="32745-191">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-191">Yes</span></span>|<span data-ttu-id="32745-192">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-192">N/A</span></span>|  
|<span data-ttu-id="32745-193">vernieuwingsperiode</span><span class="sxs-lookup"><span data-stu-id="32745-193">renewal-period</span></span>|<span data-ttu-id="32745-194">Hallo periode in seconden waarna hello quotum wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="32745-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="32745-195">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-195">Yes</span></span>|<span data-ttu-id="32745-196">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32745-197">Gebruik</span><span class="sxs-lookup"><span data-stu-id="32745-197">Usage</span></span>  
 <span data-ttu-id="32745-198">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="32745-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32745-199">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="32745-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="32745-200">**Beleid scopes:** product</span><span class="sxs-lookup"><span data-stu-id="32745-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="32745-201"><a name="LimitCallRateByKey"></a>Aanroepfrequentie per sleutel</span><span class="sxs-lookup"><span data-stu-id="32745-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="32745-202">Hallo `rate-limit-by-key` beleid voorkomt dat het gebruik van de API pieken per sleutel op basis van een door het beperken van Hallo aanroepen snelheid tooa opgegeven aantal gedurende een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="32745-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="32745-203">Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="32745-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="32745-204">Optionele incrementele voorwaarde kan worden toegevoegd als toospecify welke aanvragen naar Hallo limiet moeten worden geteld.</span><span class="sxs-lookup"><span data-stu-id="32745-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="32745-205">Wanneer dit beleid wordt geactiveerd Hallo aanroeper ontvangt een `429 Too Many Requests` statuscode van antwoord.</span><span class="sxs-lookup"><span data-stu-id="32745-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="32745-206">Zie voor meer informatie over en voorbeelden van dit beleid, [geavanceerde aanvraagbeperking met Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="32745-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="32745-207">Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="32745-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32745-208">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="32745-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="32745-209">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="32745-209">Example</span></span>  
 <span data-ttu-id="32745-210">In Hallo voorbeeld te volgen, wordt de frequentielimiet Hallo ingevoerd met Hallo aanroeper IP-adres.</span><span class="sxs-lookup"><span data-stu-id="32745-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="32745-211">Elementen</span><span class="sxs-lookup"><span data-stu-id="32745-211">Elements</span></span>  
  
|<span data-ttu-id="32745-212">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-212">Name</span></span>|<span data-ttu-id="32745-213">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-213">Description</span></span>|<span data-ttu-id="32745-214">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32745-215">opgegeven limiet</span><span class="sxs-lookup"><span data-stu-id="32745-215">set-limit</span></span>|<span data-ttu-id="32745-216">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="32745-216">Root element.</span></span>|<span data-ttu-id="32745-217">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32745-218">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="32745-218">Attributes</span></span>  
  
|<span data-ttu-id="32745-219">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-219">Name</span></span>|<span data-ttu-id="32745-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-220">Description</span></span>|<span data-ttu-id="32745-221">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-221">Required</span></span>|<span data-ttu-id="32745-222">Standaard</span><span class="sxs-lookup"><span data-stu-id="32745-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32745-223">aanroepen</span><span class="sxs-lookup"><span data-stu-id="32745-223">calls</span></span>|<span data-ttu-id="32745-224">maximum aantal aanroepen toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="32745-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="32745-225">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-225">Yes</span></span>|<span data-ttu-id="32745-226">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-226">N/A</span></span>|  
|<span data-ttu-id="32745-227">tegenpartij sleutel</span><span class="sxs-lookup"><span data-stu-id="32745-227">counter-key</span></span>|<span data-ttu-id="32745-228">Hallo sleutel toouse voor beleid voor frequentielimiet Hallo.</span><span class="sxs-lookup"><span data-stu-id="32745-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="32745-229">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-229">Yes</span></span>|<span data-ttu-id="32745-230">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-230">N/A</span></span>|  
|<span data-ttu-id="32745-231">verhoging voorwaarde</span><span class="sxs-lookup"><span data-stu-id="32745-231">increment-condition</span></span>|<span data-ttu-id="32745-232">Hallo Booleaanse expressie opgeven als Hallo-aanvraag moet worden geteld voor Hallo quotum (`true`).</span><span class="sxs-lookup"><span data-stu-id="32745-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="32745-233">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-233">No</span></span>|<span data-ttu-id="32745-234">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-234">N/A</span></span>|  
|<span data-ttu-id="32745-235">vernieuwingsperiode</span><span class="sxs-lookup"><span data-stu-id="32745-235">renewal-period</span></span>|<span data-ttu-id="32745-236">Hallo periode in seconden waarna hello quotum wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="32745-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="32745-237">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-237">Yes</span></span>|<span data-ttu-id="32745-238">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32745-239">Gebruik</span><span class="sxs-lookup"><span data-stu-id="32745-239">Usage</span></span>  
 <span data-ttu-id="32745-240">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="32745-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32745-241">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="32745-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="32745-242">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="32745-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="32745-243"><a name="RestrictCallerIPs"></a>Aanroeper IP-adressen beperken</span><span class="sxs-lookup"><span data-stu-id="32745-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="32745-244">Hallo `ip-filter` beleid filtert (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="32745-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32745-245">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="32745-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="32745-246">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="32745-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="32745-247">Elementen</span><span class="sxs-lookup"><span data-stu-id="32745-247">Elements</span></span>  
  
|<span data-ttu-id="32745-248">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-248">Name</span></span>|<span data-ttu-id="32745-249">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-249">Description</span></span>|<span data-ttu-id="32745-250">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32745-251">IP-filter</span><span class="sxs-lookup"><span data-stu-id="32745-251">ip-filter</span></span>|<span data-ttu-id="32745-252">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="32745-252">Root element.</span></span>|<span data-ttu-id="32745-253">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-253">Yes</span></span>|  
|<span data-ttu-id="32745-254">Adres</span><span class="sxs-lookup"><span data-stu-id="32745-254">address</span></span>|<span data-ttu-id="32745-255">Hiermee geeft u één IP-adres op welke toofilter.</span><span class="sxs-lookup"><span data-stu-id="32745-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="32745-256">Ten minste één `address` of `address-range` element is vereist.</span><span class="sxs-lookup"><span data-stu-id="32745-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="32745-257">adresbereik van = 'adres' naar 'adres' =</span><span class="sxs-lookup"><span data-stu-id="32745-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="32745-258">Hiermee geeft u een bereik met IP-adres op welke toofilter.</span><span class="sxs-lookup"><span data-stu-id="32745-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="32745-259">Ten minste één `address` of `address-range` element is vereist.</span><span class="sxs-lookup"><span data-stu-id="32745-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32745-260">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="32745-260">Attributes</span></span>  
  
|<span data-ttu-id="32745-261">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-261">Name</span></span>|<span data-ttu-id="32745-262">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-262">Description</span></span>|<span data-ttu-id="32745-263">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-263">Required</span></span>|<span data-ttu-id="32745-264">Standaard</span><span class="sxs-lookup"><span data-stu-id="32745-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32745-265">adresbereik van = 'adres' naar 'adres' =</span><span class="sxs-lookup"><span data-stu-id="32745-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="32745-266">Een bereik met IP-adressen tooallow of weigeren van toegang voor.</span><span class="sxs-lookup"><span data-stu-id="32745-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="32745-267">Vereist wanneer hello `address-range` element wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="32745-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="32745-268">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-268">N/A</span></span>|  
|<span data-ttu-id="32745-269">IP-filteractie = ' toestaan dat &#124; verbieden"</span><span class="sxs-lookup"><span data-stu-id="32745-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="32745-270">Geeft aan of aanroepen moeten worden toegestaan of niet voor Hallo IP-adressen en -bereiken opgegeven.</span><span class="sxs-lookup"><span data-stu-id="32745-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="32745-271">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-271">Yes</span></span>|<span data-ttu-id="32745-272">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32745-273">Gebruik</span><span class="sxs-lookup"><span data-stu-id="32745-273">Usage</span></span>  
 <span data-ttu-id="32745-274">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="32745-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32745-275">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="32745-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="32745-276">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="32745-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="32745-277"><a name="SetUsageQuota"></a>Gebruiksquotum per abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="32745-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="32745-278">Hallo `quota` beleid zorgt ervoor dat een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van per abonnement.</span><span class="sxs-lookup"><span data-stu-id="32745-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="32745-279">Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="32745-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="32745-280">[Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van Hallo-beleid voor dit beleid.</span><span class="sxs-lookup"><span data-stu-id="32745-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32745-281">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="32745-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="32745-282">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="32745-282">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="32745-283">Elementen</span><span class="sxs-lookup"><span data-stu-id="32745-283">Elements</span></span>  
  
|<span data-ttu-id="32745-284">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-284">Name</span></span>|<span data-ttu-id="32745-285">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-285">Description</span></span>|<span data-ttu-id="32745-286">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32745-287">quotum</span><span class="sxs-lookup"><span data-stu-id="32745-287">quota</span></span>|<span data-ttu-id="32745-288">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="32745-288">Root element.</span></span>|<span data-ttu-id="32745-289">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-289">Yes</span></span>|  
|<span data-ttu-id="32745-290">api</span><span class="sxs-lookup"><span data-stu-id="32745-290">api</span></span>|<span data-ttu-id="32745-291">Een of meer van deze elementen tooimpose een quotum op API's binnen Hallo product toevoegen.</span><span class="sxs-lookup"><span data-stu-id="32745-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="32745-292">Product- en API-quota worden onafhankelijk toegepast.</span><span class="sxs-lookup"><span data-stu-id="32745-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="32745-293">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-293">No</span></span>|  
|<span data-ttu-id="32745-294">bewerking</span><span class="sxs-lookup"><span data-stu-id="32745-294">operation</span></span>|<span data-ttu-id="32745-295">Een of meer van deze elementen tooimpose een quotum op bewerkingen binnen een API toevoegen.</span><span class="sxs-lookup"><span data-stu-id="32745-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="32745-296">Product, API en bewerking quota's worden onafhankelijk van elkaar toegepast.</span><span class="sxs-lookup"><span data-stu-id="32745-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="32745-297">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32745-298">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="32745-298">Attributes</span></span>  
  
|<span data-ttu-id="32745-299">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-299">Name</span></span>|<span data-ttu-id="32745-300">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-300">Description</span></span>|<span data-ttu-id="32745-301">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-301">Required</span></span>|<span data-ttu-id="32745-302">Standaard</span><span class="sxs-lookup"><span data-stu-id="32745-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32745-303">naam</span><span class="sxs-lookup"><span data-stu-id="32745-303">name</span></span>|<span data-ttu-id="32745-304">Hallo-naam van het Hallo-API of de bewerking voor welke Hallo quotum van toepassing.</span><span class="sxs-lookup"><span data-stu-id="32745-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="32745-305">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-305">Yes</span></span>|<span data-ttu-id="32745-306">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-306">N/A</span></span>|  
|<span data-ttu-id="32745-307">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="32745-307">bandwidth</span></span>|<span data-ttu-id="32745-308">maximum aantal kilobytes is toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="32745-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="32745-309">Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="32745-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="32745-310">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-310">N/A</span></span>|  
|<span data-ttu-id="32745-311">aanroepen</span><span class="sxs-lookup"><span data-stu-id="32745-311">calls</span></span>|<span data-ttu-id="32745-312">maximum aantal aanroepen toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="32745-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="32745-313">Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="32745-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="32745-314">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-314">N/A</span></span>|  
|<span data-ttu-id="32745-315">vernieuwingsperiode</span><span class="sxs-lookup"><span data-stu-id="32745-315">renewal-period</span></span>|<span data-ttu-id="32745-316">Hallo periode in seconden waarna hello quotum wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="32745-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="32745-317">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-317">Yes</span></span>|<span data-ttu-id="32745-318">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32745-319">Gebruik</span><span class="sxs-lookup"><span data-stu-id="32745-319">Usage</span></span>  
 <span data-ttu-id="32745-320">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="32745-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32745-321">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="32745-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="32745-322">**Beleid scopes:** product</span><span class="sxs-lookup"><span data-stu-id="32745-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="32745-323"><a name="SetUsageQuotaByKey"></a>Gebruiksquotum instellen door sleutel</span><span class="sxs-lookup"><span data-stu-id="32745-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="32745-324">Hallo `quota-by-key` beleid zorgt ervoor dat een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van de per-sleutel.</span><span class="sxs-lookup"><span data-stu-id="32745-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="32745-325">Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="32745-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="32745-326">Optionele incrementele voorwaarde kan worden toegevoegd als toospecify welke aanvragen naar Hallo quotum moeten worden geteld.</span><span class="sxs-lookup"><span data-stu-id="32745-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="32745-327">Zie voor meer informatie over en voorbeelden van dit beleid, [geavanceerde aanvraagbeperking met Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="32745-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="32745-328">Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="32745-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="32745-329">[Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van Hallo-beleid voor dit beleid.</span><span class="sxs-lookup"><span data-stu-id="32745-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32745-330">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="32745-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="32745-331">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="32745-331">Example</span></span>  
 <span data-ttu-id="32745-332">In Hallo voorbeeld te volgen, wordt de Hallo quotum ingevoerd met Hallo aanroeper IP-adres.</span><span class="sxs-lookup"><span data-stu-id="32745-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="32745-333">Elementen</span><span class="sxs-lookup"><span data-stu-id="32745-333">Elements</span></span>  
  
|<span data-ttu-id="32745-334">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-334">Name</span></span>|<span data-ttu-id="32745-335">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-335">Description</span></span>|<span data-ttu-id="32745-336">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32745-337">quotum</span><span class="sxs-lookup"><span data-stu-id="32745-337">quota</span></span>|<span data-ttu-id="32745-338">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="32745-338">Root element.</span></span>|<span data-ttu-id="32745-339">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32745-340">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="32745-340">Attributes</span></span>  
  
|<span data-ttu-id="32745-341">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-341">Name</span></span>|<span data-ttu-id="32745-342">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-342">Description</span></span>|<span data-ttu-id="32745-343">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-343">Required</span></span>|<span data-ttu-id="32745-344">Standaard</span><span class="sxs-lookup"><span data-stu-id="32745-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32745-345">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="32745-345">bandwidth</span></span>|<span data-ttu-id="32745-346">maximum aantal kilobytes is toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="32745-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="32745-347">Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="32745-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="32745-348">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-348">N/A</span></span>|  
|<span data-ttu-id="32745-349">aanroepen</span><span class="sxs-lookup"><span data-stu-id="32745-349">calls</span></span>|<span data-ttu-id="32745-350">maximum aantal aanroepen toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="32745-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="32745-351">Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="32745-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="32745-352">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-352">N/A</span></span>|  
|<span data-ttu-id="32745-353">tegenpartij sleutel</span><span class="sxs-lookup"><span data-stu-id="32745-353">counter-key</span></span>|<span data-ttu-id="32745-354">Hallo sleutel toouse voor Hallo quotumbeleid.</span><span class="sxs-lookup"><span data-stu-id="32745-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="32745-355">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-355">Yes</span></span>|<span data-ttu-id="32745-356">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-356">N/A</span></span>|  
|<span data-ttu-id="32745-357">verhoging voorwaarde</span><span class="sxs-lookup"><span data-stu-id="32745-357">increment-condition</span></span>|<span data-ttu-id="32745-358">Hallo Booleaanse expressie opgeven als Hallo-aanvraag moet worden geteld voor Hallo quotum (`true`)</span><span class="sxs-lookup"><span data-stu-id="32745-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="32745-359">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-359">No</span></span>|<span data-ttu-id="32745-360">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-360">N/A</span></span>|  
|<span data-ttu-id="32745-361">vernieuwingsperiode</span><span class="sxs-lookup"><span data-stu-id="32745-361">renewal-period</span></span>|<span data-ttu-id="32745-362">Hallo periode in seconden waarna hello quotum wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="32745-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="32745-363">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-363">Yes</span></span>|<span data-ttu-id="32745-364">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32745-365">Gebruik</span><span class="sxs-lookup"><span data-stu-id="32745-365">Usage</span></span>  
 <span data-ttu-id="32745-366">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="32745-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32745-367">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="32745-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="32745-368">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="32745-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="32745-369"><a name="ValidateJWT"></a>JWT valideren</span><span class="sxs-lookup"><span data-stu-id="32745-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="32745-370">Hallo `validate-jwt` beleid zorgt ervoor dat bestaan en de geldigheid van een JWT opgehaald uit beide een opgegeven HTTP-Header of een opgegeven queryparameter.</span><span class="sxs-lookup"><span data-stu-id="32745-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="32745-371">Hallo `validate-jwt` beleid vereist dat Hallo `exp` geregistreerde claim is inlcuded in Hallo JWT-token, tenzij `require-expiration-time` kenmerk is opgegeven en ingesteld te`false`.</span><span class="sxs-lookup"><span data-stu-id="32745-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="32745-372">Hallo `validate-jwt` beleid ondersteunt HS256 en RS256 ondertekenen algoritmen.</span><span class="sxs-lookup"><span data-stu-id="32745-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="32745-373">HS256 moet Hallo-sleutel worden opgegeven voor inline binnen Hallo beleid Hallo base64-gecodeerde vorm.</span><span class="sxs-lookup"><span data-stu-id="32745-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="32745-374">Hallo-sleutel heeft voor RS256 toobe bieden via een Open ID configuratie-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="32745-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32745-375">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="32745-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="32745-376">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="32745-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="32745-377">Validatie van Azure Mobile Services-tokens</span><span class="sxs-lookup"><span data-stu-id="32745-377">Azure Mobile Services token validation</span></span>  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="32745-378">Validatie van Azure Active Directory-tokens</span><span class="sxs-lookup"><span data-stu-id="32745-378">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="32745-379">Validatie van Azure Active Directory B2C-tokens</span><span class="sxs-lookup"><span data-stu-id="32745-379">Azure Active Directory B2C token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="32745-380">Toegang toooperations op basis van claims token autoriseren</span><span class="sxs-lookup"><span data-stu-id="32745-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="32745-381">Dit voorbeeld ziet u hoe toouse hello [JWT valideren](api-management-access-restriction-policies.md#ValidateJWT) beleid toopre-toegang toooperations op basis van claims token autoriseren.</span><span class="sxs-lookup"><span data-stu-id="32745-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="32745-382">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too13:50 vooruit.</span><span class="sxs-lookup"><span data-stu-id="32745-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="32745-383">Snel toosee Hallo beleid dat is geconfigureerd in de beleidseditor Hallo doorsturen too15:00 en vervolgens too18:50 voor een demonstratie van een bewerking aanroepen vanuit de ontwikkelaarsportal Hallo zowel met als zonder Hallo verificatietoken vereist.</span><span class="sxs-lookup"><span data-stu-id="32745-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="32745-384">Elementen</span><span class="sxs-lookup"><span data-stu-id="32745-384">Elements</span></span>  
  
|<span data-ttu-id="32745-385">Element</span><span class="sxs-lookup"><span data-stu-id="32745-385">Element</span></span>|<span data-ttu-id="32745-386">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-386">Description</span></span>|<span data-ttu-id="32745-387">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="32745-388">valideren jwt</span><span class="sxs-lookup"><span data-stu-id="32745-388">validate-jwt</span></span>|<span data-ttu-id="32745-389">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="32745-389">Root element.</span></span>|<span data-ttu-id="32745-390">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-390">Yes</span></span>|  
|<span data-ttu-id="32745-391">doelgroepen</span><span class="sxs-lookup"><span data-stu-id="32745-391">audiences</span></span>|<span data-ttu-id="32745-392">Bevat een lijst met toegestane doelgroep claims die gebruikt op Hallo-token worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="32745-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="32745-393">Als meerdere doelgroep waarden aanwezig zijn, wordt elke waarde wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt.</span><span class="sxs-lookup"><span data-stu-id="32745-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="32745-394">Ten minste één doelgroep moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="32745-394">At least one audience must be specified.</span></span>|<span data-ttu-id="32745-395">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-395">No</span></span>|  
|<span data-ttu-id="32745-396">ondertekening-sleutels van uitgever</span><span class="sxs-lookup"><span data-stu-id="32745-396">issuer-signing-keys</span></span>|<span data-ttu-id="32745-397">Een lijst met Base64-gecodeerd beveiliging sleutels die worden gebruikt toovalidate ondertekend tokens.</span><span class="sxs-lookup"><span data-stu-id="32745-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="32745-398">Als meerdere beveiligingssleutels aanwezig zijn, wordt elke sleutel wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt (dit is nuttig voor de overschakeling van token).</span><span class="sxs-lookup"><span data-stu-id="32745-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="32745-399">De belangrijkste elementen hebben een optioneel `id` toomatch kenmerk gebruikt tegen `kid` claim.</span><span class="sxs-lookup"><span data-stu-id="32745-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="32745-400">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-400">No</span></span>|  
|<span data-ttu-id="32745-401">uitgevers van certificaten</span><span class="sxs-lookup"><span data-stu-id="32745-401">issuers</span></span>|<span data-ttu-id="32745-402">Een lijst met toegestane principals die Hallo token uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="32745-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="32745-403">Als meerdere verlener waarden aanwezig zijn, wordt elke waarde wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt.</span><span class="sxs-lookup"><span data-stu-id="32745-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="32745-404">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-404">No</span></span>|  
|<span data-ttu-id="32745-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="32745-405">openid-config</span></span>|<span data-ttu-id="32745-406">Hallo-element dat wordt gebruikt voor het opgeven van een compatibele configuratie-eindpunt voor Open-ID is waar ondertekenen van sleutels en uitgever kan worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="32745-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="32745-407">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-407">No</span></span>|  
|<span data-ttu-id="32745-408">vereist claims</span><span class="sxs-lookup"><span data-stu-id="32745-408">required-claims</span></span>|<span data-ttu-id="32745-409">Bevat een lijst met claims verwacht toobe aanwezig is op Hallo token voor toobe als geldig beschouwd.</span><span class="sxs-lookup"><span data-stu-id="32745-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="32745-410">Wanneer Hallo `match` kenmerk is ingesteld, te`all` elke claimwaarde in Hallo beleid moet aanwezig zijn in Hallo token voor validatie toosucceed.</span><span class="sxs-lookup"><span data-stu-id="32745-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="32745-411">Wanneer Hallo `match` kenmerk is ingesteld, te`any` ten minste één claim moet aanwezig zijn in Hallo token voor validatie toosucceed.</span><span class="sxs-lookup"><span data-stu-id="32745-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="32745-412">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-412">No</span></span>|  
|<span data-ttu-id="32745-413">zumo hoofdsleutel</span><span class="sxs-lookup"><span data-stu-id="32745-413">zumo-master-key</span></span>|<span data-ttu-id="32745-414">Hoofdsleutel voor tokens die zijn uitgegeven door Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="32745-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="32745-415">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32745-416">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="32745-416">Attributes</span></span>  
  
|<span data-ttu-id="32745-417">Naam</span><span class="sxs-lookup"><span data-stu-id="32745-417">Name</span></span>|<span data-ttu-id="32745-418">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32745-418">Description</span></span>|<span data-ttu-id="32745-419">Vereist</span><span class="sxs-lookup"><span data-stu-id="32745-419">Required</span></span>|<span data-ttu-id="32745-420">Standaard</span><span class="sxs-lookup"><span data-stu-id="32745-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32745-421">tijdverschil</span><span class="sxs-lookup"><span data-stu-id="32745-421">clock-skew</span></span>|<span data-ttu-id="32745-422">TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="32745-422">Timespan.</span></span> <span data-ttu-id="32745-423">Biedt een aantal kleine eenheidsprofiel geval Hallo-token verloopt claim aanwezig in het Hallo-token is en na de huidige Hallo valt datum / tijd.</span><span class="sxs-lookup"><span data-stu-id="32745-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="32745-424">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-424">No</span></span>|<span data-ttu-id="32745-425">0 seconden</span><span class="sxs-lookup"><span data-stu-id="32745-425">0 seconds</span></span>|  
|<span data-ttu-id="32745-426">kan de niet-validatie-foutbericht</span><span class="sxs-lookup"><span data-stu-id="32745-426">failed-validation-error-message</span></span>|<span data-ttu-id="32745-427">Fout bericht tooreturn in Hallo HTTP-antwoordtekst als Hallo JWT niet kan gevalideerd worden.</span><span class="sxs-lookup"><span data-stu-id="32745-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="32745-428">Dit bericht moet de speciale tekens escape hebben.</span><span class="sxs-lookup"><span data-stu-id="32745-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="32745-429">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-429">No</span></span>|<span data-ttu-id="32745-430">Standaardfoutbericht, is afhankelijk van validatieprobleem, bijvoorbeeld 'JWT niet aanwezig."</span><span class="sxs-lookup"><span data-stu-id="32745-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="32745-431">kan geen validatie httpcode</span><span class="sxs-lookup"><span data-stu-id="32745-431">failed-validation-httpcode</span></span>|<span data-ttu-id="32745-432">HTTP-Status code tooreturn als Hallo JWT validatie niet doorstaan.</span><span class="sxs-lookup"><span data-stu-id="32745-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="32745-433">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-433">No</span></span>|<span data-ttu-id="32745-434">401</span><span class="sxs-lookup"><span data-stu-id="32745-434">401</span></span>|  
|<span data-ttu-id="32745-435">header-naam</span><span class="sxs-lookup"><span data-stu-id="32745-435">header-name</span></span>|<span data-ttu-id="32745-436">Hallo-naam van Hallo HTTP-header Hallo-token bedrijf.</span><span class="sxs-lookup"><span data-stu-id="32745-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="32745-437">Ofwel `header-name` of `query-paremeter-name` moet worden opgegeven, maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="32745-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="32745-438">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-438">N/A</span></span>|  
|<span data-ttu-id="32745-439">id</span><span class="sxs-lookup"><span data-stu-id="32745-439">id</span></span>|<span data-ttu-id="32745-440">Hallo `id` -kenmerk op Hallo `key` element kunt u toospecify Hallo tekenreeks die wordt vergeleken met `kid` claim in Hallo token (indien aanwezig) toofind uit Hallo geschikte sleutel toouse voor validatie van handtekening.</span><span class="sxs-lookup"><span data-stu-id="32745-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="32745-441">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-441">No</span></span>|<span data-ttu-id="32745-442">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-442">N/A</span></span>|  
|<span data-ttu-id="32745-443">Overeenkomst</span><span class="sxs-lookup"><span data-stu-id="32745-443">match</span></span>|<span data-ttu-id="32745-444">Hallo `match` -kenmerk op Hallo `claim` element geeft aan of de waarde van elke claim in Hallo beleid aanwezig in Hallo token voor validatie toosucceed zijn moet.</span><span class="sxs-lookup"><span data-stu-id="32745-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="32745-445">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="32745-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="32745-446">-                          `all`-de waarde van elke claim in Hallo beleid moet aanwezig zijn in Hallo token voor validatie toosucceed.</span><span class="sxs-lookup"><span data-stu-id="32745-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="32745-447">-                          `any`-ten minste één claimwaarde moet aanwezig zijn in Hallo token voor validatie toosucceed.</span><span class="sxs-lookup"><span data-stu-id="32745-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="32745-448">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-448">No</span></span>|<span data-ttu-id="32745-449">Alle</span><span class="sxs-lookup"><span data-stu-id="32745-449">all</span></span>|  
|<span data-ttu-id="32745-450">query-paremeter-naam</span><span class="sxs-lookup"><span data-stu-id="32745-450">query-paremeter-name</span></span>|<span data-ttu-id="32745-451">Hallo-naam van de queryparameter voor Hallo HALLO hallo-token bedrijf.</span><span class="sxs-lookup"><span data-stu-id="32745-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="32745-452">Ofwel `header-name` of `query-paremeter-name` moet worden opgegeven, maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="32745-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="32745-453">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-453">N/A</span></span>|  
|<span data-ttu-id="32745-454">vereisen verlooptijd vallen</span><span class="sxs-lookup"><span data-stu-id="32745-454">require-expiration-time</span></span>|<span data-ttu-id="32745-455">Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="32745-455">Boolean.</span></span> <span data-ttu-id="32745-456">Hiermee geeft u op of een claim vervaldatum in Hallo-token is vereist.</span><span class="sxs-lookup"><span data-stu-id="32745-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="32745-457">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-457">No</span></span>|<span data-ttu-id="32745-458">De waarde True</span><span class="sxs-lookup"><span data-stu-id="32745-458">true</span></span>|
|<span data-ttu-id="32745-459">vereisen schema</span><span class="sxs-lookup"><span data-stu-id="32745-459">require-scheme</span></span>|<span data-ttu-id="32745-460">naam van het token Hallo-schema, bijvoorbeeld Hallo 'Bearer'.</span><span class="sxs-lookup"><span data-stu-id="32745-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="32745-461">Wanneer dit kenmerk is ingesteld, kan Hallo beleid zorgt ervoor dat het schema is aanwezig in Hallo autorisatie-header-waarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="32745-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="32745-462">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-462">No</span></span>|<span data-ttu-id="32745-463">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-463">N/A</span></span>|
|<span data-ttu-id="32745-464">vereisen ondertekend-tokens</span><span class="sxs-lookup"><span data-stu-id="32745-464">require-signed-tokens</span></span>|<span data-ttu-id="32745-465">Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="32745-465">Boolean.</span></span> <span data-ttu-id="32745-466">Geeft aan of een token vereist toobe ondertekend.</span><span class="sxs-lookup"><span data-stu-id="32745-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="32745-467">Nee</span><span class="sxs-lookup"><span data-stu-id="32745-467">No</span></span>|<span data-ttu-id="32745-468">De waarde True</span><span class="sxs-lookup"><span data-stu-id="32745-468">true</span></span>|  
|<span data-ttu-id="32745-469">URL</span><span class="sxs-lookup"><span data-stu-id="32745-469">url</span></span>|<span data-ttu-id="32745-470">Open ID configuratie eindpunt-URL op waar de metagegevens van de Open-ID-configuratie kan worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="32745-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="32745-471">Voor Azure Active Directory gebruiken Hallo volgende URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` waarbij u de naam van uw directory-tenant, bijvoorbeeld vervangt `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="32745-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="32745-472">Ja</span><span class="sxs-lookup"><span data-stu-id="32745-472">Yes</span></span>|<span data-ttu-id="32745-473">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="32745-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32745-474">Gebruik</span><span class="sxs-lookup"><span data-stu-id="32745-474">Usage</span></span>  
 <span data-ttu-id="32745-475">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="32745-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32745-476">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="32745-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="32745-477">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="32745-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="32745-478">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32745-478">Next steps</span></span>
<span data-ttu-id="32745-479">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="32745-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
