---
title: claimtransformatiebeleidsinstellingen aaaAzure-API Management | Microsoft Docs
description: Meer informatie over Hallo claimtransformatiebeleidsinstellingen beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="3081f-103">API Management-beleidsregels voor transformatie</span><span class="sxs-lookup"><span data-stu-id="3081f-103">API Management transformation policies</span></span>
<span data-ttu-id="3081f-104">Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen.</span><span class="sxs-lookup"><span data-stu-id="3081f-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="3081f-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="3081f-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="3081f-106"><a name="TransformationPolicies"></a>Claimtransformatiebeleidsinstellingen</span><span class="sxs-lookup"><span data-stu-id="3081f-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="3081f-107">[Converteren van JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) : zet aanvraag of antwoord body van JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="3081f-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="3081f-108">[Converteren van XML-tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : zet aanvraag of antwoord body van XML-tooJSON.</span><span class="sxs-lookup"><span data-stu-id="3081f-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="3081f-109">[Zoeken en vervangen tekenreeks in de hoofdtekst](api-management-transformation-policies.md#Findandreplacestringinbody) - zoeken naar een subtekenreeks aanvraag of antwoord en wordt vervangen door een andere subtekenreeks.</span><span class="sxs-lookup"><span data-stu-id="3081f-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="3081f-110">[URL's in de inhoud te maskeren](api-management-transformation-policies.md#MaskURLSContent) -koppelingen herschrijft (maskers) antwoord Hallo body zodat ze equivalente koppeling toohello via Hallo gateway wijst.</span><span class="sxs-lookup"><span data-stu-id="3081f-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="3081f-111">[Instellen van de back-endservice](api-management-transformation-policies.md#SetBackendService) -back-endservice Hallo voor de binnenkomende aanvraag wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3081f-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="3081f-112">[Instantie ingesteld](api-management-transformation-policies.md#SetBody) -hoofdtekst van het Hallo-bericht voor binnenkomende en uitgaande aanvragen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3081f-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="3081f-113">[Set HTTP-header](api-management-transformation-policies.md#SetHTTPheader) : een waarde tooan bestaande antwoord en/of de aanvraagheader wijst of voegt een nieuwe antwoord en/of de aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="3081f-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="3081f-114">[Querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) - wordt toegevoegd, vervangt de waarde van of verwijderd van de aanvraag queryreeksparameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="3081f-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="3081f-115">[Herschrijven van URL](api-management-transformation-policies.md#RewriteURL) -zet u een aanvraag-URL van de openbare formulier toohello vorm werd verwacht door Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="3081f-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="3081f-116">[XML met behulp van een XSLT transformeren](api-management-transformation-policies.md#XSLTransform) -een XSL-transformatie tooXML in de hoofdtekst van de aanvraag of antwoord van de Hallo van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="3081f-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="3081f-117"><a name="ConvertJSONtoXML"></a>JSON tooXML converteren</span><span class="sxs-lookup"><span data-stu-id="3081f-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="3081f-118">Hallo `json-to-xml` beleid zet de hoofdtekst van een aanvraag of antwoord van de JSON-tooXML.</span><span class="sxs-lookup"><span data-stu-id="3081f-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-119">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="3081f-120">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="3081f-121">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-121">Elements</span></span>  
  
|<span data-ttu-id="3081f-122">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-122">Name</span></span>|<span data-ttu-id="3081f-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-123">Description</span></span>|<span data-ttu-id="3081f-124">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-125">JSON-to-xml</span><span class="sxs-lookup"><span data-stu-id="3081f-125">json-to-xml</span></span>|<span data-ttu-id="3081f-126">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-126">Root element.</span></span>|<span data-ttu-id="3081f-127">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3081f-128">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="3081f-128">Attributes</span></span>  
  
|<span data-ttu-id="3081f-129">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-129">Name</span></span>|<span data-ttu-id="3081f-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-130">Description</span></span>|<span data-ttu-id="3081f-131">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-131">Required</span></span>|<span data-ttu-id="3081f-132">Standaard</span><span class="sxs-lookup"><span data-stu-id="3081f-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3081f-133">toepassen</span><span class="sxs-lookup"><span data-stu-id="3081f-133">apply</span></span>|<span data-ttu-id="3081f-134">Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="3081f-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="3081f-135">conversie - altijd - altijd van toepassing.</span><span class="sxs-lookup"><span data-stu-id="3081f-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="3081f-136">convert-inhoud type-json - alleen als response Content-Type-header aanwezigheid van JSON aangeeft.</span><span class="sxs-lookup"><span data-stu-id="3081f-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="3081f-137">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-137">Yes</span></span>|<span data-ttu-id="3081f-138">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-138">N/A</span></span>|  
|<span data-ttu-id="3081f-139">Overweeg-accepteren-header</span><span class="sxs-lookup"><span data-stu-id="3081f-139">consider-accept-header</span></span>|<span data-ttu-id="3081f-140">Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="3081f-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="3081f-141">-waar - conversie van toepassing als JSON is aangevraagd in aanvraag Accept-header.</span><span class="sxs-lookup"><span data-stu-id="3081f-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="3081f-142">-ONWAAR - conversie altijd van toepassing.</span><span class="sxs-lookup"><span data-stu-id="3081f-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="3081f-143">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-143">No</span></span>|<span data-ttu-id="3081f-144">De waarde True</span><span class="sxs-lookup"><span data-stu-id="3081f-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3081f-145">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-145">Usage</span></span>  
 <span data-ttu-id="3081f-146">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-147">**Beleid secties:** binnenkomende, uitgaande, bij fouten</span><span class="sxs-lookup"><span data-stu-id="3081f-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="3081f-148">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-149"><a name="ConvertXMLtoJSON"></a>XML-tooJSON converteren</span><span class="sxs-lookup"><span data-stu-id="3081f-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="3081f-150">Hallo `xml-to-json` beleid zet de hoofdtekst van een aanvraag of antwoord van de XML-tooJSON.</span><span class="sxs-lookup"><span data-stu-id="3081f-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="3081f-151">Dit beleid kan worden gebruikt toomodernize API's op basis van de back-end van een alleen-XML-webservices.</span><span class="sxs-lookup"><span data-stu-id="3081f-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-152">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="3081f-153">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="3081f-154">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-154">Elements</span></span>  
  
|<span data-ttu-id="3081f-155">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-155">Name</span></span>|<span data-ttu-id="3081f-156">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-156">Description</span></span>|<span data-ttu-id="3081f-157">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-158">XML-json-</span><span class="sxs-lookup"><span data-stu-id="3081f-158">xml-to-json</span></span>|<span data-ttu-id="3081f-159">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-159">Root element.</span></span>|<span data-ttu-id="3081f-160">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3081f-161">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="3081f-161">Attributes</span></span>  
  
|<span data-ttu-id="3081f-162">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-162">Name</span></span>|<span data-ttu-id="3081f-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-163">Description</span></span>|<span data-ttu-id="3081f-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-164">Required</span></span>|<span data-ttu-id="3081f-165">Standaard</span><span class="sxs-lookup"><span data-stu-id="3081f-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3081f-166">type</span><span class="sxs-lookup"><span data-stu-id="3081f-166">kind</span></span>|<span data-ttu-id="3081f-167">Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="3081f-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="3081f-168">Hallo - javascript-vriendelijk - geconverteerd JSON heeft een formulier beschrijvende tooJavaScript ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="3081f-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="3081f-169">-direct - duidt hello geconverteerde JSON op Hallo van het oorspronkelijke XML-document-structuur.</span><span class="sxs-lookup"><span data-stu-id="3081f-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="3081f-170">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-170">Yes</span></span>|<span data-ttu-id="3081f-171">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-171">N/A</span></span>|  
|<span data-ttu-id="3081f-172">toepassen</span><span class="sxs-lookup"><span data-stu-id="3081f-172">apply</span></span>|<span data-ttu-id="3081f-173">Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="3081f-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="3081f-174">-altijd - altijd converteren.</span><span class="sxs-lookup"><span data-stu-id="3081f-174">-   always - convert always.</span></span><br /><span data-ttu-id="3081f-175">convert - inhoud-type-xml - alleen als response Content-Type-header aanwezigheid van XML aangeeft.</span><span class="sxs-lookup"><span data-stu-id="3081f-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="3081f-176">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-176">Yes</span></span>|<span data-ttu-id="3081f-177">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-177">N/A</span></span>|  
|<span data-ttu-id="3081f-178">Overweeg-accepteren-header</span><span class="sxs-lookup"><span data-stu-id="3081f-178">consider-accept-header</span></span>|<span data-ttu-id="3081f-179">Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="3081f-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="3081f-180">-waar - conversie van toepassing als XML is aangevraagd in aanvraag Accept-header.</span><span class="sxs-lookup"><span data-stu-id="3081f-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="3081f-181">-ONWAAR - conversie altijd van toepassing.</span><span class="sxs-lookup"><span data-stu-id="3081f-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="3081f-182">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-182">No</span></span>|<span data-ttu-id="3081f-183">De waarde True</span><span class="sxs-lookup"><span data-stu-id="3081f-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3081f-184">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-184">Usage</span></span>  
 <span data-ttu-id="3081f-185">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-186">**Beleid secties:** binnenkomende, uitgaande, bij fouten</span><span class="sxs-lookup"><span data-stu-id="3081f-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="3081f-187">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-188"><a name="Findandreplacestringinbody"></a>Zoeken en vervangen tekenreeks in de hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="3081f-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="3081f-189">Hallo `find-and-replace` beleid vindt u een aanvraag of antwoord subtekenreeks en vervangen door een andere subtekenreeks.</span><span class="sxs-lookup"><span data-stu-id="3081f-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-190">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="3081f-191">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="3081f-192">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-192">Elements</span></span>  
  
|<span data-ttu-id="3081f-193">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-193">Name</span></span>|<span data-ttu-id="3081f-194">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-194">Description</span></span>|<span data-ttu-id="3081f-195">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-196">zoeken en vervangen</span><span class="sxs-lookup"><span data-stu-id="3081f-196">find-and-replace</span></span>|<span data-ttu-id="3081f-197">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-197">Root element.</span></span>|<span data-ttu-id="3081f-198">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3081f-199">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="3081f-199">Attributes</span></span>  
  
|<span data-ttu-id="3081f-200">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-200">Name</span></span>|<span data-ttu-id="3081f-201">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-201">Description</span></span>|<span data-ttu-id="3081f-202">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-202">Required</span></span>|<span data-ttu-id="3081f-203">Standaard</span><span class="sxs-lookup"><span data-stu-id="3081f-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3081f-204">Van</span><span class="sxs-lookup"><span data-stu-id="3081f-204">from</span></span>|<span data-ttu-id="3081f-205">Hallo tekenreeks toosearch voor.</span><span class="sxs-lookup"><span data-stu-id="3081f-205">hello string toosearch for.</span></span>|<span data-ttu-id="3081f-206">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-206">Yes</span></span>|<span data-ttu-id="3081f-207">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-207">N/A</span></span>|  
|<span data-ttu-id="3081f-208">tot</span><span class="sxs-lookup"><span data-stu-id="3081f-208">to</span></span>|<span data-ttu-id="3081f-209">Hallo vervangende tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="3081f-209">hello replacement string.</span></span> <span data-ttu-id="3081f-210">Geef de vervangende tekenreeks tooremove Hallo zoeken tekenreekslengte van nul.</span><span class="sxs-lookup"><span data-stu-id="3081f-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="3081f-211">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-211">Yes</span></span>|<span data-ttu-id="3081f-212">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3081f-213">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-213">Usage</span></span>  
 <span data-ttu-id="3081f-214">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-215">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="3081f-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3081f-216">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-217"><a name="MaskURLSContent"></a>Masker URL's in de inhoud</span><span class="sxs-lookup"><span data-stu-id="3081f-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="3081f-218">Hallo `redirect-content-urls` beleid herschrijft (maskers) koppelingen in de antwoordtekst Hallo zodat ze equivalente koppeling toohello via Hallo gateway wijst.</span><span class="sxs-lookup"><span data-stu-id="3081f-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="3081f-219">Gebruik in Hallo uitgaande sectie toore schrijven antwoord hoofdtekst koppelingen toomake ze punt toohello gateway.</span><span class="sxs-lookup"><span data-stu-id="3081f-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="3081f-220">Gebruik in Hallo inkomende sectie voor een tegenovergestelde effect.</span><span class="sxs-lookup"><span data-stu-id="3081f-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3081f-221">Dit beleid verandert niet een headerwaarden, zoals `Location` headers.</span><span class="sxs-lookup"><span data-stu-id="3081f-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="3081f-222">de headerwaarden toochange hello gebruiken [set-header](api-management-transformation-policies.md#SetHTTPheader) beleid.</span><span class="sxs-lookup"><span data-stu-id="3081f-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-223">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="3081f-224">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="3081f-225">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-225">Elements</span></span>  
  
|<span data-ttu-id="3081f-226">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-226">Name</span></span>|<span data-ttu-id="3081f-227">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-227">Description</span></span>|<span data-ttu-id="3081f-228">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-229">Omleidings-inhoud-URL 's</span><span class="sxs-lookup"><span data-stu-id="3081f-229">redirect-content-urls</span></span>|<span data-ttu-id="3081f-230">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-230">Root element.</span></span>|<span data-ttu-id="3081f-231">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3081f-232">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-232">Usage</span></span>  
 <span data-ttu-id="3081f-233">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-234">**Beleid secties:** binnenkomende, uitgaande</span><span class="sxs-lookup"><span data-stu-id="3081f-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="3081f-235">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-236"><a name="SetBackendService"></a>Back-end-service instellen</span><span class="sxs-lookup"><span data-stu-id="3081f-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="3081f-237">Gebruik Hallo `set-backend-service` beleid tooredirect een binnenkomende aanvraag tooa andere back-end dan Hallo één in Hallo API-instellingen voor de bewerking is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3081f-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="3081f-238">Dit beleid wijzigingen Hallo back-end service basis-URL van het binnenkomende aanvraag toohello hello, een opgegeven in het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="3081f-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-239">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="3081f-240">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="3081f-241">In dit voorbeeld Hallo routeert beleid instellen back-end-service aanvragen op basis van Hallo versiewaarde doorgegeven Hallo query tekenreeks tooa andere back-endservice dan Hallo Hallo voor een opgegeven in de API.</span><span class="sxs-lookup"><span data-stu-id="3081f-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="3081f-242">In eerste instantie Hallo service basis-URL is afgeleid van de instellingen voor de API Hallo-back-end.</span><span class="sxs-lookup"><span data-stu-id="3081f-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="3081f-243">Dus Hallo aanvraag-URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` wordt `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` waar `http://contoso.com/api/10.4/` Hallo back-end-service URL is opgegeven in de Hallo API-instellingen.</span><span class="sxs-lookup"><span data-stu-id="3081f-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="3081f-244">Wanneer Hallo [< kiezen\> ](api-management-advanced-policies.md#choose) beleidsverklaring wordt toegepast Hallo back-end service basis-URL kan wijzigen opnieuw te`http://contoso.com/api/8.2` of `http://contoso.com/api/9.1`, afhankelijk van het Hallo-waarde van Hallo versie aanvraag-queryparameter.</span><span class="sxs-lookup"><span data-stu-id="3081f-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="3081f-245">Bijvoorbeeld, als hello waarde is `"2013-15"` Hallo van de laatste aanvraag URL wordt `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="3081f-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="3081f-246">Als verdere transformatie van Hallo-aanvraag gewenste, andere is [claimtransformatiebeleidsinstellingen](api-management-transformation-policies.md#TransformationPolicies) kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3081f-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="3081f-247">Bijvoorbeeld tooremove Hallo versie query parameter nu dat hello aanvraag wordt gerouteerd tooa versie specifieke back-end hello [querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) beleid gebruikte tooremove Hallo nu redundante version-kenmerk kan worden.</span><span class="sxs-lookup"><span data-stu-id="3081f-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="3081f-248">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="3081f-249">In dit voorbeeld Hallo beleid routes Hallo aanvraag tooa service fabric back-end Hallo Hallo userId queryreeks gebruikt als partitiesleutel Hallo en primaire replica van Hallo-partitie.</span><span class="sxs-lookup"><span data-stu-id="3081f-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="3081f-250">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-250">Elements</span></span>  
  
|<span data-ttu-id="3081f-251">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-251">Name</span></span>|<span data-ttu-id="3081f-252">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-252">Description</span></span>|<span data-ttu-id="3081f-253">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-254">set-back-end-service</span><span class="sxs-lookup"><span data-stu-id="3081f-254">set-backend-service</span></span>|<span data-ttu-id="3081f-255">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-255">Root element.</span></span>|<span data-ttu-id="3081f-256">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3081f-257">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="3081f-257">Attributes</span></span>  
  
|<span data-ttu-id="3081f-258">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-258">Name</span></span>|<span data-ttu-id="3081f-259">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-259">Description</span></span>|<span data-ttu-id="3081f-260">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-260">Required</span></span>|<span data-ttu-id="3081f-261">Standaard</span><span class="sxs-lookup"><span data-stu-id="3081f-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3081f-262">basis-url</span><span class="sxs-lookup"><span data-stu-id="3081f-262">base-url</span></span>|<span data-ttu-id="3081f-263">Nieuwe back-end service basis-URL.</span><span class="sxs-lookup"><span data-stu-id="3081f-263">New backend service base URL.</span></span>|<span data-ttu-id="3081f-264">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-264">No</span></span>|<span data-ttu-id="3081f-265">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-265">N/A</span></span>|  
|<span data-ttu-id="3081f-266">back-end-id</span><span class="sxs-lookup"><span data-stu-id="3081f-266">backend-id</span></span>|<span data-ttu-id="3081f-267">Id van Hallo back-end tooroute aan.</span><span class="sxs-lookup"><span data-stu-id="3081f-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="3081f-268">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-268">No</span></span>|<span data-ttu-id="3081f-269">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-269">N/A</span></span>|  
|<span data-ttu-id="3081f-270">SF partitiesleutel</span><span class="sxs-lookup"><span data-stu-id="3081f-270">sf-partition-key</span></span>|<span data-ttu-id="3081f-271">Alleen van toepassing wanneer het Hallo-back-end is een Service Fabric-service en wordt opgegeven met behulp van back-end-id.</span><span class="sxs-lookup"><span data-stu-id="3081f-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="3081f-272">Een specifieke partitie van de service voor naamomzetting Hallo tooresolve gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3081f-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="3081f-273">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-273">No</span></span>|<span data-ttu-id="3081f-274">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-274">N/A</span></span>|  
|<span data-ttu-id="3081f-275">SF-replica-type</span><span class="sxs-lookup"><span data-stu-id="3081f-275">sf-replica-type</span></span>|<span data-ttu-id="3081f-276">Alleen van toepassing wanneer het Hallo-back-end is een Service Fabric-service en wordt opgegeven met behulp van back-end-id.</span><span class="sxs-lookup"><span data-stu-id="3081f-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="3081f-277">Bepaalt of het Hallo-aanvraag toohello primaire of secundaire replica van een partitie moet gaan.</span><span class="sxs-lookup"><span data-stu-id="3081f-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="3081f-278">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-278">No</span></span>|<span data-ttu-id="3081f-279">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-279">N/A</span></span>|    
|<span data-ttu-id="3081f-280">SF-resolve-voorwaarde</span><span class="sxs-lookup"><span data-stu-id="3081f-280">sf-resolve-condition</span></span>|<span data-ttu-id="3081f-281">Alleen van toepassing wanneer de back-end voor Hallo is een Service Fabric-service.</span><span class="sxs-lookup"><span data-stu-id="3081f-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="3081f-282">Voorwaarde te identificeren heeft als Hallo tooService Fabric back-end aanroepen toobe herhaald met nieuwe resolutie.</span><span class="sxs-lookup"><span data-stu-id="3081f-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="3081f-283">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-283">No</span></span>|<span data-ttu-id="3081f-284">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-284">N/A</span></span>|    
|<span data-ttu-id="3081f-285">SF-service-exemplaar-name</span><span class="sxs-lookup"><span data-stu-id="3081f-285">sf-service-instance-name</span></span>|<span data-ttu-id="3081f-286">Alleen van toepassing wanneer de back-end voor Hallo is een Service Fabric-service.</span><span class="sxs-lookup"><span data-stu-id="3081f-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="3081f-287">Kan toochange service-exemplaren tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="3081f-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="3081f-288">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-288">No</span></span>|<span data-ttu-id="3081f-289">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="3081f-290">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-290">Usage</span></span>  
 <span data-ttu-id="3081f-291">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-292">**Beleid secties:** back-end voor binnenkomend verkeer</span><span class="sxs-lookup"><span data-stu-id="3081f-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="3081f-293">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-294"><a name="SetBody"></a>Set-instantie</span><span class="sxs-lookup"><span data-stu-id="3081f-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="3081f-295">Gebruik Hallo `set-body` beleid tooset Hallo berichttekst voor binnenkomende en uitgaande aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3081f-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="3081f-296">tooaccess Hallo berichttekst kunt u Hallo `context.Request.Body` eigenschap of Hallo `context.Response.Body`, afhankelijk van of Hallo-beleid in een Hallo is binnenkomend of uitgaand sectie.</span><span class="sxs-lookup"><span data-stu-id="3081f-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="3081f-297">Denk eraan dat standaard als u toegang hebben tot Hallo bericht hoofdtekst met `context.Request.Body` of `context.Response.Body`, oorspronkelijke welkomstbericht hoofdtekst verloren en wordt door te retourneren Hallo hoofdtekst terug in Hallo-expressie moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3081f-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="3081f-298">inhoud, toopreserve Hallo-instantie ingesteld Hallo `preserveContent` parameter te`true` bij het openen van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="3081f-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="3081f-299">Als `preserveContent` te is ingesteld,`true` en een andere instantie wordt geretourneerd door het Hallo-expressie Hallo geretourneerd instantie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3081f-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="3081f-300">Houd er rekening mee Hallo volgende overwegingen wanneer u Hallo `set-body` beleid.</span><span class="sxs-lookup"><span data-stu-id="3081f-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="3081f-301">Als u van Hallo gebruikmaakt `set-body` beleid tooreturn een nieuwe of bijgewerkte instantie hoeft u niet tooset `preserveContent` te`true` omdat u de nieuwe inhoud Hallo expliciet levert.</span><span class="sxs-lookup"><span data-stu-id="3081f-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="3081f-302">Hallo-inhoud van een reactie behouden bij Hallo inkomende pijplijn logisch niet omdat er nog geen reactie is.</span><span class="sxs-lookup"><span data-stu-id="3081f-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="3081f-303">Hallo-inhoud van een aanvraag behouden in de uitgaande pijplijn Hallo logisch niet omdat Hallo aanvraag al is verzonden toohello back-end op dit moment.</span><span class="sxs-lookup"><span data-stu-id="3081f-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="3081f-304">Als dit beleid wordt gebruikt wanneer er geen berichttekst, bijvoorbeeld in een inkomende GET een uitzondering opgetreden.</span><span class="sxs-lookup"><span data-stu-id="3081f-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="3081f-305">Zie voor meer informatie, Hallo `context.Request.Body`, `context.Response.Body`, en Hallo `IMessage` secties in Hallo [Context variabele](api-management-policy-expressions.md#ContextVariables) tabel.</span><span class="sxs-lookup"><span data-stu-id="3081f-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-306">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="3081f-307">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="3081f-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="3081f-308">Voorbeeld van de letterlijke tekst</span><span class="sxs-lookup"><span data-stu-id="3081f-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="3081f-309">Voorbeeld van de toegang tot Hallo instantie als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="3081f-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="3081f-310">Houd er rekening mee dat we Hallo oorspronkelijke aanvraagtekst behouden zodat we deze later in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="3081f-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="3081f-311">Voorbeeld van de toegang tot een JObject Hallo instantie.</span><span class="sxs-lookup"><span data-stu-id="3081f-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="3081f-312">Merk op dat omdat we niet reserveren van een Hallo oorspronkelijke aanvraagtekst, toegang tot het verderop in de pijplijn Hallo zal leiden tot een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="3081f-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="3081f-313">Reactie op basis van product filteren</span><span class="sxs-lookup"><span data-stu-id="3081f-313">Filter response based on product</span></span>  
 <span data-ttu-id="3081f-314">Dit voorbeeld ziet u hoe tooperform filteren op inhoud door het verwijderen van elementen uit Hallo antwoord ontvangen van de back-endservice Hallo bij gebruik van Hallo `Starter` product.</span><span class="sxs-lookup"><span data-stu-id="3081f-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="3081f-315">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too34:30 vooruit.</span><span class="sxs-lookup"><span data-stu-id="3081f-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="3081f-316">Start op 31:50 toosee een overzicht van [Hallo donker Sky Forecast API](https://developer.forecast.io/) gebruikt voor deze demonstratie.</span><span class="sxs-lookup"><span data-stu-id="3081f-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="3081f-317">Vloeibare sjablonen gebruiken bij set-instantie</span><span class="sxs-lookup"><span data-stu-id="3081f-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="3081f-318">Hallo `set-body` beleid kan worden geconfigureerd toouse hello [vloeibare](https://shopify.github.io/liquid/basics/introduction/) templating taal tootransfom Hallo hoofdtekst van een aanvraag of antwoord.</span><span class="sxs-lookup"><span data-stu-id="3081f-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="3081f-319">Dit kan zeer effectief zijn als u toocompletely wijzigen van de vorm Hallo indeling van uw bericht moet zijn.</span><span class="sxs-lookup"><span data-stu-id="3081f-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3081f-320">implementatie van vloeistof gebruikt in Hallo Hallo `set-body` beleid is geconfigureerd in de 'C#-modus'.</span><span class="sxs-lookup"><span data-stu-id="3081f-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="3081f-321">Dit is vooral belangrijk bij het uitvoeren van bewerkingen zoals filteren.</span><span class="sxs-lookup"><span data-stu-id="3081f-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="3081f-322">Als u bijvoorbeeld met een datumfilter vereist Hallo-gebruik van Pascal hoofd- en C#-datum notatie, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3081f-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="3081f-323">{{body.foo.startDateTime| Datum: 'yyyyMMddTHH:mm:ddZ'}}</span><span class="sxs-lookup"><span data-stu-id="3081f-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3081f-324">Gebruik in volgorde toocorrectly bind tooan XML-hoofdtekst met vloeibare Hallo-sjabloon, een `set-header` beleid tooset Content-Type tooeither application/xml, text/xml (of een type eindigend op + xml); voor een JSON-hoofdtekst dit moet application/json, text/json (of een type beëindigen met + json).</span><span class="sxs-lookup"><span data-stu-id="3081f-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="3081f-325">JSON-tooSOAP met een vloeibare sjabloon converteren</span><span class="sxs-lookup"><span data-stu-id="3081f-325">Convert JSON tooSOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="3081f-326">Tranform JSON met een vloeibare sjabloon</span><span class="sxs-lookup"><span data-stu-id="3081f-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="3081f-327">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-327">Elements</span></span>  
  
|<span data-ttu-id="3081f-328">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-328">Name</span></span>|<span data-ttu-id="3081f-329">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-329">Description</span></span>|<span data-ttu-id="3081f-330">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-331">set-instantie</span><span class="sxs-lookup"><span data-stu-id="3081f-331">set-body</span></span>|<span data-ttu-id="3081f-332">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-332">Root element.</span></span> <span data-ttu-id="3081f-333">Hallo platte tekst of een expressie die het retourneert een instantie bevat.</span><span class="sxs-lookup"><span data-stu-id="3081f-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="3081f-334">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="3081f-335">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="3081f-335">Properties</span></span>  
  
|<span data-ttu-id="3081f-336">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-336">Name</span></span>|<span data-ttu-id="3081f-337">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-337">Description</span></span>|<span data-ttu-id="3081f-338">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-338">Required</span></span>|<span data-ttu-id="3081f-339">Standaard</span><span class="sxs-lookup"><span data-stu-id="3081f-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3081f-340">sjabloon</span><span class="sxs-lookup"><span data-stu-id="3081f-340">template</span></span>|<span data-ttu-id="3081f-341">In de set hoofdtekst beleid Hallo gebruikte toochange hello templating modus uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3081f-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="3081f-342">Op dit moment is alleen ondersteund Hallo-waarde:</span><span class="sxs-lookup"><span data-stu-id="3081f-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="3081f-343">Hallo - vloeibare - set hoofdtekst beleid wordt Hallo vloeibare templating-engine gebruikt</span><span class="sxs-lookup"><span data-stu-id="3081f-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="3081f-344">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-344">No</span></span>|<span data-ttu-id="3081f-345">vloeistof</span><span class="sxs-lookup"><span data-stu-id="3081f-345">liquid</span></span>|  

<span data-ttu-id="3081f-346">Voor toegang tot informatie over het Hallo-aanvraag en -antwoord, kunt Hallo vloeibare sjabloon tooa context-object met de volgende eigenschappen Hallo binden:</span><span class="sxs-lookup"><span data-stu-id="3081f-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="3081f-347">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-347">Usage</span></span>  
 <span data-ttu-id="3081f-348">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-349">**Beleid secties:** inkomend, uitgaand back-end</span><span class="sxs-lookup"><span data-stu-id="3081f-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="3081f-350">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-351"><a name="SetHTTPheader"></a>Set HTTP-header</span><span class="sxs-lookup"><span data-stu-id="3081f-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="3081f-352">Hallo `set-header` beleid wijst een waarde tooan bestaande antwoord en/of de aanvraag-header of voegt een nieuwe antwoord en/of de aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="3081f-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="3081f-353">Voegt een lijst met HTTP-headers in een HTTP-bericht.</span><span class="sxs-lookup"><span data-stu-id="3081f-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="3081f-354">Wanneer in een inkomende pijplijn geplaatst, wordt dit beleid ingesteld Hallo HTTP-headers voor aanvraag van Hallo toohello doelservice doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="3081f-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="3081f-355">Wanneer in een uitgaande pijplijn geplaatst, wordt dit beleid ingesteld Hallo HTTP-headers voor antwoord Hallo toohello gatewayclient worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="3081f-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-356">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="3081f-357">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="3081f-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="3081f-358">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="3081f-359">Context informatie toohello back-endservice doorsturen</span><span class="sxs-lookup"><span data-stu-id="3081f-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="3081f-360">Dit voorbeeld toont hoe beleid voor tooapply Hallo API toosupply context informatie toohello back-endservice niveau.</span><span class="sxs-lookup"><span data-stu-id="3081f-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="3081f-361">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too10:30 vooruit.</span><span class="sxs-lookup"><span data-stu-id="3081f-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="3081f-362">Bij 12:10 is er een demo voor het aanroepen van een bewerking in de ontwikkelaarsportal Hallo waar u Hallo-beleid op het werk kunt zien.</span><span class="sxs-lookup"><span data-stu-id="3081f-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="3081f-363">Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="3081f-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="3081f-364">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-364">Elements</span></span>  
  
|<span data-ttu-id="3081f-365">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-365">Name</span></span>|<span data-ttu-id="3081f-366">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-366">Description</span></span>|<span data-ttu-id="3081f-367">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-368">set-header</span><span class="sxs-lookup"><span data-stu-id="3081f-368">set-header</span></span>|<span data-ttu-id="3081f-369">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-369">Root element.</span></span>|<span data-ttu-id="3081f-370">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-370">Yes</span></span>|  
|<span data-ttu-id="3081f-371">waarde</span><span class="sxs-lookup"><span data-stu-id="3081f-371">value</span></span>|<span data-ttu-id="3081f-372">Hiermee wordt de waarde Hallo van Hallo header toobe set.</span><span class="sxs-lookup"><span data-stu-id="3081f-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="3081f-373">Voor meerdere headers met de Hallo dezelfde naam toevoegen extra `value` elementen.</span><span class="sxs-lookup"><span data-stu-id="3081f-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="3081f-374">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="3081f-375">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="3081f-375">Properties</span></span>  
  
|<span data-ttu-id="3081f-376">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-376">Name</span></span>|<span data-ttu-id="3081f-377">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-377">Description</span></span>|<span data-ttu-id="3081f-378">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-378">Required</span></span>|<span data-ttu-id="3081f-379">Standaard</span><span class="sxs-lookup"><span data-stu-id="3081f-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3081f-380">Er bestaat actie</span><span class="sxs-lookup"><span data-stu-id="3081f-380">exists-action</span></span>|<span data-ttu-id="3081f-381">Geeft aan welke actie tootake Hallo-header is al opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3081f-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="3081f-382">Dit kenmerk moet een van de volgende waarden Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="3081f-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="3081f-383">-onderdrukkingswaarde - vervangt Hallo van bestaande Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="3081f-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="3081f-384">-skip - vervangen Hallo bestaande header-waarde niet.</span><span class="sxs-lookup"><span data-stu-id="3081f-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="3081f-385">-toevoeg - Hallo waarde toohello bestaande header-waarde wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3081f-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="3081f-386">Hallo-header verwijdert - delete - van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="3081f-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="3081f-387">Als de waarde te`override` opnemen van meerdere vermeldingen met Hallo dezelfde resulteert in het Hallo-header wordt ingesteld volgens tooall-vermeldingen (die wordt vermeld meerdere keren) naam; alleen de vermelde waarden worden ingesteld in Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="3081f-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="3081f-388">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-388">No</span></span>|<span data-ttu-id="3081f-389">overschrijven</span><span class="sxs-lookup"><span data-stu-id="3081f-389">override</span></span>|  
|<span data-ttu-id="3081f-390">naam</span><span class="sxs-lookup"><span data-stu-id="3081f-390">name</span></span>|<span data-ttu-id="3081f-391">Geeft de naam van Hallo header toobe set.</span><span class="sxs-lookup"><span data-stu-id="3081f-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="3081f-392">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-392">Yes</span></span>|<span data-ttu-id="3081f-393">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3081f-394">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-394">Usage</span></span>  
 <span data-ttu-id="3081f-395">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-396">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="3081f-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3081f-397">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-398"><a name="SetQueryStringParameter"></a>Querytekenreeksparameter instellen</span><span class="sxs-lookup"><span data-stu-id="3081f-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="3081f-399">Hallo `set-query-parameter` beleid wordt toegevoegd, vervangt de waarde van, of verwijderingen querytekenreeksparameter aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3081f-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="3081f-400">Kan worden gebruikt toopass werd verwacht door de back-endservice Hallo queryparameters die zijn optioneel of nooit aanwezig zijn op Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="3081f-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-401">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="3081f-402">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="3081f-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="3081f-403">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="3081f-404">Context informatie toohello back-endservice doorsturen</span><span class="sxs-lookup"><span data-stu-id="3081f-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="3081f-405">Dit voorbeeld toont hoe beleid voor tooapply Hallo API toosupply context informatie toohello back-endservice niveau.</span><span class="sxs-lookup"><span data-stu-id="3081f-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="3081f-406">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too10:30 vooruit.</span><span class="sxs-lookup"><span data-stu-id="3081f-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="3081f-407">Bij 12:10 is er een demo voor het aanroepen van een bewerking in de ontwikkelaarsportal Hallo waar u Hallo-beleid op het werk kunt zien.</span><span class="sxs-lookup"><span data-stu-id="3081f-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="3081f-408">Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="3081f-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="3081f-409">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-409">Elements</span></span>  
  
|<span data-ttu-id="3081f-410">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-410">Name</span></span>|<span data-ttu-id="3081f-411">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-411">Description</span></span>|<span data-ttu-id="3081f-412">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-413">query-set-parameter</span><span class="sxs-lookup"><span data-stu-id="3081f-413">set-query-parameter</span></span>|<span data-ttu-id="3081f-414">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-414">Root element.</span></span>|<span data-ttu-id="3081f-415">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-415">Yes</span></span>|  
|<span data-ttu-id="3081f-416">waarde</span><span class="sxs-lookup"><span data-stu-id="3081f-416">value</span></span>|<span data-ttu-id="3081f-417">Hiermee geeft u Hallo-waarde van Hallo query parameterset toobe.</span><span class="sxs-lookup"><span data-stu-id="3081f-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="3081f-418">Voor meerdere queryparameters Hello dezelfde naam toevoegen extra `value` elementen.</span><span class="sxs-lookup"><span data-stu-id="3081f-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="3081f-419">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="3081f-420">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="3081f-420">Properties</span></span>  
  
|<span data-ttu-id="3081f-421">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-421">Name</span></span>|<span data-ttu-id="3081f-422">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-422">Description</span></span>|<span data-ttu-id="3081f-423">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-423">Required</span></span>|<span data-ttu-id="3081f-424">Standaard</span><span class="sxs-lookup"><span data-stu-id="3081f-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3081f-425">Er bestaat actie</span><span class="sxs-lookup"><span data-stu-id="3081f-425">exists-action</span></span>|<span data-ttu-id="3081f-426">Geeft aan welke actie tootake Hallo queryparameter is al opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3081f-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="3081f-427">Dit kenmerk moet een van de volgende waarden Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="3081f-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="3081f-428">-onderdrukkingswaarde - vervangt Hallo van bestaande Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="3081f-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="3081f-429">-skip - vervangen Hallo waarde van de bestaande queryparameter niet.</span><span class="sxs-lookup"><span data-stu-id="3081f-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="3081f-430">-toevoeg - voegt Hallo waarde toohello bestaande waarde van de queryparameter.</span><span class="sxs-lookup"><span data-stu-id="3081f-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="3081f-431">de queryparameter Hallo verwijdert - delete - uit Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="3081f-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="3081f-432">Als de waarde te`override` opnemen van meerdere vermeldingen met Hallo dezelfde resulteert in een queryparameter hello wordt ingesteld volgens tooall-vermeldingen (die wordt vermeld meerdere keren) naam; alleen de vermelde waarden worden ingesteld in Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="3081f-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="3081f-433">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-433">No</span></span>|<span data-ttu-id="3081f-434">overschrijven</span><span class="sxs-lookup"><span data-stu-id="3081f-434">override</span></span>|  
|<span data-ttu-id="3081f-435">naam</span><span class="sxs-lookup"><span data-stu-id="3081f-435">name</span></span>|<span data-ttu-id="3081f-436">Geeft de naam van Hallo query parameterset toobe.</span><span class="sxs-lookup"><span data-stu-id="3081f-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="3081f-437">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-437">Yes</span></span>|<span data-ttu-id="3081f-438">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3081f-439">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-439">Usage</span></span>  
 <span data-ttu-id="3081f-440">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-441">**Beleid secties:** back-end voor binnenkomend verkeer</span><span class="sxs-lookup"><span data-stu-id="3081f-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="3081f-442">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-443"><a name="RewriteURL"></a>Herschrijven van URL 's</span><span class="sxs-lookup"><span data-stu-id="3081f-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="3081f-444">Hallo `rewrite-uri` beleid zet een aanvraag-URL van de openbare formulier toohello vorm verwacht door de webservice hello, zoals wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="3081f-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="3081f-445">Openbare URL-`http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="3081f-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="3081f-446">Aanvraag-URL-`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="3081f-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="3081f-447">Dit beleid kan worden gebruikt wanneer een menselijke en/of beschrijvende browser-URL moet worden omgezet in URL-indeling Hallo werd verwacht door de webservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="3081f-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="3081f-448">Dit beleid moet alleen toegepast wanneer een andere URL-indeling, zoals schone URL's, RESTful-URL's, gebruiksvriendelijke URL's of Zoekmachineoptimalisatie gebruiksvriendelijke URL's die zijn uitsluitend structurele URL's die niet een queryreeks bevatten en in plaats daarvan bevatten alleen Hallo pad Hallo blootstellen toobe resource (na Hallo schema- en Hallo).</span><span class="sxs-lookup"><span data-stu-id="3081f-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="3081f-449">Dit wordt vaak gedaan voor fraaie uiterlijk, bruikbaarheid of zoekmachine optimaliseringsdoeleinden (Zoekmachineoptimalisatie).</span><span class="sxs-lookup"><span data-stu-id="3081f-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3081f-450">U kunt alleen queryreeksparameters met behulp van Hallo beleid toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3081f-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="3081f-451">U kunt geen toevoegen extra Sjabloonparameters pad in Hallo herschrijven van URL's.</span><span class="sxs-lookup"><span data-stu-id="3081f-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="3081f-452">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="3081f-453">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="3081f-454">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-454">Elements</span></span>  
  
|<span data-ttu-id="3081f-455">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-455">Name</span></span>|<span data-ttu-id="3081f-456">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-456">Description</span></span>|<span data-ttu-id="3081f-457">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-458">Herschrijf-uri</span><span class="sxs-lookup"><span data-stu-id="3081f-458">rewrite-uri</span></span>|<span data-ttu-id="3081f-459">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-459">Root element.</span></span>|<span data-ttu-id="3081f-460">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3081f-461">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="3081f-461">Attributes</span></span>  
  
|<span data-ttu-id="3081f-462">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="3081f-462">Attribute</span></span>|<span data-ttu-id="3081f-463">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-463">Description</span></span>|<span data-ttu-id="3081f-464">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-464">Required</span></span>|<span data-ttu-id="3081f-465">Standaard</span><span class="sxs-lookup"><span data-stu-id="3081f-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3081f-466">sjabloon</span><span class="sxs-lookup"><span data-stu-id="3081f-466">template</span></span>|<span data-ttu-id="3081f-467">Hallo werkelijke webservice-URL met een queryreeks-parameters.</span><span class="sxs-lookup"><span data-stu-id="3081f-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="3081f-468">Bij gebruik van expressies moet Hallo gehele getal een expressie.</span><span class="sxs-lookup"><span data-stu-id="3081f-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="3081f-469">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-469">Yes</span></span>|<span data-ttu-id="3081f-470">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3081f-470">N/A</span></span>|  
|<span data-ttu-id="3081f-471">kopiëren niet-overeenkomende parameters</span><span class="sxs-lookup"><span data-stu-id="3081f-471">copy-unmatched-params</span></span>|<span data-ttu-id="3081f-472">Geeft aan of binnenkomende aanvraag Hallo niet aanwezig in de oorspronkelijke URL sjabloon Hallo queryparameters toohello URL die is gedefinieerd door Hallo herschrijven sjabloon worden toegevoegd</span><span class="sxs-lookup"><span data-stu-id="3081f-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="3081f-473">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-473">No</span></span>|<span data-ttu-id="3081f-474">De waarde True</span><span class="sxs-lookup"><span data-stu-id="3081f-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3081f-475">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-475">Usage</span></span>  
 <span data-ttu-id="3081f-476">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-477">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="3081f-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="3081f-478">**Beleid scopes:** product, API-bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="3081f-479"><a name="XSLTransform"></a>XML met behulp van een XSLT transformeren</span><span class="sxs-lookup"><span data-stu-id="3081f-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="3081f-480">Hallo `Transform XML using an XSLT` beleid van toepassing is een XSL-transformatie tooXML in de hoofdtekst van de aanvraag of antwoord van de Hallo.</span><span class="sxs-lookup"><span data-stu-id="3081f-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3081f-481">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="3081f-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="3081f-482">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3081f-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="3081f-483">Elementen</span><span class="sxs-lookup"><span data-stu-id="3081f-483">Elements</span></span>  
  
|<span data-ttu-id="3081f-484">Naam</span><span class="sxs-lookup"><span data-stu-id="3081f-484">Name</span></span>|<span data-ttu-id="3081f-485">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3081f-485">Description</span></span>|<span data-ttu-id="3081f-486">Vereist</span><span class="sxs-lookup"><span data-stu-id="3081f-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3081f-487">XSL-transformatie</span><span class="sxs-lookup"><span data-stu-id="3081f-487">xsl-transform</span></span>|<span data-ttu-id="3081f-488">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="3081f-488">Root element.</span></span>|<span data-ttu-id="3081f-489">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-489">Yes</span></span>|  
|<span data-ttu-id="3081f-490">Parameter</span><span class="sxs-lookup"><span data-stu-id="3081f-490">parameter</span></span>|<span data-ttu-id="3081f-491">Gebruikte toodefine variabelen die worden gebruikt in Hallo transformatie</span><span class="sxs-lookup"><span data-stu-id="3081f-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="3081f-492">Nee</span><span class="sxs-lookup"><span data-stu-id="3081f-492">No</span></span>|  
|<span data-ttu-id="3081f-493">xsl: Stylesheet</span><span class="sxs-lookup"><span data-stu-id="3081f-493">xsl:stylesheet</span></span>|<span data-ttu-id="3081f-494">Hoofdelement opmaakmodel.</span><span class="sxs-lookup"><span data-stu-id="3081f-494">Root stylesheet element.</span></span> <span data-ttu-id="3081f-495">Alle elementen en kenmerken die zijn gedefinieerd binnen Volg Hallo standaard [XSLT-specificatie](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="3081f-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="3081f-496">Ja</span><span class="sxs-lookup"><span data-stu-id="3081f-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3081f-497">Gebruik</span><span class="sxs-lookup"><span data-stu-id="3081f-497">Usage</span></span>  
 <span data-ttu-id="3081f-498">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3081f-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3081f-499">**Beleid secties:** binnenkomende, uitgaande</span><span class="sxs-lookup"><span data-stu-id="3081f-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="3081f-500">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="3081f-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="3081f-501">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3081f-501">Next steps</span></span>
<span data-ttu-id="3081f-502">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3081f-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
