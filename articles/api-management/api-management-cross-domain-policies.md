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
# <a name="api-management-cross-domain-policies"></a>API Management-beleid voor meerdere domeinen
Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen. Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CrossDomainPolicies"></a>Cross-domeinbeleid  
  
-   [Aanroepen tussen domeinen toestaan](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -Hallo API toegankelijk van Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -voegt tooan cross-origin-resource delen (CORS) ondersteunen of een API tooallow tussen domeinen aanroepen van clients op basis van een browser.  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) - JSON toegevoegd met de ondersteuning tooan bewerking opvulling (JSONP) of een API tooallow tussen domeinen aanroepen vanuit JavaScript-clients op basis van een browser.  
  
##  <a name="AllowCrossDomainCalls"></a>Aanroepen tussen domeinen toestaan  
 Gebruik Hallo `cross-domain` beleid toomake Hallo API die toegankelijk is vanaf de Adobe Flash en Microsoft Silverlight op browser gebaseerde clients.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|verschillende domeinen|Hoofdelement. Onderliggende elementen moeten voldoen toohello [Adobe cross-domeinbeleid bestandsspecificatie](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).|Ja|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** globale  
  
##  <a name="CORS"></a>CORS  
 Hallo `cors` beleid wordt toegevoegd voor cross-origin-resource delen (CORS) ondersteuning voor tooan bewerking of een API tooallow tussen domeinen aanroepen van clients op basis van een browser.  
  
 CORS kunt een browser en een server toointeract en bepalen of tooallow specifieke cross-origin-aanvragen (d.w.z. XMLHttpRequests aanroepen vanuit JavaScript op een webpagina tooother domeinen). Dit biedt meer flexibiliteit dan alleen toe te staan dezelfde-origin-aanvragen, maar is veiliger dan zodat alle cross-origin-aanvragen.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
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
  
### <a name="example"></a>Voorbeeld  
 In dit voorbeeld laat zien hoe toosupport voorafgaan aan de vlucht aanvraagt, zoals die met aangepaste headers of andere methoden dan GET en POST. aangepaste headers toosupport en aanvullende HTTP-woorden gebruiken Hallo `allowed-methods` en `allowed-headers` zoals weergegeven in het volgende voorbeeld Hallo secties.  
  
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
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|cors|Hoofdelement.|Ja|N.v.t.|  
|toegestane oorsprongen|Bevat `origin` elementen die Hallo toegestane oorsprongen voor aanvragen van andere domeinen beschrijven. `allowed-origins`kan bevatten één `origin` element waarmee wordt aangegeven `*` tooallow een oorsprong, of één of meer `origin` elementen die een URI bevatten.|Ja|N.v.t.|  
|Oorsprong|Hallo waarde kan zijn `*` tooallow alle oorsprongen of een URI die een enkele oorsprong aangeeft. Hallo URI moet een schema, host en poort bevatten.|Ja|Als Hallo-poort in een URI wordt weggelaten, poort 80 wordt gebruikt voor HTTP en poort 443 voor HTTPS wordt gebruikt.|  
|toegestaan methoden|Dit element is vereist als methoden dan ophalen of POST zijn toegestaan. Bevat `method` elementen die opgeeft Hallo ondersteunde HTTP-termen.|Nee|Als u deze sectie is niet aanwezig is, worden GET en POST worden ondersteund.|  
|Methode|Hiermee geeft u een HTTP-term.|Ten minste één `method` element is vereist als hello `allowed-methods` sectie aanwezig is.|N.v.t.|  
|toegestaan headers|Dit element bevat `header` elementen namen van Hallo headers die kunnen worden opgenomen in de aanvraag Hallo opgeven.|Nee|N.v.t.|  
|zichtbaar headers|Dit element bevat `header` elementen namen van Hallo headers die toegankelijk is door de client Hallo opgeven.|Nee|N.v.t.|  
|koptekst|Hiermee geeft u een header-naam.|Ten minste één `header` element is vereist in `allowed-headers` of `expose-headers` als Hallo sectie aanwezig is.|N.v.t.|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|referenties toestaan|Hallo `Access-Control-Allow-Credentials` header in Hallo voorbereidende antwoord wordt set toohello waarde van dit kenmerk en van invloed zijn op Hallo van mogelijkheid toosubmit clientreferenties in verschillende domeinen aanvragen.|Nee|ONWAAR|  
|Preflight-resultaat--maximumleeftijd|Hallo `Access-Control-Max-Age` header in Hallo voorbereidende antwoord wordt set toohello waarde van dit kenmerk en van invloed zijn op Hallo gebruikersagent mogelijkheid toocache voorafgaan aan de vlucht antwoord.|Nee|0|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** API, bewerking  
  
##  <a name="JSONP"></a>JSONP  
 Hallo `jsonp` beleid JSON wordt toegevoegd met opvulling (JSONP) ondersteuning tooan bewerking of een API-aanroepen tooallow tussen domeinen vanuit JavaScript-clients op basis van een browser. JSONP is een methode die wordt gebruikt in JavaScript-programma's toorequest gegevens van een server in een ander domein. JSONP omzeilt Hallo beperking afgedwongen door de meeste webbrowsers waarop access tooweb-pagina's in Hallo moet hetzelfde domein.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 Als u de methode Hallo zonder Hallo callback parameter aanroept? cb = XXX gewone JSON (zonder een wrapper-aanroep van functie) wordt geretourneerd.  
  
 Als u Hallo callback parameter toevoegen `?cb=XXX` JSONP gevolg hiervan zijn oorspronkelijke JSON-resultaten Hallo rond Hallo callback-functie zoals wrapping wordt geretourneerd`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|jsonp|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|callback parameternaam|Hallo tussen domeinen JavaScript-functieaanroep voorafgegaan door volledig gekwalificeerde domeinnaam Hallo waarin hello functie zich bevindt.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** uitgaand  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).  