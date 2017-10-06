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
# <a name="api-management-advanced-policies"></a>API Management Geavanceerde beleidsregels
Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen. Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AdvancedPolicies"></a>Geavanceerde beleidsregels  
  
-   [Transportbesturing](api-management-advanced-policies.md#choose) - voorwaardelijk is van toepassing op basis van resultaten van de evaluatie van Booleaanse waarde Hallo Hallo beleidsverklaringen [expressies](api-management-policy-expressions.md).  
  
-   [Doorsturen van aanvraag](#ForwardRequest) -stuurt Hallo aanvraag toohello back-endservice.

-   [Gelijktijdigheid beperken](#LimitConcurrency) -voorkomt u dat beleid wordt uitgevoerd door meer dan een opgegeven aantal aanvragen op een tijdstip Hallo ingesloten.
  
-   [Meld u tooEvent Hub](#log-to-eventhub) -verzendt berichten in Hallo indeling tooan Event Hub wordt gedefinieerd door een entiteit van het logboek opgegeven. 

-   [Antwoord model](#mock-response) -pipeline-uitvoering wordt afgebroken en een mocked antwoord geretourneerd rechtstreeks toohello aanroeper.
  
-   [Probeer](#Retry) -uitvoering van de nieuwe pogingen van Hallo ingesloten beleidsverklaringen, als en totdat Hallo-voorwaarde is voldaan. Uitvoering wordt herhaald op Hallo opgegeven tijdsintervallen en up toohello opgegeven aantal nieuwe pogingen.  
  
-   [Antwoord retourneren](#ReturnResponse) -wordt afgebroken pijplijn uitvoering en retourneert Hallo opgegeven antwoord rechtstreeks toohello aanroeper. 
  
-   [Eenzijdige aanvraag verzenden](#SendOneWayRequest) -verzendt een aanvraag toohello URL opgegeven zonder te wachten op reactie.  
  
-   [Aanvraag verzenden](#SendRequest) -verzendt een aanvraag toohello URL opgegeven.  

-   [HTTP-proxy ingesteld](#SetHttpProxy) -kunt u aanvragen tooroute doorgestuurd via een HTTP-proxy.  

-   [Stel aanvraagmethode](#SetRequestMethod) -kunt u toochange Hallo HTTP-methode voor een aanvraag.  
  
-   [Statuscode ingesteld](#SetStatus) -wijzigingen Hallo HTTP status code toohello opgegeven waarde.  
  
-   [Variabele instellen](api-management-advanced-policies.md#set-variable) -zich blijft voordoen een waarde in een benoemde [context](api-management-policy-expressions.md#ContextVariables) variabele voor latere toegang.  

-   [Tracering](#Trace) -wordt een tekenreeks toegevoegd in Hallo [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer.  
  
-   [Wacht](#Wait) -wacht voor ingesloten [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), of [transportbesturing](api-management-advanced-policies.md#choose) beleid toocomplete voordat u doorgaat.  
  
##  <a name="choose"></a>Controlestroom  
 Hallo `choose` beleid van toepassing is ingesloten beleid op basis van resultaat van evaluatie van Booleaanse expressies, vergelijkbare tooan if vervolgens else of een switch Hallo instructies in een programmeertaal maken.  
  
###  <a name="ChoosePolicyStatement"></a>Beleidsverklaring  
  
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
  
 Hallo beleid voor toegangsbeheer stroom moet ten minste één bevatten `<when/>` element. Hallo `<otherwise/>` element is optioneel. Voorwaarden `<when/>` elementen worden in volgorde van hun binnen Hallo beleid geëvalueerd. Beleid voor instructie (s) die tussen Hallo eerst `<when/>` element met kenmerk gelijk is aan voorwaarde `true` worden toegepast. Beleid omsloten Hallo `<otherwise/>` element, indien aanwezig, wordt toegepast als alle Hallo `<when/>` voorwaarde elementkenmerken zijn `false`.  
  
### <a name="examples"></a>Voorbeelden  
  
####  <a name="ChooseExample"></a>Voorbeeld  
 Hallo volgende voorbeeld toont een [variabele instellen](api-management-advanced-policies.md#set-variable) beleid en twee beleidsregels voor beheer-stroom.  
  
 Hallo-variabele beleid instellen is in binnenkomende sectie Hallo en maakt een `isMobile` Booleaanse [context](api-management-policy-expressions.md#ContextVariables) variabele die tootrue is ingesteld als hello `User-Agent` aanvraag-header bevat de tekst hello `iPad` of `iPhone`.  
  
 eerste beleid voor toegangsbeheer stroom Hallo zich ook in sectie inkomende hello en voorwaardelijk wordt een van twee [querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) beleidsregels, afhankelijk van de waarde Hallo Hallo `isMobile` context-variabele.  
  
 Hallo tweede besturingselement stroom beleid is in de uitgaande sectie Hallo en voorwaardelijk geldt Hallo [XML converteren tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) beleid wanneer `isMobile` te is ingesteld`true`.  
  
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
  
#### <a name="example"></a>Voorbeeld  
 Dit voorbeeld ziet u hoe tooperform filteren op inhoud door het verwijderen van elementen uit Hallo antwoord ontvangen van de back-endservice Hallo bij gebruik van Hallo `Starter` product. Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too34:30 vooruit. Start op 31:50 toosee een overzicht van [Hallo donker Sky Forecast API](https://developer.forecast.io/) gebruikt voor deze demonstratie.  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|Kies|Hoofdelement.|Ja|  
|Wanneer|voorwaarde toouse voor Hallo Hallo `if` of `ifelse` delen van Hallo `choose` beleid. Als hello `choose` beleid heeft meerdere `when` secties, ze worden opeenvolgend geëvalueerd. Eenmaal Hallo `condition` van een wanneer element te evalueert`true`, niet verder `when` voorwaarden worden geëvalueerd.|Ja|  
|anders|Hallo beleid codefragment toobe gebruikt als geen van Hallo bevat `when` voorwaarden te evalueren`true`.|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|  
|---------------|-----------------|--------------|  
|conditie = "Boole-expressie &#124; Constante Booleaanse'|Hallo Booleaanse expressie of constante tooevaluated wanneer Hallo die `when` beleidsverklaring wordt geëvalueerd.|Ja|  
  
###  <a name="ChooseUsage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  
  
##  <a name="ForwardRequest"></a>Doorsturen van aanvraag  
 Hallo `forward-request` beleid stuurt Hallo binnenkomende aanvraag toohello back-endservice opgegeven in de aanvraag Hallo [context](api-management-policy-expressions.md#ContextVariables). Hallo back-end service URL is opgegeven in Hallo API [instellingen](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) en kan worden gewijzigd met behulp van Hallo [back-endservice ingesteld](api-management-transformation-policies.md) beleid.  
  
> [!NOTE]
>  Verwijderen van dit beleid resulteert in het Hallo-aanvraag niet doorgestuurd toohello back-end-service en het Hallo-beleid in uitgaande sectie Hallo onmiddellijk worden geëvalueerd na geslaagde voltooiing Hallo Hallo beleidsregels in Hallo inkomende sectie.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>Voorbeelden  
  
#### <a name="example"></a>Voorbeeld  
 Hallo stuurt volgende API-niveau beleid alle aanvragen toohello back-endservice met een time-outinterval van 60 seconden.  
  
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
  
#### <a name="example"></a>Voorbeeld  
 Het beleid voor deze bewerking gebruikt Hallo `base` element tooinherit Hallo back-end-beleid van Hallo bovenliggende API-niveau bereik.  
  
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
  
#### <a name="example"></a>Voorbeeld  
 Deze bewerking beleid stuurt alle aanvragen toohello back-endservice met een time-out van 120 expliciet en neemt geen Hallo bovenliggende niveau back-end-API-beleid.  
  
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
  
#### <a name="example"></a>Voorbeeld  
 Het beleid voor deze bewerking niet doorsturen van aanvragen toohello back-endservice.  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|voorwaarts-aanvraag|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|time-out = 'integer'|Hallo-time-outinterval in seconden alvorens het Hallo-aanroep toohello back-endservice is mislukt.|Nee|Geen time-out|  
|Volg omleidingen = "true &#124; False"|Geeft aan of omleidingen van back-endservice Hallo worden gevolgd door Hallo gateway of toohello aanroeper wordt geretourneerd.|Nee|ONWAAR|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** back-end  
  
-   **Beleid scopes:** alle scopes  
  
##  <a name="LimitConcurrency"></a>Limiet gelijktijdigheid van taken  
 Hallo `limit-concurrency` beleid voorkomt dat ingesloten beleid uit door meer dan een opgegeven aantal aanvragen Hallo op een bepaald moment wordt uitgevoerd. Bij Hallo drempelwaarde overschrijdt, worden nieuwe aanvragen tooa wachtrij toegevoegd totdat Hallo maximum wachtrijlengte wordt bereikt. Bij uitputting van de wachtrij mislukken nieuwe aanvragen onmiddellijk.
  
###  <a name="LimitConcurrencyStatement"></a>Beleidsverklaring  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>Voorbeelden  
  
####  <a name="ChooseExample"></a>Voorbeeld  
 Hallo volgende voorbeeld laat zien hoe het aantal aanvragen toolimit tooa back-end op basis van het Hallo-waarde van een variabele context doorgestuurd.
 
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

### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|    
|limiet gelijktijdigheid|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|--------------|  
|sleutel|Een tekenreeks. Een expressie toegestaan. Hiermee geeft u Hallo gelijktijdigheid bereik. Kan worden gedeeld door meerdere beleidsregels.|Ja|N.v.t.|  
|maximum aantal|Een geheel getal. Hiermee geeft u het maximale aantal aanvragen dat tooenter Hallo beleid zijn toegestaan.|Ja|N.v.t.|  
|timeout|Een geheel getal. Een expressie toegestaan. Hiermee geeft u het aantal seconden dat een aanvraag wachten tooenter een scope voordat deze is mislukt met de moet Hallo ' 403 te veel aanvragen '|Nee|Infinity|  
|maximale wachtrijlengte|Een geheel getal. Een expressie toegestaan. Hiermee geeft u de maximale wachtrijlengte Hallo. Inkomende aanvragen tooenter probeert dit beleid wordt beëindigd met ' 403 te veel aanvragen ' onmiddellijk wanneer Hallo wachtrij is verbruikt.|Nee|Infinity|  
  
###  <a name="ChooseUsage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  

##  <a name="log-to-eventhub"></a>Meld u tooEvent Hub  
 Hallo `log-to-eventhub` beleid verzendt berichten in Hallo indeling tooan Event Hub gedefinieerd door een entiteit van het logboek opgegeven. Als de naam al aangeeft, worden Hallo beleid wordt gebruikt voor het opslaan van de geselecteerde aanvraag of antwoord contextinformatie voor online of offline-analyse.  
  
> [!NOTE]
>  Zie voor een stapsgewijze handleiding voor het configureren van een event hub en vastleggen van gebeurtenissen, [hoe toolog API Management-gebeurtenissen met Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>Voorbeeld  
 Elke tekenreeks kan worden gebruikt als Hallo waarde toobe vastgelegd in Event Hubs. In dit voorbeeld Hallo datum en tijd implementatie servicenaam, aanvraag-id, IP-adres en de naam van de bewerking voor alle binnenkomende oproepen zijn geregistreerde toohello event hub berichtenlogboek geregistreerd bij Hallo `contoso-logger` id.  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|logboek voor eventhub|Hoofdelement. Hallo-waarde van dit element is Hallo tekenreeks toolog tooyour event hub.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|  
|---------------|-----------------|--------------|  
|logboek-id|Hallo-id van Hallo berichtenlogboek geregistreerd met uw API Management-service.|Ja|  
|partitie-id|Hiermee geeft u een index Hallo van Hallo partitie waarin berichten worden verzonden.|Optioneel. Dit kenmerk kan niet worden gebruikt als `partition-key` wordt gebruikt.|  
|Partitiesleutel|Hiermee geeft u Hallo-waarde die voor de partitietoewijzing van de wordt gebruikt wanneer berichten worden verzonden.|Optioneel. Dit kenmerk kan niet worden gebruikt als `partition-id` wordt gebruikt.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  

##  <a name="mock-response"></a>Mock-antwoord  
Hallo `mock-response`, als de naam van de Hallo impliceert, is gebruikt toomock API's en bewerkingen. Het normale pipeline-uitvoering afgebroken en een mocked antwoord toohello aanroeper retourneert. Hallo beleid probeert altijd tooreturn reacties van hoogste betrouwbaarheid. Deze verkiest antwoord inhoud voorbeelden, indien beschikbaar. Het voorbeeld antwoorden van schema's, genereert wanneer schema's worden geleverd en voorbeelden niet. Als geen van beide voorbeelden of schema's zijn gevonden, worden de antwoorden met geen inhoud geretourneerd.
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>Voorbeelden  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|nagebootste-antwoord|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|--------------|  
|statuscode in|Hiermee geeft u de statuscode van antwoord en is de bijbehorende voorbeeld gebruikte tooselect of schema.|Nee|200|  
|type inhoud|Hiermee geeft u `Content-Type` headerwaarde antwoord en de bijbehorende voorbeeld gebruikte tooselect of schema.|Nee|Geen|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** binnenkomende, uitgaande, bij fouten  
  
-   **Beleid scopes:** alle scopes

##  <a name="Retry"></a>Probeer het opnieuw  
 Hallo `retry` beleid de onderliggende beleidsregels eenmaal wordt uitgevoerd en vervolgens probeert om opnieuw de uitvoering ervan tot Hallo opnieuw `condition` wordt `false` of probeer het opnieuw `count` leeg.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
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
  
### <a name="example"></a>Voorbeeld  
 In Hallo voorbeeld aanvraag forewarding na geprobeerd up tooten tijdstippen met behulp van de algoritme exponentiële probeer het opnieuw. Aangezien `first-fast-retry` is ingesteld toofalse, alle nieuwe pogingen worden onderwerp toohello exponsntial opnieuw algoritme.  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|retry|Hoofdelement. Kan geen ander beleid bevatten als de onderliggende elementen.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|Voorwaarde|Een boolean letterlijke waarde of [expressie](api-management-policy-expressions.md) opgeven als nieuwe pogingen moeten worden gestopt (`false`) of vervolg (`true`).|Ja|N.v.t.|  
|Aantal|Een positief getal Hallo kunt u het maximum aantal nieuwe pogingen tooattempt opgeven.|Ja|N.v.t.|  
|interval|Een positief getal in seconden hello Wacht-interval tussen nieuwe pogingen van Hallo opgeven.|Ja|N.v.t.|  
|Max-interval|Een positief getal in seconden hello maximale wachttijd-interval tussen nieuwe pogingen van Hallo opgeven. Is het gebruikte tooimplement een algoritme exponentiële probeer het opnieuw.|Nee|N.v.t.|  
|delta|Een positief getal in seconden Hallo Wacht interval verhoging opgeven. Het is gebruikte tooimplement Hallo lineaire en exponentieel opnieuw algoritmen.|Nee|N.v.t.|  
|eerste-fast-probeer het opnieuw|Als instellen te `true` , Hallo eerste nieuwe poging wordt onmiddellijk uitgevoerd.|Nee|`false`|  
  
> [!NOTE]
>  Wanneer alleen Hallo `interval` is opgegeven, **vaste** interval voor nieuwe pogingen worden uitgevoerd.  
>  Wanneer alleen Hallo `interval` en `delta` zijn opgegeven, een **lineaire** interval opnieuw proberen algoritme wordt gebruikt, waarbij de tijd tussen nieuwe pogingen berekende volgens Hallo formule - de volgende `interval + (count - 1)*delta`.  
>  Wanneer Hallo `interval`, `max-interval` en `delta` zijn opgegeven, **exponentiële** interval opnieuw proberen algoritme wordt toegepast, waarbij Hallo wachttijd tussen nieuwe pogingen Hallo groeit exponentieel van Hallo-waarde van `interval`toohello waarde `max-interval` op basis van de volgende toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) . Houd er rekening mee dat informatie over het gebruik van onderliggende beleidsbeperkingen wordt overgenomen door dit beleid.  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  
  
##  <a name="ReturnResponse"></a>Antwoord retourneren  
 Hallo `return-response` beleid annuleert pipeline-uitvoering en retourneert een standaardwaarde of een aangepast antwoord toohello aanroeper. Standaardantwoord is `200 OK` met geen hoofdcode. Aangepast antwoord kan worden opgegeven via de instructies voor een context variabele of beleid. Wanneer beide zijn opgegeven, wordt door Hallo beleidsverklaringen antwoord Hallo opgenomen in de context-variabele Hallo gewijzigd voordat het toohello aanroeper wordt geretourneerd.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|Return-antwoord|Hoofdelement.|Ja|  
|set-header|Een [set-header](api-management-transformation-policies.md#SetHTTPheader) beleidsverklaring.|Nee|  
|set-instantie|Een [set hoofdtekst](api-management-transformation-policies.md#SetBody) beleidsverklaring.|Nee|  
|status instellen|Een [status instellen](api-management-advanced-policies.md#SetStatus) beleidsverklaring.|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|  
|---------------|-----------------|--------------|  
|naam van een antwoord variabele|Hallo Hallo context variabele voor waarnaar wordt verwezen vanuit, bijvoorbeeld een upstream [aanvragen verzenden](api-management-advanced-policies.md#SendRequest) beleid en met een `Response` object|Optioneel.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  
  
##  <a name="SendOneWayRequest"></a>Eenzijdige aanvraag verzenden  
 Hallo `send-one-way-request` beleid verzendt Hallo opgegeven aanvraag toohello URL opgegeven zonder te wachten op reactie.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>Voorbeeld  
 Dit beleid voorbeeld toont een voorbeeld van het gebruik van Hallo `send-one-way-request` beleid toosend bericht tooa toegestane chatruimten als Hallo HTTP-antwoordcode groter dan of gelijk too500 is. Zie voor meer informatie over dit voorbeeld [met behulp van externe services van hello Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|een-manier-verzoek om te verzenden|Hoofdelement.|Ja|  
|URL|Hallo-URL van Hallo-aanvraag.|Er is geen als modus = kopiëren; anders Ja.|  
|Methode|Hallo HTTP-methode voor Hallo-aanvraag.|Er is geen als modus = kopiëren; anders Ja.|  
|koptekst|Aanvraag-header. Meerdere headeronderdelen voor meerdere aanvraagheaders gebruiken.|Nee|  
|Hoofdtekst|Hallo aanvraagtekst.|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|modus = 'tekenreeks'|Hiermee wordt bepaald of dit een nieuwe aanvraag of een kopie van de huidige aanvraag Hallo is. In de uitgaande modus, modus = kopie Hallo aanvraagtekst niet geïnitialiseerd.|Nee|Nieuw|  
|naam|Geeft de naam Hallo van Hallo header toobe set.|Ja|N.v.t.|  
|Er bestaat actie|Geeft aan welke actie tootake Hallo-header is al opgegeven. Dit kenmerk moet een van de volgende waarden Hallo hebben.<br /><br /> -onderdrukkingswaarde - vervangt Hallo van bestaande Hallo-header.<br />-skip - vervangen Hallo bestaande header-waarde niet.<br />-toevoeg - Hallo waarde toohello bestaande header-waarde wordt toegevoegd.<br />Hallo-header verwijdert - delete - van Hallo-aanvraag.<br /><br /> Als de waarde te`override` opnemen van meerdere vermeldingen met Hallo dezelfde resulteert in het Hallo-header wordt ingesteld volgens tooall-vermeldingen (die wordt vermeld meerdere keren) naam; alleen de vermelde waarden worden ingesteld in Hallo resultaat.|Nee|overschrijven|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  
  
##  <a name="SendRequest"></a>Aanvraag verzenden  
 Hallo `send-request` beleid verzendt Hallo opgegeven aanvraag toohello opgegeven URL, niet langer wachten dan Hallo time-outwaarde instellen.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>Voorbeeld  
 Dit voorbeeld ziet u een referentie-token met een server autorisatie eenrichtingssessie tooverify. Zie voor meer informatie over dit voorbeeld [met behulp van externe services van hello Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|aanvragen verzenden|Hoofdelement.|Ja|  
|URL|Hallo-URL van Hallo-aanvraag.|Er is geen als modus = kopiëren; anders Ja.|  
|Methode|Hallo HTTP-methode voor Hallo-aanvraag.|Er is geen als modus = kopiëren; anders Ja.|  
|koptekst|Aanvraag-header. Meerdere headeronderdelen voor meerdere aanvraagheaders gebruiken.|Nee|  
|Hoofdtekst|Hallo aanvraagtekst.|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|modus = 'tekenreeks'|Hiermee wordt bepaald of dit een nieuwe aanvraag of een kopie van de huidige aanvraag Hallo is. In de uitgaande modus, modus = kopie Hallo aanvraagtekst niet geïnitialiseerd.|Nee|Nieuw|  
|antwoord-variabele-name = 'tekenreeks'|Als deze niet aanwezig is, `context.Response` wordt gebruikt.|Nee|N.v.t.|  
|time-out = 'integer'|Hallo-time-outinterval in seconden voordat de aanroep van Hallo toohello URL is mislukt.|Nee|60|  
|fout negeren|Als true en Hallo resulteert in een fout opgetreden aanvragen:<br /><br /> -Als de naam van een antwoord variabele bevat een null-waarde is opgegeven.<br />-Als de naam van een antwoord variabele is niet opgegeven, context. Aanvraag wordt niet bijgewerkt.|Nee|ONWAAR|  
|naam|Geeft de naam Hallo van Hallo header toobe set.|Ja|N.v.t.|  
|Er bestaat actie|Geeft aan welke actie tootake Hallo-header is al opgegeven. Dit kenmerk moet een van de volgende waarden Hallo hebben.<br /><br /> -onderdrukkingswaarde - vervangt Hallo van bestaande Hallo-header.<br />-skip - vervangen Hallo bestaande header-waarde niet.<br />-toevoeg - Hallo waarde toohello bestaande header-waarde wordt toegevoegd.<br />Hallo-header verwijdert - delete - van Hallo-aanvraag.<br /><br /> Als de waarde te`override` opnemen van meerdere vermeldingen met Hallo dezelfde resulteert in het Hallo-header wordt ingesteld volgens tooall-vermeldingen (die wordt vermeld meerdere keren) naam; alleen de vermelde waarden worden ingesteld in Hallo resultaat.|Nee|overschrijven|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  
  
##  <a name="SetHttpProxy"></a>Set HTTP-proxy  
 Hallo `proxy` beleid kunt u tooroute aanvragen doorgestuurd toobackends via een HTTP-proxy. Alleen HTTP (niet HTTPS) wordt ondersteund tussen Hallo-gateway en het Hallo-proxy. Basic- en NTLM-verificatie.
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>Voorbeeld  
Houd er rekening mee Hallo gebruik van [eigenschappen](api-management-howto-properties.md) als de waarden van het Hallo-gebruikersnaam en wachtwoord tooavoid gevoelige informatie op te slaan in Hallo beleidsdocument.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|Proxy|Hoofdelement|Ja|  

### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|URL = 'tekenreeks'|Proxy-URL in de vorm Hallo van http://host:port.|Ja|N.v.t.|  
|gebruikersnaam = 'tekenreeks'|Gebruikersnaam toobe gebruikt voor verificatie met Hallo proxy.|Nee|N.v.t.|  
|wachtwoord = 'tekenreeks'|Wachtwoord toobe gebruikt voor verificatie met Hallo proxy.|Nee|N.v.t.|  

### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** alle scopes  

##  <a name="SetRequestMethod"></a>Set-aanvraagmethode  
 Hallo `set-method` beleid kunt u toochange Hallo HTTP-aanvraagmethode voor een aanvraag.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>Voorbeeld  
 Dit voorbeeld-beleid die gebruikmaakt van Hallo `set-method` beleid toont een voorbeeld van het verzenden van bericht tooa toegestane chatruimten als Hallo HTTP-antwoordcode groter dan is of gelijk too500. Zie voor meer informatie over dit voorbeeld [met behulp van externe services van hello Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|set-methode|Hoofdelement. Hallo-waarde van Hallo element geeft Hallo HTTP-methode.|Ja|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, bij fouten  
  
-   **Beleid scopes:** alle scopes  
  
##  <a name="SetStatus"></a>Set-statuscode  
 Hallo `set-status` beleid sets Hallo HTTP status code toohello opgegeven waarde.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>Voorbeeld  
 Dit voorbeeld ziet u hoe tooreturn een 401-respons als Hallo verificatietoken is ongeldig. Zie voor meer informatie [met behulp van externe services van hello Azure API Management-service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|status instellen|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|code = 'integer'|Hallo HTTP status code tooreturn.|Ja|N.v.t.|  
|reden = 'tekenreeks'|Een beschrijving van Hallo reden voor het retourneren van Hallo-statuscode.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** uitgaand, back-end op fout  
  
-   **Beleid scopes:** alle scopes  

##  <a name="set-variable"></a>Variabele instellen  
 Hallo `set-variable` beleid declareert een [context](api-management-policy-expressions.md#ContextVariables) variabele en hieraan een waarde die is opgegeven een [expressie](api-management-policy-expressions.md) of een letterlijke tekenreeks. Als het Hallo-expressie bevat een letterlijke reeks wordt geconverteerd tooa tekenreeks en Hallo type Hallo-waarde niet `System.String`.  
  
###  <a name="set-variablePolicyStatement"></a>Beleidsverklaring  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a>Voorbeeld  
 Hallo volgende voorbeeld ziet u een variabele beleid instellen in Hallo inkomende sectie. Deze variabele beleid instellen maakt een `isMobile` Booleaanse [context](api-management-policy-expressions.md#ContextVariables) variabele die tootrue is ingesteld als hello `User-Agent` aanvraag-header bevat de tekst hello `iPad` of `iPhone`.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|variabele instellen|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|  
|---------------|-----------------|--------------|  
|naam|Hallo-naam van Hallo-variabele.|Ja|  
|waarde|Hallo-waarde van Hallo-variabele. Dit kan een expressie of een letterlijke waarde zijn.|Ja|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  
  
###  <a name="set-variableAllowedTypes"></a>Toegestane typen  
 Expressies in Hallo `set-variable` beleid moet een van volgende basistypen Hallo retourneren.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.DateTime  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a>Tracering  
 Hallo `trace` beleid wordt een tekenreeks toegevoegd in Hallo [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) uitvoer. Hallo beleid worden uitgevoerd alleen wanneer tracering wordt geactiveerd, dat wil zeggen `Ocp-Apim-Trace` aanvraagheader aanwezig is en stel te`true` en `Ocp-Apim-Subscription-Key` aanvraagheader aanwezig is en bevat een geldige sleutel die is gekoppeld aan het Hallo-beheeraccount.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|tracering|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|Bron|Tekenreeks van letterlijke zinvolle toohello traceringsviewer en geven Hallo bron van het Hallo-bericht.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** alle scopes  
  
##  <a name="Wait"></a>Wacht  
 Hallo `wait` beleid bijbehorende directe onderliggende beleidsregels parallel worden uitgevoerd en wordt gewacht op alle of een van de bijbehorende directe onderliggende beleidsregels toocomplete voordat deze is voltooid. Hallo kunt wacht beleid hebben als het beleid direct onderliggende [Verzendaanvraag](api-management-advanced-policies.md#SendRequest), [waarde niet ophalen uit de cache](api-management-caching-policies.md#GetFromCacheByKey), en [transportbesturing](api-management-advanced-policies.md#choose) beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>Voorbeeld  
 In het volgende voorbeeld Hallo er zijn twee `choose` beleid als beleid direct onderliggende Hallo `wait` beleid. Elk van deze `choose` beleid parallel worden uitgevoerd. Elke `choose` beleid tooretrieve probeert een waarde in de cache. Als er een cache ontbreekt, wordt een back-endservice tooprovide Hallo waarde genoemd. In dit voorbeeld Hallo `wait` beleid niet wordt voltooid totdat alle van de bijbehorende directe onderliggende beleidsregels hebt voltooid, omdat Hallo `for` kenmerk is ingesteld, te`all`.   In dit voorbeeld Hallo context variabelen (`execute-branch-one`, `value-one`, `execute-branch-two`, en `value-two`) buiten het bereik van dit voorbeeldbeleid Hallo zijn gedeclareerd.  
  
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
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|Wacht|Hoofdelement. Alleen onderliggende elementen bevat mogelijk `send-request`, `cache-lookup-value`, en `choose` beleid.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|voor|Hiermee wordt bepaald of hello `wait` beleid wacht tot alle directe onderliggende beleidsregels toobe voltooid of slechts één. Toegestane waarden zijn:<br /><br /> -   `all`-alle directe onderliggende beleidsregels toocomplete wacht<br />-een - directe onderliggende beleid toocomplete wacht. Zodra het eerste directe onderliggende beleid Hallo is voltooid, Hallo `wait` beleid is voltooid en de uitvoering van een ander beleid direct onderliggende is beëindigd.|Nee|Alle|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end  
  
-   **Beleid scopes:**alle scopes  
  
## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, werken met beleid:
-   [Beleidsregels in API Management](api-management-howto-policies.md) 
-   [Beleidsexpressies](api-management-policy-expressions.md)
