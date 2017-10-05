---
title: Azure API Management-claimtransformatiebeleidsinstellingen | Microsoft Docs
description: Meer informatie over de claimtransformatiebeleidsinstellingen beschikbaar voor gebruik in Azure API Management.
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
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="b1270-103">API Management-beleidsregels voor transformatie</span><span class="sxs-lookup"><span data-stu-id="b1270-103">API Management transformation policies</span></span>
<span data-ttu-id="b1270-104">Dit onderwerp bevat een verwijzing voor de volgende API Management-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="b1270-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="b1270-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="b1270-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="b1270-106"><a name="TransformationPolicies"></a>Claimtransformatiebeleidsinstellingen</span><span class="sxs-lookup"><span data-stu-id="b1270-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="b1270-107">[JSON converteren naar XML](api-management-transformation-policies.md#ConvertJSONtoXML) : zet aanvraag of antwoord body van JSON naar XML.</span><span class="sxs-lookup"><span data-stu-id="b1270-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="b1270-108">[XML niet converteren naar JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : zet aanvraag of antwoord body van XML naar JSON.</span><span class="sxs-lookup"><span data-stu-id="b1270-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="b1270-109">[Zoeken en vervangen tekenreeks in de hoofdtekst](api-management-transformation-policies.md#Findandreplacestringinbody) - zoeken naar een subtekenreeks aanvraag of antwoord en wordt vervangen door een andere subtekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b1270-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="b1270-110">[URL's in de inhoud te maskeren](api-management-transformation-policies.md#MaskURLSContent) -koppelingen herschrijft (maskers) in het antwoord body zodat deze naar de equivalente koppeling via de gateway verwijzen.</span><span class="sxs-lookup"><span data-stu-id="b1270-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="b1270-111">[Stel de back-endservice](api-management-transformation-policies.md#SetBackendService) -wijzigingen van de back-endservice voor de binnenkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b1270-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="b1270-112">[Instantie ingesteld](api-management-transformation-policies.md#SetBody) -Hiermee stelt u de berichttekst voor binnenkomende en uitgaande aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b1270-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="b1270-113">[Set HTTP-header](api-management-transformation-policies.md#SetHTTPheader) : een waarde wordt toegewezen aan een bestaande antwoord en/of de aanvraag-header of voegt een nieuwe antwoord en/of de aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="b1270-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="b1270-114">[Querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) - wordt toegevoegd, vervangt de waarde van of verwijderd van de aanvraag queryreeksparameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="b1270-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="b1270-115">[Herschrijven van URL](api-management-transformation-policies.md#RewriteURL) -converteert van een aanvraag-URL van de openbare vorm aan het formulier dat werd verwacht door de webservice.</span><span class="sxs-lookup"><span data-stu-id="b1270-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="b1270-116">[XML met behulp van een XSLT transformeren](api-management-transformation-policies.md#XSLTransform) -geldt een XSL-transformatie voor XML in de hoofdtekst van de aanvraag of antwoord.</span><span class="sxs-lookup"><span data-stu-id="b1270-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="b1270-117"><a name="ConvertJSONtoXML"></a>JSON naar XML converteren</span><span class="sxs-lookup"><span data-stu-id="b1270-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="b1270-118">De `json-to-xml` beleid converteert de hoofdtekst van een aanvraag of antwoord van JSON naar XML.</span><span class="sxs-lookup"><span data-stu-id="b1270-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-119">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="b1270-120">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="b1270-121">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-121">Elements</span></span>  
  
|<span data-ttu-id="b1270-122">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-122">Name</span></span>|<span data-ttu-id="b1270-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-123">Description</span></span>|<span data-ttu-id="b1270-124">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-125">JSON-to-xml</span><span class="sxs-lookup"><span data-stu-id="b1270-125">json-to-xml</span></span>|<span data-ttu-id="b1270-126">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-126">Root element.</span></span>|<span data-ttu-id="b1270-127">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b1270-128">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="b1270-128">Attributes</span></span>  
  
|<span data-ttu-id="b1270-129">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-129">Name</span></span>|<span data-ttu-id="b1270-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-130">Description</span></span>|<span data-ttu-id="b1270-131">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-131">Required</span></span>|<span data-ttu-id="b1270-132">Standaard</span><span class="sxs-lookup"><span data-stu-id="b1270-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b1270-133">toepassen</span><span class="sxs-lookup"><span data-stu-id="b1270-133">apply</span></span>|<span data-ttu-id="b1270-134">Het kenmerk moet worden ingesteld op een van de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="b1270-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="b1270-135">conversie - altijd - altijd van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1270-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="b1270-136">convert-inhoud type-json - alleen als response Content-Type-header aanwezigheid van JSON aangeeft.</span><span class="sxs-lookup"><span data-stu-id="b1270-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="b1270-137">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-137">Yes</span></span>|<span data-ttu-id="b1270-138">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-138">N/A</span></span>|  
|<span data-ttu-id="b1270-139">Overweeg-accepteren-header</span><span class="sxs-lookup"><span data-stu-id="b1270-139">consider-accept-header</span></span>|<span data-ttu-id="b1270-140">Het kenmerk moet worden ingesteld op een van de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="b1270-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="b1270-141">-waar - conversie van toepassing als JSON is aangevraagd in aanvraag Accept-header.</span><span class="sxs-lookup"><span data-stu-id="b1270-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="b1270-142">-ONWAAR - conversie altijd van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1270-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="b1270-143">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-143">No</span></span>|<span data-ttu-id="b1270-144">De waarde True</span><span class="sxs-lookup"><span data-stu-id="b1270-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b1270-145">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-145">Usage</span></span>  
 <span data-ttu-id="b1270-146">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-147">**Beleid secties:** binnenkomende, uitgaande, bij fouten</span><span class="sxs-lookup"><span data-stu-id="b1270-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="b1270-148">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-149"><a name="ConvertXMLtoJSON"></a>XML niet converteren naar JSON</span><span class="sxs-lookup"><span data-stu-id="b1270-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="b1270-150">De `xml-to-json` beleid converteert de hoofdtekst van een aanvraag of antwoord van XML naar JSON.</span><span class="sxs-lookup"><span data-stu-id="b1270-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="b1270-151">Dit beleid kan worden gebruikt voor API's op basis van de back-end van een alleen-XML-webservices moderniseren.</span><span class="sxs-lookup"><span data-stu-id="b1270-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-152">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="b1270-153">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="b1270-154">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-154">Elements</span></span>  
  
|<span data-ttu-id="b1270-155">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-155">Name</span></span>|<span data-ttu-id="b1270-156">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-156">Description</span></span>|<span data-ttu-id="b1270-157">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-158">XML-json-</span><span class="sxs-lookup"><span data-stu-id="b1270-158">xml-to-json</span></span>|<span data-ttu-id="b1270-159">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-159">Root element.</span></span>|<span data-ttu-id="b1270-160">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b1270-161">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="b1270-161">Attributes</span></span>  
  
|<span data-ttu-id="b1270-162">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-162">Name</span></span>|<span data-ttu-id="b1270-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-163">Description</span></span>|<span data-ttu-id="b1270-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-164">Required</span></span>|<span data-ttu-id="b1270-165">Standaard</span><span class="sxs-lookup"><span data-stu-id="b1270-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b1270-166">type</span><span class="sxs-lookup"><span data-stu-id="b1270-166">kind</span></span>|<span data-ttu-id="b1270-167">Het kenmerk moet worden ingesteld op een van de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="b1270-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="b1270-168">-javascript-vriendelijk - de geconverteerde JSON heeft een formulier beschrijvende voor ontwikkelaars van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b1270-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="b1270-169">de geconverteerde JSON weerspiegelt - direct - structuur van het oorspronkelijke XML-document.</span><span class="sxs-lookup"><span data-stu-id="b1270-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="b1270-170">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-170">Yes</span></span>|<span data-ttu-id="b1270-171">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-171">N/A</span></span>|  
|<span data-ttu-id="b1270-172">toepassen</span><span class="sxs-lookup"><span data-stu-id="b1270-172">apply</span></span>|<span data-ttu-id="b1270-173">Het kenmerk moet worden ingesteld op een van de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="b1270-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="b1270-174">-altijd - altijd converteren.</span><span class="sxs-lookup"><span data-stu-id="b1270-174">-   always - convert always.</span></span><br /><span data-ttu-id="b1270-175">convert - inhoud-type-xml - alleen als response Content-Type-header aanwezigheid van XML aangeeft.</span><span class="sxs-lookup"><span data-stu-id="b1270-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="b1270-176">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-176">Yes</span></span>|<span data-ttu-id="b1270-177">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-177">N/A</span></span>|  
|<span data-ttu-id="b1270-178">Overweeg-accepteren-header</span><span class="sxs-lookup"><span data-stu-id="b1270-178">consider-accept-header</span></span>|<span data-ttu-id="b1270-179">Het kenmerk moet worden ingesteld op een van de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="b1270-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="b1270-180">-waar - conversie van toepassing als XML is aangevraagd in aanvraag Accept-header.</span><span class="sxs-lookup"><span data-stu-id="b1270-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="b1270-181">-ONWAAR - conversie altijd van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1270-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="b1270-182">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-182">No</span></span>|<span data-ttu-id="b1270-183">De waarde True</span><span class="sxs-lookup"><span data-stu-id="b1270-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b1270-184">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-184">Usage</span></span>  
 <span data-ttu-id="b1270-185">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-186">**Beleid secties:** binnenkomende, uitgaande, bij fouten</span><span class="sxs-lookup"><span data-stu-id="b1270-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="b1270-187">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-188"><a name="Findandreplacestringinbody"></a>Zoeken en vervangen tekenreeks in de hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="b1270-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="b1270-189">De `find-and-replace` beleid vindt u een aanvraag of antwoord subtekenreeks en vervangen door een andere subtekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b1270-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-190">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="b1270-191">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="b1270-192">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-192">Elements</span></span>  
  
|<span data-ttu-id="b1270-193">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-193">Name</span></span>|<span data-ttu-id="b1270-194">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-194">Description</span></span>|<span data-ttu-id="b1270-195">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-196">zoeken en vervangen</span><span class="sxs-lookup"><span data-stu-id="b1270-196">find-and-replace</span></span>|<span data-ttu-id="b1270-197">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-197">Root element.</span></span>|<span data-ttu-id="b1270-198">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b1270-199">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="b1270-199">Attributes</span></span>  
  
|<span data-ttu-id="b1270-200">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-200">Name</span></span>|<span data-ttu-id="b1270-201">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-201">Description</span></span>|<span data-ttu-id="b1270-202">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-202">Required</span></span>|<span data-ttu-id="b1270-203">Standaard</span><span class="sxs-lookup"><span data-stu-id="b1270-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b1270-204">Van</span><span class="sxs-lookup"><span data-stu-id="b1270-204">from</span></span>|<span data-ttu-id="b1270-205">De tekenreeks om naar te zoeken.</span><span class="sxs-lookup"><span data-stu-id="b1270-205">The string to search for.</span></span>|<span data-ttu-id="b1270-206">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-206">Yes</span></span>|<span data-ttu-id="b1270-207">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-207">N/A</span></span>|  
|<span data-ttu-id="b1270-208">tot</span><span class="sxs-lookup"><span data-stu-id="b1270-208">to</span></span>|<span data-ttu-id="b1270-209">De vervangende tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b1270-209">The replacement string.</span></span> <span data-ttu-id="b1270-210">Geef de vervangende tekenreekslengte van nul als u wilt verwijderen van de zoekreeks.</span><span class="sxs-lookup"><span data-stu-id="b1270-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="b1270-211">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-211">Yes</span></span>|<span data-ttu-id="b1270-212">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b1270-213">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-213">Usage</span></span>  
 <span data-ttu-id="b1270-214">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-215">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="b1270-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="b1270-216">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-217"><a name="MaskURLSContent"></a>Masker URL's in de inhoud</span><span class="sxs-lookup"><span data-stu-id="b1270-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="b1270-218">De `redirect-content-urls` beleid herschrijft koppelingen in de hoofdtekst van antwoord (maskers) zodat deze naar de equivalente koppeling via de gateway verwijzen.</span><span class="sxs-lookup"><span data-stu-id="b1270-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="b1270-219">Gebruik in de sectie uitgaande antwoord hoofdtekst koppelingen zodat deze verwijzen naar de gateway opnieuw te schrijven.</span><span class="sxs-lookup"><span data-stu-id="b1270-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="b1270-220">Gebruik in de binnenkomende sectie voor een tegenovergestelde effect.</span><span class="sxs-lookup"><span data-stu-id="b1270-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b1270-221">Dit beleid verandert niet een headerwaarden, zoals `Location` headers.</span><span class="sxs-lookup"><span data-stu-id="b1270-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="b1270-222">Koptekst om waarden te wijzigen, gebruikt u de [set-header](api-management-transformation-policies.md#SetHTTPheader) beleid.</span><span class="sxs-lookup"><span data-stu-id="b1270-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-223">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="b1270-224">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="b1270-225">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-225">Elements</span></span>  
  
|<span data-ttu-id="b1270-226">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-226">Name</span></span>|<span data-ttu-id="b1270-227">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-227">Description</span></span>|<span data-ttu-id="b1270-228">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-229">Omleidings-inhoud-URL 's</span><span class="sxs-lookup"><span data-stu-id="b1270-229">redirect-content-urls</span></span>|<span data-ttu-id="b1270-230">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-230">Root element.</span></span>|<span data-ttu-id="b1270-231">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b1270-232">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-232">Usage</span></span>  
 <span data-ttu-id="b1270-233">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-234">**Beleid secties:** binnenkomende, uitgaande</span><span class="sxs-lookup"><span data-stu-id="b1270-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="b1270-235">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-236"><a name="SetBackendService"></a>Back-end-service instellen</span><span class="sxs-lookup"><span data-stu-id="b1270-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="b1270-237">Gebruik de `set-backend-service` beleid een inkomende aanvraag omleiden naar een andere back-end dan de opgegeven in de API-instellingen voor de bewerking.</span><span class="sxs-lookup"><span data-stu-id="b1270-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="b1270-238">Dit beleid verandert de back-end service basis-URL van de inkomende aanvraag in de versie opgegeven in het beleid.</span><span class="sxs-lookup"><span data-stu-id="b1270-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-239">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="b1270-240">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-240">Example</span></span>  
  
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
<span data-ttu-id="b1270-241">In dit voorbeeld routeert set back-end service beleid aanvragen op basis van de versiewaarde in de queryreeks doorgegeven aan een andere back-endservice dan een opgegeven in de API.</span><span class="sxs-lookup"><span data-stu-id="b1270-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="b1270-242">In eerste instantie is de back-end service basis-URL afgeleid van de instellingen voor de API.</span><span class="sxs-lookup"><span data-stu-id="b1270-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="b1270-243">Dus de aanvraag-URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` wordt `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` waar `http://contoso.com/api/10.4/` is de back-end-service-URL opgegeven in de API-instellingen.</span><span class="sxs-lookup"><span data-stu-id="b1270-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="b1270-244">Wanneer de [< kiezen\> ](api-management-advanced-policies.md#choose) beleidsverklaring wordt toegepast. de back-end service basis-URL mag wijzigen opnieuw toekennen aan `http://contoso.com/api/8.2` of `http://contoso.com/api/9.1`, afhankelijk van de waarde van de queryparameter van de versie-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b1270-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="b1270-245">Bijvoorbeeld, als de waarde is `"2013-15"` de laatste aanvraag URL wordt `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="b1270-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="b1270-246">Als verdere transformatie van de aanvraag gewenste, andere is [claimtransformatiebeleidsinstellingen](api-management-transformation-policies.md#TransformationPolicies) kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b1270-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="b1270-247">Om bijvoorbeeld te verwijderen van de version-queryparameter nu dat de aanvraag wordt gerouteerd naar een versie specifieke back-end van de [querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) beleid kan worden gebruikt voor het versiekenmerk nu redundante verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b1270-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="b1270-248">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-248">Example</span></span>  
  
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
<span data-ttu-id="b1270-249">In dit voorbeeld stuurt het beleid voor de aanvraag door naar een service fabric back-end van de queryreeks userId gebruikt als de partitiesleutel en de primaire replica van de partitie.</span><span class="sxs-lookup"><span data-stu-id="b1270-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="b1270-250">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-250">Elements</span></span>  
  
|<span data-ttu-id="b1270-251">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-251">Name</span></span>|<span data-ttu-id="b1270-252">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-252">Description</span></span>|<span data-ttu-id="b1270-253">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-254">set-back-end-service</span><span class="sxs-lookup"><span data-stu-id="b1270-254">set-backend-service</span></span>|<span data-ttu-id="b1270-255">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-255">Root element.</span></span>|<span data-ttu-id="b1270-256">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b1270-257">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="b1270-257">Attributes</span></span>  
  
|<span data-ttu-id="b1270-258">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-258">Name</span></span>|<span data-ttu-id="b1270-259">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-259">Description</span></span>|<span data-ttu-id="b1270-260">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-260">Required</span></span>|<span data-ttu-id="b1270-261">Standaard</span><span class="sxs-lookup"><span data-stu-id="b1270-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b1270-262">basis-url</span><span class="sxs-lookup"><span data-stu-id="b1270-262">base-url</span></span>|<span data-ttu-id="b1270-263">Nieuwe back-end service basis-URL.</span><span class="sxs-lookup"><span data-stu-id="b1270-263">New backend service base URL.</span></span>|<span data-ttu-id="b1270-264">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-264">No</span></span>|<span data-ttu-id="b1270-265">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-265">N/A</span></span>|  
|<span data-ttu-id="b1270-266">back-end-id</span><span class="sxs-lookup"><span data-stu-id="b1270-266">backend-id</span></span>|<span data-ttu-id="b1270-267">Id van de back-end om naar te routeren.</span><span class="sxs-lookup"><span data-stu-id="b1270-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="b1270-268">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-268">No</span></span>|<span data-ttu-id="b1270-269">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-269">N/A</span></span>|  
|<span data-ttu-id="b1270-270">SF partitiesleutel</span><span class="sxs-lookup"><span data-stu-id="b1270-270">sf-partition-key</span></span>|<span data-ttu-id="b1270-271">Alleen van toepassing wanneer de back-end een Service Fabric-service is en wordt opgegeven met behulp van back-end-id.</span><span class="sxs-lookup"><span data-stu-id="b1270-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="b1270-272">Gebruikt voor het omzetten van een specifieke partitie van de service voor naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="b1270-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="b1270-273">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-273">No</span></span>|<span data-ttu-id="b1270-274">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-274">N/A</span></span>|  
|<span data-ttu-id="b1270-275">SF-replica-type</span><span class="sxs-lookup"><span data-stu-id="b1270-275">sf-replica-type</span></span>|<span data-ttu-id="b1270-276">Alleen van toepassing wanneer de back-end een Service Fabric-service is en wordt opgegeven met behulp van back-end-id.</span><span class="sxs-lookup"><span data-stu-id="b1270-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="b1270-277">Bepaalt of de aanvraag moet gaan naar de primaire of secundaire replica van een partitie.</span><span class="sxs-lookup"><span data-stu-id="b1270-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="b1270-278">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-278">No</span></span>|<span data-ttu-id="b1270-279">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-279">N/A</span></span>|    
|<span data-ttu-id="b1270-280">SF-resolve-voorwaarde</span><span class="sxs-lookup"><span data-stu-id="b1270-280">sf-resolve-condition</span></span>|<span data-ttu-id="b1270-281">Alleen van toepassing wanneer de back-end een Service Fabric-service is.</span><span class="sxs-lookup"><span data-stu-id="b1270-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="b1270-282">Voorwaarde te identificeren als de aanroep naar Service Fabric-back-end moet worden herhaald met nieuwe resolutie.</span><span class="sxs-lookup"><span data-stu-id="b1270-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="b1270-283">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-283">No</span></span>|<span data-ttu-id="b1270-284">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-284">N/A</span></span>|    
|<span data-ttu-id="b1270-285">SF-service-exemplaar-name</span><span class="sxs-lookup"><span data-stu-id="b1270-285">sf-service-instance-name</span></span>|<span data-ttu-id="b1270-286">Alleen van toepassing wanneer de back-end een Service Fabric-service is.</span><span class="sxs-lookup"><span data-stu-id="b1270-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="b1270-287">Kan service-exemplaren tijdens runtime te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b1270-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="b1270-288">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-288">No</span></span>|<span data-ttu-id="b1270-289">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="b1270-290">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-290">Usage</span></span>  
 <span data-ttu-id="b1270-291">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-292">**Beleid secties:** back-end voor binnenkomend verkeer</span><span class="sxs-lookup"><span data-stu-id="b1270-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="b1270-293">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-294"><a name="SetBody"></a>Set-instantie</span><span class="sxs-lookup"><span data-stu-id="b1270-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="b1270-295">Gebruik de `set-body` in te stellen van de berichttekst voor binnenkomende en uitgaande aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b1270-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="b1270-296">Voor toegang tot de berichttekst kunt u de `context.Request.Body` eigenschap of de `context.Response.Body`, afhankelijk van of het beleid is in de sectie binnenkomend of uitgaand.</span><span class="sxs-lookup"><span data-stu-id="b1270-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="b1270-297">Opmerking die standaard bij het openen van het bericht met behulp van body `context.Request.Body` of `context.Response.Body`, de oorspronkelijke berichttekst verloren en wordt door te retourneren van de hoofdtekst terug in de expressie moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b1270-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="b1270-298">Instellen dat de inhoud van de hoofdtekst wordt bewaard, de `preserveContent` -parameter voor `true` bij het openen van het bericht.</span><span class="sxs-lookup"><span data-stu-id="b1270-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="b1270-299">Als `preserveContent` is ingesteld op `true` en een andere instantie wordt geretourneerd door de expressie de hoofdtekst van het geretourneerde wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b1270-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="b1270-300">Houd rekening met de volgende overwegingen wanneer u de `set-body` beleid.</span><span class="sxs-lookup"><span data-stu-id="b1270-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="b1270-301">Als u de `set-body` beleid om te retourneren van een nieuwe of bijgewerkte instantie die u hoeft niet in te stellen `preserveContent` naar `true` omdat u de inhoud van de nieuwe expliciet levert.</span><span class="sxs-lookup"><span data-stu-id="b1270-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="b1270-302">Behouden van de inhoud van een reactie op in de inkomende pijplijn logisch niet omdat er nog geen reactie is.</span><span class="sxs-lookup"><span data-stu-id="b1270-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="b1270-303">Behouden van de inhoud van een aanvraag in de uitgaande pijplijn logisch niet omdat de aanvraag al is verzonden naar de back-end op dit moment.</span><span class="sxs-lookup"><span data-stu-id="b1270-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="b1270-304">Als dit beleid wordt gebruikt wanneer er geen berichttekst, bijvoorbeeld in een inkomende GET een uitzondering opgetreden.</span><span class="sxs-lookup"><span data-stu-id="b1270-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="b1270-305">Zie voor meer informatie de `context.Request.Body`, `context.Response.Body`, en de `IMessage` secties in de [Context variabele](api-management-policy-expressions.md#ContextVariables) tabel.</span><span class="sxs-lookup"><span data-stu-id="b1270-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-306">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="b1270-307">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="b1270-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="b1270-308">Voorbeeld van de letterlijke tekst</span><span class="sxs-lookup"><span data-stu-id="b1270-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="b1270-309">Voorbeeld van de toegang tot de instantie als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b1270-309">Example accessing the body as a string.</span></span> <span data-ttu-id="b1270-310">Houd er rekening mee dat we bewaard de oorspronkelijke aanvraagtekst blijven zodat we deze later in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="b1270-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
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
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="b1270-311">Voorbeeld van de toegang tot de instantie een JObject.</span><span class="sxs-lookup"><span data-stu-id="b1270-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="b1270-312">Merk op dat omdat we niet reserveren van de oorspronkelijke aanvraagtekst, toegang tot het verderop in de pijplijn zal leiden tot een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="b1270-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="b1270-313">Reactie op basis van product filteren</span><span class="sxs-lookup"><span data-stu-id="b1270-313">Filter response based on product</span></span>  
 <span data-ttu-id="b1270-314">Dit voorbeeld ziet u hoe u inhoud filteren van door gegevenselementen te verwijderen uit het antwoord ontvangen van de back-endservice bij gebruik van de `Starter` product.</span><span class="sxs-lookup"><span data-stu-id="b1270-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="b1270-315">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit te 34:30.</span><span class="sxs-lookup"><span data-stu-id="b1270-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="b1270-316">Start op 31:50 voor een overzicht van [de donker Sky Forecast API](https://developer.forecast.io/) gebruikt voor deze demonstratie.</span><span class="sxs-lookup"><span data-stu-id="b1270-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="b1270-317">Vloeibare sjablonen gebruiken bij set-instantie</span><span class="sxs-lookup"><span data-stu-id="b1270-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="b1270-318">De `set-body` beleid kan worden geconfigureerd voor het gebruik van de [vloeibare](https://shopify.github.io/liquid/basics/introduction/) templating taal transfom de hoofdtekst van een aanvraag of antwoord.</span><span class="sxs-lookup"><span data-stu-id="b1270-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="b1270-319">Dit kan zeer effectief zijn als u moet de indeling van uw bericht volledig vorm zijn.</span><span class="sxs-lookup"><span data-stu-id="b1270-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1270-320">De implementatie van vloeistof gebruikt in de `set-body` beleid is geconfigureerd in de 'C#-modus'.</span><span class="sxs-lookup"><span data-stu-id="b1270-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="b1270-321">Dit is vooral belangrijk bij het uitvoeren van bewerkingen zoals filteren.</span><span class="sxs-lookup"><span data-stu-id="b1270-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="b1270-322">Als u bijvoorbeeld met een datumfilter vereist het gebruik van Pascal hoofd- en C#-datum notatie, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b1270-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="b1270-323">{{body.foo.startDateTime| Datum: 'yyyyMMddTHH:mm:ddZ'}}</span><span class="sxs-lookup"><span data-stu-id="b1270-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1270-324">Gebruiken om correct binden aan een XML-hoofdtekst met de vloeibare sjabloon, een `set-header` beleid Content-Type instellen op application/xml, text/xml (of een type eindigend op + xml), een JSON-hoofdtekst, het application/json, text/json (of een type eindigend op + json) moet worden.</span><span class="sxs-lookup"><span data-stu-id="b1270-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="b1270-325">JSON naar SOAP met een vloeibare sjabloon converteren</span><span class="sxs-lookup"><span data-stu-id="b1270-325">Convert JSON to SOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="b1270-326">Tranform JSON met een vloeibare sjabloon</span><span class="sxs-lookup"><span data-stu-id="b1270-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="b1270-327">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-327">Elements</span></span>  
  
|<span data-ttu-id="b1270-328">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-328">Name</span></span>|<span data-ttu-id="b1270-329">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-329">Description</span></span>|<span data-ttu-id="b1270-330">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-331">set-instantie</span><span class="sxs-lookup"><span data-stu-id="b1270-331">set-body</span></span>|<span data-ttu-id="b1270-332">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-332">Root element.</span></span> <span data-ttu-id="b1270-333">Bevat de platte tekst of een expressies die een instantie retourneert.</span><span class="sxs-lookup"><span data-stu-id="b1270-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="b1270-334">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="b1270-335">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b1270-335">Properties</span></span>  
  
|<span data-ttu-id="b1270-336">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-336">Name</span></span>|<span data-ttu-id="b1270-337">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-337">Description</span></span>|<span data-ttu-id="b1270-338">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-338">Required</span></span>|<span data-ttu-id="b1270-339">Standaard</span><span class="sxs-lookup"><span data-stu-id="b1270-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b1270-340">sjabloon</span><span class="sxs-lookup"><span data-stu-id="b1270-340">template</span></span>|<span data-ttu-id="b1270-341">Gebruikt de modus templating die het beleid instellen instantie wordt uitgevoerd te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b1270-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="b1270-342">Momenteel is de enige ondersteunde waarde:</span><span class="sxs-lookup"><span data-stu-id="b1270-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="b1270-343">-vloeibare - de hoofdtekst-beleid instellen gebruikt de vloeibare templating-engine</span><span class="sxs-lookup"><span data-stu-id="b1270-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="b1270-344">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-344">No</span></span>|<span data-ttu-id="b1270-345">vloeistof</span><span class="sxs-lookup"><span data-stu-id="b1270-345">liquid</span></span>|  

<span data-ttu-id="b1270-346">Voor toegang tot informatie over de aanvraag en antwoord, kan de vloeibare sjabloon worden verbonden met een context-object met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="b1270-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="b1270-347">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-347">Usage</span></span>  
 <span data-ttu-id="b1270-348">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-349">**Beleid secties:** inkomend, uitgaand back-end</span><span class="sxs-lookup"><span data-stu-id="b1270-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="b1270-350">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-351"><a name="SetHTTPheader"></a>Set HTTP-header</span><span class="sxs-lookup"><span data-stu-id="b1270-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="b1270-352">De `set-header` beleid wordt een waarde toegewezen aan een bestaande antwoord en/of de aanvraag-header of voegt een nieuwe antwoord en/of de aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="b1270-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="b1270-353">Voegt een lijst met HTTP-headers in een HTTP-bericht.</span><span class="sxs-lookup"><span data-stu-id="b1270-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="b1270-354">Wanneer in een inkomende pijplijn geplaatst, wordt de HTTP-headers voor de aanvraag wordt doorgegeven aan de doelservice ingesteld in dit beleid.</span><span class="sxs-lookup"><span data-stu-id="b1270-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="b1270-355">Wanneer in een uitgaande pijplijn geplaatst, wordt in dit beleid wordt de HTTP-headers voor de reactie wordt verzonden naar de gateway-client ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b1270-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-356">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="b1270-357">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="b1270-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="b1270-358">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="b1270-359">Contextinformatie naar de back-endservice doorsturen</span><span class="sxs-lookup"><span data-stu-id="b1270-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="b1270-360">In dit voorbeeld laat zien hoe beleid op het niveau van de API op te geven contextinformatie voor de back-endservice toepassen.</span><span class="sxs-lookup"><span data-stu-id="b1270-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="b1270-361">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit tot en met 10:30.</span><span class="sxs-lookup"><span data-stu-id="b1270-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="b1270-362">Bij 12:10 is er een demo voor het aanroepen van een bewerking in de portal voor ontwikkelaars, waar u het beleid op het werk kunt zien.</span><span class="sxs-lookup"><span data-stu-id="b1270-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="b1270-363">Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="b1270-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="b1270-364">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-364">Elements</span></span>  
  
|<span data-ttu-id="b1270-365">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-365">Name</span></span>|<span data-ttu-id="b1270-366">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-366">Description</span></span>|<span data-ttu-id="b1270-367">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-368">set-header</span><span class="sxs-lookup"><span data-stu-id="b1270-368">set-header</span></span>|<span data-ttu-id="b1270-369">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-369">Root element.</span></span>|<span data-ttu-id="b1270-370">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-370">Yes</span></span>|  
|<span data-ttu-id="b1270-371">waarde</span><span class="sxs-lookup"><span data-stu-id="b1270-371">value</span></span>|<span data-ttu-id="b1270-372">Hiermee geeft u de waarde van de header moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b1270-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="b1270-373">Voor meerdere headers met dezelfde naam extra toevoegen `value` elementen.</span><span class="sxs-lookup"><span data-stu-id="b1270-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="b1270-374">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="b1270-375">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b1270-375">Properties</span></span>  
  
|<span data-ttu-id="b1270-376">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-376">Name</span></span>|<span data-ttu-id="b1270-377">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-377">Description</span></span>|<span data-ttu-id="b1270-378">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-378">Required</span></span>|<span data-ttu-id="b1270-379">Standaard</span><span class="sxs-lookup"><span data-stu-id="b1270-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b1270-380">Er bestaat actie</span><span class="sxs-lookup"><span data-stu-id="b1270-380">exists-action</span></span>|<span data-ttu-id="b1270-381">Hiermee geeft u op welke actie moet worden uitgevoerd wanneer de header is al opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b1270-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="b1270-382">Dit kenmerk moet een van de volgende waarden hebben.</span><span class="sxs-lookup"><span data-stu-id="b1270-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="b1270-383">-onderdrukking - vervangt de waarde van de bestaande koptekst.</span><span class="sxs-lookup"><span data-stu-id="b1270-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="b1270-384">de waarde van de bestaande header vervangen - skip - niet.</span><span class="sxs-lookup"><span data-stu-id="b1270-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="b1270-385">-toevoeg - de waarde toegevoegd aan de bestaande headerwaarde.</span><span class="sxs-lookup"><span data-stu-id="b1270-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="b1270-386">-delete - verwijdert de header van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b1270-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="b1270-387">Als de waarde `override` opnemen van meerdere vermeldingen met dezelfde naam resulteert in de koptekst wordt ingesteld in overeenstemming met alle vermeldingen (die wordt vermeld meerdere keren); alleen de vermelde waarden worden ingesteld in het resultaat.</span><span class="sxs-lookup"><span data-stu-id="b1270-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="b1270-388">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-388">No</span></span>|<span data-ttu-id="b1270-389">overschrijven</span><span class="sxs-lookup"><span data-stu-id="b1270-389">override</span></span>|  
|<span data-ttu-id="b1270-390">naam</span><span class="sxs-lookup"><span data-stu-id="b1270-390">name</span></span>|<span data-ttu-id="b1270-391">Hiermee geeft u de naam van de header moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b1270-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="b1270-392">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-392">Yes</span></span>|<span data-ttu-id="b1270-393">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b1270-394">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-394">Usage</span></span>  
 <span data-ttu-id="b1270-395">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-396">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="b1270-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="b1270-397">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-398"><a name="SetQueryStringParameter"></a>Querytekenreeksparameter instellen</span><span class="sxs-lookup"><span data-stu-id="b1270-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="b1270-399">De `set-query-parameter` beleid wordt toegevoegd, vervangt de waarde van, of verwijderingen querytekenreeksparameter aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b1270-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="b1270-400">Kan worden gebruikt voor het doorgeven van de query parameters verwacht door de back endservice die zijn optioneel of nooit voorkomen in de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b1270-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-401">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="b1270-402">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="b1270-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="b1270-403">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="b1270-404">Contextinformatie naar de back-endservice doorsturen</span><span class="sxs-lookup"><span data-stu-id="b1270-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="b1270-405">In dit voorbeeld laat zien hoe beleid op het niveau van de API op te geven contextinformatie voor de back-endservice toepassen.</span><span class="sxs-lookup"><span data-stu-id="b1270-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="b1270-406">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit tot en met 10:30.</span><span class="sxs-lookup"><span data-stu-id="b1270-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="b1270-407">Bij 12:10 is er een demo voor het aanroepen van een bewerking in de portal voor ontwikkelaars, waar u het beleid op het werk kunt zien.</span><span class="sxs-lookup"><span data-stu-id="b1270-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="b1270-408">Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="b1270-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="b1270-409">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-409">Elements</span></span>  
  
|<span data-ttu-id="b1270-410">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-410">Name</span></span>|<span data-ttu-id="b1270-411">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-411">Description</span></span>|<span data-ttu-id="b1270-412">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-413">query-set-parameter</span><span class="sxs-lookup"><span data-stu-id="b1270-413">set-query-parameter</span></span>|<span data-ttu-id="b1270-414">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-414">Root element.</span></span>|<span data-ttu-id="b1270-415">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-415">Yes</span></span>|  
|<span data-ttu-id="b1270-416">waarde</span><span class="sxs-lookup"><span data-stu-id="b1270-416">value</span></span>|<span data-ttu-id="b1270-417">Hiermee geeft u de waarde van de query-parameter moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b1270-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="b1270-418">Voor meerdere queryparameters met dezelfde naam extra toevoegen `value` elementen.</span><span class="sxs-lookup"><span data-stu-id="b1270-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="b1270-419">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="b1270-420">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b1270-420">Properties</span></span>  
  
|<span data-ttu-id="b1270-421">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-421">Name</span></span>|<span data-ttu-id="b1270-422">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-422">Description</span></span>|<span data-ttu-id="b1270-423">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-423">Required</span></span>|<span data-ttu-id="b1270-424">Standaard</span><span class="sxs-lookup"><span data-stu-id="b1270-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b1270-425">Er bestaat actie</span><span class="sxs-lookup"><span data-stu-id="b1270-425">exists-action</span></span>|<span data-ttu-id="b1270-426">Hiermee geeft u op welke actie moet worden uitgevoerd wanneer de queryparameter is al opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b1270-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="b1270-427">Dit kenmerk moet een van de volgende waarden hebben.</span><span class="sxs-lookup"><span data-stu-id="b1270-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="b1270-428">-onderdrukking - vervangt de waarde van de bestaande parameter.</span><span class="sxs-lookup"><span data-stu-id="b1270-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="b1270-429">-skip: de waarde van de bestaande query-parameter niet vervangen.</span><span class="sxs-lookup"><span data-stu-id="b1270-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="b1270-430">-toevoeg - voegt u de waarde met de waarde van de bestaande query.</span><span class="sxs-lookup"><span data-stu-id="b1270-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="b1270-431">de queryparameter verwijdert - delete - uit de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b1270-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="b1270-432">Als de waarde `override` opnemen van meerdere vermeldingen met dezelfde naam resulteert in de query-parameter worden ingesteld in overeenstemming met alle vermeldingen (die wordt vermeld meerdere keren); alleen de vermelde waarden worden ingesteld in het resultaat.</span><span class="sxs-lookup"><span data-stu-id="b1270-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="b1270-433">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-433">No</span></span>|<span data-ttu-id="b1270-434">overschrijven</span><span class="sxs-lookup"><span data-stu-id="b1270-434">override</span></span>|  
|<span data-ttu-id="b1270-435">naam</span><span class="sxs-lookup"><span data-stu-id="b1270-435">name</span></span>|<span data-ttu-id="b1270-436">Hiermee geeft u de naam van de queryparameter moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b1270-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="b1270-437">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-437">Yes</span></span>|<span data-ttu-id="b1270-438">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b1270-439">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-439">Usage</span></span>  
 <span data-ttu-id="b1270-440">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-441">**Beleid secties:** back-end voor binnenkomend verkeer</span><span class="sxs-lookup"><span data-stu-id="b1270-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="b1270-442">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-443"><a name="RewriteURL"></a>Herschrijven van URL 's</span><span class="sxs-lookup"><span data-stu-id="b1270-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="b1270-444">De `rewrite-uri` beleid omgezet in een aanvraag-URL van de openbare vorm het formulier dat werd verwacht door de webservice, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b1270-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="b1270-445">Openbare URL-`http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="b1270-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="b1270-446">Aanvraag-URL-`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="b1270-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="b1270-447">Dit beleid kan worden gebruikt wanneer een menselijke en/of beschrijvende browser-URL moet worden omgezet in de URL-indeling verwacht door de webservice.</span><span class="sxs-lookup"><span data-stu-id="b1270-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="b1270-448">Dit beleid moet alleen worden toegepast bij het blootstellen van een andere URL-indeling, zoals schone URL's, RESTful-URL's, gebruiksvriendelijke URL's of Zoekmachineoptimalisatie gebruiksvriendelijke URL's die zijn uitsluitend structurele URL's die niet een queryreeks bevatten en in plaats daarvan alleen het pad van de resource (na het schema en de autoriteit) bevatten.</span><span class="sxs-lookup"><span data-stu-id="b1270-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="b1270-449">Dit wordt vaak gedaan voor fraaie uiterlijk, bruikbaarheid of zoekmachine optimaliseringsdoeleinden (Zoekmachineoptimalisatie).</span><span class="sxs-lookup"><span data-stu-id="b1270-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b1270-450">U kunt alleen queryreeksparameters met het beleid toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b1270-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="b1270-451">U kunt geen extra Sjabloonparameters voor pad toevoegen in de URL herschrijven.</span><span class="sxs-lookup"><span data-stu-id="b1270-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="b1270-452">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="b1270-453">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="b1270-454">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-454">Elements</span></span>  
  
|<span data-ttu-id="b1270-455">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-455">Name</span></span>|<span data-ttu-id="b1270-456">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-456">Description</span></span>|<span data-ttu-id="b1270-457">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-458">Herschrijf-uri</span><span class="sxs-lookup"><span data-stu-id="b1270-458">rewrite-uri</span></span>|<span data-ttu-id="b1270-459">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-459">Root element.</span></span>|<span data-ttu-id="b1270-460">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b1270-461">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="b1270-461">Attributes</span></span>  
  
|<span data-ttu-id="b1270-462">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="b1270-462">Attribute</span></span>|<span data-ttu-id="b1270-463">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-463">Description</span></span>|<span data-ttu-id="b1270-464">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-464">Required</span></span>|<span data-ttu-id="b1270-465">Standaard</span><span class="sxs-lookup"><span data-stu-id="b1270-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="b1270-466">sjabloon</span><span class="sxs-lookup"><span data-stu-id="b1270-466">template</span></span>|<span data-ttu-id="b1270-467">De werkelijke web service-URL met een queryreeks-parameters.</span><span class="sxs-lookup"><span data-stu-id="b1270-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="b1270-468">Wanneer u expressies gebruikt, is het gehele getal moet een expressie.</span><span class="sxs-lookup"><span data-stu-id="b1270-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="b1270-469">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-469">Yes</span></span>|<span data-ttu-id="b1270-470">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b1270-470">N/A</span></span>|  
|<span data-ttu-id="b1270-471">kopiëren niet-overeenkomende parameters</span><span class="sxs-lookup"><span data-stu-id="b1270-471">copy-unmatched-params</span></span>|<span data-ttu-id="b1270-472">Hiermee geeft u op of de binnenkomende aanvraag niet aanwezig in de oorspronkelijke URL sjabloon queryparameters worden toegevoegd aan de URL die is gedefinieerd door de sjabloon opnieuw schrijven</span><span class="sxs-lookup"><span data-stu-id="b1270-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="b1270-473">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-473">No</span></span>|<span data-ttu-id="b1270-474">De waarde True</span><span class="sxs-lookup"><span data-stu-id="b1270-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b1270-475">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-475">Usage</span></span>  
 <span data-ttu-id="b1270-476">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-477">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="b1270-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b1270-478">**Beleid scopes:** product, API-bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="b1270-479"><a name="XSLTransform"></a>XML met behulp van een XSLT transformeren</span><span class="sxs-lookup"><span data-stu-id="b1270-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="b1270-480">De `Transform XML using an XSLT` beleid geldt een XSL-transformatie voor XML in de hoofdtekst van de aanvraag of antwoord.</span><span class="sxs-lookup"><span data-stu-id="b1270-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b1270-481">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="b1270-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="b1270-482">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b1270-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="b1270-483">Elementen</span><span class="sxs-lookup"><span data-stu-id="b1270-483">Elements</span></span>  
  
|<span data-ttu-id="b1270-484">Naam</span><span class="sxs-lookup"><span data-stu-id="b1270-484">Name</span></span>|<span data-ttu-id="b1270-485">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b1270-485">Description</span></span>|<span data-ttu-id="b1270-486">Vereist</span><span class="sxs-lookup"><span data-stu-id="b1270-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b1270-487">XSL-transformatie</span><span class="sxs-lookup"><span data-stu-id="b1270-487">xsl-transform</span></span>|<span data-ttu-id="b1270-488">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="b1270-488">Root element.</span></span>|<span data-ttu-id="b1270-489">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-489">Yes</span></span>|  
|<span data-ttu-id="b1270-490">Parameter</span><span class="sxs-lookup"><span data-stu-id="b1270-490">parameter</span></span>|<span data-ttu-id="b1270-491">Gebruikt voor het definiëren van variabelen die worden gebruikt in de transformatie</span><span class="sxs-lookup"><span data-stu-id="b1270-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="b1270-492">Nee</span><span class="sxs-lookup"><span data-stu-id="b1270-492">No</span></span>|  
|<span data-ttu-id="b1270-493">xsl: Stylesheet</span><span class="sxs-lookup"><span data-stu-id="b1270-493">xsl:stylesheet</span></span>|<span data-ttu-id="b1270-494">Hoofdelement opmaakmodel.</span><span class="sxs-lookup"><span data-stu-id="b1270-494">Root stylesheet element.</span></span> <span data-ttu-id="b1270-495">Ga als volgt de standaard alle elementen en kenmerken die zijn gedefinieerd binnen [XSLT-specificatie](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="b1270-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="b1270-496">Ja</span><span class="sxs-lookup"><span data-stu-id="b1270-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b1270-497">Gebruik</span><span class="sxs-lookup"><span data-stu-id="b1270-497">Usage</span></span>  
 <span data-ttu-id="b1270-498">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b1270-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b1270-499">**Beleid secties:** binnenkomende, uitgaande</span><span class="sxs-lookup"><span data-stu-id="b1270-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="b1270-500">**Beleid scopes:** wereldwijd, product, API, bewerking</span><span class="sxs-lookup"><span data-stu-id="b1270-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="b1270-501">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1270-501">Next steps</span></span>
<span data-ttu-id="b1270-502">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b1270-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
