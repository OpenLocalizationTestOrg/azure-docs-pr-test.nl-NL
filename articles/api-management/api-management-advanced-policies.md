---
title: aaaAzure API Management Geavanceerde beleidsregels | Microsoft Docs
description: Meer informatie over Hallo Geavanceerde beleidsregels beschikbaar voor gebruik in Azure API Management.
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
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="641ab-103">API Management Geavanceerde beleidsregels</span><span class="sxs-lookup"><span data-stu-id="641ab-103">API Management advanced policies</span></span>
<span data-ttu-id="641ab-104">Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen.</span><span class="sxs-lookup"><span data-stu-id="641ab-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="641ab-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="641ab-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="641ab-106"><a name="AdvancedPolicies"></a>Geavanceerde beleidsregels</span><span class="sxs-lookup"><span data-stu-id="641ab-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="641ab-107">[Transportbesturing](api-management-advanced-policies.md#choose) - voorwaardelijk is van toepassing op basis van resultaten van de evaluatie van Booleaanse waarde Hallo Hallo beleidsverklaringen [expressies](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="641ab-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="641ab-108">[Doorsturen van aanvraag](#ForwardRequest) -stuurt Hallo aanvraag toohello back-endservice.</span><span class="sxs-lookup"><span data-stu-id="641ab-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="641ab-109">[Gelijktijdigheid beperken](#LimitConcurrency) -voorkomt u dat beleid wordt uitgevoerd door meer dan een opgegeven aantal aanvragen op een tijdstip Hallo ingesloten.</span><span class="sxs-lookup"><span data-stu-id="641ab-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="641ab-110">[Meld u tooEvent Hub](#log-to-eventhub) -verzendt berichten in Hallo indeling tooan Event Hub wordt gedefinieerd door een entiteit van het logboek opgegeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="641ab-111">[Antwoord model](#mock-response) -pipeline-uitvoering wordt afgebroken en een mocked antwoord geretourneerd rechtstreeks toohello aanroeper.</span><span class="sxs-lookup"><span data-stu-id="641ab-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="641ab-112">[Probeer](#Retry) -uitvoering van de nieuwe pogingen van Hallo ingesloten beleidsverklaringen, als en totdat Hallo-voorwaarde is voldaan.</span><span class="sxs-lookup"><span data-stu-id="641ab-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="641ab-113">Uitvoering wordt herhaald op Hallo opgegeven tijdsintervallen en up toohello opgegeven aantal nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="641ab-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="641ab-114">[Antwoord retourneren](#ReturnResponse) -wordt afgebroken pijplijn uitvoering en retourneert Hallo opgegeven antwoord rechtstreeks toohello aanroeper.</span><span class="sxs-lookup"><span data-stu-id="641ab-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="641ab-115">[Eenzijdige aanvraag verzenden](#SendOneWayRequest) -verzendt een aanvraag toohello URL opgegeven zonder te wachten op reactie.</span><span class="sxs-lookup"><span data-stu-id="641ab-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="641ab-116">[Aanvraag verzenden](#SendRequest) -verzendt een aanvraag toohello URL opgegeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="641ab-117">[HTTP-proxy ingesteld](#SetHttpProxy) -kunt u aanvragen tooroute doorgestuurd via een HTTP-proxy.</span><span class="sxs-lookup"><span data-stu-id="641ab-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="641ab-118">[Stel aanvraagmethode](#SetRequestMethod) -kunt u toochange Hallo HTTP-methode voor een aanvraag.</span><span class="sxs-lookup"><span data-stu-id="641ab-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="641ab-119">[Statuscode ingesteld](#SetStatus) -wijzigingen Hallo HTTP status code toohello opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="641ab-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="641ab-120">[Variabele instellen](api-management-advanced-policies.md#set-variable) -zich blijft voordoen een waarde in een benoemde [context](api-management-policy-expressions.md#ContextVariables) variabele voor latere toegang.</span><span class="sxs-lookup"><span data-stu-id="641ab-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="641ab-121">[Tracering](#Trace) -wordt een tekenreeks toegevoegd in Hallo [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="641ab-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="641ab-122">[Wacht](#Wait) -wacht voor ingesloten [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), of [transportbesturing](api-management-advanced-policies.md#choose) beleid toocomplete voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="641ab-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="641ab-123"><a name="choose"></a>Controlestroom</span><span class="sxs-lookup"><span data-stu-id="641ab-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="641ab-124">Hallo `choose` beleid van toepassing is ingesloten beleid op basis van resultaat van evaluatie van Booleaanse expressies, vergelijkbare tooan if vervolgens else of een switch Hallo instructies in een programmeertaal maken.</span><span class="sxs-lookup"><span data-stu-id="641ab-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="641ab-125"><a name="ChoosePolicyStatement"></a>Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="641ab-126">Hallo beleid voor toegangsbeheer stroom moet ten minste één bevatten `<when/>` element.</span><span class="sxs-lookup"><span data-stu-id="641ab-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="641ab-127">Hallo `<otherwise/>` element is optioneel.</span><span class="sxs-lookup"><span data-stu-id="641ab-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="641ab-128">Voorwaarden `<when/>` elementen worden in volgorde van hun binnen Hallo beleid geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="641ab-129">Beleid voor instructie (s) die tussen Hallo eerst `<when/>` element met kenmerk gelijk is aan voorwaarde `true` worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="641ab-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="641ab-130">Beleid omsloten Hallo `<otherwise/>` element, indien aanwezig, wordt toegepast als alle Hallo `<when/>` voorwaarde elementkenmerken zijn `false`.</span><span class="sxs-lookup"><span data-stu-id="641ab-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="641ab-131">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="641ab-131">Examples</span></span>  
  
####  <span data-ttu-id="641ab-132"><a name="ChooseExample"></a>Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="641ab-133">Hallo volgende voorbeeld toont een [variabele instellen](api-management-advanced-policies.md#set-variable) beleid en twee beleidsregels voor beheer-stroom.</span><span class="sxs-lookup"><span data-stu-id="641ab-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="641ab-134">Hallo-variabele beleid instellen is in binnenkomende sectie Hallo en maakt een `isMobile` Booleaanse [context](api-management-policy-expressions.md#ContextVariables) variabele die tootrue is ingesteld als hello `User-Agent` aanvraag-header bevat de tekst hello `iPad` of `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="641ab-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="641ab-135">eerste beleid voor toegangsbeheer stroom Hallo zich ook in sectie inkomende hello en voorwaardelijk wordt een van twee [querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) beleidsregels, afhankelijk van de waarde Hallo Hallo `isMobile` context-variabele.</span><span class="sxs-lookup"><span data-stu-id="641ab-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="641ab-136">Hallo tweede besturingselement stroom beleid is in de uitgaande sectie Hallo en voorwaardelijk geldt Hallo [XML converteren tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) beleid wanneer `isMobile` te is ingesteld`true`.</span><span class="sxs-lookup"><span data-stu-id="641ab-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="641ab-137">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-137">Example</span></span>  
 <span data-ttu-id="641ab-138">Dit voorbeeld ziet u hoe tooperform filteren op inhoud door het verwijderen van elementen uit Hallo antwoord ontvangen van de back-endservice Hallo bij gebruik van Hallo `Starter` product.</span><span class="sxs-lookup"><span data-stu-id="641ab-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="641ab-139">Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too34:30 vooruit.</span><span class="sxs-lookup"><span data-stu-id="641ab-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="641ab-140">Start op 31:50 toosee een overzicht van [Hallo donker Sky Forecast API](https://developer.forecast.io/) gebruikt voor deze demonstratie.</span><span class="sxs-lookup"><span data-stu-id="641ab-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="641ab-141">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-141">Elements</span></span>  
  
|<span data-ttu-id="641ab-142">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-142">Element</span></span>|<span data-ttu-id="641ab-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-143">Description</span></span>|<span data-ttu-id="641ab-144">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-145">Kies</span><span class="sxs-lookup"><span data-stu-id="641ab-145">choose</span></span>|<span data-ttu-id="641ab-146">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-146">Root element.</span></span>|<span data-ttu-id="641ab-147">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-147">Yes</span></span>|  
|<span data-ttu-id="641ab-148">Wanneer</span><span class="sxs-lookup"><span data-stu-id="641ab-148">when</span></span>|<span data-ttu-id="641ab-149">voorwaarde toouse voor Hallo Hallo `if` of `ifelse` delen van Hallo `choose` beleid.</span><span class="sxs-lookup"><span data-stu-id="641ab-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="641ab-150">Als hello `choose` beleid heeft meerdere `when` secties, ze worden opeenvolgend geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="641ab-151">Eenmaal Hallo `condition` van een wanneer element te evalueert`true`, niet verder `when` voorwaarden worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="641ab-152">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-152">Yes</span></span>|  
|<span data-ttu-id="641ab-153">anders</span><span class="sxs-lookup"><span data-stu-id="641ab-153">otherwise</span></span>|<span data-ttu-id="641ab-154">Hallo beleid codefragment toobe gebruikt als geen van Hallo bevat `when` voorwaarden te evalueren`true`.</span><span class="sxs-lookup"><span data-stu-id="641ab-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="641ab-155">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-156">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-156">Attributes</span></span>  
  
|<span data-ttu-id="641ab-157">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-157">Attribute</span></span>|<span data-ttu-id="641ab-158">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-158">Description</span></span>|<span data-ttu-id="641ab-159">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="641ab-160">conditie = "Boole-expressie &#124; Constante Booleaanse'</span><span class="sxs-lookup"><span data-stu-id="641ab-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="641ab-161">Hallo Booleaanse expressie of constante tooevaluated wanneer Hallo die `when` beleidsverklaring wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="641ab-162">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-162">Yes</span></span>|  
  
###  <span data-ttu-id="641ab-163"><a name="ChooseUsage"></a>Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="641ab-164">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-165">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-166">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="641ab-167"><a name="ForwardRequest"></a>Doorsturen van aanvraag</span><span class="sxs-lookup"><span data-stu-id="641ab-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="641ab-168">Hallo `forward-request` beleid stuurt Hallo binnenkomende aanvraag toohello back-endservice opgegeven in de aanvraag Hallo [context](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="641ab-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="641ab-169">Hallo back-end service URL is opgegeven in Hallo API [instellingen](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) en kan worden gewijzigd met behulp van Hallo [back-endservice ingesteld](api-management-transformation-policies.md) beleid.</span><span class="sxs-lookup"><span data-stu-id="641ab-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="641ab-170">Verwijderen van dit beleid resulteert in het Hallo-aanvraag niet doorgestuurd toohello back-end-service en het Hallo-beleid in uitgaande sectie Hallo onmiddellijk worden geëvalueerd na geslaagde voltooiing Hallo Hallo beleidsregels in Hallo inkomende sectie.</span><span class="sxs-lookup"><span data-stu-id="641ab-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-171">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="641ab-172">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="641ab-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="641ab-173">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-173">Example</span></span>  
 <span data-ttu-id="641ab-174">Hallo stuurt volgende API-niveau beleid alle aanvragen toohello back-endservice met een time-outinterval van 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="641ab-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="641ab-175">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-175">Example</span></span>  
 <span data-ttu-id="641ab-176">Het beleid voor deze bewerking gebruikt Hallo `base` element tooinherit Hallo back-end-beleid van Hallo bovenliggende API-niveau bereik.</span><span class="sxs-lookup"><span data-stu-id="641ab-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="641ab-177">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-177">Example</span></span>  
 <span data-ttu-id="641ab-178">Deze bewerking beleid stuurt alle aanvragen toohello back-endservice met een time-out van 120 expliciet en neemt geen Hallo bovenliggende niveau back-end-API-beleid.</span><span class="sxs-lookup"><span data-stu-id="641ab-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="641ab-179">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-179">Example</span></span>  
 <span data-ttu-id="641ab-180">Het beleid voor deze bewerking niet doorsturen van aanvragen toohello back-endservice.</span><span class="sxs-lookup"><span data-stu-id="641ab-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="641ab-181">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-181">Elements</span></span>  
  
|<span data-ttu-id="641ab-182">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-182">Element</span></span>|<span data-ttu-id="641ab-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-183">Description</span></span>|<span data-ttu-id="641ab-184">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-185">voorwaarts-aanvraag</span><span class="sxs-lookup"><span data-stu-id="641ab-185">forward-request</span></span>|<span data-ttu-id="641ab-186">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-186">Root element.</span></span>|<span data-ttu-id="641ab-187">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-188">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-188">Attributes</span></span>  
  
|<span data-ttu-id="641ab-189">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-189">Attribute</span></span>|<span data-ttu-id="641ab-190">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-190">Description</span></span>|<span data-ttu-id="641ab-191">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-191">Required</span></span>|<span data-ttu-id="641ab-192">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="641ab-193">time-out = 'integer'</span><span class="sxs-lookup"><span data-stu-id="641ab-193">timeout="integer"</span></span>|<span data-ttu-id="641ab-194">Hallo-time-outinterval in seconden alvorens het Hallo-aanroep toohello back-endservice is mislukt.</span><span class="sxs-lookup"><span data-stu-id="641ab-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="641ab-195">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-195">No</span></span>|<span data-ttu-id="641ab-196">Geen time-out</span><span class="sxs-lookup"><span data-stu-id="641ab-196">No timeout</span></span>|  
|<span data-ttu-id="641ab-197">Volg omleidingen = "true &#124; False"</span><span class="sxs-lookup"><span data-stu-id="641ab-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="641ab-198">Geeft aan of omleidingen van back-endservice Hallo worden gevolgd door Hallo gateway of toohello aanroeper wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="641ab-199">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-199">No</span></span>|<span data-ttu-id="641ab-200">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="641ab-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-201">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-201">Usage</span></span>  
 <span data-ttu-id="641ab-202">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-203">**Beleid secties:** back-end</span><span class="sxs-lookup"><span data-stu-id="641ab-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="641ab-204">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="641ab-205"><a name="LimitConcurrency"></a>Limiet gelijktijdigheid van taken</span><span class="sxs-lookup"><span data-stu-id="641ab-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="641ab-206">Hallo `limit-concurrency` beleid voorkomt dat ingesloten beleid uit door meer dan een opgegeven aantal aanvragen Hallo op een bepaald moment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="641ab-207">Bij Hallo drempelwaarde overschrijdt, worden nieuwe aanvragen tooa wachtrij toegevoegd totdat Hallo maximum wachtrijlengte wordt bereikt.</span><span class="sxs-lookup"><span data-stu-id="641ab-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="641ab-208">Bij uitputting van de wachtrij mislukken nieuwe aanvragen onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="641ab-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="641ab-209"><a name="LimitConcurrencyStatement"></a>Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="641ab-210">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="641ab-210">Examples</span></span>  
  
####  <span data-ttu-id="641ab-211"><a name="ChooseExample"></a>Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="641ab-212">Hallo volgende voorbeeld laat zien hoe het aantal aanvragen toolimit tooa back-end op basis van het Hallo-waarde van een variabele context doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="641ab-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="641ab-213">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-213">Elements</span></span>  
  
|<span data-ttu-id="641ab-214">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-214">Element</span></span>|<span data-ttu-id="641ab-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-215">Description</span></span>|<span data-ttu-id="641ab-216">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="641ab-217">limiet gelijktijdigheid</span><span class="sxs-lookup"><span data-stu-id="641ab-217">limit-concurrency</span></span>|<span data-ttu-id="641ab-218">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-218">Root element.</span></span>|<span data-ttu-id="641ab-219">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-220">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-220">Attributes</span></span>  
  
|<span data-ttu-id="641ab-221">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-221">Attribute</span></span>|<span data-ttu-id="641ab-222">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-222">Description</span></span>|<span data-ttu-id="641ab-223">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-223">Required</span></span>|<span data-ttu-id="641ab-224">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="641ab-225">sleutel</span><span class="sxs-lookup"><span data-stu-id="641ab-225">key</span></span>|<span data-ttu-id="641ab-226">Een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="641ab-226">A string.</span></span> <span data-ttu-id="641ab-227">Een expressie toegestaan.</span><span class="sxs-lookup"><span data-stu-id="641ab-227">Expression allowed.</span></span> <span data-ttu-id="641ab-228">Hiermee geeft u Hallo gelijktijdigheid bereik.</span><span class="sxs-lookup"><span data-stu-id="641ab-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="641ab-229">Kan worden gedeeld door meerdere beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="641ab-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="641ab-230">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-230">Yes</span></span>|<span data-ttu-id="641ab-231">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-231">N/A</span></span>|  
|<span data-ttu-id="641ab-232">maximum aantal</span><span class="sxs-lookup"><span data-stu-id="641ab-232">max-count</span></span>|<span data-ttu-id="641ab-233">Een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="641ab-233">An integer.</span></span> <span data-ttu-id="641ab-234">Hiermee geeft u het maximale aantal aanvragen dat tooenter Hallo beleid zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="641ab-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="641ab-235">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-235">Yes</span></span>|<span data-ttu-id="641ab-236">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-236">N/A</span></span>|  
|<span data-ttu-id="641ab-237">timeout</span><span class="sxs-lookup"><span data-stu-id="641ab-237">timeout</span></span>|<span data-ttu-id="641ab-238">Een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="641ab-238">An integer.</span></span> <span data-ttu-id="641ab-239">Een expressie toegestaan.</span><span class="sxs-lookup"><span data-stu-id="641ab-239">Expression allowed.</span></span> <span data-ttu-id="641ab-240">Hiermee geeft u het aantal seconden dat een aanvraag wachten tooenter een scope voordat deze is mislukt met de moet Hallo ' 403 te veel aanvragen '</span><span class="sxs-lookup"><span data-stu-id="641ab-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="641ab-241">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-241">No</span></span>|<span data-ttu-id="641ab-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="641ab-242">Infinity</span></span>|  
|<span data-ttu-id="641ab-243">maximale wachtrijlengte</span><span class="sxs-lookup"><span data-stu-id="641ab-243">max-queue-length</span></span>|<span data-ttu-id="641ab-244">Een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="641ab-244">An integer.</span></span> <span data-ttu-id="641ab-245">Een expressie toegestaan.</span><span class="sxs-lookup"><span data-stu-id="641ab-245">Expression allowed.</span></span> <span data-ttu-id="641ab-246">Hiermee geeft u de maximale wachtrijlengte Hallo.</span><span class="sxs-lookup"><span data-stu-id="641ab-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="641ab-247">Inkomende aanvragen tooenter probeert dit beleid wordt beëindigd met ' 403 te veel aanvragen ' onmiddellijk wanneer Hallo wachtrij is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="641ab-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="641ab-248">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-248">No</span></span>|<span data-ttu-id="641ab-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="641ab-249">Infinity</span></span>|  
  
###  <span data-ttu-id="641ab-250"><a name="ChooseUsage"></a>Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="641ab-251">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-252">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-253">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="641ab-254"><a name="log-to-eventhub"></a>Meld u tooEvent Hub</span><span class="sxs-lookup"><span data-stu-id="641ab-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="641ab-255">Hallo `log-to-eventhub` beleid verzendt berichten in Hallo indeling tooan Event Hub gedefinieerd door een entiteit van het logboek opgegeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="641ab-256">Als de naam al aangeeft, worden Hallo beleid wordt gebruikt voor het opslaan van de geselecteerde aanvraag of antwoord contextinformatie voor online of offline-analyse.</span><span class="sxs-lookup"><span data-stu-id="641ab-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="641ab-257">Zie voor een stapsgewijze handleiding voor het configureren van een event hub en vastleggen van gebeurtenissen, [hoe toolog API Management-gebeurtenissen met Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="641ab-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-258">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="641ab-259">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-259">Example</span></span>  
 <span data-ttu-id="641ab-260">Elke tekenreeks kan worden gebruikt als Hallo waarde toobe vastgelegd in Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="641ab-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="641ab-261">In dit voorbeeld Hallo datum en tijd implementatie servicenaam, aanvraag-id, IP-adres en de naam van de bewerking voor alle binnenkomende oproepen zijn geregistreerde toohello event hub berichtenlogboek geregistreerd bij Hallo `contoso-logger` id.</span><span class="sxs-lookup"><span data-stu-id="641ab-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="641ab-262">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-262">Elements</span></span>  
  
|<span data-ttu-id="641ab-263">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-263">Element</span></span>|<span data-ttu-id="641ab-264">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-264">Description</span></span>|<span data-ttu-id="641ab-265">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-266">logboek voor eventhub</span><span class="sxs-lookup"><span data-stu-id="641ab-266">log-to-eventhub</span></span>|<span data-ttu-id="641ab-267">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-267">Root element.</span></span> <span data-ttu-id="641ab-268">Hallo-waarde van dit element is Hallo tekenreeks toolog tooyour event hub.</span><span class="sxs-lookup"><span data-stu-id="641ab-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="641ab-269">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-270">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-270">Attributes</span></span>  
  
|<span data-ttu-id="641ab-271">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-271">Attribute</span></span>|<span data-ttu-id="641ab-272">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-272">Description</span></span>|<span data-ttu-id="641ab-273">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="641ab-274">logboek-id</span><span class="sxs-lookup"><span data-stu-id="641ab-274">logger-id</span></span>|<span data-ttu-id="641ab-275">Hallo-id van Hallo berichtenlogboek geregistreerd met uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="641ab-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="641ab-276">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-276">Yes</span></span>|  
|<span data-ttu-id="641ab-277">partitie-id</span><span class="sxs-lookup"><span data-stu-id="641ab-277">partition-id</span></span>|<span data-ttu-id="641ab-278">Hiermee geeft u een index Hallo van Hallo partitie waarin berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="641ab-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="641ab-279">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="641ab-279">Optional.</span></span> <span data-ttu-id="641ab-280">Dit kenmerk kan niet worden gebruikt als `partition-key` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="641ab-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="641ab-281">Partitiesleutel</span><span class="sxs-lookup"><span data-stu-id="641ab-281">partition-key</span></span>|<span data-ttu-id="641ab-282">Hiermee geeft u Hallo-waarde die voor de partitietoewijzing van de wordt gebruikt wanneer berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="641ab-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="641ab-283">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="641ab-283">Optional.</span></span> <span data-ttu-id="641ab-284">Dit kenmerk kan niet worden gebruikt als `partition-id` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="641ab-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-285">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-285">Usage</span></span>  
 <span data-ttu-id="641ab-286">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-287">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-288">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="641ab-289"><a name="mock-response"></a>Mock-antwoord</span><span class="sxs-lookup"><span data-stu-id="641ab-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="641ab-290">Hallo `mock-response`, als de naam van de Hallo impliceert, is gebruikt toomock API's en bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="641ab-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="641ab-291">Het normale pipeline-uitvoering afgebroken en een mocked antwoord toohello aanroeper retourneert.</span><span class="sxs-lookup"><span data-stu-id="641ab-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="641ab-292">Hallo beleid probeert altijd tooreturn reacties van hoogste betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="641ab-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="641ab-293">Deze verkiest antwoord inhoud voorbeelden, indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="641ab-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="641ab-294">Het voorbeeld antwoorden van schema's, genereert wanneer schema's worden geleverd en voorbeelden niet.</span><span class="sxs-lookup"><span data-stu-id="641ab-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="641ab-295">Als geen van beide voorbeelden of schema's zijn gevonden, worden de antwoorden met geen inhoud geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-296">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="641ab-297">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="641ab-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="641ab-298">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-298">Elements</span></span>  
  
|<span data-ttu-id="641ab-299">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-299">Element</span></span>|<span data-ttu-id="641ab-300">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-300">Description</span></span>|<span data-ttu-id="641ab-301">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-302">nagebootste-antwoord</span><span class="sxs-lookup"><span data-stu-id="641ab-302">mock-response</span></span>|<span data-ttu-id="641ab-303">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-303">Root element.</span></span>|<span data-ttu-id="641ab-304">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-305">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-305">Attributes</span></span>  
  
|<span data-ttu-id="641ab-306">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-306">Attribute</span></span>|<span data-ttu-id="641ab-307">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-307">Description</span></span>|<span data-ttu-id="641ab-308">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-308">Required</span></span>|<span data-ttu-id="641ab-309">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="641ab-310">statuscode in</span><span class="sxs-lookup"><span data-stu-id="641ab-310">status-code</span></span>|<span data-ttu-id="641ab-311">Hiermee geeft u de statuscode van antwoord en is de bijbehorende voorbeeld gebruikte tooselect of schema.</span><span class="sxs-lookup"><span data-stu-id="641ab-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="641ab-312">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-312">No</span></span>|<span data-ttu-id="641ab-313">200</span><span class="sxs-lookup"><span data-stu-id="641ab-313">200</span></span>|  
|<span data-ttu-id="641ab-314">type inhoud</span><span class="sxs-lookup"><span data-stu-id="641ab-314">content-type</span></span>|<span data-ttu-id="641ab-315">Hiermee geeft u `Content-Type` headerwaarde antwoord en de bijbehorende voorbeeld gebruikte tooselect of schema.</span><span class="sxs-lookup"><span data-stu-id="641ab-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="641ab-316">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-316">No</span></span>|<span data-ttu-id="641ab-317">Geen</span><span class="sxs-lookup"><span data-stu-id="641ab-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-318">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-318">Usage</span></span>  
 <span data-ttu-id="641ab-319">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-320">**Beleid secties:** binnenkomende, uitgaande, bij fouten</span><span class="sxs-lookup"><span data-stu-id="641ab-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="641ab-321">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="641ab-322"><a name="Retry"></a>Probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="641ab-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="641ab-323">Hallo `retry` beleid de onderliggende beleidsregels eenmaal wordt uitgevoerd en vervolgens probeert om opnieuw de uitvoering ervan tot Hallo opnieuw `condition` wordt `false` of probeer het opnieuw `count` leeg.</span><span class="sxs-lookup"><span data-stu-id="641ab-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-324">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="641ab-325">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-325">Example</span></span>  
 <span data-ttu-id="641ab-326">In Hallo voorbeeld aanvraag forewarding na geprobeerd up tooten tijdstippen met behulp van de algoritme exponentiële probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="641ab-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="641ab-327">Aangezien `first-fast-retry` is ingesteld toofalse, alle nieuwe pogingen worden onderwerp toohello exponsntial opnieuw algoritme.</span><span class="sxs-lookup"><span data-stu-id="641ab-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="641ab-328">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-328">Elements</span></span>  
  
|<span data-ttu-id="641ab-329">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-329">Element</span></span>|<span data-ttu-id="641ab-330">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-330">Description</span></span>|<span data-ttu-id="641ab-331">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-332">retry</span><span class="sxs-lookup"><span data-stu-id="641ab-332">retry</span></span>|<span data-ttu-id="641ab-333">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-333">Root element.</span></span> <span data-ttu-id="641ab-334">Kan geen ander beleid bevatten als de onderliggende elementen.</span><span class="sxs-lookup"><span data-stu-id="641ab-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="641ab-335">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-336">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-336">Attributes</span></span>  
  
|<span data-ttu-id="641ab-337">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-337">Attribute</span></span>|<span data-ttu-id="641ab-338">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-338">Description</span></span>|<span data-ttu-id="641ab-339">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-339">Required</span></span>|<span data-ttu-id="641ab-340">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="641ab-341">Voorwaarde</span><span class="sxs-lookup"><span data-stu-id="641ab-341">condition</span></span>|<span data-ttu-id="641ab-342">Een boolean letterlijke waarde of [expressie](api-management-policy-expressions.md) opgeven als nieuwe pogingen moeten worden gestopt (`false`) of vervolg (`true`).</span><span class="sxs-lookup"><span data-stu-id="641ab-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="641ab-343">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-343">Yes</span></span>|<span data-ttu-id="641ab-344">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-344">N/A</span></span>|  
|<span data-ttu-id="641ab-345">Aantal</span><span class="sxs-lookup"><span data-stu-id="641ab-345">count</span></span>|<span data-ttu-id="641ab-346">Een positief getal Hallo kunt u het maximum aantal nieuwe pogingen tooattempt opgeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="641ab-347">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-347">Yes</span></span>|<span data-ttu-id="641ab-348">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-348">N/A</span></span>|  
|<span data-ttu-id="641ab-349">interval</span><span class="sxs-lookup"><span data-stu-id="641ab-349">interval</span></span>|<span data-ttu-id="641ab-350">Een positief getal in seconden hello Wacht-interval tussen nieuwe pogingen van Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="641ab-351">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-351">Yes</span></span>|<span data-ttu-id="641ab-352">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-352">N/A</span></span>|  
|<span data-ttu-id="641ab-353">Max-interval</span><span class="sxs-lookup"><span data-stu-id="641ab-353">max-interval</span></span>|<span data-ttu-id="641ab-354">Een positief getal in seconden hello maximale wachttijd-interval tussen nieuwe pogingen van Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="641ab-355">Is het gebruikte tooimplement een algoritme exponentiële probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="641ab-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="641ab-356">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-356">No</span></span>|<span data-ttu-id="641ab-357">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-357">N/A</span></span>|  
|<span data-ttu-id="641ab-358">delta</span><span class="sxs-lookup"><span data-stu-id="641ab-358">delta</span></span>|<span data-ttu-id="641ab-359">Een positief getal in seconden Hallo Wacht interval verhoging opgeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="641ab-360">Het is gebruikte tooimplement Hallo lineaire en exponentieel opnieuw algoritmen.</span><span class="sxs-lookup"><span data-stu-id="641ab-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="641ab-361">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-361">No</span></span>|<span data-ttu-id="641ab-362">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-362">N/A</span></span>|  
|<span data-ttu-id="641ab-363">eerste-fast-probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="641ab-363">first-fast-retry</span></span>|<span data-ttu-id="641ab-364">Als instellen te `true` , Hallo eerste nieuwe poging wordt onmiddellijk uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="641ab-365">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="641ab-366">Wanneer alleen Hallo `interval` is opgegeven, **vaste** interval voor nieuwe pogingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="641ab-367">Wanneer alleen Hallo `interval` en `delta` zijn opgegeven, een **lineaire** interval opnieuw proberen algoritme wordt gebruikt, waarbij de tijd tussen nieuwe pogingen berekende volgens Hallo formule - de volgende `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="641ab-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="641ab-368">Wanneer Hallo `interval`, `max-interval` en `delta` zijn opgegeven, **exponentiële** interval opnieuw proberen algoritme wordt toegepast, waarbij Hallo wachttijd tussen nieuwe pogingen Hallo groeit exponentieel van Hallo-waarde van `interval`toohello waarde `max-interval` op basis van de volgende toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="641ab-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="641ab-369">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-369">Usage</span></span>  
 <span data-ttu-id="641ab-370">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="641ab-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="641ab-371">Houd er rekening mee dat informatie over het gebruik van onderliggende beleidsbeperkingen wordt overgenomen door dit beleid.</span><span class="sxs-lookup"><span data-stu-id="641ab-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="641ab-372">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-373">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="641ab-374"><a name="ReturnResponse"></a>Antwoord retourneren</span><span class="sxs-lookup"><span data-stu-id="641ab-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="641ab-375">Hallo `return-response` beleid annuleert pipeline-uitvoering en retourneert een standaardwaarde of een aangepast antwoord toohello aanroeper.</span><span class="sxs-lookup"><span data-stu-id="641ab-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="641ab-376">Standaardantwoord is `200 OK` met geen hoofdcode.</span><span class="sxs-lookup"><span data-stu-id="641ab-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="641ab-377">Aangepast antwoord kan worden opgegeven via de instructies voor een context variabele of beleid.</span><span class="sxs-lookup"><span data-stu-id="641ab-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="641ab-378">Wanneer beide zijn opgegeven, wordt door Hallo beleidsverklaringen antwoord Hallo opgenomen in de context-variabele Hallo gewijzigd voordat het toohello aanroeper wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-379">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="641ab-380">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="641ab-381">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-381">Elements</span></span>  
  
|<span data-ttu-id="641ab-382">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-382">Element</span></span>|<span data-ttu-id="641ab-383">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-383">Description</span></span>|<span data-ttu-id="641ab-384">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-385">Return-antwoord</span><span class="sxs-lookup"><span data-stu-id="641ab-385">return-response</span></span>|<span data-ttu-id="641ab-386">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-386">Root element.</span></span>|<span data-ttu-id="641ab-387">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-387">Yes</span></span>|  
|<span data-ttu-id="641ab-388">set-header</span><span class="sxs-lookup"><span data-stu-id="641ab-388">set-header</span></span>|<span data-ttu-id="641ab-389">Een [set-header](api-management-transformation-policies.md#SetHTTPheader) beleidsverklaring.</span><span class="sxs-lookup"><span data-stu-id="641ab-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="641ab-390">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-390">No</span></span>|  
|<span data-ttu-id="641ab-391">set-instantie</span><span class="sxs-lookup"><span data-stu-id="641ab-391">set-body</span></span>|<span data-ttu-id="641ab-392">Een [set hoofdtekst](api-management-transformation-policies.md#SetBody) beleidsverklaring.</span><span class="sxs-lookup"><span data-stu-id="641ab-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="641ab-393">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-393">No</span></span>|  
|<span data-ttu-id="641ab-394">status instellen</span><span class="sxs-lookup"><span data-stu-id="641ab-394">set-status</span></span>|<span data-ttu-id="641ab-395">Een [status instellen](api-management-advanced-policies.md#SetStatus) beleidsverklaring.</span><span class="sxs-lookup"><span data-stu-id="641ab-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="641ab-396">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-397">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-397">Attributes</span></span>  
  
|<span data-ttu-id="641ab-398">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-398">Attribute</span></span>|<span data-ttu-id="641ab-399">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-399">Description</span></span>|<span data-ttu-id="641ab-400">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="641ab-401">naam van een antwoord variabele</span><span class="sxs-lookup"><span data-stu-id="641ab-401">response-variable-name</span></span>|<span data-ttu-id="641ab-402">Hallo Hallo context variabele voor waarnaar wordt verwezen vanuit, bijvoorbeeld een upstream [aanvragen verzenden](api-management-advanced-policies.md#SendRequest) beleid en met een `Response` object</span><span class="sxs-lookup"><span data-stu-id="641ab-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="641ab-403">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="641ab-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-404">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-404">Usage</span></span>  
 <span data-ttu-id="641ab-405">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-406">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-407">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="641ab-408"><a name="SendOneWayRequest"></a>Eenzijdige aanvraag verzenden</span><span class="sxs-lookup"><span data-stu-id="641ab-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="641ab-409">Hallo `send-one-way-request` beleid verzendt Hallo opgegeven aanvraag toohello URL opgegeven zonder te wachten op reactie.</span><span class="sxs-lookup"><span data-stu-id="641ab-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-410">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="641ab-411">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-411">Example</span></span>  
 <span data-ttu-id="641ab-412">Dit beleid voorbeeld toont een voorbeeld van het gebruik van Hallo `send-one-way-request` beleid toosend bericht tooa toegestane chatruimten als Hallo HTTP-antwoordcode groter dan of gelijk too500 is.</span><span class="sxs-lookup"><span data-stu-id="641ab-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="641ab-413">Zie voor meer informatie over dit voorbeeld [met behulp van externe services van hello Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="641ab-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="641ab-414">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-414">Elements</span></span>  
  
|<span data-ttu-id="641ab-415">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-415">Element</span></span>|<span data-ttu-id="641ab-416">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-416">Description</span></span>|<span data-ttu-id="641ab-417">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-418">een-manier-verzoek om te verzenden</span><span class="sxs-lookup"><span data-stu-id="641ab-418">send-one-way-request</span></span>|<span data-ttu-id="641ab-419">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-419">Root element.</span></span>|<span data-ttu-id="641ab-420">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-420">Yes</span></span>|  
|<span data-ttu-id="641ab-421">URL</span><span class="sxs-lookup"><span data-stu-id="641ab-421">url</span></span>|<span data-ttu-id="641ab-422">Hallo-URL van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="641ab-422">hello URL of hello request.</span></span>|<span data-ttu-id="641ab-423">Er is geen als modus = kopiëren; anders Ja.</span><span class="sxs-lookup"><span data-stu-id="641ab-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="641ab-424">Methode</span><span class="sxs-lookup"><span data-stu-id="641ab-424">method</span></span>|<span data-ttu-id="641ab-425">Hallo HTTP-methode voor Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="641ab-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="641ab-426">Er is geen als modus = kopiëren; anders Ja.</span><span class="sxs-lookup"><span data-stu-id="641ab-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="641ab-427">koptekst</span><span class="sxs-lookup"><span data-stu-id="641ab-427">header</span></span>|<span data-ttu-id="641ab-428">Aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="641ab-428">Request header.</span></span> <span data-ttu-id="641ab-429">Meerdere headeronderdelen voor meerdere aanvraagheaders gebruiken.</span><span class="sxs-lookup"><span data-stu-id="641ab-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="641ab-430">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-430">No</span></span>|  
|<span data-ttu-id="641ab-431">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="641ab-431">body</span></span>|<span data-ttu-id="641ab-432">Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="641ab-432">hello request body.</span></span>|<span data-ttu-id="641ab-433">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-434">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-434">Attributes</span></span>  
  
|<span data-ttu-id="641ab-435">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-435">Attribute</span></span>|<span data-ttu-id="641ab-436">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-436">Description</span></span>|<span data-ttu-id="641ab-437">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-437">Required</span></span>|<span data-ttu-id="641ab-438">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="641ab-439">modus = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="641ab-439">mode="string"</span></span>|<span data-ttu-id="641ab-440">Hiermee wordt bepaald of dit een nieuwe aanvraag of een kopie van de huidige aanvraag Hallo is.</span><span class="sxs-lookup"><span data-stu-id="641ab-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="641ab-441">In de uitgaande modus, modus = kopie Hallo aanvraagtekst niet geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="641ab-442">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-442">No</span></span>|<span data-ttu-id="641ab-443">Nieuw</span><span class="sxs-lookup"><span data-stu-id="641ab-443">New</span></span>|  
|<span data-ttu-id="641ab-444">naam</span><span class="sxs-lookup"><span data-stu-id="641ab-444">name</span></span>|<span data-ttu-id="641ab-445">Geeft de naam Hallo van Hallo header toobe set.</span><span class="sxs-lookup"><span data-stu-id="641ab-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="641ab-446">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-446">Yes</span></span>|<span data-ttu-id="641ab-447">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-447">N/A</span></span>|  
|<span data-ttu-id="641ab-448">Er bestaat actie</span><span class="sxs-lookup"><span data-stu-id="641ab-448">exists-action</span></span>|<span data-ttu-id="641ab-449">Geeft aan welke actie tootake Hallo-header is al opgegeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="641ab-450">Dit kenmerk moet een van de volgende waarden Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="641ab-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="641ab-451">-onderdrukkingswaarde - vervangt Hallo van bestaande Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="641ab-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="641ab-452">-skip - vervangen Hallo bestaande header-waarde niet.</span><span class="sxs-lookup"><span data-stu-id="641ab-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="641ab-453">-toevoeg - Hallo waarde toohello bestaande header-waarde wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="641ab-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="641ab-454">Hallo-header verwijdert - delete - van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="641ab-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="641ab-455">Als de waarde te`override` opnemen van meerdere vermeldingen met Hallo dezelfde resulteert in het Hallo-header wordt ingesteld volgens tooall-vermeldingen (die wordt vermeld meerdere keren) naam; alleen de vermelde waarden worden ingesteld in Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="641ab-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="641ab-456">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-456">No</span></span>|<span data-ttu-id="641ab-457">overschrijven</span><span class="sxs-lookup"><span data-stu-id="641ab-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-458">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-458">Usage</span></span>  
 <span data-ttu-id="641ab-459">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-460">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-461">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="641ab-462"><a name="SendRequest"></a>Aanvraag verzenden</span><span class="sxs-lookup"><span data-stu-id="641ab-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="641ab-463">Hallo `send-request` beleid verzendt Hallo opgegeven aanvraag toohello opgegeven URL, niet langer wachten dan Hallo time-outwaarde instellen.</span><span class="sxs-lookup"><span data-stu-id="641ab-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-464">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="641ab-465">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-465">Example</span></span>  
 <span data-ttu-id="641ab-466">Dit voorbeeld ziet u een referentie-token met een server autorisatie eenrichtingssessie tooverify.</span><span class="sxs-lookup"><span data-stu-id="641ab-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="641ab-467">Zie voor meer informatie over dit voorbeeld [met behulp van externe services van hello Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="641ab-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
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
  
### <a name="elements"></a><span data-ttu-id="641ab-468">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-468">Elements</span></span>  
  
|<span data-ttu-id="641ab-469">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-469">Element</span></span>|<span data-ttu-id="641ab-470">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-470">Description</span></span>|<span data-ttu-id="641ab-471">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-472">aanvragen verzenden</span><span class="sxs-lookup"><span data-stu-id="641ab-472">send-request</span></span>|<span data-ttu-id="641ab-473">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-473">Root element.</span></span>|<span data-ttu-id="641ab-474">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-474">Yes</span></span>|  
|<span data-ttu-id="641ab-475">URL</span><span class="sxs-lookup"><span data-stu-id="641ab-475">url</span></span>|<span data-ttu-id="641ab-476">Hallo-URL van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="641ab-476">hello URL of hello request.</span></span>|<span data-ttu-id="641ab-477">Er is geen als modus = kopiëren; anders Ja.</span><span class="sxs-lookup"><span data-stu-id="641ab-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="641ab-478">Methode</span><span class="sxs-lookup"><span data-stu-id="641ab-478">method</span></span>|<span data-ttu-id="641ab-479">Hallo HTTP-methode voor Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="641ab-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="641ab-480">Er is geen als modus = kopiëren; anders Ja.</span><span class="sxs-lookup"><span data-stu-id="641ab-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="641ab-481">koptekst</span><span class="sxs-lookup"><span data-stu-id="641ab-481">header</span></span>|<span data-ttu-id="641ab-482">Aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="641ab-482">Request header.</span></span> <span data-ttu-id="641ab-483">Meerdere headeronderdelen voor meerdere aanvraagheaders gebruiken.</span><span class="sxs-lookup"><span data-stu-id="641ab-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="641ab-484">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-484">No</span></span>|  
|<span data-ttu-id="641ab-485">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="641ab-485">body</span></span>|<span data-ttu-id="641ab-486">Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="641ab-486">hello request body.</span></span>|<span data-ttu-id="641ab-487">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-488">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-488">Attributes</span></span>  
  
|<span data-ttu-id="641ab-489">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-489">Attribute</span></span>|<span data-ttu-id="641ab-490">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-490">Description</span></span>|<span data-ttu-id="641ab-491">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-491">Required</span></span>|<span data-ttu-id="641ab-492">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="641ab-493">modus = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="641ab-493">mode="string"</span></span>|<span data-ttu-id="641ab-494">Hiermee wordt bepaald of dit een nieuwe aanvraag of een kopie van de huidige aanvraag Hallo is.</span><span class="sxs-lookup"><span data-stu-id="641ab-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="641ab-495">In de uitgaande modus, modus = kopie Hallo aanvraagtekst niet geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="641ab-496">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-496">No</span></span>|<span data-ttu-id="641ab-497">Nieuw</span><span class="sxs-lookup"><span data-stu-id="641ab-497">New</span></span>|  
|<span data-ttu-id="641ab-498">antwoord-variabele-name = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="641ab-498">response-variable-name="string"</span></span>|<span data-ttu-id="641ab-499">Als deze niet aanwezig is, `context.Response` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="641ab-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="641ab-500">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-500">No</span></span>|<span data-ttu-id="641ab-501">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-501">N/A</span></span>|  
|<span data-ttu-id="641ab-502">time-out = 'integer'</span><span class="sxs-lookup"><span data-stu-id="641ab-502">timeout="integer"</span></span>|<span data-ttu-id="641ab-503">Hallo-time-outinterval in seconden voordat de aanroep van Hallo toohello URL is mislukt.</span><span class="sxs-lookup"><span data-stu-id="641ab-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="641ab-504">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-504">No</span></span>|<span data-ttu-id="641ab-505">60</span><span class="sxs-lookup"><span data-stu-id="641ab-505">60</span></span>|  
|<span data-ttu-id="641ab-506">fout negeren</span><span class="sxs-lookup"><span data-stu-id="641ab-506">ignore-error</span></span>|<span data-ttu-id="641ab-507">Als true en Hallo resulteert in een fout opgetreden aanvragen:</span><span class="sxs-lookup"><span data-stu-id="641ab-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="641ab-508">-Als de naam van een antwoord variabele bevat een null-waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="641ab-509">-Als de naam van een antwoord variabele is niet opgegeven, context. Aanvraag wordt niet bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="641ab-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="641ab-510">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-510">No</span></span>|<span data-ttu-id="641ab-511">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="641ab-511">false</span></span>|  
|<span data-ttu-id="641ab-512">naam</span><span class="sxs-lookup"><span data-stu-id="641ab-512">name</span></span>|<span data-ttu-id="641ab-513">Geeft de naam Hallo van Hallo header toobe set.</span><span class="sxs-lookup"><span data-stu-id="641ab-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="641ab-514">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-514">Yes</span></span>|<span data-ttu-id="641ab-515">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-515">N/A</span></span>|  
|<span data-ttu-id="641ab-516">Er bestaat actie</span><span class="sxs-lookup"><span data-stu-id="641ab-516">exists-action</span></span>|<span data-ttu-id="641ab-517">Geeft aan welke actie tootake Hallo-header is al opgegeven.</span><span class="sxs-lookup"><span data-stu-id="641ab-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="641ab-518">Dit kenmerk moet een van de volgende waarden Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="641ab-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="641ab-519">-onderdrukkingswaarde - vervangt Hallo van bestaande Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="641ab-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="641ab-520">-skip - vervangen Hallo bestaande header-waarde niet.</span><span class="sxs-lookup"><span data-stu-id="641ab-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="641ab-521">-toevoeg - Hallo waarde toohello bestaande header-waarde wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="641ab-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="641ab-522">Hallo-header verwijdert - delete - van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="641ab-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="641ab-523">Als de waarde te`override` opnemen van meerdere vermeldingen met Hallo dezelfde resulteert in het Hallo-header wordt ingesteld volgens tooall-vermeldingen (die wordt vermeld meerdere keren) naam; alleen de vermelde waarden worden ingesteld in Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="641ab-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="641ab-524">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-524">No</span></span>|<span data-ttu-id="641ab-525">overschrijven</span><span class="sxs-lookup"><span data-stu-id="641ab-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-526">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-526">Usage</span></span>  
 <span data-ttu-id="641ab-527">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-528">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-529">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="641ab-530"><a name="SetHttpProxy"></a>Set HTTP-proxy</span><span class="sxs-lookup"><span data-stu-id="641ab-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="641ab-531">Hallo `proxy` beleid kunt u tooroute aanvragen doorgestuurd toobackends via een HTTP-proxy.</span><span class="sxs-lookup"><span data-stu-id="641ab-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="641ab-532">Alleen HTTP (niet HTTPS) wordt ondersteund tussen Hallo-gateway en het Hallo-proxy.</span><span class="sxs-lookup"><span data-stu-id="641ab-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="641ab-533">Basic- en NTLM-verificatie.</span><span class="sxs-lookup"><span data-stu-id="641ab-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-534">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="641ab-535">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-535">Example</span></span>  
<span data-ttu-id="641ab-536">Houd er rekening mee Hallo gebruik van [eigenschappen](api-management-howto-properties.md) als de waarden van het Hallo-gebruikersnaam en wachtwoord tooavoid gevoelige informatie op te slaan in Hallo beleidsdocument.</span><span class="sxs-lookup"><span data-stu-id="641ab-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="641ab-537">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-537">Elements</span></span>  
  
|<span data-ttu-id="641ab-538">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-538">Element</span></span>|<span data-ttu-id="641ab-539">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-539">Description</span></span>|<span data-ttu-id="641ab-540">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-541">Proxy</span><span class="sxs-lookup"><span data-stu-id="641ab-541">proxy</span></span>|<span data-ttu-id="641ab-542">Hoofdelement</span><span class="sxs-lookup"><span data-stu-id="641ab-542">Root element</span></span>|<span data-ttu-id="641ab-543">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="641ab-544">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-544">Attributes</span></span>  
  
|<span data-ttu-id="641ab-545">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-545">Attribute</span></span>|<span data-ttu-id="641ab-546">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-546">Description</span></span>|<span data-ttu-id="641ab-547">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-547">Required</span></span>|<span data-ttu-id="641ab-548">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="641ab-549">URL = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="641ab-549">url="string"</span></span>|<span data-ttu-id="641ab-550">Proxy-URL in de vorm Hallo van http://host:port.</span><span class="sxs-lookup"><span data-stu-id="641ab-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="641ab-551">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-551">Yes</span></span>|<span data-ttu-id="641ab-552">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-552">N/A</span></span>|  
|<span data-ttu-id="641ab-553">gebruikersnaam = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="641ab-553">username="string"</span></span>|<span data-ttu-id="641ab-554">Gebruikersnaam toobe gebruikt voor verificatie met Hallo proxy.</span><span class="sxs-lookup"><span data-stu-id="641ab-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="641ab-555">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-555">No</span></span>|<span data-ttu-id="641ab-556">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-556">N/A</span></span>|  
|<span data-ttu-id="641ab-557">wachtwoord = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="641ab-557">password="string"</span></span>|<span data-ttu-id="641ab-558">Wachtwoord toobe gebruikt voor verificatie met Hallo proxy.</span><span class="sxs-lookup"><span data-stu-id="641ab-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="641ab-559">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-559">No</span></span>|<span data-ttu-id="641ab-560">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="641ab-561">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-561">Usage</span></span>  
 <span data-ttu-id="641ab-562">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-563">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="641ab-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="641ab-564">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="641ab-565"><a name="SetRequestMethod"></a>Set-aanvraagmethode</span><span class="sxs-lookup"><span data-stu-id="641ab-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="641ab-566">Hallo `set-method` beleid kunt u toochange Hallo HTTP-aanvraagmethode voor een aanvraag.</span><span class="sxs-lookup"><span data-stu-id="641ab-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-567">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="641ab-568">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-568">Example</span></span>  
 <span data-ttu-id="641ab-569">Dit voorbeeld-beleid die gebruikmaakt van Hallo `set-method` beleid toont een voorbeeld van het verzenden van bericht tooa toegestane chatruimten als Hallo HTTP-antwoordcode groter dan is of gelijk too500.</span><span class="sxs-lookup"><span data-stu-id="641ab-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="641ab-570">Zie voor meer informatie over dit voorbeeld [met behulp van externe services van hello Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="641ab-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="641ab-571">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-571">Elements</span></span>  
  
|<span data-ttu-id="641ab-572">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-572">Element</span></span>|<span data-ttu-id="641ab-573">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-573">Description</span></span>|<span data-ttu-id="641ab-574">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-575">set-methode</span><span class="sxs-lookup"><span data-stu-id="641ab-575">set-method</span></span>|<span data-ttu-id="641ab-576">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-576">Root element.</span></span> <span data-ttu-id="641ab-577">Hallo-waarde van Hallo element geeft Hallo HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="641ab-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="641ab-578">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-579">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-579">Usage</span></span>  
 <span data-ttu-id="641ab-580">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-581">**Beleid secties:** inkomend, bij fouten</span><span class="sxs-lookup"><span data-stu-id="641ab-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="641ab-582">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="641ab-583"><a name="SetStatus"></a>Set-statuscode</span><span class="sxs-lookup"><span data-stu-id="641ab-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="641ab-584">Hallo `set-status` beleid sets Hallo HTTP status code toohello opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="641ab-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-585">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="641ab-586">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-586">Example</span></span>  
 <span data-ttu-id="641ab-587">Dit voorbeeld ziet u hoe tooreturn een 401-respons als Hallo verificatietoken is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="641ab-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="641ab-588">Zie voor meer informatie [met behulp van externe services van hello Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="641ab-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="641ab-589">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-589">Elements</span></span>  
  
|<span data-ttu-id="641ab-590">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-590">Element</span></span>|<span data-ttu-id="641ab-591">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-591">Description</span></span>|<span data-ttu-id="641ab-592">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-593">status instellen</span><span class="sxs-lookup"><span data-stu-id="641ab-593">set-status</span></span>|<span data-ttu-id="641ab-594">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-594">Root element.</span></span>|<span data-ttu-id="641ab-595">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-596">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-596">Attributes</span></span>  
  
|<span data-ttu-id="641ab-597">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-597">Attribute</span></span>|<span data-ttu-id="641ab-598">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-598">Description</span></span>|<span data-ttu-id="641ab-599">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-599">Required</span></span>|<span data-ttu-id="641ab-600">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="641ab-601">code = 'integer'</span><span class="sxs-lookup"><span data-stu-id="641ab-601">code="integer"</span></span>|<span data-ttu-id="641ab-602">Hallo HTTP status code tooreturn.</span><span class="sxs-lookup"><span data-stu-id="641ab-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="641ab-603">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-603">Yes</span></span>|<span data-ttu-id="641ab-604">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-604">N/A</span></span>|  
|<span data-ttu-id="641ab-605">reden = 'tekenreeks'</span><span class="sxs-lookup"><span data-stu-id="641ab-605">reason="string"</span></span>|<span data-ttu-id="641ab-606">Een beschrijving van Hallo reden voor het retourneren van Hallo-statuscode.</span><span class="sxs-lookup"><span data-stu-id="641ab-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="641ab-607">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-607">Yes</span></span>|<span data-ttu-id="641ab-608">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-609">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-609">Usage</span></span>  
 <span data-ttu-id="641ab-610">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-611">**Beleid secties:** uitgaand, back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-612">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="641ab-613"><a name="set-variable"></a>Variabele instellen</span><span class="sxs-lookup"><span data-stu-id="641ab-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="641ab-614">Hallo `set-variable` beleid declareert een [context](api-management-policy-expressions.md#ContextVariables) variabele en hieraan een waarde die is opgegeven een [expressie](api-management-policy-expressions.md) of een letterlijke tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="641ab-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="641ab-615">Als het Hallo-expressie bevat een letterlijke reeks wordt geconverteerd tooa tekenreeks en Hallo type Hallo-waarde niet `System.String`.</span><span class="sxs-lookup"><span data-stu-id="641ab-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="641ab-616"><a name="set-variablePolicyStatement"></a>Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="641ab-617"><a name="set-variableExample"></a>Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="641ab-618">Hallo volgende voorbeeld ziet u een variabele beleid instellen in Hallo inkomende sectie.</span><span class="sxs-lookup"><span data-stu-id="641ab-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="641ab-619">Deze variabele beleid instellen maakt een `isMobile` Booleaanse [context](api-management-policy-expressions.md#ContextVariables) variabele die tootrue is ingesteld als hello `User-Agent` aanvraag-header bevat de tekst hello `iPad` of `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="641ab-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="641ab-620">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-620">Elements</span></span>  
  
|<span data-ttu-id="641ab-621">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-621">Element</span></span>|<span data-ttu-id="641ab-622">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-622">Description</span></span>|<span data-ttu-id="641ab-623">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-624">variabele instellen</span><span class="sxs-lookup"><span data-stu-id="641ab-624">set-variable</span></span>|<span data-ttu-id="641ab-625">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-625">Root element.</span></span>|<span data-ttu-id="641ab-626">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-627">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-627">Attributes</span></span>  
  
|<span data-ttu-id="641ab-628">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-628">Attribute</span></span>|<span data-ttu-id="641ab-629">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-629">Description</span></span>|<span data-ttu-id="641ab-630">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="641ab-631">naam</span><span class="sxs-lookup"><span data-stu-id="641ab-631">name</span></span>|<span data-ttu-id="641ab-632">Hallo-naam van Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="641ab-632">hello name of hello variable.</span></span>|<span data-ttu-id="641ab-633">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-633">Yes</span></span>|  
|<span data-ttu-id="641ab-634">waarde</span><span class="sxs-lookup"><span data-stu-id="641ab-634">value</span></span>|<span data-ttu-id="641ab-635">Hallo-waarde van Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="641ab-635">hello value of hello variable.</span></span> <span data-ttu-id="641ab-636">Dit kan een expressie of een letterlijke waarde zijn.</span><span class="sxs-lookup"><span data-stu-id="641ab-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="641ab-637">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-638">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-638">Usage</span></span>  
 <span data-ttu-id="641ab-639">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-640">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-641">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="641ab-642"><a name="set-variableAllowedTypes"></a>Toegestane typen</span><span class="sxs-lookup"><span data-stu-id="641ab-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="641ab-643">Expressies in Hallo `set-variable` beleid moet een van volgende basistypen Hallo retourneren.</span><span class="sxs-lookup"><span data-stu-id="641ab-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="641ab-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="641ab-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="641ab-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="641ab-645">System.SByte</span></span>  
  
-   <span data-ttu-id="641ab-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="641ab-646">System.Byte</span></span>  
  
-   <span data-ttu-id="641ab-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="641ab-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="641ab-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="641ab-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="641ab-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="641ab-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="641ab-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="641ab-650">System.Int16</span></span>  
  
-   <span data-ttu-id="641ab-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="641ab-651">System.Int32</span></span>  
  
-   <span data-ttu-id="641ab-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="641ab-652">System.Int64</span></span>  
  
-   <span data-ttu-id="641ab-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="641ab-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="641ab-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="641ab-654">System.Single</span></span>  
  
-   <span data-ttu-id="641ab-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="641ab-655">System.Double</span></span>  
  
-   <span data-ttu-id="641ab-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="641ab-656">System.Guid</span></span>  
  
-   <span data-ttu-id="641ab-657">System.String</span><span class="sxs-lookup"><span data-stu-id="641ab-657">System.String</span></span>  
  
-   <span data-ttu-id="641ab-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="641ab-658">System.Char</span></span>  
  
-   <span data-ttu-id="641ab-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="641ab-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="641ab-660">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="641ab-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="641ab-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="641ab-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="641ab-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="641ab-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="641ab-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="641ab-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="641ab-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="641ab-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="641ab-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="641ab-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="641ab-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="641ab-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="641ab-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="641ab-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="641ab-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="641ab-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="641ab-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="641ab-669">System.Single?</span></span>  
  
-   <span data-ttu-id="641ab-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="641ab-670">System.Double?</span></span>  
  
-   <span data-ttu-id="641ab-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="641ab-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="641ab-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="641ab-672">System.String?</span></span>  
  
-   <span data-ttu-id="641ab-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="641ab-673">System.Char?</span></span>  
  
-   <span data-ttu-id="641ab-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="641ab-674">System.DateTime?</span></span>  

##  <span data-ttu-id="641ab-675"><a name="Trace"></a>Tracering</span><span class="sxs-lookup"><span data-stu-id="641ab-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="641ab-676">Hallo `trace` beleid wordt een tekenreeks toegevoegd in Hallo [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="641ab-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="641ab-677">Hallo beleid worden uitgevoerd alleen wanneer tracering wordt geactiveerd, dat wil zeggen `Ocp-Apim-Trace` aanvraagheader aanwezig is en stel te`true` en `Ocp-Apim-Subscription-Key` aanvraagheader aanwezig is en bevat een geldige sleutel die is gekoppeld aan het Hallo-beheeraccount.</span><span class="sxs-lookup"><span data-stu-id="641ab-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-678">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="641ab-679">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-679">Elements</span></span>  
  
|<span data-ttu-id="641ab-680">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-680">Element</span></span>|<span data-ttu-id="641ab-681">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-681">Description</span></span>|<span data-ttu-id="641ab-682">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-683">tracering</span><span class="sxs-lookup"><span data-stu-id="641ab-683">trace</span></span>|<span data-ttu-id="641ab-684">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-684">Root element.</span></span>|<span data-ttu-id="641ab-685">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-686">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-686">Attributes</span></span>  
  
|<span data-ttu-id="641ab-687">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-687">Attribute</span></span>|<span data-ttu-id="641ab-688">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-688">Description</span></span>|<span data-ttu-id="641ab-689">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-689">Required</span></span>|<span data-ttu-id="641ab-690">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="641ab-691">Bron</span><span class="sxs-lookup"><span data-stu-id="641ab-691">source</span></span>|<span data-ttu-id="641ab-692">Tekenreeks van letterlijke zinvolle toohello traceringsviewer en geven Hallo bron van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="641ab-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="641ab-693">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-693">Yes</span></span>|<span data-ttu-id="641ab-694">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="641ab-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-695">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-695">Usage</span></span>  
 <span data-ttu-id="641ab-696">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="641ab-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="641ab-697">**Beleid secties:** inkomend, uitgaand back-end op fout</span><span class="sxs-lookup"><span data-stu-id="641ab-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="641ab-698">**Beleid scopes:** alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="641ab-699"><a name="Wait"></a>Wacht</span><span class="sxs-lookup"><span data-stu-id="641ab-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="641ab-700">Hallo `wait` beleid bijbehorende directe onderliggende beleidsregels parallel worden uitgevoerd en wordt gewacht op alle of een van de bijbehorende directe onderliggende beleidsregels toocomplete voordat deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="641ab-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="641ab-701">Hallo kunt wacht beleid hebben als het beleid direct onderliggende [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), en [transportbesturing](api-management-advanced-policies.md#choose) beleid.</span><span class="sxs-lookup"><span data-stu-id="641ab-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="641ab-702">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="641ab-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="641ab-703">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="641ab-703">Example</span></span>  
 <span data-ttu-id="641ab-704">In het volgende voorbeeld Hallo er zijn twee `choose` beleid als beleid direct onderliggende Hallo `wait` beleid.</span><span class="sxs-lookup"><span data-stu-id="641ab-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="641ab-705">Elk van deze `choose` beleid parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="641ab-706">Elke `choose` beleid tooretrieve probeert een waarde in de cache.</span><span class="sxs-lookup"><span data-stu-id="641ab-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="641ab-707">Als er een cache ontbreekt, wordt een back-endservice tooprovide Hallo waarde genoemd.</span><span class="sxs-lookup"><span data-stu-id="641ab-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="641ab-708">In dit voorbeeld Hallo `wait` beleid niet wordt voltooid totdat alle van de bijbehorende directe onderliggende beleidsregels hebt voltooid, omdat Hallo `for` kenmerk is ingesteld, te`all`.</span><span class="sxs-lookup"><span data-stu-id="641ab-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="641ab-709">In dit voorbeeld Hallo context variabelen (`execute-branch-one`, `value-one`, `execute-branch-two`, en `value-two`) buiten het bereik van dit voorbeeldbeleid Hallo zijn gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="641ab-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="641ab-710">Elementen</span><span class="sxs-lookup"><span data-stu-id="641ab-710">Elements</span></span>  
  
|<span data-ttu-id="641ab-711">Element</span><span class="sxs-lookup"><span data-stu-id="641ab-711">Element</span></span>|<span data-ttu-id="641ab-712">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-712">Description</span></span>|<span data-ttu-id="641ab-713">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="641ab-714">Wacht</span><span class="sxs-lookup"><span data-stu-id="641ab-714">wait</span></span>|<span data-ttu-id="641ab-715">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="641ab-715">Root element.</span></span> <span data-ttu-id="641ab-716">Alleen onderliggende elementen bevat mogelijk `send-request`, `cache-lookup-value`, en `choose` beleid.</span><span class="sxs-lookup"><span data-stu-id="641ab-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="641ab-717">Ja</span><span class="sxs-lookup"><span data-stu-id="641ab-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="641ab-718">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="641ab-718">Attributes</span></span>  
  
|<span data-ttu-id="641ab-719">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="641ab-719">Attribute</span></span>|<span data-ttu-id="641ab-720">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="641ab-720">Description</span></span>|<span data-ttu-id="641ab-721">Vereist</span><span class="sxs-lookup"><span data-stu-id="641ab-721">Required</span></span>|<span data-ttu-id="641ab-722">Standaard</span><span class="sxs-lookup"><span data-stu-id="641ab-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="641ab-723">voor</span><span class="sxs-lookup"><span data-stu-id="641ab-723">for</span></span>|<span data-ttu-id="641ab-724">Hiermee wordt bepaald of hello `wait` beleid wacht tot alle directe onderliggende beleidsregels toobe voltooid of slechts één.</span><span class="sxs-lookup"><span data-stu-id="641ab-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="641ab-725">Toegestane waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="641ab-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="641ab-726">-   `all`-alle directe onderliggende beleidsregels toocomplete wacht</span><span class="sxs-lookup"><span data-stu-id="641ab-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="641ab-727">-een - directe onderliggende beleid toocomplete wacht.</span><span class="sxs-lookup"><span data-stu-id="641ab-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="641ab-728">Zodra het eerste directe onderliggende beleid Hallo is voltooid, Hallo `wait` beleid is voltooid en de uitvoering van een ander beleid direct onderliggende is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="641ab-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="641ab-729">Nee</span><span class="sxs-lookup"><span data-stu-id="641ab-729">No</span></span>|<span data-ttu-id="641ab-730">Alle</span><span class="sxs-lookup"><span data-stu-id="641ab-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="641ab-731">Gebruik</span><span class="sxs-lookup"><span data-stu-id="641ab-731">Usage</span></span>  
 <span data-ttu-id="641ab-732">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="641ab-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="641ab-733">**Beleid secties:** inkomend, uitgaand back-end</span><span class="sxs-lookup"><span data-stu-id="641ab-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="641ab-734">**Beleid scopes:**alle scopes</span><span class="sxs-lookup"><span data-stu-id="641ab-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="641ab-735">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="641ab-735">Next steps</span></span>
<span data-ttu-id="641ab-736">Zie voor meer informatie, werken met beleid:</span><span class="sxs-lookup"><span data-stu-id="641ab-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="641ab-737">Beleidsregels in API Management</span><span class="sxs-lookup"><span data-stu-id="641ab-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="641ab-738">Beleidsexpressies</span><span class="sxs-lookup"><span data-stu-id="641ab-738">Policy expressions</span></span>](api-management-policy-expressions.md)
