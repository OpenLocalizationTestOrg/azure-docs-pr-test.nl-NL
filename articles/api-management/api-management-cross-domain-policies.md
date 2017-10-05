---
title: Azure API Management beleid voor meerdere domeinen | Microsoft Docs
description: Meer informatie over het beleid tussen domeinen beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="133cf-103">API Management-beleid voor meerdere domeinen</span><span class="sxs-lookup"><span data-stu-id="133cf-103">API Management cross domain policies</span></span>
<span data-ttu-id="133cf-104">Dit onderwerp bevat een verwijzing voor de volgende API Management-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="133cf-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="133cf-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="133cf-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="133cf-106"><a name="CrossDomainPolicies"></a>Cross-domeinbeleid</span><span class="sxs-lookup"><span data-stu-id="133cf-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="133cf-107">[Aanroepen tussen domeinen toestaan](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -de API van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients toegankelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="133cf-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="133cf-108">[CORS](api-management-cross-domain-policies.md#CORS) -cross-origin-resource delen (CORS) ondersteuning voor een bewerking of een API om toe te staan tussen domeinen aanroepen van clients op basis van een browser wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="133cf-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="133cf-109">[JSONP](api-management-cross-domain-policies.md#JSONP) -JSON wordt toegevoegd met ondersteuning voor een bewerking of een API om toe te staan tussen domeinen aanroepen vanuit JavaScript-browser gebaseerde clients opvulling (JSONP).</span><span class="sxs-lookup"><span data-stu-id="133cf-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="133cf-110"><a name="AllowCrossDomainCalls"></a>Aanroepen tussen domeinen toestaan</span><span class="sxs-lookup"><span data-stu-id="133cf-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="133cf-111">Gebruik de `cross-domain` beleid voor de API om toegankelijk te maken van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.</span><span class="sxs-lookup"><span data-stu-id="133cf-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="133cf-112">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="133cf-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="133cf-113">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="133cf-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="133cf-114">Elementen</span><span class="sxs-lookup"><span data-stu-id="133cf-114">Elements</span></span>  
  
|<span data-ttu-id="133cf-115">Naam</span><span class="sxs-lookup"><span data-stu-id="133cf-115">Name</span></span>|<span data-ttu-id="133cf-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="133cf-116">Description</span></span>|<span data-ttu-id="133cf-117">Vereist</span><span class="sxs-lookup"><span data-stu-id="133cf-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="133cf-118">verschillende domeinen</span><span class="sxs-lookup"><span data-stu-id="133cf-118">cross-domain</span></span>|<span data-ttu-id="133cf-119">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="133cf-119">Root element.</span></span> <span data-ttu-id="133cf-120">Onderliggende elementen moeten voldoen aan de [Adobe cross-domeinbeleid bestandsspecificatie](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="133cf-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="133cf-121">Ja</span><span class="sxs-lookup"><span data-stu-id="133cf-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="133cf-122">Gebruik</span><span class="sxs-lookup"><span data-stu-id="133cf-122">Usage</span></span>  
 <span data-ttu-id="133cf-123">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="133cf-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="133cf-124">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="133cf-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="133cf-125">**Beleid scopes:** globale</span><span class="sxs-lookup"><span data-stu-id="133cf-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="133cf-126"><a name="CORS"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="133cf-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="133cf-127">De `cors` beleid cross-origin-resource delen (CORS) ondersteuning voor een bewerking of een API om toe te staan tussen domeinen aanroepen van clients op basis van een browser wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="133cf-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="133cf-128">CORS kunt een browser en een server om te communiceren en bepalen of bepaalde cross-origin-aanvragen (d.w.z. XMLHttpRequests aanroepen van JavaScript aangebracht op een webpagina in andere domeinen) toestaan.</span><span class="sxs-lookup"><span data-stu-id="133cf-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="133cf-129">Dit biedt meer flexibiliteit dan alleen toe te staan dezelfde-origin-aanvragen, maar is veiliger dan zodat alle cross-origin-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="133cf-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="133cf-130">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="133cf-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="133cf-131">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="133cf-131">Example</span></span>  
 <span data-ttu-id="133cf-132">In dit voorbeeld laat zien hoe ter ondersteuning van voorafgaan aan de vlucht aanvragen, zoals die met aangepaste headers of andere methoden dan GET en POST.</span><span class="sxs-lookup"><span data-stu-id="133cf-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="133cf-133">Ter ondersteuning van aangepaste headers en aanvullende HTTP-termen, gebruikt u de `allowed-methods` en `allowed-headers` secties zoals weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="133cf-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="133cf-134">Elementen</span><span class="sxs-lookup"><span data-stu-id="133cf-134">Elements</span></span>  
  
|<span data-ttu-id="133cf-135">Naam</span><span class="sxs-lookup"><span data-stu-id="133cf-135">Name</span></span>|<span data-ttu-id="133cf-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="133cf-136">Description</span></span>|<span data-ttu-id="133cf-137">Vereist</span><span class="sxs-lookup"><span data-stu-id="133cf-137">Required</span></span>|<span data-ttu-id="133cf-138">Standaard</span><span class="sxs-lookup"><span data-stu-id="133cf-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="133cf-139">cors</span><span class="sxs-lookup"><span data-stu-id="133cf-139">cors</span></span>|<span data-ttu-id="133cf-140">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="133cf-140">Root element.</span></span>|<span data-ttu-id="133cf-141">Ja</span><span class="sxs-lookup"><span data-stu-id="133cf-141">Yes</span></span>|<span data-ttu-id="133cf-142">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="133cf-142">N/A</span></span>|  
|<span data-ttu-id="133cf-143">toegestane oorsprongen</span><span class="sxs-lookup"><span data-stu-id="133cf-143">allowed-origins</span></span>|<span data-ttu-id="133cf-144">Bevat `origin` elementen die de toegestane oorsprongen voor aanvragen van andere domeinen beschrijven.</span><span class="sxs-lookup"><span data-stu-id="133cf-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="133cf-145">`allowed-origins`kan bevatten één `origin` element waarmee wordt aangegeven `*` om toe te staan een oorsprong, of één of meer `origin` elementen die een URI bevatten.</span><span class="sxs-lookup"><span data-stu-id="133cf-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="133cf-146">Ja</span><span class="sxs-lookup"><span data-stu-id="133cf-146">Yes</span></span>|<span data-ttu-id="133cf-147">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="133cf-147">N/A</span></span>|  
|<span data-ttu-id="133cf-148">Oorsprong</span><span class="sxs-lookup"><span data-stu-id="133cf-148">origin</span></span>|<span data-ttu-id="133cf-149">De waarde kan zijn `*` toegestaan om alle oorsprongen of een URI die een enkele oorsprong aangeeft.</span><span class="sxs-lookup"><span data-stu-id="133cf-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="133cf-150">De URI moet een schema, host en poort bevatten.</span><span class="sxs-lookup"><span data-stu-id="133cf-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="133cf-151">Ja</span><span class="sxs-lookup"><span data-stu-id="133cf-151">Yes</span></span>|<span data-ttu-id="133cf-152">Als de poort in een URI wordt weggelaten, wordt poort 80 wordt gebruikt voor HTTP en poort 443 voor HTTPS wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="133cf-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="133cf-153">toegestaan methoden</span><span class="sxs-lookup"><span data-stu-id="133cf-153">allowed-methods</span></span>|<span data-ttu-id="133cf-154">Dit element is vereist als methoden dan ophalen of POST zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="133cf-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="133cf-155">Bevat `method` elementen die opgeeft van de ondersteunde HTTP-termen.</span><span class="sxs-lookup"><span data-stu-id="133cf-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="133cf-156">Nee</span><span class="sxs-lookup"><span data-stu-id="133cf-156">No</span></span>|<span data-ttu-id="133cf-157">Als u deze sectie is niet aanwezig is, worden GET en POST worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="133cf-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="133cf-158">Methode</span><span class="sxs-lookup"><span data-stu-id="133cf-158">method</span></span>|<span data-ttu-id="133cf-159">Hiermee geeft u een HTTP-term.</span><span class="sxs-lookup"><span data-stu-id="133cf-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="133cf-160">Ten minste één `method` element is vereist als de `allowed-methods` sectie aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="133cf-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="133cf-161">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="133cf-161">N/A</span></span>|  
|<span data-ttu-id="133cf-162">toegestaan headers</span><span class="sxs-lookup"><span data-stu-id="133cf-162">allowed-headers</span></span>|<span data-ttu-id="133cf-163">Dit element bevat `header` elementen geven van namen van de headers die kunnen worden opgenomen in de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="133cf-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="133cf-164">Nee</span><span class="sxs-lookup"><span data-stu-id="133cf-164">No</span></span>|<span data-ttu-id="133cf-165">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="133cf-165">N/A</span></span>|  
|<span data-ttu-id="133cf-166">zichtbaar headers</span><span class="sxs-lookup"><span data-stu-id="133cf-166">expose-headers</span></span>|<span data-ttu-id="133cf-167">Dit element bevat `header` elementen geven van namen van de headers die toegankelijk is door de client.</span><span class="sxs-lookup"><span data-stu-id="133cf-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="133cf-168">Nee</span><span class="sxs-lookup"><span data-stu-id="133cf-168">No</span></span>|<span data-ttu-id="133cf-169">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="133cf-169">N/A</span></span>|  
|<span data-ttu-id="133cf-170">koptekst</span><span class="sxs-lookup"><span data-stu-id="133cf-170">header</span></span>|<span data-ttu-id="133cf-171">Hiermee geeft u een header-naam.</span><span class="sxs-lookup"><span data-stu-id="133cf-171">Specifies a header name.</span></span>|<span data-ttu-id="133cf-172">Ten minste één `header` element is vereist in `allowed-headers` of `expose-headers` als de sectie aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="133cf-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="133cf-173">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="133cf-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="133cf-174">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="133cf-174">Attributes</span></span>  
  
|<span data-ttu-id="133cf-175">Naam</span><span class="sxs-lookup"><span data-stu-id="133cf-175">Name</span></span>|<span data-ttu-id="133cf-176">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="133cf-176">Description</span></span>|<span data-ttu-id="133cf-177">Vereist</span><span class="sxs-lookup"><span data-stu-id="133cf-177">Required</span></span>|<span data-ttu-id="133cf-178">Standaard</span><span class="sxs-lookup"><span data-stu-id="133cf-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="133cf-179">referenties toestaan</span><span class="sxs-lookup"><span data-stu-id="133cf-179">allow-credentials</span></span>|<span data-ttu-id="133cf-180">De `Access-Control-Allow-Credentials` header in het voorbereidende antwoord op de waarde van dit kenmerk worden ingesteld en van invloed zijn op de client de referenties in verschillende domeinen aanvragen indienen.</span><span class="sxs-lookup"><span data-stu-id="133cf-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="133cf-181">Nee</span><span class="sxs-lookup"><span data-stu-id="133cf-181">No</span></span>|<span data-ttu-id="133cf-182">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="133cf-182">false</span></span>|  
|<span data-ttu-id="133cf-183">Preflight-resultaat--maximumleeftijd</span><span class="sxs-lookup"><span data-stu-id="133cf-183">preflight-result-max-age</span></span>|<span data-ttu-id="133cf-184">De `Access-Control-Max-Age` header in het voorbereidende antwoord aan de waarde van dit kenmerk wordt ingesteld en van invloed zijn op de gebruikersagent cacheantwoord voorafgaan aan de vlucht.</span><span class="sxs-lookup"><span data-stu-id="133cf-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="133cf-185">Nee</span><span class="sxs-lookup"><span data-stu-id="133cf-185">No</span></span>|<span data-ttu-id="133cf-186">0</span><span class="sxs-lookup"><span data-stu-id="133cf-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="133cf-187">Gebruik</span><span class="sxs-lookup"><span data-stu-id="133cf-187">Usage</span></span>  
 <span data-ttu-id="133cf-188">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="133cf-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="133cf-189">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="133cf-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="133cf-190">**Beleid scopes:** API, bewerking</span><span class="sxs-lookup"><span data-stu-id="133cf-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="133cf-191"><a name="JSONP"></a>JSONP</span><span class="sxs-lookup"><span data-stu-id="133cf-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="133cf-192">De `jsonp` beleid wordt JSON met ondersteuning voor opvulling (JSONP) toegevoegd aan een bewerking of een API om toe te staan tussen domeinen aanroepen vanuit JavaScript-clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="133cf-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="133cf-193">JSONP is een methode in JavaScript-programma's voor gegevens van aanvragen van een server in een ander domein.</span><span class="sxs-lookup"><span data-stu-id="133cf-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="133cf-194">JSONP omzeilt de beperking die wordt afgedwongen door de meeste webbrowsers waarop toegang tot webpagina's, in hetzelfde domein moet.</span><span class="sxs-lookup"><span data-stu-id="133cf-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="133cf-195">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="133cf-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="133cf-196">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="133cf-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="133cf-197">Als u de methode zonder de parameter callback aanroepen? cb = XXX gewone JSON (zonder een wrapper-aanroep van functie) wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="133cf-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="133cf-198">Als u de parameter callback toevoegt `?cb=XXX` een JSONP-resultaat wordt geretourneerd, resultaten rond de callback-functie, zoals de oorspronkelijke JSON wrapping`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="133cf-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="133cf-199">Elementen</span><span class="sxs-lookup"><span data-stu-id="133cf-199">Elements</span></span>  
  
|<span data-ttu-id="133cf-200">Naam</span><span class="sxs-lookup"><span data-stu-id="133cf-200">Name</span></span>|<span data-ttu-id="133cf-201">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="133cf-201">Description</span></span>|<span data-ttu-id="133cf-202">Vereist</span><span class="sxs-lookup"><span data-stu-id="133cf-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="133cf-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="133cf-203">jsonp</span></span>|<span data-ttu-id="133cf-204">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="133cf-204">Root element.</span></span>|<span data-ttu-id="133cf-205">Ja</span><span class="sxs-lookup"><span data-stu-id="133cf-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="133cf-206">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="133cf-206">Attributes</span></span>  
  
|<span data-ttu-id="133cf-207">Naam</span><span class="sxs-lookup"><span data-stu-id="133cf-207">Name</span></span>|<span data-ttu-id="133cf-208">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="133cf-208">Description</span></span>|<span data-ttu-id="133cf-209">Vereist</span><span class="sxs-lookup"><span data-stu-id="133cf-209">Required</span></span>|<span data-ttu-id="133cf-210">Standaard</span><span class="sxs-lookup"><span data-stu-id="133cf-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="133cf-211">callback parameternaam</span><span class="sxs-lookup"><span data-stu-id="133cf-211">callback-parameter-name</span></span>|<span data-ttu-id="133cf-212">De verschillende domeinen JavaScript functieaanroep voorafgegaan door de volledig gekwalificeerde domeinnaam waarin de functie zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="133cf-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="133cf-213">Ja</span><span class="sxs-lookup"><span data-stu-id="133cf-213">Yes</span></span>|<span data-ttu-id="133cf-214">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="133cf-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="133cf-215">Gebruik</span><span class="sxs-lookup"><span data-stu-id="133cf-215">Usage</span></span>  
 <span data-ttu-id="133cf-216">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="133cf-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="133cf-217">**Beleid secties:** uitgaand</span><span class="sxs-lookup"><span data-stu-id="133cf-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="133cf-218">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="133cf-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="133cf-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="133cf-219">Next steps</span></span>
<span data-ttu-id="133cf-220">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="133cf-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  