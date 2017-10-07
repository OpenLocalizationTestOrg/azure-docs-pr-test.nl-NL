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
# <a name="api-management-transformation-policies"></a>API Management-beleidsregels voor transformatie
Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen. Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a>Claimtransformatiebeleidsinstellingen  
  
-   [Converteren van JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) : zet aanvraag of antwoord body van JSON tooXML.  
  
-   [Converteren van XML-tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : zet aanvraag of antwoord body van XML-tooJSON.  
  
-   [Zoeken en vervangen tekenreeks in de hoofdtekst](api-management-transformation-policies.md#Findandreplacestringinbody) - zoeken naar een subtekenreeks aanvraag of antwoord en wordt vervangen door een andere subtekenreeks.  
  
-   [URL's in de inhoud te maskeren](api-management-transformation-policies.md#MaskURLSContent) -koppelingen herschrijft (maskers) antwoord Hallo body zodat ze equivalente koppeling toohello via Hallo gateway wijst.  
  
-   [Instellen van de back-endservice](api-management-transformation-policies.md#SetBackendService) -back-endservice Hallo voor de binnenkomende aanvraag wordt gewijzigd.  
  
-   [Instantie ingesteld](api-management-transformation-policies.md#SetBody) -hoofdtekst van het Hallo-bericht voor binnenkomende en uitgaande aanvragen ingesteld.  
  
-   [Set HTTP-header](api-management-transformation-policies.md#SetHTTPheader) : een waarde tooan bestaande antwoord en/of de aanvraagheader wijst of voegt een nieuwe antwoord en/of de aanvraag-header.  
  
-   [Querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) - wordt toegevoegd, vervangt de waarde van of verwijderd van de aanvraag queryreeksparameter opgeven.  
  
-   [Herschrijven van URL](api-management-transformation-policies.md#RewriteURL) -zet u een aanvraag-URL van de openbare formulier toohello vorm werd verwacht door Hallo-webservice.  
  
-   [XML met behulp van een XSLT transformeren](api-management-transformation-policies.md#XSLTransform) -een XSL-transformatie tooXML in de hoofdtekst van de aanvraag of antwoord van de Hallo van toepassing is.  
  
##  <a name="ConvertJSONtoXML"></a>JSON tooXML converteren  
 Hallo `json-to-xml` beleid zet de hoofdtekst van een aanvraag of antwoord van de JSON-tooXML.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Voorbeeld  
  
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
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|JSON-to-xml|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|toepassen|Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.<br /><br /> conversie - altijd - altijd van toepassing.<br />convert-inhoud type-json - alleen als response Content-Type-header aanwezigheid van JSON aangeeft.|Ja|N.v.t.|  
|Overweeg-accepteren-header|Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.<br /><br /> -waar - conversie van toepassing als JSON is aangevraagd in aanvraag Accept-header.<br />-ONWAAR - conversie altijd van toepassing.|Nee|De waarde True|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** binnenkomende, uitgaande, bij fouten  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="ConvertXMLtoJSON"></a>XML-tooJSON converteren  
 Hallo `xml-to-json` beleid zet de hoofdtekst van een aanvraag of antwoord van de XML-tooJSON. Dit beleid kan worden gebruikt toomodernize API's op basis van de back-end van een alleen-XML-webservices.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Voorbeeld  
  
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
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|XML-json-|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|type|Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.<br /><br /> Hallo - javascript-vriendelijk - geconverteerd JSON heeft een formulier beschrijvende tooJavaScript ontwikkelaars.<br />-direct - duidt hello geconverteerde JSON op Hallo van het oorspronkelijke XML-document-structuur.|Ja|N.v.t.|  
|toepassen|Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.<br /><br /> -altijd - altijd converteren.<br />convert - inhoud-type-xml - alleen als response Content-Type-header aanwezigheid van XML aangeeft.|Ja|N.v.t.|  
|Overweeg-accepteren-header|Hallo-kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.<br /><br /> -waar - conversie van toepassing als XML is aangevraagd in aanvraag Accept-header.<br />-ONWAAR - conversie altijd van toepassing.|Nee|De waarde True|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** binnenkomende, uitgaande, bij fouten  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="Findandreplacestringinbody"></a>Zoeken en vervangen tekenreeks in de hoofdtekst  
 Hallo `find-and-replace` beleid vindt u een aanvraag of antwoord subtekenreeks en vervangen door een andere subtekenreeks.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|zoeken en vervangen|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|Van|Hallo tekenreeks toosearch voor.|Ja|N.v.t.|  
|tot|Hallo vervangende tekenreeks. Geef de vervangende tekenreeks tooremove Hallo zoeken tekenreekslengte van nul.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="MaskURLSContent"></a>Masker URL's in de inhoud  
 Hallo `redirect-content-urls` beleid herschrijft (maskers) koppelingen in de antwoordtekst Hallo zodat ze equivalente koppeling toohello via Hallo gateway wijst. Gebruik in Hallo uitgaande sectie toore schrijven antwoord hoofdtekst koppelingen toomake ze punt toohello gateway. Gebruik in Hallo inkomende sectie voor een tegenovergestelde effect.  
  
> [!NOTE]
>  Dit beleid verandert niet een headerwaarden, zoals `Location` headers. de headerwaarden toochange hello gebruiken [set-header](api-management-transformation-policies.md#SetHTTPheader) beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|Omleidings-inhoud-URL 's|Hoofdelement.|Ja|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** binnenkomende, uitgaande  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="SetBackendService"></a>Back-end-service instellen  
 Gebruik Hallo `set-backend-service` beleid tooredirect een binnenkomende aanvraag tooa andere back-end dan Hallo één in Hallo API-instellingen voor de bewerking is opgegeven. Dit beleid wijzigingen Hallo back-end service basis-URL van het binnenkomende aanvraag toohello hello, een opgegeven in het Hallo-beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>Voorbeeld  
  
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
In dit voorbeeld Hallo routeert beleid instellen back-end-service aanvragen op basis van Hallo versiewaarde doorgegeven Hallo query tekenreeks tooa andere back-endservice dan Hallo Hallo voor een opgegeven in de API.
  
In eerste instantie Hallo service basis-URL is afgeleid van de instellingen voor de API Hallo-back-end. Dus Hallo aanvraag-URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` wordt `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` waar `http://contoso.com/api/10.4/` Hallo back-end-service URL is opgegeven in de Hallo API-instellingen.  
  
Wanneer Hallo [< kiezen\> ](api-management-advanced-policies.md#choose) beleidsverklaring wordt toegepast Hallo back-end service basis-URL kan wijzigen opnieuw te`http://contoso.com/api/8.2` of `http://contoso.com/api/9.1`, afhankelijk van het Hallo-waarde van Hallo versie aanvraag-queryparameter. Bijvoorbeeld, als hello waarde is `"2013-15"` Hallo van de laatste aanvraag URL wordt `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Als verdere transformatie van Hallo-aanvraag gewenste, andere is [claimtransformatiebeleidsinstellingen](api-management-transformation-policies.md#TransformationPolicies) kan worden gebruikt. Bijvoorbeeld tooremove Hallo versie query parameter nu dat hello aanvraag wordt gerouteerd tooa versie specifieke back-end hello [querytekenreeksparameter ingesteld](api-management-transformation-policies.md#SetQueryStringParameter) beleid gebruikte tooremove Hallo nu redundante version-kenmerk kan worden.  
  
### <a name="example"></a>Voorbeeld  
  
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
In dit voorbeeld Hallo beleid routes Hallo aanvraag tooa service fabric back-end Hallo Hallo userId queryreeks gebruikt als partitiesleutel Hallo en primaire replica van Hallo-partitie.  

### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|set-back-end-service|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|basis-url|Nieuwe back-end service basis-URL.|Nee|N.v.t.|  
|back-end-id|Id van Hallo back-end tooroute aan.|Nee|N.v.t.|  
|SF partitiesleutel|Alleen van toepassing wanneer het Hallo-back-end is een Service Fabric-service en wordt opgegeven met behulp van back-end-id. Een specifieke partitie van de service voor naamomzetting Hallo tooresolve gebruikt.|Nee|N.v.t.|  
|SF-replica-type|Alleen van toepassing wanneer het Hallo-back-end is een Service Fabric-service en wordt opgegeven met behulp van back-end-id. Bepaalt of het Hallo-aanvraag toohello primaire of secundaire replica van een partitie moet gaan. |Nee|N.v.t.|    
|SF-resolve-voorwaarde|Alleen van toepassing wanneer de back-end voor Hallo is een Service Fabric-service. Voorwaarde te identificeren heeft als Hallo tooService Fabric back-end aanroepen toobe herhaald met nieuwe resolutie.|Nee|N.v.t.|    
|SF-service-exemplaar-name|Alleen van toepassing wanneer de back-end voor Hallo is een Service Fabric-service. Kan toochange service-exemplaren tijdens runtime. |Nee|N.v.t.|    

### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** back-end voor binnenkomend verkeer  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="SetBody"></a>Set-instantie  
 Gebruik Hallo `set-body` beleid tooset Hallo berichttekst voor binnenkomende en uitgaande aanvragen. tooaccess Hallo berichttekst kunt u Hallo `context.Request.Body` eigenschap of Hallo `context.Response.Body`, afhankelijk van of Hallo-beleid in een Hallo is binnenkomend of uitgaand sectie.  
  
> [!IMPORTANT]
>  Denk eraan dat standaard als u toegang hebben tot Hallo bericht hoofdtekst met `context.Request.Body` of `context.Response.Body`, oorspronkelijke welkomstbericht hoofdtekst verloren en wordt door te retourneren Hallo hoofdtekst terug in Hallo-expressie moet worden ingesteld. inhoud, toopreserve Hallo-instantie ingesteld Hallo `preserveContent` parameter te`true` bij het openen van het Hallo-bericht. Als `preserveContent` te is ingesteld,`true` en een andere instantie wordt geretourneerd door het Hallo-expressie Hallo geretourneerd instantie wordt gebruikt.  
>   
>  Houd er rekening mee Hallo volgende overwegingen wanneer u Hallo `set-body` beleid.  
>   
>  -   Als u van Hallo gebruikmaakt `set-body` beleid tooreturn een nieuwe of bijgewerkte instantie hoeft u niet tooset `preserveContent` te`true` omdat u de nieuwe inhoud Hallo expliciet levert.  
> -   Hallo-inhoud van een reactie behouden bij Hallo inkomende pijplijn logisch niet omdat er nog geen reactie is.  
> -   Hallo-inhoud van een aanvraag behouden in de uitgaande pijplijn Hallo logisch niet omdat Hallo aanvraag al is verzonden toohello back-end op dit moment.  
> -   Als dit beleid wordt gebruikt wanneer er geen berichttekst, bijvoorbeeld in een inkomende GET een uitzondering opgetreden.  
  
 Zie voor meer informatie, Hallo `context.Request.Body`, `context.Response.Body`, en Hallo `IMessage` secties in Hallo [Context variabele](api-management-policy-expressions.md#ContextVariables) tabel.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Voorbeelden  
  
#### <a name="literal-text-example"></a>Voorbeeld van de letterlijke tekst  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>Voorbeeld van de toegang tot Hallo instantie als een tekenreeks. Houd er rekening mee dat we Hallo oorspronkelijke aanvraagtekst behouden zodat we deze later in Hallo pijplijn.
  
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
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Voorbeeld van de toegang tot een JObject Hallo instantie. Merk op dat omdat we niet reserveren van een Hallo oorspronkelijke aanvraagtekst, toegang tot het verderop in de pijplijn Hallo zal leiden tot een uitzondering.  
  
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
  
#### <a name="filter-response-based-on-product"></a>Reactie op basis van product filteren  
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

### <a name="using-liquid-templates-with-set-body"></a>Vloeibare sjablonen gebruiken bij set-instantie 
Hallo `set-body` beleid kan worden geconfigureerd toouse hello [vloeibare](https://shopify.github.io/liquid/basics/introduction/) templating taal tootransfom Hallo hoofdtekst van een aanvraag of antwoord. Dit kan zeer effectief zijn als u toocompletely wijzigen van de vorm Hallo indeling van uw bericht moet zijn.

> [!IMPORTANT]
> implementatie van vloeistof gebruikt in Hallo Hallo `set-body` beleid is geconfigureerd in de 'C#-modus'. Dit is vooral belangrijk bij het uitvoeren van bewerkingen zoals filteren. Als u bijvoorbeeld met een datumfilter vereist Hallo-gebruik van Pascal hoofd- en C#-datum notatie, bijvoorbeeld:
>
> {{body.foo.startDateTime| Datum: 'yyyyMMddTHH:mm:ddZ'}}

> [!IMPORTANT]
> Gebruik in volgorde toocorrectly bind tooan XML-hoofdtekst met vloeibare Hallo-sjabloon, een `set-header` beleid tooset Content-Type tooeither application/xml, text/xml (of een type eindigend op + xml); voor een JSON-hoofdtekst dit moet application/json, text/json (of een type beëindigen met + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>JSON-tooSOAP met een vloeibare sjabloon converteren
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

#### <a name="tranform-json-using-a-liquid-template"></a>Tranform JSON met een vloeibare sjabloon
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|set-instantie|Hoofdelement. Hallo platte tekst of een expressie die het retourneert een instantie bevat.|Ja|  

### <a name="properties"></a>Eigenschappen  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|sjabloon|In de set hoofdtekst beleid Hallo gebruikte toochange hello templating modus uitgevoerd. Op dit moment is alleen ondersteund Hallo-waarde:<br /><br />Hallo - vloeibare - set hoofdtekst beleid wordt Hallo vloeibare templating-engine gebruikt |Nee|vloeistof|  

Voor toegang tot informatie over het Hallo-aanvraag en -antwoord, kunt Hallo vloeibare sjabloon tooa context-object met de volgende eigenschappen Hallo binden: <br />
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



### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="SetHTTPheader"></a>Set HTTP-header  
 Hallo `set-header` beleid wijst een waarde tooan bestaande antwoord en/of de aanvraag-header of voegt een nieuwe antwoord en/of de aanvraag-header.  
  
 Voegt een lijst met HTTP-headers in een HTTP-bericht. Wanneer in een inkomende pijplijn geplaatst, wordt dit beleid ingesteld Hallo HTTP-headers voor aanvraag van Hallo toohello doelservice doorgegeven. Wanneer in een uitgaande pijplijn geplaatst, wordt dit beleid ingesteld Hallo HTTP-headers voor antwoord Hallo toohello gatewayclient worden verzonden.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Voorbeelden  
  
#### <a name="example"></a>Voorbeeld  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Context informatie toohello back-endservice doorsturen  
 Dit voorbeeld toont hoe beleid voor tooapply Hallo API toosupply context informatie toohello back-endservice niveau. Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too10:30 vooruit. Bij 12:10 is er een demo voor het aanroepen van een bewerking in de ontwikkelaarsportal Hallo waar u Hallo-beleid op het werk kunt zien.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|set-header|Hoofdelement.|Ja|  
|waarde|Hiermee wordt de waarde Hallo van Hallo header toobe set. Voor meerdere headers met de Hallo dezelfde naam toevoegen extra `value` elementen.|Ja|  
  
### <a name="properties"></a>Eigenschappen  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|Er bestaat actie|Geeft aan welke actie tootake Hallo-header is al opgegeven. Dit kenmerk moet een van de volgende waarden Hallo hebben.<br /><br /> -onderdrukkingswaarde - vervangt Hallo van bestaande Hallo-header.<br />-skip - vervangen Hallo bestaande header-waarde niet.<br />-toevoeg - Hallo waarde toohello bestaande header-waarde wordt toegevoegd.<br />Hallo-header verwijdert - delete - van Hallo-aanvraag.<br /><br /> Als de waarde te`override` opnemen van meerdere vermeldingen met Hallo dezelfde resulteert in het Hallo-header wordt ingesteld volgens tooall-vermeldingen (die wordt vermeld meerdere keren) naam; alleen de vermelde waarden worden ingesteld in Hallo resultaat.|Nee|overschrijven|  
|naam|Geeft de naam van Hallo header toobe set.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="SetQueryStringParameter"></a>Querytekenreeksparameter instellen  
 Hallo `set-query-parameter` beleid wordt toegevoegd, vervangt de waarde van, of verwijderingen querytekenreeksparameter aanvragen. Kan worden gebruikt toopass werd verwacht door de back-endservice Hallo queryparameters die zijn optioneel of nooit aanwezig zijn op Hallo-aanvraag.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Voorbeelden  
  
#### <a name="example"></a>Voorbeeld  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Context informatie toohello back-endservice doorsturen  
 Dit voorbeeld toont hoe beleid voor tooapply Hallo API toosupply context informatie toohello back-endservice niveau. Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too10:30 vooruit. Bij 12:10 is er een demo voor het aanroepen van een bewerking in de ontwikkelaarsportal Hallo waar u Hallo-beleid op het werk kunt zien.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|query-set-parameter|Hoofdelement.|Ja|  
|waarde|Hiermee geeft u Hallo-waarde van Hallo query parameterset toobe. Voor meerdere queryparameters Hello dezelfde naam toevoegen extra `value` elementen.|Ja|  
  
### <a name="properties"></a>Eigenschappen  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|Er bestaat actie|Geeft aan welke actie tootake Hallo queryparameter is al opgegeven. Dit kenmerk moet een van de volgende waarden Hallo hebben.<br /><br /> -onderdrukkingswaarde - vervangt Hallo van bestaande Hallo-parameter.<br />-skip - vervangen Hallo waarde van de bestaande queryparameter niet.<br />-toevoeg - voegt Hallo waarde toohello bestaande waarde van de queryparameter.<br />de queryparameter Hallo verwijdert - delete - uit Hallo-aanvraag.<br /><br /> Als de waarde te`override` opnemen van meerdere vermeldingen met Hallo dezelfde resulteert in een queryparameter hello wordt ingesteld volgens tooall-vermeldingen (die wordt vermeld meerdere keren) naam; alleen de vermelde waarden worden ingesteld in Hallo resultaat.|Nee|overschrijven|  
|naam|Geeft de naam van Hallo query parameterset toobe.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** back-end voor binnenkomend verkeer  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="RewriteURL"></a>Herschrijven van URL 's  
 Hallo `rewrite-uri` beleid zet een aanvraag-URL van de openbare formulier toohello vorm verwacht door de webservice hello, zoals wordt weergegeven in het volgende voorbeeld Hallo.  
  
-   Openbare URL-`http://api.example.com/storenumber/ordernumber`  
  
-   Aanvraag-URL-`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 Dit beleid kan worden gebruikt wanneer een menselijke en/of beschrijvende browser-URL moet worden omgezet in URL-indeling Hallo werd verwacht door de webservice Hallo. Dit beleid moet alleen toegepast wanneer een andere URL-indeling, zoals schone URL's, RESTful-URL's, gebruiksvriendelijke URL's of Zoekmachineoptimalisatie gebruiksvriendelijke URL's die zijn uitsluitend structurele URL's die niet een queryreeks bevatten en in plaats daarvan bevatten alleen Hallo pad Hallo blootstellen toobe resource (na Hallo schema- en Hallo). Dit wordt vaak gedaan voor fraaie uiterlijk, bruikbaarheid of zoekmachine optimaliseringsdoeleinden (Zoekmachineoptimalisatie).  
  
> [!NOTE]
>  U kunt alleen queryreeksparameters met behulp van Hallo beleid toevoegen. U kunt geen toevoegen extra Sjabloonparameters pad in Hallo herschrijven van URL's.  

### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>Voorbeeld  
  
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

### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|Herschrijf-uri|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Kenmerk|Beschrijving|Vereist|Standaard|  
|---------------|-----------------|--------------|-------------|  
|sjabloon|Hallo werkelijke webservice-URL met een queryreeks-parameters. Bij gebruik van expressies moet Hallo gehele getal een expressie.|Ja|N.v.t.|  
|kopiëren niet-overeenkomende parameters|Geeft aan of binnenkomende aanvraag Hallo niet aanwezig in de oorspronkelijke URL sjabloon Hallo queryparameters toohello URL die is gedefinieerd door Hallo herschrijven sjabloon worden toegevoegd|Nee|De waarde True|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** product, API-bewerking  
  
##  <a name="XSLTransform"></a>XML met behulp van een XSLT transformeren  
 Hallo `Transform XML using an XSLT` beleid van toepassing is een XSL-transformatie tooXML in de hoofdtekst van de aanvraag of antwoord van de Hallo.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
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
  
### <a name="example"></a>Voorbeeld  
  
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
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|XSL-transformatie|Hoofdelement.|Ja|  
|Parameter|Gebruikte toodefine variabelen die worden gebruikt in Hallo transformatie|Nee|  
|xsl: Stylesheet|Hoofdelement opmaakmodel. Alle elementen en kenmerken die zijn gedefinieerd binnen Volg Hallo standaard [XSLT-specificatie](http://www.w3.org/TR/xslt)|Ja|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** binnenkomende, uitgaande  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).  
