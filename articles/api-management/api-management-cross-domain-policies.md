---
title: aaaAzure API Management beleid voor meerdere domeinen | Microsoft Docs
description: Meer informatie over Hallo beleid voor meerdere domeinen beschikbaar voor gebruik in Azure API Management.
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
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="012f7-103">API Management-beleid voor meerdere domeinen</span><span class="sxs-lookup"><span data-stu-id="012f7-103">API Management cross domain policies</span></span>
<span data-ttu-id="012f7-104">Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen.</span><span class="sxs-lookup"><span data-stu-id="012f7-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="012f7-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="012f7-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="012f7-106"><a name="CrossDomainPolicies"></a>Cross-domeinbeleid</span><span class="sxs-lookup"><span data-stu-id="012f7-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="012f7-107">[Aanroepen tussen domeinen toestaan](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -Hallo API toegankelijk van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.</span><span class="sxs-lookup"><span data-stu-id="012f7-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="012f7-108">[CORS](api-management-cross-domain-policies.md#CORS) -voegt tooan cross-origin-resource delen (CORS) ondersteunen of een API tooallow tussen domeinen aanroepen van clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="012f7-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="012f7-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - JSON toegevoegd met de ondersteuning tooan bewerking opvulling (JSONP) of een API tooallow tussen domeinen aanroepen vanuit JavaScript-clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="012f7-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="012f7-110"><a name="AllowCrossDomainCalls"></a>Aanroepen tussen domeinen toestaan</span><span class="sxs-lookup"><span data-stu-id="012f7-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="012f7-111">Gebruik Hallo `cross-domain` beleid toomake Hallo API die toegankelijk is vanaf de Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.</span><span class="sxs-lookup"><span data-stu-id="012f7-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="012f7-112">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="012f7-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="012f7-113">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="012f7-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="012f7-114">Elementen</span><span class="sxs-lookup"><span data-stu-id="012f7-114">Elements</span></span>  
  
|<span data-ttu-id="012f7-115">Naam</span><span class="sxs-lookup"><span data-stu-id="012f7-115">Name</span></span>|<span data-ttu-id="012f7-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="012f7-116">Description</span></span>|<span data-ttu-id="012f7-117">Vereist</span><span class="sxs-lookup"><span data-stu-id="012f7-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="012f7-118">verschillende domeinen</span><span class="sxs-lookup"><span data-stu-id="012f7-118">cross-domain</span></span>|<span data-ttu-id="012f7-119">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="012f7-119">Root element.</span></span> <span data-ttu-id="012f7-120">Onderliggende elementen moeten voldoen toohello [Adobe cross-domeinbeleid bestandsspecificatie](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="012f7-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="012f7-121">Ja</span><span class="sxs-lookup"><span data-stu-id="012f7-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="012f7-122">Gebruik</span><span class="sxs-lookup"><span data-stu-id="012f7-122">Usage</span></span>  
 <span data-ttu-id="012f7-123">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="012f7-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="012f7-124">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="012f7-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="012f7-125">**Beleid scopes:** globale</span><span class="sxs-lookup"><span data-stu-id="012f7-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="012f7-126"><a name="CORS"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="012f7-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="012f7-127">Hallo `cors` beleid wordt toegevoegd voor cross-origin-resource delen (CORS) ondersteuning voor tooan bewerking of een API tooallow tussen domeinen aanroepen van clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="012f7-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="012f7-128">CORS kunt een browser en een server toointeract en bepalen of tooallow specifieke cross-origin-aanvragen (d.w.z. XMLHttpRequests aanroepen vanuit JavaScript op een webpagina tooother domeinen).</span><span class="sxs-lookup"><span data-stu-id="012f7-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="012f7-129">Dit biedt meer flexibiliteit dan alleen toe te staan dezelfde-origin-aanvragen, maar is veiliger dan zodat alle cross-origin-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="012f7-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="012f7-130">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="012f7-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="012f7-131">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="012f7-131">Example</span></span>  
 <span data-ttu-id="012f7-132">In dit voorbeeld laat zien hoe toosupport voorafgaan aan de vlucht aanvraagt, zoals die met aangepaste headers of andere methoden dan GET en POST.</span><span class="sxs-lookup"><span data-stu-id="012f7-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="012f7-133">aangepaste headers toosupport en aanvullende HTTP-woorden gebruiken Hallo `allowed-methods` en `allowed-headers` zoals weergegeven in het volgende voorbeeld Hallo secties.</span><span class="sxs-lookup"><span data-stu-id="012f7-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="012f7-134">Elementen</span><span class="sxs-lookup"><span data-stu-id="012f7-134">Elements</span></span>  
  
|<span data-ttu-id="012f7-135">Naam</span><span class="sxs-lookup"><span data-stu-id="012f7-135">Name</span></span>|<span data-ttu-id="012f7-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="012f7-136">Description</span></span>|<span data-ttu-id="012f7-137">Vereist</span><span class="sxs-lookup"><span data-stu-id="012f7-137">Required</span></span>|<span data-ttu-id="012f7-138">Standaard</span><span class="sxs-lookup"><span data-stu-id="012f7-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="012f7-139">cors</span><span class="sxs-lookup"><span data-stu-id="012f7-139">cors</span></span>|<span data-ttu-id="012f7-140">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="012f7-140">Root element.</span></span>|<span data-ttu-id="012f7-141">Ja</span><span class="sxs-lookup"><span data-stu-id="012f7-141">Yes</span></span>|<span data-ttu-id="012f7-142">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="012f7-142">N/A</span></span>|  
|<span data-ttu-id="012f7-143">toegestane oorsprongen</span><span class="sxs-lookup"><span data-stu-id="012f7-143">allowed-origins</span></span>|<span data-ttu-id="012f7-144">Bevat `origin` elementen die Hallo toegestane oorsprongen voor aanvragen van andere domeinen beschrijven.</span><span class="sxs-lookup"><span data-stu-id="012f7-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="012f7-145">`allowed-origins`kan bevatten één `origin` element waarmee wordt aangegeven `*` tooallow een oorsprong, of één of meer `origin` elementen die een URI bevatten.</span><span class="sxs-lookup"><span data-stu-id="012f7-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="012f7-146">Ja</span><span class="sxs-lookup"><span data-stu-id="012f7-146">Yes</span></span>|<span data-ttu-id="012f7-147">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="012f7-147">N/A</span></span>|  
|<span data-ttu-id="012f7-148">Oorsprong</span><span class="sxs-lookup"><span data-stu-id="012f7-148">origin</span></span>|<span data-ttu-id="012f7-149">Hallo waarde kan zijn `*` tooallow alle oorsprongen of een URI die een enkele oorsprong aangeeft.</span><span class="sxs-lookup"><span data-stu-id="012f7-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="012f7-150">Hallo URI moet een schema, host en poort bevatten.</span><span class="sxs-lookup"><span data-stu-id="012f7-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="012f7-151">Ja</span><span class="sxs-lookup"><span data-stu-id="012f7-151">Yes</span></span>|<span data-ttu-id="012f7-152">Als Hallo-poort in een URI wordt weggelaten, poort 80 wordt gebruikt voor HTTP en poort 443 voor HTTPS wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="012f7-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="012f7-153">toegestaan methoden</span><span class="sxs-lookup"><span data-stu-id="012f7-153">allowed-methods</span></span>|<span data-ttu-id="012f7-154">Dit element is vereist als methoden dan ophalen of POST zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="012f7-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="012f7-155">Bevat `method` elementen die opgeeft Hallo ondersteunde HTTP-termen.</span><span class="sxs-lookup"><span data-stu-id="012f7-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="012f7-156">Nee</span><span class="sxs-lookup"><span data-stu-id="012f7-156">No</span></span>|<span data-ttu-id="012f7-157">Als u deze sectie is niet aanwezig is, worden GET en POST worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="012f7-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="012f7-158">Methode</span><span class="sxs-lookup"><span data-stu-id="012f7-158">method</span></span>|<span data-ttu-id="012f7-159">Hiermee geeft u een HTTP-term.</span><span class="sxs-lookup"><span data-stu-id="012f7-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="012f7-160">Ten minste één `method` element is vereist als hello `allowed-methods` sectie aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="012f7-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="012f7-161">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="012f7-161">N/A</span></span>|  
|<span data-ttu-id="012f7-162">toegestaan headers</span><span class="sxs-lookup"><span data-stu-id="012f7-162">allowed-headers</span></span>|<span data-ttu-id="012f7-163">Dit element bevat `header` elementen namen van Hallo headers die kunnen worden opgenomen in de aanvraag Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="012f7-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="012f7-164">Nee</span><span class="sxs-lookup"><span data-stu-id="012f7-164">No</span></span>|<span data-ttu-id="012f7-165">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="012f7-165">N/A</span></span>|  
|<span data-ttu-id="012f7-166">zichtbaar headers</span><span class="sxs-lookup"><span data-stu-id="012f7-166">expose-headers</span></span>|<span data-ttu-id="012f7-167">Dit element bevat `header` elementen namen van Hallo headers die toegankelijk is door de client Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="012f7-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="012f7-168">Nee</span><span class="sxs-lookup"><span data-stu-id="012f7-168">No</span></span>|<span data-ttu-id="012f7-169">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="012f7-169">N/A</span></span>|  
|<span data-ttu-id="012f7-170">koptekst</span><span class="sxs-lookup"><span data-stu-id="012f7-170">header</span></span>|<span data-ttu-id="012f7-171">Hiermee geeft u een header-naam.</span><span class="sxs-lookup"><span data-stu-id="012f7-171">Specifies a header name.</span></span>|<span data-ttu-id="012f7-172">Ten minste één `header` element is vereist in `allowed-headers` of `expose-headers` als Hallo sectie aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="012f7-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="012f7-173">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="012f7-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="012f7-174">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="012f7-174">Attributes</span></span>  
  
|<span data-ttu-id="012f7-175">Naam</span><span class="sxs-lookup"><span data-stu-id="012f7-175">Name</span></span>|<span data-ttu-id="012f7-176">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="012f7-176">Description</span></span>|<span data-ttu-id="012f7-177">Vereist</span><span class="sxs-lookup"><span data-stu-id="012f7-177">Required</span></span>|<span data-ttu-id="012f7-178">Standaard</span><span class="sxs-lookup"><span data-stu-id="012f7-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="012f7-179">referenties toestaan</span><span class="sxs-lookup"><span data-stu-id="012f7-179">allow-credentials</span></span>|<span data-ttu-id="012f7-180">Hallo `Access-Control-Allow-Credentials` header in Hallo voorbereidende antwoord wordt set toohello waarde van dit kenmerk en van invloed zijn op Hallo van mogelijkheid toosubmit clientreferenties in verschillende domeinen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="012f7-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="012f7-181">Nee</span><span class="sxs-lookup"><span data-stu-id="012f7-181">No</span></span>|<span data-ttu-id="012f7-182">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="012f7-182">false</span></span>|  
|<span data-ttu-id="012f7-183">Preflight-resultaat--maximumleeftijd</span><span class="sxs-lookup"><span data-stu-id="012f7-183">preflight-result-max-age</span></span>|<span data-ttu-id="012f7-184">Hallo `Access-Control-Max-Age` header in Hallo voorbereidende antwoord wordt set toohello waarde van dit kenmerk en van invloed zijn op Hallo gebruikersagent mogelijkheid toocache voorafgaan aan de vlucht antwoord.</span><span class="sxs-lookup"><span data-stu-id="012f7-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="012f7-185">Nee</span><span class="sxs-lookup"><span data-stu-id="012f7-185">No</span></span>|<span data-ttu-id="012f7-186">0</span><span class="sxs-lookup"><span data-stu-id="012f7-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="012f7-187">Gebruik</span><span class="sxs-lookup"><span data-stu-id="012f7-187">Usage</span></span>  
 <span data-ttu-id="012f7-188">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="012f7-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="012f7-189">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="012f7-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="012f7-190">**Beleid scopes:** API, bewerking</span><span class="sxs-lookup"><span data-stu-id="012f7-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="012f7-191"><a name="JSONP"></a>JSONP</span><span class="sxs-lookup"><span data-stu-id="012f7-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="012f7-192">Hallo `jsonp` beleid JSON wordt toegevoegd met opvulling (JSONP) ondersteuning tooan bewerking of een API-aanroepen tooallow tussen domeinen vanuit JavaScript-clients op basis van een browser.</span><span class="sxs-lookup"><span data-stu-id="012f7-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="012f7-193">JSONP is een methode die wordt gebruikt in JavaScript-programma's toorequest gegevens van een server in een ander domein.</span><span class="sxs-lookup"><span data-stu-id="012f7-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="012f7-194">JSONP omzeilt Hallo beperking afgedwongen door de meeste webbrowsers waarop access tooweb-pagina's in Hallo moet hetzelfde domein.</span><span class="sxs-lookup"><span data-stu-id="012f7-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="012f7-195">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="012f7-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="012f7-196">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="012f7-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="012f7-197">Als u de methode Hallo zonder Hallo callback parameter aanroept? cb = XXX gewone JSON (zonder een wrapper-aanroep van functie) wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="012f7-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="012f7-198">Als u Hallo callback parameter toevoegen `?cb=XXX` JSONP gevolg hiervan zijn oorspronkelijke JSON-resultaten Hallo rond Hallo callback-functie zoals wrapping wordt geretourneerd`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="012f7-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="012f7-199">Elementen</span><span class="sxs-lookup"><span data-stu-id="012f7-199">Elements</span></span>  
  
|<span data-ttu-id="012f7-200">Naam</span><span class="sxs-lookup"><span data-stu-id="012f7-200">Name</span></span>|<span data-ttu-id="012f7-201">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="012f7-201">Description</span></span>|<span data-ttu-id="012f7-202">Vereist</span><span class="sxs-lookup"><span data-stu-id="012f7-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="012f7-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="012f7-203">jsonp</span></span>|<span data-ttu-id="012f7-204">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="012f7-204">Root element.</span></span>|<span data-ttu-id="012f7-205">Ja</span><span class="sxs-lookup"><span data-stu-id="012f7-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="012f7-206">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="012f7-206">Attributes</span></span>  
  
|<span data-ttu-id="012f7-207">Naam</span><span class="sxs-lookup"><span data-stu-id="012f7-207">Name</span></span>|<span data-ttu-id="012f7-208">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="012f7-208">Description</span></span>|<span data-ttu-id="012f7-209">Vereist</span><span class="sxs-lookup"><span data-stu-id="012f7-209">Required</span></span>|<span data-ttu-id="012f7-210">Standaard</span><span class="sxs-lookup"><span data-stu-id="012f7-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="012f7-211">callback parameternaam</span><span class="sxs-lookup"><span data-stu-id="012f7-211">callback-parameter-name</span></span>|<span data-ttu-id="012f7-212">Hallo tussen domeinen JavaScript-functieaanroep voorafgegaan door volledig gekwalificeerde domeinnaam Hallo waarin hello functie zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="012f7-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="012f7-213">Ja</span><span class="sxs-lookup"><span data-stu-id="012f7-213">Yes</span></span>|<span data-ttu-id="012f7-214">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="012f7-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="012f7-215">Gebruik</span><span class="sxs-lookup"><span data-stu-id="012f7-215">Usage</span></span>  
 <span data-ttu-id="012f7-216">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="012f7-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="012f7-217">**Beleid secties:** uitgaand</span><span class="sxs-lookup"><span data-stu-id="012f7-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="012f7-218">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="012f7-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="012f7-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="012f7-219">Next steps</span></span>
<span data-ttu-id="012f7-220">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="012f7-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  