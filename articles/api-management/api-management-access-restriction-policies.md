---
title: Azure API Management-beperking beleid | Microsoft Docs
description: Meer informatie over de beperking toegangsbeleid beschikbaar voor gebruik in Azure API Management.
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
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="72485-103">Beperking van API Management toegangsbeleid</span><span class="sxs-lookup"><span data-stu-id="72485-103">API Management access restriction policies</span></span>
<span data-ttu-id="72485-104">Dit onderwerp bevat een verwijzing voor de volgende API Management-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="72485-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="72485-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="72485-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="72485-106"><a name="AccessRestrictionPolicies"></a>Softwarerestrictiebeleid toegang</span><span class="sxs-lookup"><span data-stu-id="72485-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="72485-107">[Controle van HTTP-header](api-management-access-restriction-policies.md#CheckHTTPHeader) -afdwingt bestaan en/of de waarde van een HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="72485-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="72485-108">[Aanroepfrequentie per abonnement](api-management-access-restriction-policies.md#LimitCallRate) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per abonnement op basis van een.</span><span class="sxs-lookup"><span data-stu-id="72485-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="72485-109">[Aanroepfrequentie per sleutel](#LimitCallRateByKey) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per sleutel op basis van een.</span><span class="sxs-lookup"><span data-stu-id="72485-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="72485-110">[Aanroeper IP-adressen beperken](api-management-access-restriction-policies.md#RestrictCallerIPs) -Filters (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="72485-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="72485-111">[Gebruiksquotum per abonnement instellen](api-management-access-restriction-policies.md#SetUsageQuota) -Hiermee kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van per abonnement afdwingen.</span><span class="sxs-lookup"><span data-stu-id="72485-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="72485-112">[Gebruiksquotum instellen door sleutel](#SetUsageQuotaByKey) -Hiermee kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van de sleutel per afdwingen.</span><span class="sxs-lookup"><span data-stu-id="72485-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="72485-113">[Valideren van JWT](api-management-access-restriction-policies.md#ValidateJWT) -afdwingt bestaan en de geldigheid van een JWT opgehaald uit een opgegeven HTTP-koptekst of een opgegeven queryparameter.</span><span class="sxs-lookup"><span data-stu-id="72485-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="72485-114"><a name="CheckHTTPHeader"></a>Controleer de HTTP-header</span><span class="sxs-lookup"><span data-stu-id="72485-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="72485-115">Gebruik de `check-header` beleid af te dwingen dat een aanvraag een opgegeven HTTP-header heeft.</span><span class="sxs-lookup"><span data-stu-id="72485-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="72485-116">U kunt eventueel controleren of de header is een specifieke waarde of het selectievakje voor een bereik van toegestane waarden.</span><span class="sxs-lookup"><span data-stu-id="72485-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="72485-117">Als de controle mislukt, wordt het beleid wordt beëindigd aanvraagverwerking en retourneert het HTTP-status code en de fout bericht opgegeven door het beleid.</span><span class="sxs-lookup"><span data-stu-id="72485-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72485-118">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="72485-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="72485-119">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72485-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="72485-120">Elementen</span><span class="sxs-lookup"><span data-stu-id="72485-120">Elements</span></span>  
  
|<span data-ttu-id="72485-121">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-121">Name</span></span>|<span data-ttu-id="72485-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-122">Description</span></span>|<span data-ttu-id="72485-123">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="72485-124">controle-header</span><span class="sxs-lookup"><span data-stu-id="72485-124">check-header</span></span>|<span data-ttu-id="72485-125">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="72485-125">Root element.</span></span>|<span data-ttu-id="72485-126">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-126">Yes</span></span>|  
|<span data-ttu-id="72485-127">waarde</span><span class="sxs-lookup"><span data-stu-id="72485-127">value</span></span>|<span data-ttu-id="72485-128">Toegestane waarde voor HTTP-header.</span><span class="sxs-lookup"><span data-stu-id="72485-128">Allowed HTTP header value.</span></span> <span data-ttu-id="72485-129">Als meerdere elementen van de waarde worden opgegeven, de controle wordt beschouwd als geslaagd als een van de waarden een overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="72485-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="72485-130">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72485-131">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="72485-131">Attributes</span></span>  
  
|<span data-ttu-id="72485-132">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-132">Name</span></span>|<span data-ttu-id="72485-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-133">Description</span></span>|<span data-ttu-id="72485-134">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-134">Required</span></span>|<span data-ttu-id="72485-135">Standaard</span><span class="sxs-lookup"><span data-stu-id="72485-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="72485-136">kan de niet-controle-foutbericht</span><span class="sxs-lookup"><span data-stu-id="72485-136">failed-check-error-message</span></span>|<span data-ttu-id="72485-137">Het foutbericht te retourneren in de HTTP-antwoordtekst als de header bestaat niet of een ongeldige waarde heeft.</span><span class="sxs-lookup"><span data-stu-id="72485-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="72485-138">Dit bericht moet de speciale tekens escape hebben.</span><span class="sxs-lookup"><span data-stu-id="72485-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="72485-139">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-139">Yes</span></span>|<span data-ttu-id="72485-140">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-140">N/A</span></span>|  
|<span data-ttu-id="72485-141">Kan controle httpcode</span><span class="sxs-lookup"><span data-stu-id="72485-141">failed-check-httpcode</span></span>|<span data-ttu-id="72485-142">HTTP-statuscode te retourneren als de header bestaat niet of een ongeldige waarde heeft.</span><span class="sxs-lookup"><span data-stu-id="72485-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="72485-143">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-143">Yes</span></span>|<span data-ttu-id="72485-144">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-144">N/A</span></span>|  
|<span data-ttu-id="72485-145">header-naam</span><span class="sxs-lookup"><span data-stu-id="72485-145">header-name</span></span>|<span data-ttu-id="72485-146">De naam van de HTTP-Header om te controleren.</span><span class="sxs-lookup"><span data-stu-id="72485-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="72485-147">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-147">Yes</span></span>|<span data-ttu-id="72485-148">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-148">N/A</span></span>|  
|<span data-ttu-id="72485-149">negeren geval</span><span class="sxs-lookup"><span data-stu-id="72485-149">ignore-case</span></span>|<span data-ttu-id="72485-150">Kan worden ingesteld op True of False.</span><span class="sxs-lookup"><span data-stu-id="72485-150">Can be set to True or False.</span></span> <span data-ttu-id="72485-151">Als is ingesteld op True aanvraag wordt genegeerd wanneer de waarde voor header met de set van acceptabele waarden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="72485-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="72485-152">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-152">Yes</span></span>|<span data-ttu-id="72485-153">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72485-154">Gebruik</span><span class="sxs-lookup"><span data-stu-id="72485-154">Usage</span></span>  
 <span data-ttu-id="72485-155">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72485-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72485-156">**Beleid secties:** binnenkomende, uitgaande</span><span class="sxs-lookup"><span data-stu-id="72485-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="72485-157">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="72485-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="72485-158"><a name="LimitCallRate"></a>Aanroepfrequentie per abonnement</span><span class="sxs-lookup"><span data-stu-id="72485-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="72485-159">De `rate-limit` API gebruikspieken op basis van per abonnement wordt verhinderd door het beperken van de aanroepfrequentie met een opgegeven aantal gedurende een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="72485-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="72485-160">Wanneer dit beleid wordt geactiveerd. de aanroeper ontvangt een `429 Too Many Requests` statuscode van antwoord.</span><span class="sxs-lookup"><span data-stu-id="72485-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="72485-161">Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="72485-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="72485-162">[Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van het beleid voor dit beleid.</span><span class="sxs-lookup"><span data-stu-id="72485-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72485-163">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="72485-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="72485-164">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72485-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="72485-165">Elementen</span><span class="sxs-lookup"><span data-stu-id="72485-165">Elements</span></span>  
  
|<span data-ttu-id="72485-166">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-166">Name</span></span>|<span data-ttu-id="72485-167">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-167">Description</span></span>|<span data-ttu-id="72485-168">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="72485-169">opgegeven limiet</span><span class="sxs-lookup"><span data-stu-id="72485-169">set-limit</span></span>|<span data-ttu-id="72485-170">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="72485-170">Root element.</span></span>|<span data-ttu-id="72485-171">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-171">Yes</span></span>|  
|<span data-ttu-id="72485-172">api</span><span class="sxs-lookup"><span data-stu-id="72485-172">api</span></span>|<span data-ttu-id="72485-173">Voeg een of meer van deze elementen te leggen frequentielimiet aanroep op API's binnen het product.</span><span class="sxs-lookup"><span data-stu-id="72485-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="72485-174">Producten en -API aanroepen snelheid limieten onafhankelijk worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="72485-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="72485-175">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-175">No</span></span>|  
|<span data-ttu-id="72485-176">bewerking</span><span class="sxs-lookup"><span data-stu-id="72485-176">operation</span></span>|<span data-ttu-id="72485-177">Een of meer van deze elementen te leggen van de frequentielimiet van een aanroep op bewerkingen binnen een API toevoegen.</span><span class="sxs-lookup"><span data-stu-id="72485-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="72485-178">Product, API en bewerking aanroepen snelheid limieten onafhankelijk worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="72485-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="72485-179">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72485-180">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="72485-180">Attributes</span></span>  
  
|<span data-ttu-id="72485-181">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-181">Name</span></span>|<span data-ttu-id="72485-182">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-182">Description</span></span>|<span data-ttu-id="72485-183">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-183">Required</span></span>|<span data-ttu-id="72485-184">Standaard</span><span class="sxs-lookup"><span data-stu-id="72485-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="72485-185">naam</span><span class="sxs-lookup"><span data-stu-id="72485-185">name</span></span>|<span data-ttu-id="72485-186">De naam van de API voor de frequentielimiet wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="72485-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="72485-187">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-187">Yes</span></span>|<span data-ttu-id="72485-188">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-188">N/A</span></span>|  
|<span data-ttu-id="72485-189">aanroepen</span><span class="sxs-lookup"><span data-stu-id="72485-189">calls</span></span>|<span data-ttu-id="72485-190">Het maximum aantal aanroepen toegestaan tijdens het tijdsinterval die is opgegeven in de `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="72485-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="72485-191">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-191">Yes</span></span>|<span data-ttu-id="72485-192">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-192">N/A</span></span>|  
|<span data-ttu-id="72485-193">vernieuwingsperiode</span><span class="sxs-lookup"><span data-stu-id="72485-193">renewal-period</span></span>|<span data-ttu-id="72485-194">De tijd in seconden waarna het quotum wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="72485-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="72485-195">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-195">Yes</span></span>|<span data-ttu-id="72485-196">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72485-197">Gebruik</span><span class="sxs-lookup"><span data-stu-id="72485-197">Usage</span></span>  
 <span data-ttu-id="72485-198">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72485-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72485-199">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="72485-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="72485-200">**Beleid scopes:** product</span><span class="sxs-lookup"><span data-stu-id="72485-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="72485-201"><a name="LimitCallRateByKey"></a>Aanroepfrequentie per sleutel</span><span class="sxs-lookup"><span data-stu-id="72485-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="72485-202">De `rate-limit-by-key` API gebruikspieken op basis van de sleutel per wordt verhinderd door het beperken van de aanroepfrequentie met een opgegeven aantal gedurende een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="72485-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="72485-203">De sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="72485-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="72485-204">Optionele incrementele voorwaarde kan worden toegevoegd om op te geven welke aanvragen naar de limiet moeten worden geteld.</span><span class="sxs-lookup"><span data-stu-id="72485-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="72485-205">Wanneer dit beleid wordt geactiveerd. de aanroeper ontvangt een `429 Too Many Requests` statuscode van antwoord.</span><span class="sxs-lookup"><span data-stu-id="72485-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="72485-206">Zie voor meer informatie over en voorbeelden van dit beleid, [geavanceerde aanvraagbeperking met Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="72485-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="72485-207">Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="72485-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72485-208">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="72485-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="72485-209">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72485-209">Example</span></span>  
 <span data-ttu-id="72485-210">In het volgende voorbeeld wordt de frequentielimiet ingevoerd door de aanroeper IP-adres.</span><span class="sxs-lookup"><span data-stu-id="72485-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="72485-211">Elementen</span><span class="sxs-lookup"><span data-stu-id="72485-211">Elements</span></span>  
  
|<span data-ttu-id="72485-212">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-212">Name</span></span>|<span data-ttu-id="72485-213">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-213">Description</span></span>|<span data-ttu-id="72485-214">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="72485-215">opgegeven limiet</span><span class="sxs-lookup"><span data-stu-id="72485-215">set-limit</span></span>|<span data-ttu-id="72485-216">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="72485-216">Root element.</span></span>|<span data-ttu-id="72485-217">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72485-218">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="72485-218">Attributes</span></span>  
  
|<span data-ttu-id="72485-219">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-219">Name</span></span>|<span data-ttu-id="72485-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-220">Description</span></span>|<span data-ttu-id="72485-221">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-221">Required</span></span>|<span data-ttu-id="72485-222">Standaard</span><span class="sxs-lookup"><span data-stu-id="72485-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="72485-223">aanroepen</span><span class="sxs-lookup"><span data-stu-id="72485-223">calls</span></span>|<span data-ttu-id="72485-224">Het maximum aantal aanroepen toegestaan tijdens het tijdsinterval die is opgegeven in de `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="72485-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="72485-225">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-225">Yes</span></span>|<span data-ttu-id="72485-226">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-226">N/A</span></span>|  
|<span data-ttu-id="72485-227">tegenpartij sleutel</span><span class="sxs-lookup"><span data-stu-id="72485-227">counter-key</span></span>|<span data-ttu-id="72485-228">De sleutel moet worden gebruikt voor het frequentielimietbeleid.</span><span class="sxs-lookup"><span data-stu-id="72485-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="72485-229">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-229">Yes</span></span>|<span data-ttu-id="72485-230">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-230">N/A</span></span>|  
|<span data-ttu-id="72485-231">verhoging voorwaarde</span><span class="sxs-lookup"><span data-stu-id="72485-231">increment-condition</span></span>|<span data-ttu-id="72485-232">De Boole-expressie opgeven als de aanvraag moet worden geteld voor het quotum (`true`).</span><span class="sxs-lookup"><span data-stu-id="72485-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="72485-233">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-233">No</span></span>|<span data-ttu-id="72485-234">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-234">N/A</span></span>|  
|<span data-ttu-id="72485-235">vernieuwingsperiode</span><span class="sxs-lookup"><span data-stu-id="72485-235">renewal-period</span></span>|<span data-ttu-id="72485-236">De tijd in seconden waarna het quotum wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="72485-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="72485-237">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-237">Yes</span></span>|<span data-ttu-id="72485-238">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72485-239">Gebruik</span><span class="sxs-lookup"><span data-stu-id="72485-239">Usage</span></span>  
 <span data-ttu-id="72485-240">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72485-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72485-241">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="72485-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="72485-242">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="72485-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="72485-243"><a name="RestrictCallerIPs"></a>Aanroeper IP-adressen beperken</span><span class="sxs-lookup"><span data-stu-id="72485-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="72485-244">De `ip-filter` beleid filtert (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="72485-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72485-245">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="72485-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="72485-246">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72485-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="72485-247">Elementen</span><span class="sxs-lookup"><span data-stu-id="72485-247">Elements</span></span>  
  
|<span data-ttu-id="72485-248">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-248">Name</span></span>|<span data-ttu-id="72485-249">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-249">Description</span></span>|<span data-ttu-id="72485-250">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="72485-251">IP-filter</span><span class="sxs-lookup"><span data-stu-id="72485-251">ip-filter</span></span>|<span data-ttu-id="72485-252">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="72485-252">Root element.</span></span>|<span data-ttu-id="72485-253">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-253">Yes</span></span>|  
|<span data-ttu-id="72485-254">Adres</span><span class="sxs-lookup"><span data-stu-id="72485-254">address</span></span>|<span data-ttu-id="72485-255">Hiermee geeft u een enkel IP-adres waarop u wilt filteren.</span><span class="sxs-lookup"><span data-stu-id="72485-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="72485-256">Ten minste één `address` of `address-range` element is vereist.</span><span class="sxs-lookup"><span data-stu-id="72485-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="72485-257">adresbereik van = 'adres' naar 'adres' =</span><span class="sxs-lookup"><span data-stu-id="72485-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="72485-258">Hiermee geeft u een bereik met IP-adres waarop u wilt filteren.</span><span class="sxs-lookup"><span data-stu-id="72485-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="72485-259">Ten minste één `address` of `address-range` element is vereist.</span><span class="sxs-lookup"><span data-stu-id="72485-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72485-260">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="72485-260">Attributes</span></span>  
  
|<span data-ttu-id="72485-261">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-261">Name</span></span>|<span data-ttu-id="72485-262">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-262">Description</span></span>|<span data-ttu-id="72485-263">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-263">Required</span></span>|<span data-ttu-id="72485-264">Standaard</span><span class="sxs-lookup"><span data-stu-id="72485-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="72485-265">adresbereik van = 'adres' naar 'adres' =</span><span class="sxs-lookup"><span data-stu-id="72485-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="72485-266">Een bereik van IP-adressen wilt toestaan of weigeren van toegang voor.</span><span class="sxs-lookup"><span data-stu-id="72485-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="72485-267">Vereist wanneer de `address-range` element wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="72485-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="72485-268">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-268">N/A</span></span>|  
|<span data-ttu-id="72485-269">IP-filteractie = ' toestaan dat &#124; verbieden"</span><span class="sxs-lookup"><span data-stu-id="72485-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="72485-270">Geeft aan of aanroepen moeten worden toegestaan of niet voor het opgegeven IP-adressen en de bereiken.</span><span class="sxs-lookup"><span data-stu-id="72485-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="72485-271">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-271">Yes</span></span>|<span data-ttu-id="72485-272">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72485-273">Gebruik</span><span class="sxs-lookup"><span data-stu-id="72485-273">Usage</span></span>  
 <span data-ttu-id="72485-274">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72485-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72485-275">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="72485-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="72485-276">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="72485-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="72485-277"><a name="SetUsageQuota"></a>Gebruiksquotum per abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="72485-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="72485-278">De `quota` beleid zorgt ervoor dat een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van per abonnement.</span><span class="sxs-lookup"><span data-stu-id="72485-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="72485-279">Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="72485-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="72485-280">[Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van het beleid voor dit beleid.</span><span class="sxs-lookup"><span data-stu-id="72485-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72485-281">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="72485-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="72485-282">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72485-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="72485-283">Elementen</span><span class="sxs-lookup"><span data-stu-id="72485-283">Elements</span></span>  
  
|<span data-ttu-id="72485-284">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-284">Name</span></span>|<span data-ttu-id="72485-285">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-285">Description</span></span>|<span data-ttu-id="72485-286">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="72485-287">quotum</span><span class="sxs-lookup"><span data-stu-id="72485-287">quota</span></span>|<span data-ttu-id="72485-288">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="72485-288">Root element.</span></span>|<span data-ttu-id="72485-289">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-289">Yes</span></span>|  
|<span data-ttu-id="72485-290">api</span><span class="sxs-lookup"><span data-stu-id="72485-290">api</span></span>|<span data-ttu-id="72485-291">Voeg een of meer van deze elementen te leggen een quotum op API's binnen het product.</span><span class="sxs-lookup"><span data-stu-id="72485-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="72485-292">Product- en API-quota worden onafhankelijk toegepast.</span><span class="sxs-lookup"><span data-stu-id="72485-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="72485-293">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-293">No</span></span>|  
|<span data-ttu-id="72485-294">bewerking</span><span class="sxs-lookup"><span data-stu-id="72485-294">operation</span></span>|<span data-ttu-id="72485-295">Een of meer van deze elementen te leggen een quotum op bewerkingen binnen een API toevoegen.</span><span class="sxs-lookup"><span data-stu-id="72485-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="72485-296">Product, API en bewerking quota's worden onafhankelijk van elkaar toegepast.</span><span class="sxs-lookup"><span data-stu-id="72485-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="72485-297">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72485-298">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="72485-298">Attributes</span></span>  
  
|<span data-ttu-id="72485-299">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-299">Name</span></span>|<span data-ttu-id="72485-300">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-300">Description</span></span>|<span data-ttu-id="72485-301">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-301">Required</span></span>|<span data-ttu-id="72485-302">Standaard</span><span class="sxs-lookup"><span data-stu-id="72485-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="72485-303">naam</span><span class="sxs-lookup"><span data-stu-id="72485-303">name</span></span>|<span data-ttu-id="72485-304">De naam van de API of de bewerking waarvoor het quotum van toepassing.</span><span class="sxs-lookup"><span data-stu-id="72485-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="72485-305">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-305">Yes</span></span>|<span data-ttu-id="72485-306">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-306">N/A</span></span>|  
|<span data-ttu-id="72485-307">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="72485-307">bandwidth</span></span>|<span data-ttu-id="72485-308">Het maximum aantal kilobytes is toegestaan tijdens het tijdsinterval die is opgegeven in de `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="72485-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="72485-309">Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="72485-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="72485-310">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-310">N/A</span></span>|  
|<span data-ttu-id="72485-311">aanroepen</span><span class="sxs-lookup"><span data-stu-id="72485-311">calls</span></span>|<span data-ttu-id="72485-312">Het maximum aantal aanroepen toegestaan tijdens het tijdsinterval die is opgegeven in de `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="72485-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="72485-313">Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="72485-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="72485-314">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-314">N/A</span></span>|  
|<span data-ttu-id="72485-315">vernieuwingsperiode</span><span class="sxs-lookup"><span data-stu-id="72485-315">renewal-period</span></span>|<span data-ttu-id="72485-316">De tijd in seconden waarna het quotum wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="72485-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="72485-317">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-317">Yes</span></span>|<span data-ttu-id="72485-318">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72485-319">Gebruik</span><span class="sxs-lookup"><span data-stu-id="72485-319">Usage</span></span>  
 <span data-ttu-id="72485-320">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72485-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72485-321">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="72485-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="72485-322">**Beleid scopes:** product</span><span class="sxs-lookup"><span data-stu-id="72485-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="72485-323"><a name="SetUsageQuotaByKey"></a>Gebruiksquotum instellen door sleutel</span><span class="sxs-lookup"><span data-stu-id="72485-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="72485-324">De `quota-by-key` beleid zorgt ervoor dat een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van de per-sleutel.</span><span class="sxs-lookup"><span data-stu-id="72485-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="72485-325">De sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.</span><span class="sxs-lookup"><span data-stu-id="72485-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="72485-326">Optionele incrementele voorwaarde kan worden toegevoegd om op te geven welke aanvragen naar het quotum moeten worden geteld.</span><span class="sxs-lookup"><span data-stu-id="72485-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="72485-327">Zie voor meer informatie over en voorbeelden van dit beleid, [geavanceerde aanvraagbeperking met Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="72485-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="72485-328">Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="72485-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="72485-329">[Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van het beleid voor dit beleid.</span><span class="sxs-lookup"><span data-stu-id="72485-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72485-330">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="72485-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="72485-331">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72485-331">Example</span></span>  
 <span data-ttu-id="72485-332">In het volgende voorbeeld wordt het quotum ingevoerd door de aanroeper IP-adres.</span><span class="sxs-lookup"><span data-stu-id="72485-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="72485-333">Elementen</span><span class="sxs-lookup"><span data-stu-id="72485-333">Elements</span></span>  
  
|<span data-ttu-id="72485-334">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-334">Name</span></span>|<span data-ttu-id="72485-335">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-335">Description</span></span>|<span data-ttu-id="72485-336">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="72485-337">quotum</span><span class="sxs-lookup"><span data-stu-id="72485-337">quota</span></span>|<span data-ttu-id="72485-338">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="72485-338">Root element.</span></span>|<span data-ttu-id="72485-339">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72485-340">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="72485-340">Attributes</span></span>  
  
|<span data-ttu-id="72485-341">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-341">Name</span></span>|<span data-ttu-id="72485-342">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-342">Description</span></span>|<span data-ttu-id="72485-343">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-343">Required</span></span>|<span data-ttu-id="72485-344">Standaard</span><span class="sxs-lookup"><span data-stu-id="72485-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="72485-345">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="72485-345">bandwidth</span></span>|<span data-ttu-id="72485-346">Het maximum aantal kilobytes is toegestaan tijdens het tijdsinterval die is opgegeven in de `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="72485-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="72485-347">Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="72485-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="72485-348">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-348">N/A</span></span>|  
|<span data-ttu-id="72485-349">aanroepen</span><span class="sxs-lookup"><span data-stu-id="72485-349">calls</span></span>|<span data-ttu-id="72485-350">Het maximum aantal aanroepen toegestaan tijdens het tijdsinterval die is opgegeven in de `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="72485-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="72485-351">Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="72485-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="72485-352">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-352">N/A</span></span>|  
|<span data-ttu-id="72485-353">tegenpartij sleutel</span><span class="sxs-lookup"><span data-stu-id="72485-353">counter-key</span></span>|<span data-ttu-id="72485-354">De sleutel moet worden gebruikt voor het quotumbeleid.</span><span class="sxs-lookup"><span data-stu-id="72485-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="72485-355">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-355">Yes</span></span>|<span data-ttu-id="72485-356">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-356">N/A</span></span>|  
|<span data-ttu-id="72485-357">verhoging voorwaarde</span><span class="sxs-lookup"><span data-stu-id="72485-357">increment-condition</span></span>|<span data-ttu-id="72485-358">De Boole-expressie opgeven als de aanvraag moet worden geteld voor het quotum (`true`)</span><span class="sxs-lookup"><span data-stu-id="72485-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="72485-359">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-359">No</span></span>|<span data-ttu-id="72485-360">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-360">N/A</span></span>|  
|<span data-ttu-id="72485-361">vernieuwingsperiode</span><span class="sxs-lookup"><span data-stu-id="72485-361">renewal-period</span></span>|<span data-ttu-id="72485-362">De tijd in seconden waarna het quotum wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="72485-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="72485-363">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-363">Yes</span></span>|<span data-ttu-id="72485-364">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72485-365">Gebruik</span><span class="sxs-lookup"><span data-stu-id="72485-365">Usage</span></span>  
 <span data-ttu-id="72485-366">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72485-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72485-367">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="72485-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="72485-368">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="72485-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="72485-369"><a name="ValidateJWT"></a>JWT valideren</span><span class="sxs-lookup"><span data-stu-id="72485-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="72485-370">De `validate-jwt` beleid zorgt ervoor dat bestaan en de geldigheid van een JWT opgehaald uit beide een opgegeven HTTP-Header of een opgegeven queryparameter.</span><span class="sxs-lookup"><span data-stu-id="72485-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="72485-371">De `validate-jwt` beleid vereist dat de `exp` geregistreerde claim inlcuded in de JWT-token is tenzij `require-expiration-time` kenmerk is opgegeven en ingesteld op `false`.</span><span class="sxs-lookup"><span data-stu-id="72485-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="72485-372">De `validate-jwt` beleid ondersteunt HS256 en RS256 ondertekenen algoritmen.</span><span class="sxs-lookup"><span data-stu-id="72485-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="72485-373">HS256 moet de sleutel worden opgegeven voor inline in het beleid in het formulier base64-gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="72485-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="72485-374">De sleutel heeft voor RS256 om via een Open ID configuratie-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="72485-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72485-375">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="72485-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
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
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="72485-376">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="72485-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="72485-377">Validatie van Azure Mobile Services-tokens</span><span class="sxs-lookup"><span data-stu-id="72485-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="72485-378">Validatie van Azure Active Directory-tokens</span><span class="sxs-lookup"><span data-stu-id="72485-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="72485-379">Validatie van Azure Active Directory B2C-tokens</span><span class="sxs-lookup"><span data-stu-id="72485-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="72485-380">Toegang verlenen aan bewerkingen op basis van claims token</span><span class="sxs-lookup"><span data-stu-id="72485-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="72485-381">Dit voorbeeld ziet u hoe u de [JWT valideren](api-management-access-restriction-policies.md#ValidateJWT) beleid vooraf toegang verlenen aan bewerkingen op basis van claims token.</span><span class="sxs-lookup"><span data-stu-id="72485-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="72485-382">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit tot 13:50.</span><span class="sxs-lookup"><span data-stu-id="72485-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="72485-383">Snel doorsturen naar 15:00 voor een overzicht van het beleid dat is geconfigureerd in de beleidseditor en vervolgens naar 18:50 voor een demonstratie van een bewerking aanroepen vanuit de ontwikkelaarsportal zowel met als zonder de vereiste verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="72485-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="72485-384">Elementen</span><span class="sxs-lookup"><span data-stu-id="72485-384">Elements</span></span>  
  
|<span data-ttu-id="72485-385">Element</span><span class="sxs-lookup"><span data-stu-id="72485-385">Element</span></span>|<span data-ttu-id="72485-386">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-386">Description</span></span>|<span data-ttu-id="72485-387">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72485-388">valideren jwt</span><span class="sxs-lookup"><span data-stu-id="72485-388">validate-jwt</span></span>|<span data-ttu-id="72485-389">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="72485-389">Root element.</span></span>|<span data-ttu-id="72485-390">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-390">Yes</span></span>|  
|<span data-ttu-id="72485-391">doelgroepen</span><span class="sxs-lookup"><span data-stu-id="72485-391">audiences</span></span>|<span data-ttu-id="72485-392">Bevat een lijst van toegestane doelgroep claims die gebruikt op het token worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="72485-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="72485-393">Als meerdere doelgroep waarden aanwezig zijn, wordt elke waarde wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt.</span><span class="sxs-lookup"><span data-stu-id="72485-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="72485-394">Ten minste één doelgroep moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="72485-394">At least one audience must be specified.</span></span>|<span data-ttu-id="72485-395">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-395">No</span></span>|  
|<span data-ttu-id="72485-396">ondertekening-sleutels van uitgever</span><span class="sxs-lookup"><span data-stu-id="72485-396">issuer-signing-keys</span></span>|<span data-ttu-id="72485-397">Een lijst met Base64-gecodeerd beveiligingssleutels gebruikt om ondertekende tokens te valideren.</span><span class="sxs-lookup"><span data-stu-id="72485-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="72485-398">Als meerdere beveiligingssleutels aanwezig zijn, wordt elke sleutel wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt (dit is nuttig voor de overschakeling van token).</span><span class="sxs-lookup"><span data-stu-id="72485-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="72485-399">De belangrijkste elementen hebben een optioneel `id` kenmerk dat wordt gebruikt voor het vergelijken van `kid` claim.</span><span class="sxs-lookup"><span data-stu-id="72485-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="72485-400">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-400">No</span></span>|  
|<span data-ttu-id="72485-401">uitgevers van certificaten</span><span class="sxs-lookup"><span data-stu-id="72485-401">issuers</span></span>|<span data-ttu-id="72485-402">Een lijst met toegestane principals die het token heeft uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="72485-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="72485-403">Als meerdere verlener waarden aanwezig zijn, wordt elke waarde wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt.</span><span class="sxs-lookup"><span data-stu-id="72485-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="72485-404">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-404">No</span></span>|  
|<span data-ttu-id="72485-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="72485-405">openid-config</span></span>|<span data-ttu-id="72485-406">Het element dat wordt gebruikt voor het opgeven van een compatibele configuratie-eindpunt voor Open-ID is waar ondertekenen van sleutels en uitgever kan worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="72485-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="72485-407">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-407">No</span></span>|  
|<span data-ttu-id="72485-408">vereist claims</span><span class="sxs-lookup"><span data-stu-id="72485-408">required-claims</span></span>|<span data-ttu-id="72485-409">Bevat een lijst met claims aanwezig zijn op het token als geldig beschouwd als deze wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="72485-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="72485-410">Wanneer de `match` kenmerk is ingesteld op `all` elke claimwaarde in het beleid moet aanwezig zijn in het token voor de validatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="72485-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="72485-411">Wanneer de `match` kenmerk is ingesteld op `any` ten minste één claim moet aanwezig zijn in het token voor de validatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="72485-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="72485-412">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-412">No</span></span>|  
|<span data-ttu-id="72485-413">zumo hoofdsleutel</span><span class="sxs-lookup"><span data-stu-id="72485-413">zumo-master-key</span></span>|<span data-ttu-id="72485-414">Hoofdsleutel voor tokens die zijn uitgegeven door Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="72485-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="72485-415">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72485-416">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="72485-416">Attributes</span></span>  
  
|<span data-ttu-id="72485-417">Naam</span><span class="sxs-lookup"><span data-stu-id="72485-417">Name</span></span>|<span data-ttu-id="72485-418">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72485-418">Description</span></span>|<span data-ttu-id="72485-419">Vereist</span><span class="sxs-lookup"><span data-stu-id="72485-419">Required</span></span>|<span data-ttu-id="72485-420">Standaard</span><span class="sxs-lookup"><span data-stu-id="72485-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="72485-421">tijdverschil</span><span class="sxs-lookup"><span data-stu-id="72485-421">clock-skew</span></span>|<span data-ttu-id="72485-422">TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="72485-422">Timespan.</span></span> <span data-ttu-id="72485-423">Biedt een aantal kleine eenheidsprofiel voor het geval van het token verloopt claim aanwezig in het token is en na de huidige datum valt / tijd.</span><span class="sxs-lookup"><span data-stu-id="72485-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="72485-424">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-424">No</span></span>|<span data-ttu-id="72485-425">0 seconden</span><span class="sxs-lookup"><span data-stu-id="72485-425">0 seconds</span></span>|  
|<span data-ttu-id="72485-426">kan de niet-validatie-foutbericht</span><span class="sxs-lookup"><span data-stu-id="72485-426">failed-validation-error-message</span></span>|<span data-ttu-id="72485-427">Het foutbericht te retourneren in de HTTP-antwoordtekst als de JWT niet kan gevalideerd worden.</span><span class="sxs-lookup"><span data-stu-id="72485-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="72485-428">Dit bericht moet de speciale tekens escape hebben.</span><span class="sxs-lookup"><span data-stu-id="72485-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="72485-429">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-429">No</span></span>|<span data-ttu-id="72485-430">Standaardfoutbericht, is afhankelijk van validatieprobleem, bijvoorbeeld 'JWT niet aanwezig."</span><span class="sxs-lookup"><span data-stu-id="72485-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="72485-431">kan geen validatie httpcode</span><span class="sxs-lookup"><span data-stu-id="72485-431">failed-validation-httpcode</span></span>|<span data-ttu-id="72485-432">HTTP-statuscode te retourneren als de JWT niet gevalideerd worden.</span><span class="sxs-lookup"><span data-stu-id="72485-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="72485-433">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-433">No</span></span>|<span data-ttu-id="72485-434">401</span><span class="sxs-lookup"><span data-stu-id="72485-434">401</span></span>|  
|<span data-ttu-id="72485-435">header-naam</span><span class="sxs-lookup"><span data-stu-id="72485-435">header-name</span></span>|<span data-ttu-id="72485-436">De naam van de HTTP-header van het token.</span><span class="sxs-lookup"><span data-stu-id="72485-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="72485-437">Ofwel `header-name` of `query-paremeter-name` moet worden opgegeven, maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="72485-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="72485-438">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-438">N/A</span></span>|  
|<span data-ttu-id="72485-439">id</span><span class="sxs-lookup"><span data-stu-id="72485-439">id</span></span>|<span data-ttu-id="72485-440">De `id` -kenmerk uit voor de `key` element kunt u opgeven van de tekenreeks die wordt vergeleken met `kid` claim in het token (indien aanwezig) om erachter te komen met de juiste sleutel moet worden gebruikt voor validatie van handtekening.</span><span class="sxs-lookup"><span data-stu-id="72485-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="72485-441">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-441">No</span></span>|<span data-ttu-id="72485-442">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-442">N/A</span></span>|  
|<span data-ttu-id="72485-443">Overeenkomst</span><span class="sxs-lookup"><span data-stu-id="72485-443">match</span></span>|<span data-ttu-id="72485-444">De `match` -kenmerk uit voor de `claim` element geeft aan of de waarde van elke claim in het beleid aanwezig zijn in het token voor de validatie moet mislukt.</span><span class="sxs-lookup"><span data-stu-id="72485-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="72485-445">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="72485-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="72485-446">-                          `all`-de waarde van elke claim in het beleid moet aanwezig zijn in het token voor de validatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="72485-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="72485-447">-                          `any`-ten minste één claimwaarde moet aanwezig zijn in het token voor de validatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="72485-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="72485-448">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-448">No</span></span>|<span data-ttu-id="72485-449">Alle</span><span class="sxs-lookup"><span data-stu-id="72485-449">all</span></span>|  
|<span data-ttu-id="72485-450">query-paremeter-naam</span><span class="sxs-lookup"><span data-stu-id="72485-450">query-paremeter-name</span></span>|<span data-ttu-id="72485-451">De naam van de de queryparameter van het token.</span><span class="sxs-lookup"><span data-stu-id="72485-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="72485-452">Ofwel `header-name` of `query-paremeter-name` moet worden opgegeven, maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="72485-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="72485-453">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-453">N/A</span></span>|  
|<span data-ttu-id="72485-454">vereisen verlooptijd vallen</span><span class="sxs-lookup"><span data-stu-id="72485-454">require-expiration-time</span></span>|<span data-ttu-id="72485-455">Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="72485-455">Boolean.</span></span> <span data-ttu-id="72485-456">Hiermee geeft u op of een claim vervaldatum in het token is vereist.</span><span class="sxs-lookup"><span data-stu-id="72485-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="72485-457">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-457">No</span></span>|<span data-ttu-id="72485-458">De waarde True</span><span class="sxs-lookup"><span data-stu-id="72485-458">true</span></span>|
|<span data-ttu-id="72485-459">vereisen schema</span><span class="sxs-lookup"><span data-stu-id="72485-459">require-scheme</span></span>|<span data-ttu-id="72485-460">De naam van het token schema, bijvoorbeeld 'Bearer'.</span><span class="sxs-lookup"><span data-stu-id="72485-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="72485-461">Wanneer dit kenmerk is ingesteld, kan het beleid zorgt ervoor dat het opgegeven schema is aanwezig in de waarde van de autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="72485-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="72485-462">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-462">No</span></span>|<span data-ttu-id="72485-463">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-463">N/A</span></span>|
|<span data-ttu-id="72485-464">vereisen ondertekend-tokens</span><span class="sxs-lookup"><span data-stu-id="72485-464">require-signed-tokens</span></span>|<span data-ttu-id="72485-465">Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="72485-465">Boolean.</span></span> <span data-ttu-id="72485-466">Geeft aan of een token vereist om te worden ondertekend.</span><span class="sxs-lookup"><span data-stu-id="72485-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="72485-467">Nee</span><span class="sxs-lookup"><span data-stu-id="72485-467">No</span></span>|<span data-ttu-id="72485-468">De waarde True</span><span class="sxs-lookup"><span data-stu-id="72485-468">true</span></span>|  
|<span data-ttu-id="72485-469">URL</span><span class="sxs-lookup"><span data-stu-id="72485-469">url</span></span>|<span data-ttu-id="72485-470">Open ID configuratie eindpunt-URL op waar de metagegevens van de Open-ID-configuratie kan worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="72485-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="72485-471">Gebruik de volgende URL voor Azure Active Directory: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` waarbij u de naam van uw directory-tenant, bijvoorbeeld vervangt `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="72485-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="72485-472">Ja</span><span class="sxs-lookup"><span data-stu-id="72485-472">Yes</span></span>|<span data-ttu-id="72485-473">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="72485-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72485-474">Gebruik</span><span class="sxs-lookup"><span data-stu-id="72485-474">Usage</span></span>  
 <span data-ttu-id="72485-475">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72485-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72485-476">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="72485-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="72485-477">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="72485-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="72485-478">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72485-478">Next steps</span></span>
<span data-ttu-id="72485-479">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="72485-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
