---
title: aaaAzure API Management cachebeleidsregels | Microsoft Docs
description: Meer informatie over Hallo cachebeleidsregels beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>De cachebeleidsregels API Management
Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen. Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a>Cachebeleidsregels  
  
-   Antwoord cachebeleidsregels  
  
    -   [Ophalen uit de cache](api-management-caching-policies.md#GetFromCache) -cache uitvoeren opzoeken en retourneren een geldige in cache opgeslagen reacties indien beschikbaar.  
  
    -   [Opslaan van toocache](api-management-caching-policies.md#StoreToCache) - Caches reacties op basis van toohello opgegeven cache-control-configuratie.  
  
-   Waarde cachebeleidsregels  
  
    -   [Waarde niet ophalen uit de cache](#GetFromCacheByKey) -ophalen van een item in de cache per sleutel.  
  
    -   [Waarde opslaan in cache](#StoreToCacheByKey) -opslaan van een item in Hallo cache per sleutel.  
  
    -   [Waarde verwijderen uit de cache](#RemoveCacheByKey) -verwijderen van een item in Hallo cache per sleutel.  
  
##  <a name="GetFromCache"></a>Ophalen uit de cache  
 Gebruik Hallo `cache-lookup` tooperform beleidscache opzoeken en retourneren een geldige cacheantwoord indien beschikbaar. Dit beleid kan worden toegepast in gevallen waar antwoordinhoud statisch gedurende een periode blijft. Antwoord in cache opslaan minder bandbreedte en verwerking van vereisten opgelegd voor het Hallo back-end web server en lagere latentie, waargenomen door de consument API.  
  
> [!NOTE]
>  Dit beleid moet zijn gekoppeld aan een [Store toocache](api-management-caching-policies.md#StoreToCache) beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>Voorbeelden  
  
#### <a name="example"></a>Voorbeeld  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Voorbeeld met behulp van beleidsexpressies  
 Dit voorbeeld ziet u hoe tootooconfigure API Management antwoord in cache plaatsen dat overeenkomt met het antwoord in cache opslaan van back-endservice zoals opgegeven door Hallo HALLO hallo duur van de service back `Cache-Control` richtlijn. Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too25:25 vooruit.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|cache-lookup|Hoofdelement.|Ja|  
|door header Vary|De antwoorden per waarde voor de opgegeven header, zoals accepteren, Accept-Charset Accept-Encoding, Accept-Language autorisatie Expect, van de Host, cache beginnen op If-Match.|Nee|  
|variëren door-query-parameter|De cache beginnen op antwoorden per waarde voor opgegeven queryparameters. Voer één of meerdere parameters. Gebruik puntkomma als scheidingsteken. Als niets wordt opgegeven, worden alle queryparameters gebruikt.|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|toestaan dat persoonlijke-antwoord-schrijfcache|Als de waarde te`true`, kunt opslaan in cache van aanvragen met een autorisatie-header.|Nee|ONWAAR|  
|downstream-caching-type|Dit kenmerk moet worden ingesteld als tooone Hallo waarden te volgen.<br /><br /> -none - downstream opslaan in cache is niet toegestaan.<br />-persoonlijke - downstream persoonlijke opslaan in cache is toegestaan.<br />-openbaar: persoonlijke en gedeelde downstream cache is toegestaan.|Nee|Geen|  
|must-revalidate|Als downstream caching is ingeschakeld dit kenmerk wordt in- of uitschakelen Hallo `must-revalidate` cache-control-instructie in de antwoorden van de gateway.|Nee|De waarde True|  
|door ontwikkelaars variëren|Stel te`true` toocache antwoorden per developer-sleutel.|Nee|ONWAAR|  
|variëren-in-developer-groepen|Stel te`true` toocache antwoorden per gebruikersrol.|Nee|ONWAAR|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** API, bewerking, product  
  
##  <a name="StoreToCache"></a>Store toocache  
 Hallo `cache-store` beleid caches reacties op basis van toohello cache-instellingen opgegeven. Dit beleid kan worden toegepast in gevallen waar antwoordinhoud statisch gedurende een periode blijft. Antwoord in cache opslaan minder bandbreedte en verwerking van vereisten opgelegd voor het Hallo back-end web server en lagere latentie, waargenomen door de consument API.  
  
> [!NOTE]
>  Dit beleid moet zijn gekoppeld aan een [ophalen uit de cache](api-management-caching-policies.md#GetFromCache) beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Voorbeelden  
  
#### <a name="example"></a>Voorbeeld  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Voorbeeld met behulp van beleidsexpressies  
 Dit voorbeeld ziet u hoe tootooconfigure API Management antwoord in cache plaatsen dat overeenkomt met het antwoord in cache opslaan van back-endservice zoals opgegeven door Hallo HALLO hallo duur van de service back `Cache-Control` richtlijn. Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too25:25 vooruit.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Zie voor meer informatie [beleidsexpressies](api-management-policy-expressions.md) en [Context variabele](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|opslag van de cache|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|Duur|Time-to-live Hallo in cache opgeslagen vermeldingen, in seconden opgegeven.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** uitgaand  
  
-   **Beleid scopes:** API, bewerking, product  
  
##  <a name="GetFromCacheByKey"></a>Waarde niet ophalen uit de cache  
 Gebruik Hallo `cache-lookup-value` beleid tooperform opzoeken in de cache per sleutel en een in cache opgeslagen waarde retourneren. Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.  
  
> [!NOTE]
>  Dit beleid moet zijn gekoppeld aan een [waarde opslaan in cache](#StoreToCacheByKey) beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Voorbeeld  
 Zie voor meer informatie over en voorbeelden van dit beleid, [aangepast opslaan in cache in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|cache-lookup-waarde|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|standaard-waarde|Een waarde die wordt toegewezen variabele toohello als sleutel zoeken in het cachegeheugen Hallo geresulteerd in een ontbreekt. Als dit kenmerk niet is opgegeven, `null` is toegewezen.|Nee|`null`|  
|sleutel|Toouse sleutelwaarde in Hallo opzoeken in de cache.|Ja|N.v.t.|  
|naam variabele|Naam van Hallo [context variabele](api-management-policy-expressions.md#ContextVariables) Hallo opgezocht waarde wordt toegewezen als de zoekopdracht is geslaagd. Als lookup in een ontbreekt resulteert, Hallo variabele waarde Hallo Hallo wordt toegewezen `default-value` kenmerk of `null`als hello `default-value` kenmerk wordt weggelaten.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** algemeen API, bewerking, product  
  
##  <a name="StoreToCacheByKey"></a>Waarde opslaan in cache  
 Hallo `cache-store-value` opslag van de cache per sleutel uitvoert. Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.  
  
> [!NOTE]
>  Dit beleid moet zijn gekoppeld aan een [waarde niet ophalen uit de cache](#GetFromCacheByKey) beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>Voorbeeld  
 Zie voor meer informatie over en voorbeelden van dit beleid, [aangepast opslaan in cache in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|cache-store-waarde|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|Duur|Waarde wordt in de cache voor Hallo opgegeven duurwaarde, in seconden opgegeven.|Ja|N.v.t.|  
|sleutel|Waarde van de belangrijkste Hallo cache worden opgeslagen onder.|Ja|N.v.t.|  
|waarde|Hallo waarde toobe in de cache opgeslagen.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** algemeen API, bewerking, product  
  
###  <a name="RemoveCacheByKey"></a>Waarde uit cache verwijderen  
 Hallo `cache-remove-value` een geïdentificeerd door de sleutel in de cache-item wordt verwijderd. Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met.  
  
#### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Voorbeeld  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|cache-remove-waarde|Hoofdelement.|Ja|  
  
#### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|sleutel|Hallo-sleutel van Hallo is eerder in cache opgeslagen waarde toobe verwijderd uit het Hallo-cachegeheugen.|Ja|N.v.t.|  
  
#### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Beleid secties:** inkomend, uitgaand back-end op fout  
  
-   **Beleid scopes:** algemeen API, bewerking, product  
  

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).  