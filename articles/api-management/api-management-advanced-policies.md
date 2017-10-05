---
title: Azure API Management Geavanceerde beleidsregels | Microsoft Docs
description: Meer informatie over de geavanceerde beleidsregels beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0c65ac74316421a0258f01143baa25ffecb5be3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="bb3c5-103">API Management Geavanceerde beleidsregels</span><span class="sxs-lookup"><span data-stu-id="bb3c5-103">API Management advanced policies</span></span>
<span data-ttu-id="bb3c5-104">Dit onderwerp bevat een verwijzing voor de volgende API Management-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="bb3c5-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="bb3c5-106"><a name="AdvancedPolicies"></a>Geavanceerde beleidsregels</span><span class="sxs-lookup"><span data-stu-id="bb3c5-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="bb3c5-107">[Transportbesturing](api-management-advanced-policies.md#choose) - voorwaardelijk is van toepassing op basis van de resultaten van de evaluatie van Booleaanse waarde beleidsverklaringen [expressies](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="bb3c5-108">[Doorsturen van aanvraag](#ForwardRequest) -stuurt de aanvraag naar de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>

-   <span data-ttu-id="bb3c5-109">[Gelijktijdigheid beperken](#LimitConcurrency) -voorkomt u dat beleid uit door meer dan het opgegeven aantal aanvragen wordt uitgevoerd op een tijdstip ingesloten.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than the specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="bb3c5-110">[Logboek naar Event Hub](#log-to-eventhub) -berichten in de opgegeven indeling verzendt naar een Event Hub gedefinieerd door een entiteit berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-110">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="bb3c5-111">[Antwoord model](#mock-response) -pipeline-uitvoering wordt afgebroken en retourneert een mocked antwoord rechtstreeks aan de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="bb3c5-112">[Probeer](#Retry) -uitvoering van de ingesloten beleidsverklaringen pogingen als en pas de voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-112">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="bb3c5-113">Uitvoering wordt herhaald op de opgegeven tijdsintervallen en tot het opgegeven aantal nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-113">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="bb3c5-114">[Antwoord retourneren](#ReturnResponse) -pipeline-uitvoering wordt afgebroken en retourneert het opgegeven antwoord rechtstreeks naar de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span> 
  
-   <span data-ttu-id="bb3c5-115">[Eenzijdige aanvraag verzenden](#SendOneWayRequest) -verzendt een aanvraag naar de opgegeven URL zonder te wachten op reactie.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-115">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="bb3c5-116">[Aanvraag verzenden](#SendRequest) -verzendt een aanvraag naar de opgegeven URL.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-116">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  

-   <span data-ttu-id="bb3c5-117">[HTTP-proxy ingesteld](#SetHttpProxy) -kunt u de aanvragen van de route die zijn doorgestuurd via een HTTP-proxy.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-117">[Set HTTP proxy](#SetHttpProxy) - Allows you to route forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="bb3c5-118">[Stel aanvraagmethode](#SetRequestMethod) -kunt u de HTTP-methode voor een aanvraag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-118">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="bb3c5-119">[Statuscode ingesteld](#SetStatus) -wijzigingen van de HTTP-statuscode in de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-119">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="bb3c5-120">[Variabele instellen](api-management-advanced-policies.md#set-variable) -zich blijft voordoen een waarde in een benoemde [context](api-management-policy-expressions.md#ContextVariables) variabele voor latere toegang.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="bb3c5-121">[Tracering](#Trace) -voegt een tekenreeks in de [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-121">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="bb3c5-122">[Wacht](#Wait) -wacht voor ingesloten [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), of [transportbesturing](api-management-advanced-policies.md#choose) beleid om te voltooien voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <span data-ttu-id="bb3c5-123"><a name="choose"></a>Controlestroom</span><span class="sxs-lookup"><span data-stu-id="bb3c5-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="bb3c5-124">De `choose` beleid van toepassing is ingesloten beleid op basis van het resultaat van evaluatie van Booleaanse expressies, vergelijkbaar met een if-then-else of een switch instructies in een programmeertaal maken.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-124">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="bb3c5-125"><a name="ChoosePolicyStatement"></a>Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="bb3c5-126">Het beleid voor toegangsbeheer stroom moet ten minste één bevatten `<when/>` element.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-126">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="bb3c5-127">De `<otherwise/>` element is optioneel.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-127">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="bb3c5-128">Voorwaarden `<when/>` elementen worden geëvalueerd in de volgorde van de weergave in het beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-128">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="bb3c5-129">Beleid voor instructie (s) die tussen de eerste `<when/>` element met kenmerk gelijk is aan voorwaarde `true` worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-129">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="bb3c5-130">Beleidsregels die tussen de `<otherwise/>` element, indien aanwezig, wordt toegepast als alle van de `<when/>` voorwaarde elementkenmerken zijn `false`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-130">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="bb3c5-131">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="bb3c5-131">Examples</span></span>  
  
####  <span data-ttu-id="bb3c5-132"><a name="ChooseExample"></a>Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="bb3c5-133">Het volgende voorbeeld toont een [variabele instellen](api-management-advanced-policies.md#set-variable) beleid en twee beleidsregels voor beheer-stroom.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-133">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="bb3c5-134">De variabele beleid instellen in de sectie inkomende en genereert een `isMobile` Booleaanse [context](api-management-policy-expressions.md#ContextVariables) variabele die is ingesteld op true als de `User-Agent` aanvraag-header bevat de tekst `iPad` of `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-134">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="bb3c5-135">Het eerste beleid voor toegangsbeheer stroom is ook in de sectie inkomende en voorwaardelijk wordt een van twee [querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) beleidsregels, afhankelijk van de waarde van de `isMobile` context-variabele.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-135">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="bb3c5-136">Het tweede beleid voor toegangsbeheer stroom is in de sectie uitgaande en voorwaardelijk geldt de [XML converteren naar JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) beleid wanneer `isMobile` is ingesteld op `true`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-136">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="bb3c5-137">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-137">Example</span></span>  
 <span data-ttu-id="bb3c5-138">Dit voorbeeld ziet u hoe u inhoud filteren van door gegevenselementen te verwijderen uit het antwoord ontvangen van de back-endservice bij gebruik van de `Starter` product.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-138">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="bb3c5-139">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit te 34:30.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="bb3c5-140">Start op 31:50 voor een overzicht van [de donker Sky Forecast API](https://developer.forecast.io/) gebruikt voor deze demonstratie.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-140">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="bb3c5-141">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-141">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-142">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-142">Element</span></span>|<span data-ttu-id="bb3c5-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-143">Description</span></span>|<span data-ttu-id="bb3c5-144">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-145">Kies</span><span class="sxs-lookup"><span data-stu-id="bb3c5-145">choose</span></span>|<span data-ttu-id="bb3c5-146">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-146">Root element.</span></span>|<span data-ttu-id="bb3c5-147">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-147">Yes</span></span>|  
|<span data-ttu-id="bb3c5-148">Wanneer</span><span class="sxs-lookup"><span data-stu-id="bb3c5-148">when</span></span>|<span data-ttu-id="bb3c5-149">De voorwaarde moet worden gebruikt voor de `if` of `ifelse` delen van de `choose` beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-149">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="bb3c5-150">Als de `choose` beleid heeft meerdere `when` secties, ze worden opeenvolgend geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-150">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="bb3c5-151">Eenmaal de `condition` van een wanneer element resulteert in `true`, niet verder `when` voorwaarden worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-151">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="bb3c5-152">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-152">Yes</span></span>|  
|<span data-ttu-id="bb3c5-153">anders</span><span class="sxs-lookup"><span data-stu-id="bb3c5-153">otherwise</span></span>|<span data-ttu-id="bb3c5-154">Bevat het fragment beleid moet worden gebruikt als geen van de `when` voorwaarden worden geëvalueerd tot `true`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-154">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="bb3c5-155">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-156">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-156">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-157">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-157">Attribute</span></span>|<span data-ttu-id="bb3c5-158">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-158">Description</span></span>|<span data-ttu-id="bb3c5-159">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-160">conditie = "Boole-expressie &#124; Constante Booleaanse'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="bb3c5-161">De Boole-expressie of een constante geëvalueerd wanneer de die `when` beleidsverklaring wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-161">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="bb3c5-162">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-162">Yes</span></span>|  
  
###  <span data-ttu-id="bb3c5-163"><a name="ChooseUsage"></a>Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="bb3c5-164">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-164">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-165">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-166">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bb3c5-167"><a name="ForwardRequest"></a>Doorsturen van aanvraag</span><span class="sxs-lookup"><span data-stu-id="bb3c5-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="bb3c5-168">De `forward-request` beleid stuurt de binnenkomende aanvraag naar de back-endservice die is opgegeven in de aanvraag [context](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-168">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="bb3c5-169">De back-end-service-URL is opgegeven in de API [instellingen](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) en kan worden gewijzigd met behulp van de [back-endservice ingesteld](api-management-transformation-policies.md) beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-169">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bb3c5-170">Verwijderen van deze resultaten van Groepsbeleid in de aanvraag niet wordt doorgestuurd naar de back-end worden-service en het beleid in de sectie uitgaande geëvalueerd onmiddellijk na de geslaagde voltooiing van het beleid in de sectie inkomende.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-170">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-171">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="bb3c5-172">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="bb3c5-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="bb3c5-173">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-173">Example</span></span>  
 <span data-ttu-id="bb3c5-174">Het volgende beleid van de API-niveau verzendt alle aanvragen naar de back endservice met een time-outinterval van 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-174">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="bb3c5-175">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-175">Example</span></span>  
 <span data-ttu-id="bb3c5-176">Het beleid voor deze bewerking gebruikt de `base` element worden overgenomen van het back-end-beleid van het bovenliggende niveau API-bereik.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-176">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="bb3c5-177">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-177">Example</span></span>  
 <span data-ttu-id="bb3c5-178">Deze bewerking beleid expliciet stuurt alle aanvragen naar de back endservice met een time-out van 120 en het is niet overgenomen van het bovenliggende niveau back-end-API-beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-178">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="bb3c5-179">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-179">Example</span></span>  
 <span data-ttu-id="bb3c5-180">Dit beleid op het niveau bewerking doorstuurt geen aanvragen voor de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-180">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-181">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-181">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-182">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-182">Element</span></span>|<span data-ttu-id="bb3c5-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-183">Description</span></span>|<span data-ttu-id="bb3c5-184">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-185">voorwaarts-aanvraag</span><span class="sxs-lookup"><span data-stu-id="bb3c5-185">forward-request</span></span>|<span data-ttu-id="bb3c5-186">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-186">Root element.</span></span>|<span data-ttu-id="bb3c5-187">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-188">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-188">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-189">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-189">Attribute</span></span>|<span data-ttu-id="bb3c5-190">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-190">Description</span></span>|<span data-ttu-id="bb3c5-191">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-191">Required</span></span>|<span data-ttu-id="bb3c5-192">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bb3c5-193">time-out = 'integer'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-193">timeout="integer"</span></span>|<span data-ttu-id="bb3c5-194">De time-outinterval in seconden voordat de aanroep naar de back endservice is mislukt.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-194">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="bb3c5-195">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-195">No</span></span>|<span data-ttu-id="bb3c5-196">Geen time-out</span><span class="sxs-lookup"><span data-stu-id="bb3c5-196">No timeout</span></span>|  
|<span data-ttu-id="bb3c5-197">Volg omleidingen = "true &#124; False"</span><span class="sxs-lookup"><span data-stu-id="bb3c5-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="bb3c5-198">Hiermee geeft u op of omleidingen vanaf de back-endservice worden gevolgd door de gateway of geretourneerd naar de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-198">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="bb3c5-199">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-199">No</span></span>|<span data-ttu-id="bb3c5-200">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="bb3c5-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-201">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-201">Usage</span></span>  
 <span data-ttu-id="bb3c5-202">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-203">**Beleid secties:** back-end</span><span class="sxs-lookup"><span data-stu-id="bb3c5-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="bb3c5-204">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bb3c5-205"><a name="LimitConcurrency"></a>Limiet gelijktijdigheid van taken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="bb3c5-206">De `limit-concurrency` ingesloten beleid uit door meer dan het opgegeven aantal aanvragen wordt uitgevoerd op een bepaald moment wordt verhinderd door beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-206">The `limit-concurrency` policy prevents enclosed policies from executing by more than the specified number of requests at a given time.</span></span> <span data-ttu-id="bb3c5-207">Nieuwe aanvragen worden toegevoegd aan een wachtrij op die de drempelwaarde overschrijden, totdat de maximum wachtrijlengte wordt bereikt.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-207">Upon exceeding the threshold, new requests are added to a queue, until the maximum queue length is achieved.</span></span> <span data-ttu-id="bb3c5-208">Bij uitputting van de wachtrij mislukken nieuwe aanvragen onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="bb3c5-209"><a name="LimitConcurrencyStatement"></a>Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="bb3c5-210">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="bb3c5-210">Examples</span></span>  
  
####  <span data-ttu-id="bb3c5-211"><a name="ChooseExample"></a>Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="bb3c5-212">Het volgende voorbeeld laat zien hoe u wilt beperken het aantal aanvragen worden doorgestuurd naar een back-end op basis van de waarde van een variabele context.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-212">The following example demonstrates how to limit number of requests forwarded to a backend based on the value of a context variable.</span></span>
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a><span data-ttu-id="bb3c5-213">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-213">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-214">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-214">Element</span></span>|<span data-ttu-id="bb3c5-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-215">Description</span></span>|<span data-ttu-id="bb3c5-216">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="bb3c5-217">limiet gelijktijdigheid</span><span class="sxs-lookup"><span data-stu-id="bb3c5-217">limit-concurrency</span></span>|<span data-ttu-id="bb3c5-218">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-218">Root element.</span></span>|<span data-ttu-id="bb3c5-219">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-220">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-220">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-221">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-221">Attribute</span></span>|<span data-ttu-id="bb3c5-222">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-222">Description</span></span>|<span data-ttu-id="bb3c5-223">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-223">Required</span></span>|<span data-ttu-id="bb3c5-224">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="bb3c5-225">sleutel</span><span class="sxs-lookup"><span data-stu-id="bb3c5-225">key</span></span>|<span data-ttu-id="bb3c5-226">Een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-226">A string.</span></span> <span data-ttu-id="bb3c5-227">Een expressie toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-227">Expression allowed.</span></span> <span data-ttu-id="bb3c5-228">Hiermee geeft u het bereik gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-228">Specifies the concurrency scope.</span></span> <span data-ttu-id="bb3c5-229">Kan worden gedeeld door meerdere beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="bb3c5-230">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-230">Yes</span></span>|<span data-ttu-id="bb3c5-231">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-231">N/A</span></span>|  
|<span data-ttu-id="bb3c5-232">maximum aantal</span><span class="sxs-lookup"><span data-stu-id="bb3c5-232">max-count</span></span>|<span data-ttu-id="bb3c5-233">Een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-233">An integer.</span></span> <span data-ttu-id="bb3c5-234">Hiermee geeft u het maximale aantal aanvragen die zijn toegestaan in te voeren van het beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-234">Specifies a maximum number of requests that are allowed to enter the policy.</span></span>|<span data-ttu-id="bb3c5-235">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-235">Yes</span></span>|<span data-ttu-id="bb3c5-236">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-236">N/A</span></span>|  
|<span data-ttu-id="bb3c5-237">Time-out</span><span class="sxs-lookup"><span data-stu-id="bb3c5-237">timeout</span></span>|<span data-ttu-id="bb3c5-238">Een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-238">An integer.</span></span> <span data-ttu-id="bb3c5-239">Een expressie toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-239">Expression allowed.</span></span> <span data-ttu-id="bb3c5-240">Hiermee geeft u het aantal seconden dat een aanvraag wachten moet om in te voeren van een scope voordat deze is mislukt met ' 403 te veel aanvragen '</span><span class="sxs-lookup"><span data-stu-id="bb3c5-240">Specifies the number of seconds a request should wait to enter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="bb3c5-241">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-241">No</span></span>|<span data-ttu-id="bb3c5-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="bb3c5-242">Infinity</span></span>|  
|<span data-ttu-id="bb3c5-243">maximale wachtrijlengte</span><span class="sxs-lookup"><span data-stu-id="bb3c5-243">max-queue-length</span></span>|<span data-ttu-id="bb3c5-244">Een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-244">An integer.</span></span> <span data-ttu-id="bb3c5-245">Een expressie toegestaan.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-245">Expression allowed.</span></span> <span data-ttu-id="bb3c5-246">Hiermee geeft u de maximum wachtrijlengte.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-246">Specifies the maximum queue length.</span></span> <span data-ttu-id="bb3c5-247">Inkomende aanvragen probeert in te voeren van dit beleid wordt gestopt met ' 403 te veel aanvragen ' onmiddellijk wanneer de wachtrij is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-247">Incoming requests trying to enter this policy will be terminated with “403 Too Many Requests” immediately when the queue is exhausted.</span></span>|<span data-ttu-id="bb3c5-248">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-248">No</span></span>|<span data-ttu-id="bb3c5-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="bb3c5-249">Infinity</span></span>|  
  
###  <span data-ttu-id="bb3c5-250"><a name="ChooseUsage"></a>Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="bb3c5-251">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-251">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-252">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-253">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bb3c5-254"><a name="log-to-eventhub"></a>Logboek naar Event Hub</span><span class="sxs-lookup"><span data-stu-id="bb3c5-254"><a name="log-to-eventhub"></a> Log to Event Hub</span></span>  
 <span data-ttu-id="bb3c5-255">De `log-to-eventhub` beleid verzendt berichten in de opgegeven indeling naar een Event Hub gedefinieerd door een entiteit berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-255">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="bb3c5-256">Als de naam al aangeeft, wordt het beleid wordt gebruikt voor het opslaan van de geselecteerde aanvraag of antwoord contextinformatie voor online of offline-analyse.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-256">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bb3c5-257">Zie voor een stapsgewijze handleiding voor het configureren van een event hub en vastleggen van gebeurtenissen, [het registreren van API Management-gebeurtenissen met Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-257">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-258">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-259">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-259">Example</span></span>  
 <span data-ttu-id="bb3c5-260">Elke tekenreeks kan worden gebruikt als de waarde worden geregistreerd in Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-260">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="bb3c5-261">In dit voorbeeld is de datum en tijd, implementatie-servicenaam, aanvraag-id, IP-adres en de naam van de bewerking voor alle binnenkomende oproepen worden geregistreerd in de event hub berichtenlogboek geregistreerd bij de `contoso-logger` id.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-261">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-262">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-262">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-263">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-263">Element</span></span>|<span data-ttu-id="bb3c5-264">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-264">Description</span></span>|<span data-ttu-id="bb3c5-265">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-266">logboek voor eventhub</span><span class="sxs-lookup"><span data-stu-id="bb3c5-266">log-to-eventhub</span></span>|<span data-ttu-id="bb3c5-267">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-267">Root element.</span></span> <span data-ttu-id="bb3c5-268">De waarde van dit element is de tekenreeks aan te melden naar uw event hub.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-268">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="bb3c5-269">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-270">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-270">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-271">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-271">Attribute</span></span>|<span data-ttu-id="bb3c5-272">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-272">Description</span></span>|<span data-ttu-id="bb3c5-273">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-274">logboek-id</span><span class="sxs-lookup"><span data-stu-id="bb3c5-274">logger-id</span></span>|<span data-ttu-id="bb3c5-275">De id van het logboek geregistreerd bij uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-275">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="bb3c5-276">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-276">Yes</span></span>|  
|<span data-ttu-id="bb3c5-277">partitie-id</span><span class="sxs-lookup"><span data-stu-id="bb3c5-277">partition-id</span></span>|<span data-ttu-id="bb3c5-278">Hiermee geeft u de index van de partitie waarin berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-278">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="bb3c5-279">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-279">Optional.</span></span> <span data-ttu-id="bb3c5-280">Dit kenmerk kan niet worden gebruikt als `partition-key` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="bb3c5-281">Partitiesleutel</span><span class="sxs-lookup"><span data-stu-id="bb3c5-281">partition-key</span></span>|<span data-ttu-id="bb3c5-282">Hiermee geeft u de waarde voor de partitietoewijzing van de wordt gebruikt wanneer berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-282">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="bb3c5-283">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-283">Optional.</span></span> <span data-ttu-id="bb3c5-284">Dit kenmerk kan niet worden gebruikt als `partition-id` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-285">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-285">Usage</span></span>  
 <span data-ttu-id="bb3c5-286">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-286">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-287">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-288">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bb3c5-289"><a name="mock-response"></a>Mock-antwoord</span><span class="sxs-lookup"><span data-stu-id="bb3c5-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="bb3c5-290">De `mock-response`, als de naam al aangeeft, wordt gebruikt voor het model van de API's en bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-290">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="bb3c5-291">Het normale pipeline-uitvoering wordt afgebroken en retourneert een mocked antwoord aan de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-291">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="bb3c5-292">Het beleid probeert altijd te retourneren van reacties van hoogste betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-292">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="bb3c5-293">Deze verkiest antwoord inhoud voorbeelden, indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="bb3c5-294">Het voorbeeld antwoorden van schema's, genereert wanneer schema's worden geleverd en voorbeelden niet.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="bb3c5-295">Als geen van beide voorbeelden of schema's zijn gevonden, worden de antwoorden met geen inhoud geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-296">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="bb3c5-297">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="bb3c5-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-298">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-298">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-299">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-299">Element</span></span>|<span data-ttu-id="bb3c5-300">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-300">Description</span></span>|<span data-ttu-id="bb3c5-301">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-302">nagebootste-antwoord</span><span class="sxs-lookup"><span data-stu-id="bb3c5-302">mock-response</span></span>|<span data-ttu-id="bb3c5-303">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-303">Root element.</span></span>|<span data-ttu-id="bb3c5-304">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-305">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-305">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-306">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-306">Attribute</span></span>|<span data-ttu-id="bb3c5-307">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-307">Description</span></span>|<span data-ttu-id="bb3c5-308">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-308">Required</span></span>|<span data-ttu-id="bb3c5-309">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="bb3c5-310">statuscode in</span><span class="sxs-lookup"><span data-stu-id="bb3c5-310">status-code</span></span>|<span data-ttu-id="bb3c5-311">Hiermee geeft u de statuscode van antwoord en wordt gebruikt om bijbehorende voorbeeld of schema te selecteren.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-311">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="bb3c5-312">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-312">No</span></span>|<span data-ttu-id="bb3c5-313">200</span><span class="sxs-lookup"><span data-stu-id="bb3c5-313">200</span></span>|  
|<span data-ttu-id="bb3c5-314">type inhoud</span><span class="sxs-lookup"><span data-stu-id="bb3c5-314">content-type</span></span>|<span data-ttu-id="bb3c5-315">Hiermee geeft u `Content-Type` headerwaarde antwoord en wordt gebruikt om bijbehorende voorbeeld of schema te selecteren.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-315">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="bb3c5-316">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-316">No</span></span>|<span data-ttu-id="bb3c5-317">Geen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-318">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-318">Usage</span></span>  
 <span data-ttu-id="bb3c5-319">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-319">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-320">**Beleid secties:** binnenkomende, uitgaande, bij fouten</span><span class="sxs-lookup"><span data-stu-id="bb3c5-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-321">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="bb3c5-322"><a name="Retry"></a>Probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="bb3c5-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="bb3c5-323">De `retry` beleid de onderliggende beleidsregels eenmaal wordt uitgevoerd en vervolgens probeert om opnieuw de uitvoering ervan totdat de nieuwe poging `condition` wordt `false` of probeer het opnieuw `count` leeg.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-323">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-324">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-324">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-325">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-325">Example</span></span>  
 <span data-ttu-id="bb3c5-326">In het volgende voorbeeldaanvraag forewarding wordt opnieuw geprobeerd maximaal tien keer met exponentiële algoritme proberen.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-326">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="bb3c5-327">Aangezien `first-fast-retry` is ingesteld op false, alle pogingen zijn onderworpen aan de algoritme van exponsntial probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-327">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-328">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-328">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-329">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-329">Element</span></span>|<span data-ttu-id="bb3c5-330">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-330">Description</span></span>|<span data-ttu-id="bb3c5-331">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-332">Probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="bb3c5-332">retry</span></span>|<span data-ttu-id="bb3c5-333">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-333">Root element.</span></span> <span data-ttu-id="bb3c5-334">Kan geen ander beleid bevatten als de onderliggende elementen.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="bb3c5-335">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-336">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-336">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-337">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-337">Attribute</span></span>|<span data-ttu-id="bb3c5-338">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-338">Description</span></span>|<span data-ttu-id="bb3c5-339">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-339">Required</span></span>|<span data-ttu-id="bb3c5-340">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bb3c5-341">Voorwaarde</span><span class="sxs-lookup"><span data-stu-id="bb3c5-341">condition</span></span>|<span data-ttu-id="bb3c5-342">Een boolean letterlijke waarde of [expressie](api-management-policy-expressions.md) opgeven als nieuwe pogingen moeten worden gestopt (`false`) of vervolg (`true`).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="bb3c5-343">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-343">Yes</span></span>|<span data-ttu-id="bb3c5-344">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-344">N/A</span></span>|  
|<span data-ttu-id="bb3c5-345">Aantal</span><span class="sxs-lookup"><span data-stu-id="bb3c5-345">count</span></span>|<span data-ttu-id="bb3c5-346">Een positief getal dat aangeeft het maximale aantal nieuwe pogingen om te proberen.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-346">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="bb3c5-347">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-347">Yes</span></span>|<span data-ttu-id="bb3c5-348">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-348">N/A</span></span>|  
|<span data-ttu-id="bb3c5-349">Interval</span><span class="sxs-lookup"><span data-stu-id="bb3c5-349">interval</span></span>|<span data-ttu-id="bb3c5-350">Een positief getal in seconden, geven de wachtinterval tussen het opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-350">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="bb3c5-351">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-351">Yes</span></span>|<span data-ttu-id="bb3c5-352">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-352">N/A</span></span>|  
|<span data-ttu-id="bb3c5-353">Max-interval</span><span class="sxs-lookup"><span data-stu-id="bb3c5-353">max-interval</span></span>|<span data-ttu-id="bb3c5-354">Een positief getal in seconden voor het opgeven van de maximale wachttijd interval tussen de pogingen.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-354">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="bb3c5-355">Wordt gebruikt voor het implementeren van een algoritme exponentiële probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-355">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="bb3c5-356">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-356">No</span></span>|<span data-ttu-id="bb3c5-357">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-357">N/A</span></span>|  
|<span data-ttu-id="bb3c5-358">delta</span><span class="sxs-lookup"><span data-stu-id="bb3c5-358">delta</span></span>|<span data-ttu-id="bb3c5-359">Een positief getal in seconden, de wachttijd interval verhoging opgeven.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-359">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="bb3c5-360">Wordt gebruikt voor het implementeren van de algoritmen lineaire en exponentieel probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-360">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="bb3c5-361">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-361">No</span></span>|<span data-ttu-id="bb3c5-362">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-362">N/A</span></span>|  
|<span data-ttu-id="bb3c5-363">eerste-fast-probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="bb3c5-363">first-fast-retry</span></span>|<span data-ttu-id="bb3c5-364">Indien ingesteld op `true` , de eerste nieuwe poging wordt onmiddellijk uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-364">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="bb3c5-365">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="bb3c5-366">Wanneer alleen de `interval` is opgegeven, **vaste** interval voor nieuwe pogingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-366">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="bb3c5-367">Wanneer alleen de `interval` en `delta` zijn opgegeven, een **lineaire** interval opnieuw proberen algoritme wordt gebruikt, waarbij de tijd tussen nieuwe pogingen wordt berekend op basis van de volgende formule - `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-367">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="bb3c5-368">Wanneer de `interval`, `max-interval` en `delta` zijn opgegeven, **exponentiële** interval opnieuw proberen algoritme wordt toegepast, waarbij de wachttijd tussen de pogingen groeit exponentieel van de waarde van `interval` naar de waarde `max-interval` volgens de volgende forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-368">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-369">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-369">Usage</span></span>  
 <span data-ttu-id="bb3c5-370">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="bb3c5-370">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="bb3c5-371">Houd er rekening mee dat informatie over het gebruik van onderliggende beleidsbeperkingen wordt overgenomen door dit beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="bb3c5-372">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-373">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bb3c5-374"><a name="ReturnResponse"></a>Antwoord retourneren</span><span class="sxs-lookup"><span data-stu-id="bb3c5-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="bb3c5-375">De `return-response` beleid annuleert pipeline-uitvoering en retourneert een standaardwaarde of een aangepast antwoord naar de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-375">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="bb3c5-376">Standaardantwoord is `200 OK` met geen hoofdcode.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="bb3c5-377">Aangepast antwoord kan worden opgegeven via de instructies voor een context variabele of beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="bb3c5-378">Wanneer beide zijn opgegeven, wordt de reactie die is opgenomen in de context-variabele voordat het naar de aanroeper wordt geretourneerd door de beleidsverklaringen gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-378">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-379">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-380">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-381">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-381">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-382">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-382">Element</span></span>|<span data-ttu-id="bb3c5-383">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-383">Description</span></span>|<span data-ttu-id="bb3c5-384">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-385">Return-antwoord</span><span class="sxs-lookup"><span data-stu-id="bb3c5-385">return-response</span></span>|<span data-ttu-id="bb3c5-386">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-386">Root element.</span></span>|<span data-ttu-id="bb3c5-387">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-387">Yes</span></span>|  
|<span data-ttu-id="bb3c5-388">set-header</span><span class="sxs-lookup"><span data-stu-id="bb3c5-388">set-header</span></span>|<span data-ttu-id="bb3c5-389">Een [set-header](api-management-transformation-policies.md#SetHTTPheader) beleidsverklaring.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="bb3c5-390">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-390">No</span></span>|  
|<span data-ttu-id="bb3c5-391">set-instantie</span><span class="sxs-lookup"><span data-stu-id="bb3c5-391">set-body</span></span>|<span data-ttu-id="bb3c5-392">Een [set hoofdtekst](api-management-transformation-policies.md#SetBody) beleidsverklaring.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="bb3c5-393">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-393">No</span></span>|  
|<span data-ttu-id="bb3c5-394">status instellen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-394">set-status</span></span>|<span data-ttu-id="bb3c5-395">Een [status instellen](api-management-advanced-policies.md#SetStatus) beleidsverklaring.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="bb3c5-396">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-397">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-397">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-398">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-398">Attribute</span></span>|<span data-ttu-id="bb3c5-399">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-399">Description</span></span>|<span data-ttu-id="bb3c5-400">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-401">naam van een antwoord variabele</span><span class="sxs-lookup"><span data-stu-id="bb3c5-401">response-variable-name</span></span>|<span data-ttu-id="bb3c5-402">De naam van de variabele context waarnaar wordt verwezen vanuit, bijvoorbeeld een upstream [aanvragen verzenden](api-management-advanced-policies.md#SendRequest) beleid en met een `Response` object</span><span class="sxs-lookup"><span data-stu-id="bb3c5-402">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="bb3c5-403">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-404">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-404">Usage</span></span>  
 <span data-ttu-id="bb3c5-405">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-405">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-406">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-407">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bb3c5-408"><a name="SendOneWayRequest"></a>Eenzijdige aanvraag verzenden</span><span class="sxs-lookup"><span data-stu-id="bb3c5-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="bb3c5-409">De `send-one-way-request` beleid voor de opgegeven aanvraag verzendt naar de opgegeven URL zonder te wachten op reactie.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-409">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-410">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-411">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-411">Example</span></span>  
 <span data-ttu-id="bb3c5-412">Dit beleid voorbeeld toont een voorbeeld van het gebruik van de `send-one-way-request` beleid een bericht te verzenden naar toegestane chatruimten als de HTTP-antwoordcode groter dan of gelijk zijn aan 500 is.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-412">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="bb3c5-413">Zie voor meer informatie over dit voorbeeld [met behulp van externe services van de Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-413">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-414">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-414">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-415">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-415">Element</span></span>|<span data-ttu-id="bb3c5-416">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-416">Description</span></span>|<span data-ttu-id="bb3c5-417">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-418">een-manier-verzoek om te verzenden</span><span class="sxs-lookup"><span data-stu-id="bb3c5-418">send-one-way-request</span></span>|<span data-ttu-id="bb3c5-419">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-419">Root element.</span></span>|<span data-ttu-id="bb3c5-420">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-420">Yes</span></span>|  
|<span data-ttu-id="bb3c5-421">URL</span><span class="sxs-lookup"><span data-stu-id="bb3c5-421">url</span></span>|<span data-ttu-id="bb3c5-422">De URL van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-422">The URL of the request.</span></span>|<span data-ttu-id="bb3c5-423">Er is geen als modus = kopiëren; anders Ja.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bb3c5-424">Methode</span><span class="sxs-lookup"><span data-stu-id="bb3c5-424">method</span></span>|<span data-ttu-id="bb3c5-425">De HTTP-methode voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-425">The HTTP method for the request.</span></span>|<span data-ttu-id="bb3c5-426">Er is geen als modus = kopiëren; anders Ja.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bb3c5-427">koptekst</span><span class="sxs-lookup"><span data-stu-id="bb3c5-427">header</span></span>|<span data-ttu-id="bb3c5-428">Aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-428">Request header.</span></span> <span data-ttu-id="bb3c5-429">Meerdere headeronderdelen voor meerdere aanvraagheaders gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="bb3c5-430">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-430">No</span></span>|  
|<span data-ttu-id="bb3c5-431">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="bb3c5-431">body</span></span>|<span data-ttu-id="bb3c5-432">De aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-432">The request body.</span></span>|<span data-ttu-id="bb3c5-433">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-434">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-434">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-435">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-435">Attribute</span></span>|<span data-ttu-id="bb3c5-436">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-436">Description</span></span>|<span data-ttu-id="bb3c5-437">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-437">Required</span></span>|<span data-ttu-id="bb3c5-438">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bb3c5-439">modus = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-439">mode="string"</span></span>|<span data-ttu-id="bb3c5-440">Hiermee wordt bepaald of dit een nieuwe aanvraag of een kopie van de huidige aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-440">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="bb3c5-441">In de uitgaande modus, modus = kopiëren de aanvraagtekst niet geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-441">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="bb3c5-442">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-442">No</span></span>|<span data-ttu-id="bb3c5-443">Nieuw</span><span class="sxs-lookup"><span data-stu-id="bb3c5-443">New</span></span>|  
|<span data-ttu-id="bb3c5-444">naam</span><span class="sxs-lookup"><span data-stu-id="bb3c5-444">name</span></span>|<span data-ttu-id="bb3c5-445">Hiermee geeft u de naam van de header moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-445">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="bb3c5-446">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-446">Yes</span></span>|<span data-ttu-id="bb3c5-447">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-447">N/A</span></span>|  
|<span data-ttu-id="bb3c5-448">Er bestaat actie</span><span class="sxs-lookup"><span data-stu-id="bb3c5-448">exists-action</span></span>|<span data-ttu-id="bb3c5-449">Hiermee geeft u op welke actie moet worden uitgevoerd wanneer de header is al opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-449">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="bb3c5-450">Dit kenmerk moet een van de volgende waarden hebben.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-450">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="bb3c5-451">-onderdrukking - vervangt de waarde van de bestaande koptekst.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-451">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="bb3c5-452">de waarde van de bestaande header vervangen - skip - niet.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-452">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="bb3c5-453">-toevoeg - de waarde toegevoegd aan de bestaande headerwaarde.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-453">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="bb3c5-454">-delete - verwijdert de header van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-454">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="bb3c5-455">Als de waarde `override` opnemen van meerdere vermeldingen met dezelfde naam resulteert in de koptekst wordt ingesteld in overeenstemming met alle vermeldingen (die wordt vermeld meerdere keren); alleen de vermelde waarden worden ingesteld in het resultaat.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-455">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="bb3c5-456">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-456">No</span></span>|<span data-ttu-id="bb3c5-457">overschrijven</span><span class="sxs-lookup"><span data-stu-id="bb3c5-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-458">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-458">Usage</span></span>  
 <span data-ttu-id="bb3c5-459">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-459">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-460">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-461">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bb3c5-462"><a name="SendRequest"></a>Aanvraag verzenden</span><span class="sxs-lookup"><span data-stu-id="bb3c5-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="bb3c5-463">De `send-request` beleid voor de opgegeven aanvraag verzendt naar de opgegeven URL wacht niet langer dan de ingestelde time-out-waarde.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-463">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-464">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-465">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-465">Example</span></span>  
 <span data-ttu-id="bb3c5-466">In dit voorbeeld ziet een manier om te controleren of de verwijzing naar een token met een server voor autorisatie.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-466">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="bb3c5-467">Zie voor meer informatie over dit voorbeeld [met behulp van externe services van de Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-467">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-468">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-468">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-469">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-469">Element</span></span>|<span data-ttu-id="bb3c5-470">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-470">Description</span></span>|<span data-ttu-id="bb3c5-471">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-472">aanvragen verzenden</span><span class="sxs-lookup"><span data-stu-id="bb3c5-472">send-request</span></span>|<span data-ttu-id="bb3c5-473">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-473">Root element.</span></span>|<span data-ttu-id="bb3c5-474">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-474">Yes</span></span>|  
|<span data-ttu-id="bb3c5-475">URL</span><span class="sxs-lookup"><span data-stu-id="bb3c5-475">url</span></span>|<span data-ttu-id="bb3c5-476">De URL van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-476">The URL of the request.</span></span>|<span data-ttu-id="bb3c5-477">Er is geen als modus = kopiëren; anders Ja.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bb3c5-478">Methode</span><span class="sxs-lookup"><span data-stu-id="bb3c5-478">method</span></span>|<span data-ttu-id="bb3c5-479">De HTTP-methode voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-479">The HTTP method for the request.</span></span>|<span data-ttu-id="bb3c5-480">Er is geen als modus = kopiëren; anders Ja.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bb3c5-481">koptekst</span><span class="sxs-lookup"><span data-stu-id="bb3c5-481">header</span></span>|<span data-ttu-id="bb3c5-482">Aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-482">Request header.</span></span> <span data-ttu-id="bb3c5-483">Meerdere headeronderdelen voor meerdere aanvraagheaders gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="bb3c5-484">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-484">No</span></span>|  
|<span data-ttu-id="bb3c5-485">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="bb3c5-485">body</span></span>|<span data-ttu-id="bb3c5-486">De aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-486">The request body.</span></span>|<span data-ttu-id="bb3c5-487">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-488">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-488">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-489">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-489">Attribute</span></span>|<span data-ttu-id="bb3c5-490">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-490">Description</span></span>|<span data-ttu-id="bb3c5-491">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-491">Required</span></span>|<span data-ttu-id="bb3c5-492">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bb3c5-493">modus = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-493">mode="string"</span></span>|<span data-ttu-id="bb3c5-494">Hiermee wordt bepaald of dit een nieuwe aanvraag of een kopie van de huidige aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-494">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="bb3c5-495">In de uitgaande modus, modus = kopiëren de aanvraagtekst niet geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-495">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="bb3c5-496">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-496">No</span></span>|<span data-ttu-id="bb3c5-497">Nieuw</span><span class="sxs-lookup"><span data-stu-id="bb3c5-497">New</span></span>|  
|<span data-ttu-id="bb3c5-498">antwoord-variabele-name = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-498">response-variable-name="string"</span></span>|<span data-ttu-id="bb3c5-499">Als deze niet aanwezig is, `context.Response` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="bb3c5-500">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-500">No</span></span>|<span data-ttu-id="bb3c5-501">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-501">N/A</span></span>|  
|<span data-ttu-id="bb3c5-502">time-out = 'integer'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-502">timeout="integer"</span></span>|<span data-ttu-id="bb3c5-503">De time-outinterval in seconden voordat de aanroep naar de URL is mislukt.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-503">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="bb3c5-504">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-504">No</span></span>|<span data-ttu-id="bb3c5-505">60</span><span class="sxs-lookup"><span data-stu-id="bb3c5-505">60</span></span>|  
|<span data-ttu-id="bb3c5-506">fout negeren</span><span class="sxs-lookup"><span data-stu-id="bb3c5-506">ignore-error</span></span>|<span data-ttu-id="bb3c5-507">Indien true en de aanvraag resulteert in een fout opgetreden:</span><span class="sxs-lookup"><span data-stu-id="bb3c5-507">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="bb3c5-508">-Als de naam van een antwoord variabele bevat een null-waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="bb3c5-509">-Als de naam van een antwoord variabele is niet opgegeven, context. Aanvraag wordt niet bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="bb3c5-510">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-510">No</span></span>|<span data-ttu-id="bb3c5-511">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="bb3c5-511">false</span></span>|  
|<span data-ttu-id="bb3c5-512">naam</span><span class="sxs-lookup"><span data-stu-id="bb3c5-512">name</span></span>|<span data-ttu-id="bb3c5-513">Hiermee geeft u de naam van de header moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-513">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="bb3c5-514">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-514">Yes</span></span>|<span data-ttu-id="bb3c5-515">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-515">N/A</span></span>|  
|<span data-ttu-id="bb3c5-516">Er bestaat actie</span><span class="sxs-lookup"><span data-stu-id="bb3c5-516">exists-action</span></span>|<span data-ttu-id="bb3c5-517">Hiermee geeft u op welke actie moet worden uitgevoerd wanneer de header is al opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-517">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="bb3c5-518">Dit kenmerk moet een van de volgende waarden hebben.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-518">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="bb3c5-519">-onderdrukking - vervangt de waarde van de bestaande koptekst.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-519">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="bb3c5-520">de waarde van de bestaande header vervangen - skip - niet.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-520">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="bb3c5-521">-toevoeg - de waarde toegevoegd aan de bestaande headerwaarde.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-521">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="bb3c5-522">-delete - verwijdert de header van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-522">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="bb3c5-523">Als de waarde `override` opnemen van meerdere vermeldingen met dezelfde naam resulteert in de koptekst wordt ingesteld in overeenstemming met alle vermeldingen (die wordt vermeld meerdere keren); alleen de vermelde waarden worden ingesteld in het resultaat.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-523">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="bb3c5-524">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-524">No</span></span>|<span data-ttu-id="bb3c5-525">overschrijven</span><span class="sxs-lookup"><span data-stu-id="bb3c5-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-526">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-526">Usage</span></span>  
 <span data-ttu-id="bb3c5-527">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-527">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-528">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-529">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bb3c5-530"><a name="SetHttpProxy"></a>Set HTTP-proxy</span><span class="sxs-lookup"><span data-stu-id="bb3c5-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="bb3c5-531">De `proxy` beleid kunt u op route-aanvragen worden doorgestuurd naar de back-ends via een HTTP-proxy.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-531">The `proxy` policy allows you to route requests forwarded to backends via an HTTP proxy.</span></span> <span data-ttu-id="bb3c5-532">Alleen HTTP (niet HTTPS) wordt ondersteund tussen de gateway en de proxy.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-532">Only HTTP (not HTTPS) is supported between the gateway and the proxy.</span></span> <span data-ttu-id="bb3c5-533">Basic- en NTLM-verificatie.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-534">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-535">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-535">Example</span></span>  
<span data-ttu-id="bb3c5-536">Let op het gebruik van [eigenschappen](api-management-howto-properties.md) als waarden van de gebruikersnaam en wachtwoord om te voorkomen dat gevoelige informatie op te slaan in het beleidsdocument.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-536">Note the use of [properties](api-management-howto-properties.md) as values of the username and password to avoid storing sensitive information in the policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-537">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-537">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-538">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-538">Element</span></span>|<span data-ttu-id="bb3c5-539">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-539">Description</span></span>|<span data-ttu-id="bb3c5-540">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-541">Proxy</span><span class="sxs-lookup"><span data-stu-id="bb3c5-541">proxy</span></span>|<span data-ttu-id="bb3c5-542">Hoofdelement</span><span class="sxs-lookup"><span data-stu-id="bb3c5-542">Root element</span></span>|<span data-ttu-id="bb3c5-543">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="bb3c5-544">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-544">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-545">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-545">Attribute</span></span>|<span data-ttu-id="bb3c5-546">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-546">Description</span></span>|<span data-ttu-id="bb3c5-547">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-547">Required</span></span>|<span data-ttu-id="bb3c5-548">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bb3c5-549">URL = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-549">url="string"</span></span>|<span data-ttu-id="bb3c5-550">Proxy-URL in de vorm van http://host:port.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-550">Proxy URL in the form of http://host:port.</span></span>|<span data-ttu-id="bb3c5-551">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-551">Yes</span></span>|<span data-ttu-id="bb3c5-552">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-552">N/A</span></span>|  
|<span data-ttu-id="bb3c5-553">gebruikersnaam = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-553">username="string"</span></span>|<span data-ttu-id="bb3c5-554">De gebruikersnaam moet worden gebruikt voor verificatie met de proxy.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-554">Username to be used for authentication with the proxy.</span></span>|<span data-ttu-id="bb3c5-555">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-555">No</span></span>|<span data-ttu-id="bb3c5-556">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-556">N/A</span></span>|  
|<span data-ttu-id="bb3c5-557">wachtwoord = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-557">password="string"</span></span>|<span data-ttu-id="bb3c5-558">Wachtwoord moet worden gebruikt voor verificatie met de proxy.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-558">Password to be used for authentication with the proxy.</span></span>|<span data-ttu-id="bb3c5-559">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-559">No</span></span>|<span data-ttu-id="bb3c5-560">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="bb3c5-561">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-561">Usage</span></span>  
 <span data-ttu-id="bb3c5-562">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-562">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-563">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="bb3c5-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="bb3c5-564">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bb3c5-565"><a name="SetRequestMethod"></a>Set-aanvraagmethode</span><span class="sxs-lookup"><span data-stu-id="bb3c5-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="bb3c5-566">De `set-method` beleid kunt u de HTTP-aanvraagmethode voor een aanvraag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-566">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-567">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-568">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-568">Example</span></span>  
 <span data-ttu-id="bb3c5-569">Dit voorbeeld-beleid die gebruikmaakt van de `set-method` beleid toont een voorbeeld van een bericht verzenden naar toegestane chatruimten als de HTTP-antwoordcode groter dan of gelijk zijn aan 500 is.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-569">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="bb3c5-570">Zie voor meer informatie over dit voorbeeld [met behulp van externe services van de Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-570">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-571">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-571">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-572">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-572">Element</span></span>|<span data-ttu-id="bb3c5-573">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-573">Description</span></span>|<span data-ttu-id="bb3c5-574">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-575">set-methode</span><span class="sxs-lookup"><span data-stu-id="bb3c5-575">set-method</span></span>|<span data-ttu-id="bb3c5-576">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-576">Root element.</span></span> <span data-ttu-id="bb3c5-577">De waarde van het element bevat de HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-577">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="bb3c5-578">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-579">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-579">Usage</span></span>  
 <span data-ttu-id="bb3c5-580">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-580">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-581">**Beleid secties:** inkomend, bij fouten</span><span class="sxs-lookup"><span data-stu-id="bb3c5-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-582">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bb3c5-583"><a name="SetStatus"></a>Set-statuscode</span><span class="sxs-lookup"><span data-stu-id="bb3c5-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="bb3c5-584">De `set-status` beleid wordt de HTTP-statuscode ingesteld op de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-584">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-585">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-586">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-586">Example</span></span>  
 <span data-ttu-id="bb3c5-587">In dit voorbeeld laat zien hoe een 401-respons retourneren als het verificatietoken ongeldig is.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-587">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="bb3c5-588">Zie voor meer informatie [met behulp van externe services van de Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="bb3c5-588">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-589">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-589">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-590">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-590">Element</span></span>|<span data-ttu-id="bb3c5-591">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-591">Description</span></span>|<span data-ttu-id="bb3c5-592">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-593">status instellen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-593">set-status</span></span>|<span data-ttu-id="bb3c5-594">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-594">Root element.</span></span>|<span data-ttu-id="bb3c5-595">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-596">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-596">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-597">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-597">Attribute</span></span>|<span data-ttu-id="bb3c5-598">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-598">Description</span></span>|<span data-ttu-id="bb3c5-599">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-599">Required</span></span>|<span data-ttu-id="bb3c5-600">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bb3c5-601">code = 'integer'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-601">code="integer"</span></span>|<span data-ttu-id="bb3c5-602">De HTTP-statuscode te retourneren.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-602">The HTTP status code to return.</span></span>|<span data-ttu-id="bb3c5-603">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-603">Yes</span></span>|<span data-ttu-id="bb3c5-604">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-604">N/A</span></span>|  
|<span data-ttu-id="bb3c5-605">reden = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="bb3c5-605">reason="string"</span></span>|<span data-ttu-id="bb3c5-606">Een beschrijving van de reden voor het retourneren van de statuscode.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-606">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="bb3c5-607">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-607">Yes</span></span>|<span data-ttu-id="bb3c5-608">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-609">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-609">Usage</span></span>  
 <span data-ttu-id="bb3c5-610">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-610">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-611">**Beleid secties:** uitgaand, back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-612">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bb3c5-613"><a name="set-variable"></a>Variabele instellen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="bb3c5-614">De `set-variable` beleid declareert een [context](api-management-policy-expressions.md#ContextVariables) variabele en hieraan een waarde die is opgegeven een [expressie](api-management-policy-expressions.md) of een letterlijke tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-614">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="bb3c5-615">Als de expressie een letterlijke reeks bevat wordt geconverteerd naar een tekenreeks en het type van de waarde niet `System.String`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-615">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="bb3c5-616"><a name="set-variablePolicyStatement"></a>Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="bb3c5-617"><a name="set-variableExample"></a>Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="bb3c5-618">Het volgende voorbeeld wordt een variabele beleid instellen in de sectie binnenkomend.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-618">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="bb3c5-619">Deze variabele beleid instellen maakt een `isMobile` Booleaanse [context](api-management-policy-expressions.md#ContextVariables) variabele die is ingesteld op true als de `User-Agent` aanvraag-header bevat de tekst `iPad` of `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-620">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-620">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-621">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-621">Element</span></span>|<span data-ttu-id="bb3c5-622">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-622">Description</span></span>|<span data-ttu-id="bb3c5-623">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-624">variabele instellen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-624">set-variable</span></span>|<span data-ttu-id="bb3c5-625">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-625">Root element.</span></span>|<span data-ttu-id="bb3c5-626">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-627">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-627">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-628">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-628">Attribute</span></span>|<span data-ttu-id="bb3c5-629">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-629">Description</span></span>|<span data-ttu-id="bb3c5-630">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-631">naam</span><span class="sxs-lookup"><span data-stu-id="bb3c5-631">name</span></span>|<span data-ttu-id="bb3c5-632">De naam van de variabele.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-632">The name of the variable.</span></span>|<span data-ttu-id="bb3c5-633">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-633">Yes</span></span>|  
|<span data-ttu-id="bb3c5-634">waarde</span><span class="sxs-lookup"><span data-stu-id="bb3c5-634">value</span></span>|<span data-ttu-id="bb3c5-635">De waarde van de variabele.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-635">The value of the variable.</span></span> <span data-ttu-id="bb3c5-636">Dit kan een expressie of een letterlijke waarde zijn.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="bb3c5-637">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-638">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-638">Usage</span></span>  
 <span data-ttu-id="bb3c5-639">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-639">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-640">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-641">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="bb3c5-642"><a name="set-variableAllowedTypes"></a>Toegestane typen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="bb3c5-643">Expressies in de `set-variable` beleid moet een van de volgende eenvoudige typen retourneren.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-643">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="bb3c5-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="bb3c5-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="bb3c5-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="bb3c5-645">System.SByte</span></span>  
  
-   <span data-ttu-id="bb3c5-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="bb3c5-646">System.Byte</span></span>  
  
-   <span data-ttu-id="bb3c5-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="bb3c5-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="bb3c5-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="bb3c5-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="bb3c5-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="bb3c5-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="bb3c5-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="bb3c5-650">System.Int16</span></span>  
  
-   <span data-ttu-id="bb3c5-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="bb3c5-651">System.Int32</span></span>  
  
-   <span data-ttu-id="bb3c5-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="bb3c5-652">System.Int64</span></span>  
  
-   <span data-ttu-id="bb3c5-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="bb3c5-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="bb3c5-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="bb3c5-654">System.Single</span></span>  
  
-   <span data-ttu-id="bb3c5-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="bb3c5-655">System.Double</span></span>  
  
-   <span data-ttu-id="bb3c5-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="bb3c5-656">System.Guid</span></span>  
  
-   <span data-ttu-id="bb3c5-657">System.String</span><span class="sxs-lookup"><span data-stu-id="bb3c5-657">System.String</span></span>  
  
-   <span data-ttu-id="bb3c5-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="bb3c5-658">System.Char</span></span>  
  
-   <span data-ttu-id="bb3c5-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="bb3c5-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="bb3c5-660">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="bb3c5-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="bb3c5-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="bb3c5-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="bb3c5-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="bb3c5-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="bb3c5-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="bb3c5-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="bb3c5-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="bb3c5-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="bb3c5-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-669">System.Single?</span></span>  
  
-   <span data-ttu-id="bb3c5-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-670">System.Double?</span></span>  
  
-   <span data-ttu-id="bb3c5-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="bb3c5-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-672">System.String?</span></span>  
  
-   <span data-ttu-id="bb3c5-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-673">System.Char?</span></span>  
  
-   <span data-ttu-id="bb3c5-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="bb3c5-674">System.DateTime?</span></span>  

##  <span data-ttu-id="bb3c5-675"><a name="Trace"></a>Tracering</span><span class="sxs-lookup"><span data-stu-id="bb3c5-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="bb3c5-676">De `trace` beleid wordt toegevoegd een tekenreeks in de [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-676">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="bb3c5-677">Het beleid wordt uitgevoerd, alleen wanneer tracering wordt geactiveerd, dat wil zeggen `Ocp-Apim-Trace` aanvraagheader aanwezig is en is ingesteld op `true` en `Ocp-Apim-Subscription-Key` aanvraagheader aanwezig is en een geldige sleutel die is gekoppeld aan het beheerdersaccount bevat.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-677">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-678">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-679">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-679">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-680">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-680">Element</span></span>|<span data-ttu-id="bb3c5-681">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-681">Description</span></span>|<span data-ttu-id="bb3c5-682">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-683">tracering</span><span class="sxs-lookup"><span data-stu-id="bb3c5-683">trace</span></span>|<span data-ttu-id="bb3c5-684">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-684">Root element.</span></span>|<span data-ttu-id="bb3c5-685">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-686">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-686">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-687">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-687">Attribute</span></span>|<span data-ttu-id="bb3c5-688">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-688">Description</span></span>|<span data-ttu-id="bb3c5-689">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-689">Required</span></span>|<span data-ttu-id="bb3c5-690">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bb3c5-691">Bron</span><span class="sxs-lookup"><span data-stu-id="bb3c5-691">source</span></span>|<span data-ttu-id="bb3c5-692">Letterlijke tekenreeks relevant zijn voor de traceringsviewer en de bron van het bericht op te geven.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-692">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="bb3c5-693">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-693">Yes</span></span>|<span data-ttu-id="bb3c5-694">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-695">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-695">Usage</span></span>  
 <span data-ttu-id="bb3c5-696">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="bb3c5-696">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="bb3c5-697">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="bb3c5-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bb3c5-698">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bb3c5-699"><a name="Wait"></a>Wacht</span><span class="sxs-lookup"><span data-stu-id="bb3c5-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="bb3c5-700">De `wait` beleid bijbehorende directe onderliggende beleidsregels parallel worden uitgevoerd en wordt gewacht op alle of een van de bijbehorende directe onderliggende beleidsregels te voltooien voordat deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-700">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="bb3c5-701">Het beleid voor de wachttijd kan hebben als het beleid direct onderliggende [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), en [transportbesturing](api-management-advanced-policies.md#choose) beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-701">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bb3c5-702">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="bb3c5-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bb3c5-703">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bb3c5-703">Example</span></span>  
 <span data-ttu-id="bb3c5-704">In het volgende voorbeeld zijn er twee `choose` beleid als beleid direct onderliggende van de `wait` beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-704">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="bb3c5-705">Elk van deze `choose` beleid parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="bb3c5-706">Elke `choose` beleid probeert op te halen van een waarde in de cache.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-706">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="bb3c5-707">Als er een cache ontbreekt, wordt een back-endservice aangeroepen om de waarde.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-707">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="bb3c5-708">In dit voorbeeld de `wait` beleid niet wordt voltooid totdat alle van de bijbehorende directe onderliggende beleidsregels hebt voltooid, omdat de `for` kenmerk is ingesteld op `all`.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-708">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="bb3c5-709">In dit voorbeeld de variabelen context (`execute-branch-one`, `value-one`, `execute-branch-two`, en `value-two`) zijn gedeclareerd buiten het bereik van dit voorbeeldbeleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-709">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bb3c5-710">Elementen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-710">Elements</span></span>  
  
|<span data-ttu-id="bb3c5-711">Element</span><span class="sxs-lookup"><span data-stu-id="bb3c5-711">Element</span></span>|<span data-ttu-id="bb3c5-712">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-712">Description</span></span>|<span data-ttu-id="bb3c5-713">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bb3c5-714">Wacht</span><span class="sxs-lookup"><span data-stu-id="bb3c5-714">wait</span></span>|<span data-ttu-id="bb3c5-715">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-715">Root element.</span></span> <span data-ttu-id="bb3c5-716">Alleen onderliggende elementen bevat mogelijk `send-request`, `cache-lookup-value`, en `choose` beleid.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="bb3c5-717">Ja</span><span class="sxs-lookup"><span data-stu-id="bb3c5-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bb3c5-718">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="bb3c5-718">Attributes</span></span>  
  
|<span data-ttu-id="bb3c5-719">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="bb3c5-719">Attribute</span></span>|<span data-ttu-id="bb3c5-720">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bb3c5-720">Description</span></span>|<span data-ttu-id="bb3c5-721">Vereist</span><span class="sxs-lookup"><span data-stu-id="bb3c5-721">Required</span></span>|<span data-ttu-id="bb3c5-722">Standaard</span><span class="sxs-lookup"><span data-stu-id="bb3c5-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bb3c5-723">voor</span><span class="sxs-lookup"><span data-stu-id="bb3c5-723">for</span></span>|<span data-ttu-id="bb3c5-724">Hiermee wordt bepaald of de `wait` beleid wacht tot alle directe onderliggende beleidsregels is voltooid of alleen bestaan.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-724">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="bb3c5-725">Toegestane waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="bb3c5-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="bb3c5-726">-   `all`-Wacht totdat alle directe onderliggende beleidsregels om te voltooien</span><span class="sxs-lookup"><span data-stu-id="bb3c5-726">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="bb3c5-727">-een - wachten op een directe onderliggende beleid om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-727">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="bb3c5-728">Zodra het eerste directe onderliggende beleid is voltooid, de `wait` beleid is voltooid en de uitvoering van een ander beleid direct onderliggende is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="bb3c5-728">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="bb3c5-729">Nee</span><span class="sxs-lookup"><span data-stu-id="bb3c5-729">No</span></span>|<span data-ttu-id="bb3c5-730">Alle</span><span class="sxs-lookup"><span data-stu-id="bb3c5-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bb3c5-731">Gebruik</span><span class="sxs-lookup"><span data-stu-id="bb3c5-731">Usage</span></span>  
 <span data-ttu-id="bb3c5-732">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="bb3c5-732">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bb3c5-733">**Beleid secties:** inkomend, uitgaand back-end</span><span class="sxs-lookup"><span data-stu-id="bb3c5-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="bb3c5-734">**Beleid scopes:**alle scopes</span><span class="sxs-lookup"><span data-stu-id="bb3c5-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="bb3c5-735">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bb3c5-735">Next steps</span></span>
<span data-ttu-id="bb3c5-736">Zie voor meer informatie, werken met beleid:</span><span class="sxs-lookup"><span data-stu-id="bb3c5-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="bb3c5-737">Beleidsregels in API Management</span><span class="sxs-lookup"><span data-stu-id="bb3c5-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="bb3c5-738">Beleidsexpressies</span><span class="sxs-lookup"><span data-stu-id="bb3c5-738">Policy expressions</span></span>](api-management-policy-expressions.md)
